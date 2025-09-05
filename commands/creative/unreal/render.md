# builder:unreal:render - virtual production & cinematics

real-time rendering, virtual production workflows, and cinematic output with unreal engine's advanced rendering features.

## <input>

- **render type**: realtime/offline/virtual production
- **output format**: video/image sequence/live stream
- **quality settings**: preview/production/broadcast
- **camera setup**: virtual/tracked/multi-cam
- **environment**: led wall/green screen/full cg

## <sequence>

1. **scene preparation**
   - configure lighting
   - set up cameras
   - prepare environments
   - optimize assets

2. **rendering setup**
   - configure pipelines
   - set quality levels
   - enable features
   - setup outputs

3. **production**
   - execute renders
   - monitor performance
   - adjust in real-time
   - export results

## <virtual-production>

### in-camera vfx setup
```python
import unreal

class VirtualProductionSetup:
    """
    Configure virtual production with led walls
    """
    
    def __init__(self):
        self.ndisplay_config = unreal.DisplayClusterConfigurationData()
        self.stage_actor = None
        self.tracking_system = None
        
    def setup_led_wall(self, wall_config):
        """
        Configure led wall for icvfx
        """
        # create ndisplay configuration
        cluster_config = {
            "cluster_nodes": [
                {
                    "id": "node_0",
                    "host": "192.168.1.100",
                    "viewports": [
                        {
                            "id": "vp_center",
                            "x": 0, "y": 0,
                            "width": 7680,
                            "height": 4320,
                            "screen": "led_wall_center"
                        },
                        {
                            "id": "vp_left",
                            "x": -7680, "y": 0,
                            "width": 3840,
                            "height": 4320,
                            "screen": "led_wall_left"
                        },
                        {
                            "id": "vp_right",
                            "x": 7680, "y": 0,
                            "width": 3840,
                            "height": 4320,
                            "screen": "led_wall_right"
                        }
                    ]
                }
            ],
            "screens": [
                {
                    "id": "led_wall_center",
                    "size": {"x": 12.0, "y": 6.0},
                    "origin": {"x": 0, "y": 0, "z": 0}
                }
            ]
        }
        
        # apply configuration
        self.ndisplay_config.import_data(cluster_config)
        
        # create stage actor
        self.stage_actor = unreal.EditorLevelLibrary.spawn_actor_from_class(
            unreal.DisplayClusterRootActor,
            unreal.Vector(0, 0, 0),
            unreal.Rotator(0, 0, 0)
        )
        
        self.stage_actor.config_data = self.ndisplay_config
        
        return self.stage_actor
    
    def setup_camera_tracking(self, tracking_type="vive"):
        """
        Configure camera tracking system
        """
        # enable live link
        live_link = unreal.LiveLinkSubsystem()
        
        if tracking_type == "vive":
            # vive tracker setup
            source_settings = unreal.LiveLinkViveTrackerSourceSettings()
            source_settings.tracker_id = "LHR-12345678"
            source_settings.tracking_space = "stage"
            
        elif tracking_type == "optitrack":
            # optitrack setup
            source_settings = unreal.LiveLinkOptitrackSourceSettings()
            source_settings.server_address = "192.168.1.50"
            source_settings.client_address = "192.168.1.100"
            
        elif tracking_type == "aruco":
            # aruco marker tracking
            source_settings = unreal.LiveLinkArucoSourceSettings()
            source_settings.camera_index = 0
            source_settings.marker_size = 0.1
            
        # create tracking source
        tracking_source = live_link.create_source(source_settings)
        
        # attach to camera
        camera_actor = unreal.EditorLevelLibrary.get_selected_level_actors()[0]
        if camera_actor:
            live_link_component = camera_actor.add_component(
                unreal.LiveLinkComponentController
            )
            live_link_component.subject_representation = tracking_source
            
        return tracking_source
    
    def configure_inner_frustum(self, camera, led_screen):
        """
        Setup inner frustum for proper perspective
        """
        # calculate frustum
        frustum_settings = unreal.DisplayClusterConfigurationICVFX_CameraSettings()
        
        frustum_settings.enable_inner_frustum = True
        frustum_settings.camera_location = camera.get_actor_location()
        frustum_settings.camera_rotation = camera.get_actor_rotation()
        frustum_settings.field_of_view = camera.field_of_view
        
        # chromakey settings for green screen extension
        frustum_settings.chromakey_settings.enable = True
        frustum_settings.chromakey_settings.chromakey_color = unreal.LinearColor(0, 1, 0, 1)
        frustum_settings.chromakey_settings.chromakey_tolerance = 0.3
        
        # apply to ndisplay
        self.ndisplay_config.stage_settings.inner_frustum = frustum_settings
```

### sequencer automation
```python
class SequencerAutomation:
    """
    Cinematic sequencer automation
    """
    
    def create_cinematic_sequence(self, sequence_name, duration=300):
        """
        Create and configure level sequence
        """
        # create sequence asset
        sequence = unreal.AssetToolsHelpers.get_asset_tools().create_asset(
            sequence_name,
            "/Game/Cinematics",
            unreal.LevelSequence,
            unreal.LevelSequenceFactoryNew()
        )
        
        # set duration
        sequence.set_playback_range(0, duration)
        sequence.set_display_rate(unreal.FrameRate(30, 1))
        
        # add master track
        master_track = sequence.add_master_track(unreal.MovieSceneCinematicShotTrack)
        
        return sequence
    
    def add_camera_to_sequence(self, sequence, camera_actor):
        """
        Add camera with cuts track
        """
        # add camera binding
        camera_binding = sequence.add_possessable(camera_actor)
        
        # add transform track
        transform_track = camera_binding.add_track(unreal.MovieScene3DTransformTrack)
        transform_section = transform_track.add_section()
        transform_section.set_range(sequence.get_playback_range())
        
        # add camera cuts track
        camera_cut_track = sequence.add_master_track(unreal.MovieSceneCameraCutTrack)
        camera_cut_section = camera_cut_track.add_section()
        camera_cut_section.set_range(sequence.get_playback_range())
        camera_cut_section.set_camera_binding_id(camera_binding)
        
        return camera_binding
    
    def animate_camera_movement(self, sequence, camera_binding, keyframes):
        """
        Create camera animation
        """
        transform_track = camera_binding.find_track(unreal.MovieScene3DTransformTrack)
        transform_section = transform_track.get_sections()[0]
        
        # get transform channels
        channels = transform_section.get_channels()
        
        for time, location, rotation in keyframes:
            frame = unreal.FrameNumber(int(time * 30))  # 30fps
            
            # location keys
            channels[0].add_key(frame, location.x)  # x
            channels[1].add_key(frame, location.y)  # y
            channels[2].add_key(frame, location.z)  # z
            
            # rotation keys
            channels[3].add_key(frame, rotation.pitch)
            channels[4].add_key(frame, rotation.yaw)
            channels[5].add_key(frame, rotation.roll)
```

### rendering pipeline
```python
class RenderingPipeline:
    """
    Advanced rendering configuration
    """
    
    def setup_movie_render_queue(self, sequence, output_config):
        """
        Configure movie render pipeline
        """
        # create render job
        queue = unreal.MoviePipelineQueueEngineSubsystem()
        job = queue.allocate_new_job(unreal.MoviePipelineExecutorJob)
        
        job.sequence = unreal.SoftObjectPath(sequence.get_path_name())
        job.map = unreal.SoftObjectPath(unreal.EditorLevelLibrary.get_editor_world())
        
        # create master config
        config = job.get_configuration()
        
        # output settings
        output_setting = config.add_setting(unreal.MoviePipelineOutputSetting)
        output_setting.output_directory = unreal.DirectoryPath(output_config["path"])
        output_setting.file_name_format = output_config["naming"]
        output_setting.output_resolution = unreal.IntPoint(
            output_config["width"],
            output_config["height"]
        )
        output_setting.output_frame_rate = unreal.FrameRate(
            output_config["fps"], 1
        )
        
        # add render passes
        self.add_render_passes(config, output_config["passes"])
        
        # quality settings
        self.configure_quality_settings(config, output_config["quality"])
        
        return job
    
    def add_render_passes(self, config, passes):
        """
        Configure render passes
        """
        available_passes = {
            "beauty": unreal.MoviePipelineDeferredPassBase,
            "depth": unreal.MoviePipelineImagePassBase,
            "motion_vectors": unreal.MoviePipelineImagePassBase,
            "normals": unreal.MoviePipelineImagePassBase,
            "object_id": unreal.MoviePipelineImagePassBase
        }
        
        for pass_name in passes:
            if pass_name == "beauty":
                # main beauty pass
                deferred_pass = config.add_setting(
                    unreal.MoviePipelineDeferredPassBase
                )
                deferred_pass.disable_multisample_effects = False
                
            elif pass_name == "depth":
                # depth pass
                depth_pass = config.add_setting(
                    unreal.MoviePipelineImagePassBase
                )
                depth_pass.pass_name = "SceneDepth"
                
            elif pass_name == "motion_vectors":
                # motion vectors for compositing
                motion_pass = config.add_setting(
                    unreal.MoviePipelineImagePassBase
                )
                motion_pass.pass_name = "MotionVectors"
    
    def configure_quality_settings(self, config, quality_level):
        """
        Set render quality parameters
        """
        quality_presets = {
            "preview": {
                "spatial_samples": 1,
                "temporal_samples": 1,
                "override_aa": False,
                "motion_blur": 0.0
            },
            "production": {
                "spatial_samples": 4,
                "temporal_samples": 8,
                "override_aa": True,
                "motion_blur": 0.5
            },
            "broadcast": {
                "spatial_samples": 8,
                "temporal_samples": 16,
                "override_aa": True,
                "motion_blur": 0.5
            }
        }
        
        preset = quality_presets.get(quality_level, quality_presets["production"])
        
        # anti-aliasing settings
        aa_setting = config.add_setting(unreal.MoviePipelineAntiAliasingSetting)
        aa_setting.spatial_sample_count = preset["spatial_samples"]
        aa_setting.temporal_sample_count = preset["temporal_samples"]
        aa_setting.override_anti_aliasing = preset["override_aa"]
        
        # motion blur
        if preset["motion_blur"] > 0:
            motion_blur = config.add_setting(unreal.MoviePipelineMotionBlurSetting)
            motion_blur.motion_blur_amount = preset["motion_blur"]
            
        # console variables for quality
        console_vars = config.add_setting(unreal.MoviePipelineConsoleVariableSetting)
        console_vars.console_variables = {
            "r.MotionBlurQuality": "4",
            "r.DepthOfFieldQuality": "4",
            "r.Shadow.MaxCSMResolution": "4096",
            "r.Shadow.RadiusThreshold": "0.01",
            "r.Lumen.Reflections.Quality": "3",
            "r.Lumen.TraceMeshSDFs": "1",
            "r.RayTracing.Shadows": "1",
            "r.RayTracing.Reflections": "1"
        }
```

### real-time optimization
```python
def optimize_for_realtime(target_fps=60):
    """
    Optimize scene for real-time rendering
    """
    optimizations = []
    
    # scalability settings
    scalability = unreal.SystemLibrary.execute_console_command
    
    if target_fps >= 60:
        # high performance mode
        scalability(None, "sg.ViewDistanceQuality 2")
        scalability(None, "sg.AntiAliasingQuality 2")
        scalability(None, "sg.ShadowQuality 2")
        scalability(None, "sg.PostProcessQuality 2")
        scalability(None, "sg.TextureQuality 2")
        scalability(None, "sg.EffectsQuality 2")
        optimizations.append("Performance mode enabled")
        
    else:
        # quality mode
        scalability(None, "sg.ViewDistanceQuality 3")
        scalability(None, "sg.AntiAliasingQuality 3")
        scalability(None, "sg.ShadowQuality 3")
        scalability(None, "sg.PostProcessQuality 3")
        scalability(None, "sg.TextureQuality 3")
        scalability(None, "sg.EffectsQuality 3")
        optimizations.append("Quality mode enabled")
    
    # lumen settings
    scalability(None, "r.Lumen.ScreenProbeGather.ScreenTraces 1")
    scalability(None, "r.Lumen.ScreenProbeGather.DownsampleFactor 2")
    
    # nanite settings
    scalability(None, "r.Nanite 1")
    scalability(None, "r.Nanite.MaxPixelsPerEdge 1.0")
    
    return optimizations
```

## <output>

### render report
```
RENDER COMPLETE
===============
Type: Virtual Production
Resolution: 7680x4320
Frame Rate: 30fps
Duration: 2m 30s (4500 frames)

Render Passes:
 - Beauty Pass
 - Depth Pass
 - Motion Vectors
 - Object IDs
 - Cryptomatte

Performance:
- Average FPS: 28.7
- GPU Usage: 94%
- Memory Usage: 18.2 GB
- Render Time: 6h 23m

Virtual Production Setup:
 - LED Wall Configuration
 - Camera Tracking Active
 - Inner Frustum Calibrated
 - Color Pipeline Matched

Output Location:
/Renders/VP_Project_001/
```

## <components>

<use>@file:../../../components/next-command.md</use>

## <next>

### production workflows
- `/builder:unreal:deploy` - distribute renders
- `/video-studio` - post-production
- `/motion` - animation refinement

---

*orchestrates virtual production and cinematic rendering with unreal engine*
