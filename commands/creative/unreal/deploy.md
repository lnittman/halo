# builder:unreal:deploy - packaging and distribution

comprehensive deployment pipeline for unreal engine projects across all platforms with optimization and distribution.

## <input>

- **target platforms**: win/mac/linux/console/mobile/vr
- **build type**: development/shipping/distribution
- **deployment method**: store/direct/cloud/enterprise
- **certification**: platform requirements
- **distribution**: steam/epic/app stores

## <sequence>

1. **pre-deployment**
   - validate project
   - check requirements
   - prepare assets
   - configure settings

2. **packaging**
   - build executables
   - create installers
   - sign binaries
   - generate manifests

3. **distribution**
   - upload to stores
   - deploy to cloud
   - create patches
   - manage versions

## <packaging>

### multi-platform packaging
```python
import unreal
import subprocess
import os
import json

class DeploymentPipeline:
    """
    Automated deployment for all platforms
    """
    
    def __init__(self, project_path):
        self.project_path = project_path
        self.engine_path = unreal.Paths.engine_dir()
        self.uat_path = os.path.join(
            self.engine_path,
            "Build/BatchFiles/RunUAT.bat"
        )
        
    def deploy_all_platforms(self, platforms, config="Shipping"):
        """
        Deploy to multiple platforms
        """
        deployment_results = {}
        
        for platform in platforms:
            print(f"Deploying for {platform}...")
            
            if platform == "Windows":
                result = self.deploy_windows(config)
            elif platform == "Mac":
                result = self.deploy_mac(config)
            elif platform == "Linux":
                result = self.deploy_linux(config)
            elif platform == "Android":
                result = self.deploy_android(config)
            elif platform == "iOS":
                result = self.deploy_ios(config)
            elif platform == "Steam":
                result = self.deploy_steam(config)
            elif platform == "EpicGames":
                result = self.deploy_epic(config)
            else:
                result = {"error": f"Unknown platform: {platform}"}
                
            deployment_results[platform] = result
            
        return deployment_results
    
    def deploy_windows(self, config):
        """
        Windows deployment with installer
        """
        # package for windows
        cmd = [
            self.uat_path,
            "BuildCookRun",
            f"-project={self.project_path}",
            "-platform=Win64",
            f"-clientconfig={config}",
            "-cook", "-allmaps",
            "-build", "-stage", "-pak", "-archive",
            "-archivedirectory=Builds/Windows",
            "-compressed", "-distribution"
        ]
        
        result = subprocess.run(cmd, capture_output=True)
        
        if result.returncode == 0:
            # create installer
            installer_path = self.create_windows_installer()
            
            # sign executable
            self.sign_windows_binary(installer_path)
            
            return {
                "success": True,
                "installer": installer_path,
                "size": os.path.getsize(installer_path)
            }
            
        return {"success": False, "error": result.stderr}
    
    def create_windows_installer(self):
        """
        Create nsis installer for windows
        """
        nsis_script = """
        !define PRODUCT_NAME "MyGame"
        !define PRODUCT_VERSION "1.0.0"
        !define PRODUCT_PUBLISHER "MyCompany"
        
        Name "${PRODUCT_NAME}"
        OutFile "Setup_${PRODUCT_NAME}_${PRODUCT_VERSION}.exe"
        InstallDir "$PROGRAMFILES64\\${PRODUCT_NAME}"
        
        Section "Main"
            SetOutPath "$INSTDIR"
            File /r "Builds\\Windows\\*.*"
            
            ; Create shortcuts
            CreateDirectory "$SMPROGRAMS\\${PRODUCT_NAME}"
            CreateShortCut "$SMPROGRAMS\\${PRODUCT_NAME}\\${PRODUCT_NAME}.lnk" \
                          "$INSTDIR\\${PRODUCT_NAME}.exe"
            CreateShortCut "$DESKTOP\\${PRODUCT_NAME}.lnk" \
                          "$INSTDIR\\${PRODUCT_NAME}.exe"
            
            ; Write uninstaller
            WriteUninstaller "$INSTDIR\\Uninstall.exe"
            
            ; Registry keys
            WriteRegStr HKLM "Software\\${PRODUCT_PUBLISHER}\\${PRODUCT_NAME}" \
                        "InstallDir" "$INSTDIR"
            WriteRegStr HKLM "Software\\${PRODUCT_PUBLISHER}\\${PRODUCT_NAME}" \
                        "Version" "${PRODUCT_VERSION}"
        SectionEnd
        
        Section "Uninstall"
            Delete "$INSTDIR\\*.*"
            RMDir /r "$INSTDIR"
            Delete "$SMPROGRAMS\\${PRODUCT_NAME}\\*.*"
            RMDir "$SMPROGRAMS\\${PRODUCT_NAME}"
            Delete "$DESKTOP\\${PRODUCT_NAME}.lnk"
            DeleteRegKey HKLM "Software\\${PRODUCT_PUBLISHER}\\${PRODUCT_NAME}"
        SectionEnd
        """
        
        # write nsis script
        script_path = "installer.nsi"
        with open(script_path, 'w') as f:
            f.write(nsis_script)
            
        # compile installer
        subprocess.run(["makensis", script_path])
        
        return f"Setup_MyGame_1.0.0.exe"
    
    def sign_windows_binary(self, exe_path):
        """
        Sign windows executable
        """
        # use signtool with certificate
        cmd = [
            "signtool", "sign",
            "/f", "certificate.pfx",
            "/p", os.environ.get("CERT_PASSWORD", ""),
            "/t", "http://timestamp.digicert.com",
            "/d", "MyGame",
            exe_path
        ]
        
        subprocess.run(cmd)
```

### mobile deployment
```python
class MobileDeployment:
    """
    Mobile platform deployment
    """
    
    def deploy_android(self, config):
        """
        Android apk/aab deployment
        """
        # configure android settings
        android_config = {
            "package_name": "com.company.mygame",
            "version_code": 1,
            "version_name": "1.0.0",
            "min_sdk": 21,
            "target_sdk": 33,
            "permissions": [
                "android.permission.INTERNET",
                "android.permission.ACCESS_NETWORK_STATE"
            ]
        }
        
        # build for android
        cmd = [
            "RunUAT.bat", "BuildCookRun",
            "-project=MyGame.uproject",
            "-platform=Android",
            "-cookflavor=Android_ASTC",
            f"-clientconfig={config}",
            "-targetsdkversion=33",
            "-build", "-cook", "-package", "-stage",
            "-distribution"
        ]
        
        # build apk
        subprocess.run(cmd + ["-packagetype=apk"])
        
        # build aab for google play
        subprocess.run(cmd + ["-packagetype=aab"])
        
        # sign with release key
        self.sign_android_package()
        
        return {
            "apk": "MyGame.apk",
            "aab": "MyGame.aab",
            "ready_for_store": True
        }
    
    def deploy_ios(self, config):
        """
        iOS ipa deployment
        """
        # ios configuration
        ios_config = {
            "bundle_identifier": "com.company.mygame",
            "version": "1.0.0",
            "build": "1",
            "minimum_ios": "12.0",
            "device_families": ["iPhone", "iPad"]
        }
        
        # build for ios
        cmd = [
            "RunUAT.sh", "BuildCookRun",
            "-project=MyGame.uproject",
            "-platform=IOS",
            f"-clientconfig={config}",
            "-build", "-cook", "-package", "-stage",
            "-distribution",
            "-archive", "-ipa",
            "-provision=Distribution.mobileprovision",
            "-certificate=iPhone Distribution"
        ]
        
        result = subprocess.run(cmd, capture_output=True)
        
        if result.returncode == 0:
            # validate with app store
            validation = self.validate_ios_app()
            
            # upload to testflight
            if validation["valid"]:
                self.upload_to_testflight()
                
            return {
                "ipa": "MyGame.ipa",
                "validated": validation["valid"],
                "testflight": True
            }
            
        return {"success": False}
    
    def validate_ios_app(self):
        """
        Validate ios app for app store
        """
        cmd = [
            "xcrun", "altool",
            "--validate-app",
            "-f", "MyGame.ipa",
            "-u", "apple_id@example.com",
            "-p", "@keychain:AC_PASSWORD"
        ]
        
        result = subprocess.run(cmd, capture_output=True)
        
        return {
            "valid": result.returncode == 0,
            "issues": result.stderr.decode() if result.returncode != 0 else None
        }
```

### store deployment
```python
class StoreDeployment:
    """
    Deploy to digital stores
    """
    
    def deploy_to_steam(self, app_id):
        """
        Steam deployment via steamcmd
        """
        # create app manifest
        vdf_content = f"""
        "AppBuild"
        {{
            "AppID" "{app_id}"
            "Desc" "MyGame Release Build"
            "ContentRoot" "./Builds/Windows/"
            "BuildOutput" "./BuildOutput/"
            
            "Depots"
            {{
                "{app_id + 1}"
                {{
                    "FileMapping"
                    {{
                        "LocalPath" "*"
                        "DepotPath" "."
                        "Recursive" "1"
                    }}
                }}
            }}
        }}
        """
        
        # write vdf file
        with open("app_build.vdf", 'w') as f:
            f.write(vdf_content)
            
        # upload to steam
        cmd = [
            "steamcmd",
            "+login", "steam_username",
            "+run_app_build", "app_build.vdf",
            "+quit"
        ]
        
        subprocess.run(cmd)
        
        return {"uploaded": True, "app_id": app_id}
    
    def deploy_to_epic(self, product_id):
        """
        Epic games store deployment
        """
        # use buildpatchtools
        cmd = [
            "BuildPatchTool.exe",
            "-mode=PatchGeneration",
            "-BuildRoot=Builds/Windows",
            "-CloudDir=EpicCloud",
            "-AppName=MyGame",
            "-AppLaunch=MyGame.exe",
            "-AppArgs=\"\"",
            "-BuildVersion=1.0.0"
        ]
        
        subprocess.run(cmd)
        
        # upload to epic backend
        upload_cmd = [
            "BuildPatchTool.exe",
            "-mode=ChunkUpload",
            "-CloudDir=EpicCloud",
            "-AppName=MyGame",
            "-ProductId=" + product_id
        ]
        
        subprocess.run(upload_cmd)
        
        return {"uploaded": True, "product_id": product_id}
```

### cloud deployment
```python
class CloudDeployment:
    """
    Deploy to cloud platforms
    """
    
    def deploy_to_aws(self, region="us-east-1"):
        """
        Deploy to aws gamelift
        """
        import boto3
        
        gamelift = boto3.client('gamelift', region_name=region)
        
        # upload build
        build_response = gamelift.create_build(
            Name="MyGame-Build",
            Version="1.0.0",
            StorageLocation={
                'Bucket': 'mygame-builds',
                'Key': 'builds/mygame-server.zip'
            },
            OperatingSystem='WINDOWS_2016'
        )
        
        build_id = build_response['Build']['BuildId']
        
        # create fleet
        fleet_response = gamelift.create_fleet(
            Name="MyGame-Fleet",
            BuildId=build_id,
            EC2InstanceType='c5.large',
            RuntimeConfiguration={
                'ServerProcesses': [
                    {
                        'LaunchPath': '/local/game/MyGameServer.exe',
                        'Parameters': '-log',
                        'ConcurrentExecutions': 1
                    }
                ]
            }
        )
        
        return {
            "build_id": build_id,
            "fleet_id": fleet_response['FleetAttributes']['FleetId'],
            "status": "deploying"
        }
    
    def deploy_to_playfab(self):
        """
        Deploy to azure playfab
        """
        # use playfab multiplayer servers
        config = {
            "BuildName": "MyGame-Build",
            "ContainerFlavor": "CustomLinux",
            "VmSize": "Standard_D2as_v4",
            "MultiplayerServerCountPerVm": 1,
            "Ports": [
                {"Name": "game", "Num": 7777, "Protocol": "UDP"}
            ],
            "Regions": [
                {"Region": "EastUs", "MaxServers": 10}
            ]
        }
        
        # upload via playfab api
        # implementation details...
        
        return {"deployed": True}
```

### version management
```python
class VersionManagement:
    """
    Handle versioning and patches
    """
    
    def create_patch(self, base_version, new_version):
        """
        Create differential patch
        """
        # use unreal pak tool
        cmd = [
            "UnrealPak.exe",
            f"Patch_{base_version}_to_{new_version}.pak",
            "-Create=PatchList.txt",
            "-Compress",
            "-Diff",
            f"-DiffBase=Builds/v{base_version}"
        ]
        
        subprocess.run(cmd)
        
        # create manifest
        manifest = {
            "from_version": base_version,
            "to_version": new_version,
            "patch_file": f"Patch_{base_version}_to_{new_version}.pak",
            "size": os.path.getsize(f"Patch_{base_version}_to_{new_version}.pak"),
            "checksum": self.calculate_checksum()
        }
        
        return manifest
    
    def setup_auto_update(self):
        """
        Configure auto-update system
        """
        update_config = {
            "update_server": "https://updates.mygame.com",
            "check_interval": 3600,
            "auto_download": True,
            "auto_install": False,
            "channels": ["stable", "beta", "experimental"]
        }
        
        return update_config
```

## <output>

### deployment summary
```
DEPLOYMENT COMPLETE
===================
Version: 1.0.0
Build: 20240315-1234

Platform Deployments:
 - Windows - Setup.exe (2.4 GB)
 - Mac - MyGame.app (2.6 GB)
 - Linux - MyGame.tar.gz (2.3 GB)
 - Android - MyGame.aab (1.8 GB)
 - iOS - MyGame.ipa (1.9 GB)

Store Status:
 - Steam - Uploaded (AppID: 123456)
 - Epic Games - Published
 - Google Play - In Review
 - App Store - TestFlight Ready

Cloud Deployment:
 - AWS GameLift - 10 instances running
 - PlayFab - 5 regions active

Patch System:
- Base Version: 1.0.0
- Patch Ready: No
- Auto-Update: Configured

Distribution URLs:
- Direct: https://download.mygame.com
- CDN: https://cdn.mygame.com
- Mirror: https://mirror.mygame.com
```

## <components>

<use>@file:~/.halo/components/next-command.md</use>

## <next>

### post-deployment
- monitor analytics
- gather feedback
- prepare patches
- plan updates

---

*comprehensive deployment pipeline for unreal engine projects*
