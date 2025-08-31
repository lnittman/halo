# builder:unreal:build - compilation and packaging

automated build pipeline for unreal engine projects with multi-platform support, optimization, and deployment preparation.

## <input>

- **project path**: .uproject file location
- **target platform**: win64/mac/linux/android/ios
- **build config**: debug/development/shipping
- **cook options**: maps, content, localization
- **package options**: distribution settings

## <sequence>

1. **pre-build validation**
   - verify source code
   - check dependencies
   - validate assets
   - clean intermediates

2. **compilation**
   - generate project files
   - compile c++ code
   - build shaders
   - link binaries

3. **content cooking**
   - process assets
   - optimize textures
   - compress data
   - generate paks

4. **packaging**
   - create installer
   - sign binaries
   - generate manifests
   - prepare distribution

## <automation>

### uat build pipeline
```bash
# comprehensive build command
RunUAT.bat BuildCookRun \
  -project="C:/Projects/MyGame/MyGame.uproject" \
  -platform=Win64 \
  -clientconfig=Development \
  -serverconfig=Development \
  -cook -allmaps \
  -build -stage -pak -archive \
  -archivedirectory="C:/Builds" \
  -compressed -iterate \
  -utf8output
```

### python build automation
```python
import unreal
import subprocess
import os
import json

class UnrealBuildAutomation:
    def __init__(self, project_path):
        self.project_path = project_path
        self.engine_path = unreal.Paths.engine_dir()
        self.uat_path = os.path.join(
            self.engine_path, 
            "Build/BatchFiles/RunUAT.bat"
        )
        
    def build_project(self, platform="Win64", config="Development"):
        """
        Execute full build pipeline
        """
        print(f"Building {self.project_path} for {platform}...")
        
        # clean previous builds
        self.clean_build()
        
        # generate project files
        self.generate_project_files()
        
        # compile code
        self.compile_code(platform, config)
        
        # cook content
        self.cook_content(platform)
        
        # package build
        self.package_build(platform, config)
        
        # run post-build tasks
        self.post_build_tasks()
        
    def clean_build(self):
        """
        Clean intermediate and saved folders
        """
        folders_to_clean = [
            "Intermediate",
            "Saved/Cooked",
            "Saved/StagedBuilds",
            "Binaries"
        ]
        
        project_dir = os.path.dirname(self.project_path)
        for folder in folders_to_clean:
            folder_path = os.path.join(project_dir, folder)
            if os.path.exists(folder_path):
                print(f"Cleaning {folder}...")
                shutil.rmtree(folder_path, ignore_errors=True)
                
    def generate_project_files(self):
        """
        Generate visual studio project files
        """
        ubt_path = os.path.join(
            self.engine_path,
            "Binaries/DotNET/UnrealBuildTool/UnrealBuildTool.exe"
        )
        
        cmd = [
            ubt_path,
            "-projectfiles",
            f"-project={self.project_path}",
            "-game",
            "-rocket",
            "-progress"
        ]
        
        subprocess.run(cmd, check=True)
        
    def compile_code(self, platform, config):
        """
        Compile c++ source code
        """
        cmd = [
            self.uat_path,
            "BuildCookRun",
            f"-project={self.project_path}",
            f"-platform={platform}",
            f"-clientconfig={config}",
            "-build",
            "-nocompileeditor",
            "-installed",
            "-cook",
            "-stage",
            "-archive"
        ]
        
        result = subprocess.run(cmd, capture_output=True, text=True)
        if result.returncode != 0:
            raise Exception(f"Build failed: {result.stderr}")
            
    def cook_content(self, platform):
        """
        Cook content for target platform
        """
        cook_settings = {
            "Win64": {
                "targetplatform": "WindowsClient",
                "cookflavor": "",
                "clienttargetplatform": "Windows"
            },
            "Mac": {
                "targetplatform": "Mac",
                "cookflavor": "",
                "clienttargetplatform": "Mac"
            },
            "Linux": {
                "targetplatform": "LinuxServer",
                "cookflavor": "",
                "clienttargetplatform": "Linux"
            },
            "Android": {
                "targetplatform": "Android",
                "cookflavor": "Android_ASTC",
                "clienttargetplatform": "Android"
            },
            "iOS": {
                "targetplatform": "IOS",
                "cookflavor": "",
                "clienttargetplatform": "IOS"
            }
        }
        
        settings = cook_settings.get(platform, cook_settings["Win64"])
        
        cmd = [
            os.path.join(self.engine_path, "Binaries/Win64/UnrealEditor-Cmd.exe"),
            self.project_path,
            "-run=Cook",
            f"-targetplatform={settings['targetplatform']}",
            "-iterate",
            "-unversioned",
            "-compressed",
            "-additionalcookeroptions=-deterministic"
        ]
        
        if settings['cookflavor']:
            cmd.append(f"-cookflavor={settings['cookflavor']}")
            
        subprocess.run(cmd, check=True)
```

### incremental builds
```python
def setup_incremental_build():
    """
    Configure incremental build system
    """
    build_config = {
        "bUseIncrementalBuild": True,
        "bUseUnityBuild": True,
        "bUsePCHFiles": True,
        "bUsePrecompiled": True,
        "bShareMaterialShaderCode": True,
        "bSharedMaterialNativeLibraries": True,
        "NumIncludedBytesPerUnityCPP": 384000,
        "bFastMonoCalls": True,
        "bEnableOptimization": True
    }
    
    # write to buildconfiguration.xml
    config_path = "Config/DefaultBuildSettings.ini"
    with open(config_path, 'w') as f:
        for key, value in build_config.items():
            f.write(f"{key}={value}\n")
```

## <platforms>

### windows build
```bash
# windows 64-bit shipping build
RunUAT.bat BuildCookRun \
  -project="MyGame.uproject" \
  -platform=Win64 \
  -clientconfig=Shipping \
  -cook -allmaps -compressed \
  -stage -pak -archive \
  -archivedirectory="Builds/Windows" \
  -build -CrashReporter \
  -nodebuginfo
```

### mac build
```bash
# macos universal binary
RunUAT.sh BuildCookRun \
  -project="MyGame.uproject" \
  -platform=Mac \
  -clientconfig=Shipping \
  -architectures=arm64+x86_64 \
  -cook -stage -pak -archive \
  -archivedirectory="Builds/Mac"
```

### linux build
```bash
# linux dedicated server
RunUAT.sh BuildCookRun \
  -project="MyGame.uproject" \
  -platform=Linux \
  -serverconfig=Shipping \
  -noclient -server \
  -cook -stage -pak -archive \
  -archivedirectory="Builds/Linux"
```

### mobile builds
```python
def build_mobile(platform="Android"):
    """
    Build for mobile platforms
    """
    if platform == "Android":
        cmd = [
            "RunUAT.bat", "BuildCookRun",
            "-project=MyGame.uproject",
            "-platform=Android",
            "-cookflavor=Android_ASTC",
            "-clientconfig=Shipping",
            "-targetsdkversion=33",
            "-distribution",
            "-cook", "-package", "-stage"
        ]
    elif platform == "iOS":
        cmd = [
            "RunUAT.sh", "BuildCookRun",
            "-project=MyGame.uproject",
            "-platform=IOS",
            "-clientconfig=Shipping",
            "-distribution",
            "-codebundle",
            "-cook", "-package", "-stage",
            "-archive", "-ipa"
        ]
    
    subprocess.run(cmd, check=True)
```

## <optimization>

### build performance
```python
def optimize_build_performance():
    """
    Configure build for maximum speed
    """
    optimizations = {
        # use build acceleration
        "bAllowXGE": True,
        "bAllowSNDBS": True,
        "bAllowFASTBuild": True,
        
        # parallel execution
        "MaxProcessorCount": os.cpu_count(),
        "ProcessorCountMultiplier": 1.5,
        "bAllowParallelExecutor": True,
        
        # caching
        "bUseCachedResults": True,
        "bUseSharedBuildEnvironment": True,
        "bUseSharedPCH": True,
        
        # distributed builds
        "bAllowDistcc": True,
        "bAllowDistributedCompilation": True
    }
    
    return optimizations
```

### content optimization
```python
def optimize_cooked_content():
    """
    Optimize assets during cooking
    """
    cook_options = [
        "-iterate",  # only cook changed content
        "-compressed",  # compress cooked packages
        "-additionalcookeroptions=-deterministic",
        "-additionalcookeroptions=-zenstore",  # use zen store
        "-additionalcookeroptions=-diffonly",  # only cook differences
        "-skipcookingeditorcontent",  # skip editor-only content
        "-cookall",  # cook all content
        "-unversioned"  # don't version cooked packages
    ]
    
    # texture optimization
    texture_settings = {
        "streaming_pool_size": 1000,  # mb
        "max_texture_size": 2048,
        "texture_compression": "dxt5",
        "generate_mipmaps": True
    }
    
    # mesh optimization
    mesh_settings = {
        "auto_generate_lods": True,
        "lod_count": 4,
        "reduction_settings": "aggressive",
        "use_nanite": True
    }
    
    return cook_options, texture_settings, mesh_settings
```

## <validation>

### build verification
```python
def verify_build(build_path):
    """
    Validate build output
    """
    checks = []
    
    # check executable exists
    exe_path = os.path.join(build_path, "WindowsNoEditor/MyGame.exe")
    if os.path.exists(exe_path):
        checks.append("Executable found")
        
        # check file size
        size_mb = os.path.getsize(exe_path) / (1024 * 1024)
        checks.append(f"Executable size: {size_mb:.2f} MB")
    else:
        checks.append("Executable missing")
    
    # check pak files
    pak_files = glob.glob(os.path.join(build_path, "**/*.pak"), recursive=True)
    if pak_files:
        checks.append(f"{len(pak_files)} PAK files found")
        total_size = sum(os.path.getsize(f) for f in pak_files)
        checks.append(f"Total PAK size: {total_size / (1024**3):.2f} GB")
    else:
        checks.append("No PAK files found")
    
    # check for debug symbols
    pdb_files = glob.glob(os.path.join(build_path, "**/*.pdb"), recursive=True)
    if pdb_files:
        checks.append("Debug symbols included (remove for shipping)")
    
    return checks
```

### automated testing
```python
def run_build_tests():
    """
    Execute automated tests on build
    """
    test_cmd = [
        "UnrealEditor-Cmd.exe",
        "MyGame.uproject",
        "-ExecCmds=Automation RunTests Project.Functional",
        "-unattended",
        "-nopause",
        "-nosplash",
        "-log=TestResults.log"
    ]
    
    result = subprocess.run(test_cmd, capture_output=True)
    
    # parse test results
    with open("TestResults.log", 'r') as f:
        log_content = f.read()
        
    passed = log_content.count("Test Passed")
    failed = log_content.count("Test Failed")
    
    return {
        "passed": passed,
        "failed": failed,
        "success_rate": (passed / (passed + failed)) * 100 if (passed + failed) > 0 else 0
    }
```

## <output>

### build report
```
BUILD COMPLETE
==============
Project: MyGame
Platform: Win64
Configuration: Shipping
Duration: 12m 34s

Build Stats:
- Source files compiled: 247
- Shaders compiled: 3,421
- Assets cooked: 8,532
- Package size: 2.4 GB

Optimizations Applied:
 - Unity build enabled
 - PCH usage optimized
 - Parallel compilation (16 cores)
 - Incremental cooking
 - Asset compression enabled

Test Results:
- Unit tests: 142/142 passed
- Integration tests: 38/40 passed
- Performance benchmarks: All within target

Output Location:
C:/Builds/MyGame-Win64-Shipping/
```

## <components>

<use>@file:~/.halo/components/next-command.md</use>

## <next>

### deployment workflow
- `/builder:unreal:deploy` - distribute to platforms
- `/builder:unreal:render` - generate cinematics
- `/builder:unreal:python` - automate post-build

---

*automates unreal engine build pipeline with multi-platform support*
