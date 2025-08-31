# builder:unreal - unreal engine orchestration

comprehensive unreal engine 5 development orchestration for real-time 3d projects, virtual production, and interactive experiences.

## <input>

- **project path**: unreal project directory (.uproject location)
- **code/files**: source code, blueprints, assets
- **requirements**: project specifications and goals
- **platform targets**: windows/mac/linux/console/mobile
- **context**: development phase and priorities

## <sequence>

1. **project analysis**
   - scan project structure
   - identify engine version
   - analyze dependencies
   - evaluate asset pipeline

2. **development orchestration**
   - select appropriate workflow
   - configure build pipeline
   - set up automation
   - initialize tools

3. **implementation**
   - execute development tasks
   - manage assets
   - optimize performance
   - test and validate

## <intelligence>

### workflow detection
```python
def detect_workflow(project):
    indicators = {
        'virtual_production': ['led_wall', 'icvfx', 'virtual_set'],
        'game_development': ['gameplay', 'multiplayer', 'game_mode'],
        'archviz': ['architectural', 'interior', 'walkthrough'],
        'film_production': ['sequencer', 'cinematic', 'render_queue'],
        'simulation': ['physics', 'dynamics', 'training']
    }
    return analyze_project_type(project, indicators)
```

### automation strategy
- python scripting for editor automation
- blueprint for runtime logic
- c++ for performance-critical code
- uat for build automation

## <execution>

### project initialization
```bash
# create new unreal project
UnrealEditor-Cmd.exe -run=pythonscript -script="
import unreal
project = unreal.ProjectManager.create_project(
    name='MyProject',
    template='ThirdPerson',
    location='/path/to/project'
)
"
```

### asset pipeline
```python
# python asset automation
import unreal

def process_assets():
    asset_tools = unreal.AssetToolsHelpers.get_asset_tools()
    editor_util = unreal.EditorUtilityLibrary
    
    # batch import assets
    import_task = unreal.AssetImportTask()
    import_task.filename = '/path/to/assets'
    import_task.destination_path = '/Game/Assets'
    import_task.automated = True
    
    asset_tools.import_asset_tasks([import_task])
    
    # optimize textures
    for texture in editor_util.get_selected_assets():
        if isinstance(texture, unreal.Texture2D):
            texture.set_editor_property('lod_bias', 0)
            texture.set_editor_property('compression_settings', 
                                       unreal.TextureCompressionSettings.TC_DEFAULT)
```

### blueprint automation
```python
# create blueprint programmatically
def create_blueprint_actor():
    factory = unreal.BlueprintFactory()
    factory.parent_class = unreal.Actor
    
    asset_tools = unreal.AssetToolsHelpers.get_asset_tools()
    blueprint = asset_tools.create_asset(
        'BP_CustomActor',
        '/Game/Blueprints',
        unreal.Blueprint,
        factory
    )
    
    # add components
    subsystem = unreal.get_engine_subsystem(unreal.SubobjectDataSubsystem)
    root_data = subsystem.k2_gather_subobject_data_for_blueprint(blueprint)[0]
    
    # add mesh component
    mesh_data, _ = subsystem.add_new_subobject(
        unreal.StaticMeshComponent,
        root_data
    )
    
    return blueprint
```

### build automation
```bash
# uat build command
RunUAT.bat BuildCookRun \
  -project="MyProject.uproject" \
  -platform=Win64 \
  -clientconfig=Development \
  -cook -build -stage -package \
  -compressed -iterate
```

## <tools>

### python editor api
- `unreal.EditorAssetLibrary`: asset management
- `unreal.EditorLevelLibrary`: level manipulation
- `unreal.EditorUtilityLibrary`: editor utilities
- `unreal.SequencerTools`: cinematic automation

### command line tools
- `UnrealEditor-Cmd.exe`: headless editor operations
- `RunUAT.bat/sh`: automation tool
- `UnrealBuildTool`: compilation and linking

### blueprint utilities
- editor utility widgets for ui
- editor utility blueprints for automation
- blutilities for asset actions

## <optimization>

### performance profiling
```python
# profile and optimize
def profile_scene():
    profiler = unreal.ProfilerSubsystem()
    
    # start profiling
    profiler.start_capturing()
    
    # run test scenario
    unreal.EditorLevelLibrary.editor_play_simulate()
    unreal.SystemLibrary.delay(10.0)
    
    # stop and analyze
    profiler.stop_capturing()
    report = profiler.generate_report()
    
    # identify bottlenecks
    for metric in report.metrics:
        if metric.gpu_time > 16.0:  # >60fps threshold
            print(f"GPU bottleneck: {metric.name}")
        if metric.game_thread_time > 16.0:
            print(f"CPU bottleneck: {metric.name}")
```

### asset optimization
- texture streaming pools
- lod generation
- nanite for high-poly meshes
- lumen for dynamic gi
- world partition for large worlds

## <output>

### deliverables
1. **project files**
   - .uproject configuration
   - source code (c++/python)
   - blueprint assets
   - content packages

2. **build artifacts**
   - executable packages
   - cooked content
   - deployment configs
   - performance reports

3. **documentation**
   - technical specs
   - api documentation
   - workflow guides
   - optimization notes

## <rules>

### best practices
- use version control (perforce/git)
- maintain asset naming conventions
- implement proper folder structure
- optimize early and often
- test on target hardware

### performance targets
- 60+ fps for real-time
- <100ms input latency
- <4gb memory footprint
- fast iteration times

## <components>

<use>@file:~/.halo/components/next-command.md</use>

## <connections>

### workflow paths
- **virtual production** → `/builder:unreal:render`
- **game development** → `/builder:unreal:blueprint`
- **automation** → `/builder:unreal:python`
- **deployment** → `/builder:unreal:deploy`

### integration points
- connects with `/video-studio` for production
- interfaces with `/3d-artist` for assets
- works with `/motion` for animation
- integrates with `/tech` for optimization

## <examples>

### virtual production setup
```bash
/builder:unreal "set up led wall virtual production with 
real-time camera tracking and in-camera vfx for 
mandalorian-style production"
```

### game prototype
```bash
/builder:unreal "create multiplayer fps prototype with 
basic movement, shooting, and networking using 
blueprints and c++"
```

### architectural visualization
```bash
/builder:unreal "build interactive archviz walkthrough 
with realistic lighting, materials, and vr support 
using lumen and nanite"
```

---

*orchestrates unreal engine development with comprehensive automation and optimization*
