# builder:unreal:prime - project initialization

comprehensive unreal engine project setup with full sdk integration, automation configuration, and development environment preparation.

## <input>

- **project name**: target project identifier
- **project type**: game/film/archviz/simulation/vr
- **engine version**: ue5.4/5.5/5.6 or source build
- **target platforms**: deployment targets
- **team size**: solo/small/large team setup

## <sequence>

1. **environment verification**
   - check engine installation
   - verify sdk requirements
   - validate dependencies
   - confirm tool availability

2. **project creation**
   - initialize project structure
   - configure engine settings
   - set up source control
   - establish conventions

3. **automation setup**
   - enable python plugin
   - configure build scripts
   - set up ci/cd pipeline
   - initialize testing

## <initialization>

### engine setup
```bash
# verify unreal installation
UE_PATH="/Program Files/Epic Games/UE_5.6"
if [ ! -d "$UE_PATH" ]; then
    echo "Installing Unreal Engine..."
    # epic games launcher cli or source build
fi

# verify python plugin
"$UE_PATH/Engine/Binaries/Win64/UnrealEditor-Cmd.exe" \
  -run=pythonscript -script="
import unreal
print('Python {} initialized'.format(sys.version))
"
```

### project scaffolding
```python
import unreal
import os

def create_project_structure(project_name, template="ThirdPerson"):
    """
    Create comprehensive project structure
    """
    # create project
    project_path = f"C:/Projects/{project_name}"
    
    # generate .uproject
    project_settings = {
        "FileVersion": 3,
        "EngineAssociation": "5.6",
        "Category": "",
        "Description": f"{project_name} - Unreal Engine Project",
        "Modules": [
            {
                "Name": project_name,
                "Type": "Runtime",
                "LoadingPhase": "Default"
            }
        ],
        "Plugins": [
            {"Name": "PythonScriptPlugin", "Enabled": True},
            {"Name": "EditorScriptingUtilities", "Enabled": True},
            {"Name": "SequencerScripting", "Enabled": True},
            {"Name": "MovieRenderPipeline", "Enabled": True}
        ]
    }
    
    # create folder structure
    folders = [
        "Content/Blueprints",
        "Content/Materials",
        "Content/Meshes",
        "Content/Textures",
        "Content/Audio",
        "Content/Cinematics",
        "Content/Particles",
        "Content/UI",
        "Source",
        "Config",
        "Build",
        "Saved",
        "Intermediate",
        "Documentation",
        "Scripts/Python",
        "Scripts/Automation"
    ]
    
    for folder in folders:
        os.makedirs(os.path.join(project_path, folder), exist_ok=True)
    
    return project_path
```

### development environment
```python
# configure editor settings
def setup_editor_preferences():
    editor_prefs = unreal.EditorPreferences()
    
    # performance settings
    editor_prefs.set_editor_property("use_less_cpu_when_in_background", True)
    editor_prefs.set_editor_property("monitor_editor_performance", True)
    
    # workflow settings
    editor_prefs.set_editor_property("enable_auto_save", True)
    editor_prefs.set_editor_property("auto_save_time_minutes", 10)
    editor_prefs.set_editor_property("auto_save_warning_seconds", 30)
    
    # source control
    source_control = unreal.SourceControl()
    source_control.set_provider("Git")  # or "Perforce"
    source_control.connect()
```

## <automation>

### python initialization
```python
# init_unreal.py - auto-loaded on startup
import unreal
import sys
import os

# add project scripts to path
project_scripts = os.path.join(
    unreal.Paths.project_dir(), 
    "Scripts/Python"
)
sys.path.append(project_scripts)

# import project utilities
try:
    import project_utils
    import asset_pipeline
    import build_automation
    print("Project automation loaded successfully")
except ImportError as e:
    print(f"Failed to load project scripts: {e}")

# register startup hooks
@unreal.on_editor_startup
def on_startup():
    print(f"Project initialized: {unreal.Paths.project_name()}")
    # run startup tasks
    verify_project_integrity()
    update_asset_registry()
    check_for_updates()

@unreal.on_editor_shutdown  
def on_shutdown():
    print("Saving project state...")
    save_editor_layout()
    backup_critical_assets()
```

### build configuration
```xml
<!-- DefaultEngine.ini -->
[/Script/Engine.Engine]
+ActiveGameNameRedirects=(OldGameName="TP_Blank",NewGameName="/Script/MyProject")
+ActiveGameNameRedirects=(OldGameName="/Script/TP_Blank",NewGameName="/Script/MyProject")

[/Script/UnrealEd.ProjectPackagingSettings]
Build=IfProjectHasCode
BuildConfiguration=PPBC_Development
StagingDirectory=(Path="Builds")
FullRebuild=False
ForDistribution=False
IncludeDebugFiles=False
UsePakFile=True
bGenerateChunks=False
bChunkHardReferencesOnly=False
bBuildHttpChunkInstallData=False
HttpChunkInstallDataDirectory=(Path="")
HttpChunkInstallDataVersion=
IncludePrerequisites=True
IncludeAppLocalPrerequisites=False
bShareMaterialShaderCode=True
bSharedMaterialNativeLibraries=True
ApplocalPrerequisitesDirectory=(Path="")
IncludeCrashReporter=False
InternationalizationPreset=English
-CulturesToStage=en
+CulturesToStage=en
```

### ci/cd pipeline
```yaml
# .github/workflows/unreal-ci.yml
name: Unreal Engine CI

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: windows-latest
    
    steps:
    - uses: actions/checkout@v2
    
    - name: Setup Unreal Engine
      run: |
        # download engine if needed
        # or use pre-installed version
        
    - name: Generate Project Files
      run: |
        UnrealBuildTool.exe -projectfiles -project="MyProject.uproject"
        
    - name: Build Project
      run: |
        RunUAT.bat BuildCookRun -project="MyProject.uproject" \
          -platform=Win64 -clientconfig=Development \
          -build -cook -stage -archive
          
    - name: Run Tests
      run: |
        UnrealEditor-Cmd.exe "MyProject.uproject" \
          -ExecCmds="Automation RunTests Project" \
          -unattended -nopause -nosplash
          
    - name: Package Build
      run: |
        RunUAT.bat BuildCookRun -project="MyProject.uproject" \
          -platform=Win64 -clientconfig=Shipping \
          -cook -package -stage -archive -archivedirectory="Output"
```

## <configuration>

### project settings
```python
def configure_project_settings():
    """
    Configure optimal project settings
    """
    project_settings = unreal.ProjectSettings()
    
    # rendering settings
    project_settings.set_setting(
        "/Script/Engine.RendererSettings",
        "r.DefaultFeature.AutoExposure", False
    )
    project_settings.set_setting(
        "/Script/Engine.RendererSettings", 
        "r.DefaultFeature.MotionBlur", False
    )
    
    # enable nanite
    project_settings.set_setting(
        "/Script/Engine.RendererSettings",
        "r.Nanite", True
    )
    
    # enable lumen
    project_settings.set_setting(
        "/Script/Engine.RendererSettings",
        "r.Lumen.Enable", True
    )
    
    # world partition for large worlds
    project_settings.set_setting(
        "/Script/Engine.WorldSettings",
        "bEnableWorldPartition", True
    )
```

### platform configuration
```python
def setup_platform_targets(platforms):
    """
    Configure platform-specific settings
    """
    for platform in platforms:
        if platform == "Windows":
            setup_windows_target()
        elif platform == "Mac":
            setup_mac_target()
        elif platform == "Linux":
            setup_linux_target()
        elif platform == "Android":
            setup_android_target()
        elif platform == "iOS":
            setup_ios_target()

def setup_windows_target():
    # windows-specific settings
    settings = {
        "TargetedRHIs": ["D3D12", "D3D11"],
        "MinimumOSVersion": "Windows 10",
        "AudioDevice": "XAudio2",
        "DefaultGraphicsPerformance": "Maximum"
    }
    apply_platform_settings("Windows", settings)
```

## <validation>

### project verification
```python
def verify_project_integrity():
    """
    Comprehensive project validation
    """
    checks = []
    
    # check folder structure
    required_folders = [
        "Content", "Config", "Source", "Scripts"
    ]
    for folder in required_folders:
        path = os.path.join(unreal.Paths.project_dir(), folder)
        if os.path.exists(path):
            checks.append(f"{folder} directory exists")
        else:
            checks.append(f"{folder} directory missing")
            os.makedirs(path, exist_ok=True)
    
    # check plugins
    required_plugins = [
        "PythonScriptPlugin",
        "EditorScriptingUtilities"
    ]
    
    enabled_plugins = unreal.PluginManager.get_enabled_plugins()
    for plugin in required_plugins:
        if plugin in enabled_plugins:
            checks.append(f"{plugin} enabled")
        else:
            checks.append(f"{plugin} disabled")
            unreal.PluginManager.enable_plugin(plugin)
    
    # check engine version
    engine_version = unreal.SystemLibrary.get_engine_version()
    if engine_version >= "5.4":
        checks.append(f"Engine version {engine_version}")
    else:
        checks.append(f"Engine version {engine_version} (consider upgrading)")
    
    return checks
```

## <output>

### initialization report
```
PROJECT INITIALIZATION COMPLETE
================================
Project: MyUnrealProject
Engine: 5.6.0
Platform: Windows
Template: ThirdPerson

 - Project structure created
 - Python automation enabled
 - Build scripts configured
 - Version control initialized
 - CI/CD pipeline ready

Automation Scripts:
- init_unreal.py (loaded on startup)
- build_automation.py
- asset_pipeline.py
- test_runner.py

Next Steps:
1. Run /builder:unreal:assets to import content
2. Use /builder:unreal:blueprint for gameplay
3. Configure /builder:unreal:render for visuals
```

## <components>

<use>@file:~/.halo/components/next-command.md</use>

## <next>

### recommended workflows
- `/builder:unreal:assets` - import and optimize assets
- `/builder:unreal:blueprint` - create gameplay logic
- `/builder:unreal:python` - automate workflows
- `/builder:unreal:build` - compile and package

---

*initializes comprehensive unreal engine project with full automation setup*
