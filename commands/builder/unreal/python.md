# 🐍 builder:unreal:python - automation scripting

comprehensive python automation for unreal engine editor workflows, asset pipelines, and build processes.

## <input>

- **script type**: editor/asset/build/test automation
- **target scope**: project-wide or specific assets
- **automation goals**: workflow optimization needs
- **integration points**: external tools/pipelines
- **execution mode**: immediate/startup/scheduled

## <sequence>

1. **environment setup**
   - verify python plugin
   - configure paths
   - import modules
   - check dependencies

2. **script development**
   - create automation logic
   - implement error handling
   - add progress feedback
   - setup logging

3. **integration**
   - bind to editor events
   - create ui panels
   - schedule execution
   - export results

## <automation>

### editor automation framework
```python
import unreal
import os
import json
import datetime
from typing import List, Dict, Any

class UnrealAutomation:
    """
    Core automation framework for unreal engine
    """
    
    def __init__(self):
        self.editor_asset_lib = unreal.EditorAssetLibrary
        self.editor_util = unreal.EditorUtilityLibrary
        self.asset_tools = unreal.AssetToolsHelpers.get_asset_tools()
        self.level_lib = unreal.EditorLevelLibrary
        self.log = unreal.log
        
    def batch_process_assets(self, 
                           asset_paths: List[str], 
                           process_func: callable,
                           report_progress: bool = True):
        """
        Process multiple assets with progress reporting
        """
        total = len(asset_paths)
        
        with unreal.ScopedSlowTask(total, "Processing Assets") as task:
            task.make_dialog(True)
            
            results = []
            for i, asset_path in enumerate(asset_paths):
                if task.should_cancel():
                    break
                    
                task.enter_progress_frame(1, f"Processing {asset_path}")
                
                try:
                    asset = self.editor_asset_lib.load_asset(asset_path)
                    result = process_func(asset)
                    results.append({
                        "asset": asset_path,
                        "status": "success",
                        "result": result
                    })
                except Exception as e:
                    results.append({
                        "asset": asset_path,
                        "status": "error",
                        "error": str(e)
                    })
                    self.log_error(f"Failed to process {asset_path}: {e}")
            
        return results
    
    def automate_import(self, source_dir: str, target_dir: str = "/Game/"):
        """
        Automated asset import pipeline
        """
        import_tasks = []
        
        # scan source directory
        for root, dirs, files in os.walk(source_dir):
            for file in files:
                file_path = os.path.join(root, file)
                ext = os.path.splitext(file)[1].lower()
                
                # determine asset type
                if ext in ['.fbx', '.obj', '.dae']:
                    task = self.create_mesh_import_task(file_path, target_dir)
                elif ext in ['.png', '.jpg', '.tga', '.exr']:
                    task = self.create_texture_import_task(file_path, target_dir)
                elif ext in ['.wav', '.mp3', '.ogg']:
                    task = self.create_audio_import_task(file_path, target_dir)
                else:
                    continue
                    
                import_tasks.append(task)
        
        # execute import
        if import_tasks:
            self.asset_tools.import_asset_tasks(import_tasks)
            self.log(f"Imported {len(import_tasks)} assets")
            
        return import_tasks
    
    def create_mesh_import_task(self, file_path: str, target_dir: str):
        """
        Configure mesh import settings
        """
        task = unreal.AssetImportTask()
        task.filename = file_path
        task.destination_path = target_dir + "Meshes"
        task.automated = True
        task.save = True
        task.replace_existing = True
        
        # mesh specific options
        options = unreal.FbxImportUI()
        options.import_mesh = True
        options.import_textures = True
        options.import_materials = True
        options.import_as_skeletal = False
        
        # static mesh options
        options.static_mesh_import_data.import_translation = unreal.Vector(0, 0, 0)
        options.static_mesh_import_data.import_rotation = unreal.Rotator(0, 0, 0)
        options.static_mesh_import_data.import_uniform_scale = 1.0
        options.static_mesh_import_data.combine_meshes = True
        options.static_mesh_import_data.generate_lightmap_uv = True
        options.static_mesh_import_data.auto_generate_collision = True
        
        task.options = options
        return task
```

### asset pipeline automation
```python
class AssetPipelineAutomation:
    """
    Automated asset processing pipeline
    """
    
    def optimize_textures(self, texture_assets: List):
        """
        Batch optimize texture settings
        """
        optimizations = []
        
        for texture in texture_assets:
            if not isinstance(texture, unreal.Texture2D):
                continue
                
            original_size = texture.get_editor_property("source_uncompressed_size")
            
            # apply optimizations
            texture.set_editor_property("compression_settings", 
                                       unreal.TextureCompressionSettings.TC_DEFAULT)
            texture.set_editor_property("mip_gen_settings",
                                       unreal.TextureMipGenSettings.TMGS_FROM_TEXTURE_GROUP)
            texture.set_editor_property("lod_bias", 0)
            texture.set_editor_property("never_stream", False)
            
            # set appropriate texture group
            if "normal" in texture.get_name().lower():
                texture.set_editor_property("lod_group",
                                          unreal.TextureGroup.TEXTUREGROUP_WORLD_NORMAL_MAP)
            elif "ui" in texture.get_path_name().lower():
                texture.set_editor_property("lod_group",
                                          unreal.TextureGroup.TEXTUREGROUP_UI)
            else:
                texture.set_editor_property("lod_group",
                                          unreal.TextureGroup.TEXTUREGROUP_WORLD)
            
            # save changes
            unreal.EditorAssetLibrary.save_asset(texture.get_path_name())
            
            optimizations.append({
                "asset": texture.get_name(),
                "original_size": original_size,
                "optimized": True
            })
            
        return optimizations
    
    def generate_lods(self, static_meshes: List):
        """
        Auto-generate LODs for static meshes
        """
        lod_settings = []
        
        for mesh in static_meshes:
            if not isinstance(mesh, unreal.StaticMesh):
                continue
                
            # configure lod settings
            lod_params = unreal.EditorScriptingMeshReductionOptions()
            
            # lod 0 is base mesh
            # generate 3 additional lods
            lod_configs = [
                (1, 0.75, 2.0),  # lod1: 75% triangles, 2x distance
                (2, 0.5, 4.0),   # lod2: 50% triangles, 4x distance
                (3, 0.25, 8.0)   # lod3: 25% triangles, 8x distance
            ]
            
            for lod_index, percent, distance in lod_configs:
                lod_params.reduction_settings = unreal.MeshReductionSettings()
                lod_params.reduction_settings.percent_triangles = percent
                lod_params.reduction_settings.screen_size = distance
                
                # apply lod
                unreal.EditorStaticMeshLibrary.set_lod_reduction_settings(
                    mesh, lod_index, lod_params
                )
            
            # enable auto lod
            mesh.set_editor_property("auto_compute_lod_screen_size", True)
            
            lod_settings.append({
                "mesh": mesh.get_name(),
                "lod_count": len(lod_configs) + 1,
                "auto_compute": True
            })
            
        return lod_settings
```

### level automation
```python
class LevelAutomation:
    """
    Level and world automation tools
    """
    
    def batch_place_actors(self, actor_class, positions: List[tuple]):
        """
        Place multiple actors in level
        """
        placed_actors = []
        
        for x, y, z in positions:
            location = unreal.Vector(x, y, z)
            rotation = unreal.Rotator(0, 0, 0)
            
            actor = unreal.EditorLevelLibrary.spawn_actor_from_class(
                actor_class,
                location,
                rotation
            )
            
            placed_actors.append(actor)
            
        return placed_actors
    
    def organize_level_actors(self):
        """
        Organize actors into folders
        """
        all_actors = unreal.EditorLevelLibrary.get_all_level_actors()
        
        organization = {
            "Lights": [],
            "Meshes": [],
            "Volumes": [],
            "Gameplay": [],
            "Effects": [],
            "Audio": [],
            "Other": []
        }
        
        for actor in all_actors:
            if actor.get_class().get_name().startswith("Light"):
                organization["Lights"].append(actor)
            elif isinstance(actor, unreal.StaticMeshActor):
                organization["Meshes"].append(actor)
            elif "Volume" in actor.get_class().get_name():
                organization["Volumes"].append(actor)
            elif isinstance(actor, unreal.ParticleSystemActor):
                organization["Effects"].append(actor)
            elif isinstance(actor, unreal.AmbientSound):
                organization["Audio"].append(actor)
            else:
                organization["Other"].append(actor)
        
        # create folders and move actors
        for folder_name, actors in organization.items():
            if actors:
                for actor in actors:
                    actor.set_folder_path(folder_name)
                    
        return organization
```

### build automation
```python
class BuildAutomation:
    """
    Automated build and deployment
    """
    
    def automated_build_pipeline(self, platforms: List[str]):
        """
        Run complete build pipeline
        """
        import subprocess
        
        project_path = unreal.Paths.project_file_path()
        engine_dir = unreal.Paths.engine_dir()
        
        build_results = []
        
        for platform in platforms:
            # configure build
            build_config = self.get_platform_config(platform)
            
            # run uat
            uat_path = os.path.join(engine_dir, "Build/BatchFiles/RunUAT.bat")
            
            cmd = [
                uat_path,
                "BuildCookRun",
                f"-project={project_path}",
                f"-platform={platform}",
                f"-clientconfig={build_config['config']}",
                "-cook", "-build", "-stage", "-pak", "-archive",
                f"-archivedirectory={build_config['output']}"
            ]
            
            # execute build
            result = subprocess.run(cmd, capture_output=True, text=True)
            
            build_results.append({
                "platform": platform,
                "success": result.returncode == 0,
                "output": result.stdout,
                "errors": result.stderr
            })
            
        return build_results
    
    def get_platform_config(self, platform: str) -> Dict:
        """
        Get platform-specific build configuration
        """
        configs = {
            "Win64": {
                "config": "Shipping",
                "output": "Builds/Windows",
                "architecture": "x64"
            },
            "Mac": {
                "config": "Shipping",
                "output": "Builds/Mac",
                "architecture": "universal"
            },
            "Linux": {
                "config": "Shipping",
                "output": "Builds/Linux",
                "architecture": "x86_64"
            },
            "Android": {
                "config": "Shipping",
                "output": "Builds/Android",
                "architecture": "arm64-v8a"
            },
            "iOS": {
                "config": "Shipping",
                "output": "Builds/iOS",
                "architecture": "arm64"
            }
        }
        
        return configs.get(platform, configs["Win64"])
```

### testing automation
```python
class TestAutomation:
    """
    Automated testing framework
    """
    
    def run_automation_tests(self, test_filter: str = "Project"):
        """
        Execute automation tests
        """
        automation = unreal.AutomationLibrary()
        
        # get available tests
        test_names = automation.get_automation_test_names(test_filter)
        
        results = []
        
        with unreal.ScopedSlowTask(len(test_names), "Running Tests") as task:
            task.make_dialog(True)
            
            for test_name in test_names:
                task.enter_progress_frame(1, f"Running {test_name}")
                
                # run test
                test_result = automation.run_automation_test(test_name)
                
                results.append({
                    "test": test_name,
                    "passed": test_result.succeeded,
                    "warnings": test_result.warnings,
                    "errors": test_result.errors,
                    "duration": test_result.duration
                })
                
        return results
    
    def performance_profiling(self):
        """
        Run performance profiling
        """
        # start stat capture
        unreal.SystemLibrary.execute_console_command(
            None, "stat startfile"
        )
        
        # run test scenario
        unreal.SystemLibrary.delay(10.0)
        
        # stop capture
        unreal.SystemLibrary.execute_console_command(
            None, "stat stopfile"
        )
        
        # analyze results
        profile_path = os.path.join(
            unreal.Paths.project_saved_dir(),
            "Profiling/UnrealStats"
        )
        
        return profile_path
```

## <ui-tools>

### editor utility widgets
```python
def create_automation_ui():
    """
    Create custom editor ui for automation
    """
    # create editor utility widget blueprint
    factory = unreal.EditorUtilityWidgetBlueprintFactory()
    
    widget_bp = unreal.AssetToolsHelpers.get_asset_tools().create_asset(
        "EUW_AutomationPanel",
        "/Game/Editor",
        unreal.EditorUtilityWidgetBlueprint,
        factory
    )
    
    # register as tab
    unreal.EditorUtilitySubsystem().register_tab_and_get_id(
        widget_bp,
        "AutomationPanel"
    )
    
    return widget_bp
```

## <output>

### automation report
```
AUTOMATION EXECUTION COMPLETE
=============================
Script: asset_pipeline_optimization.py
Duration: 4m 23s

Assets Processed:
- Textures: 342 optimized
- Meshes: 156 (LODs generated)
- Materials: 89 updated
- Blueprints: 23 compiled

Optimizations:
✓ Texture memory reduced by 42%
✓ Draw calls reduced by 28%
✓ Shader complexity improved
✓ Load times decreased by 3.2s

Test Results:
- Unit Tests: 156/156 passed
- Integration: 42/42 passed
- Performance: All within budget

Errors: 0
Warnings: 3
```

## <components>

<use>@file:~/.halo/components/next-command.md</use>

## <next>

### automation workflows
- `/builder:unreal:render` - automate cinematics
- `/builder:unreal:build` - ci/cd pipeline
- `/builder:unreal:assets` - batch processing

---

*comprehensive python automation for unreal engine workflows*