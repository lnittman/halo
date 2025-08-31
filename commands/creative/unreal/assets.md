# builder:unreal:assets - asset pipeline management

comprehensive asset management, optimization, and pipeline automation for unreal engine projects.

## <input>

- **asset types**: meshes/textures/materials/animations
- **source paths**: import directories or files
- **optimization level**: performance/quality/balanced
- **target platforms**: platform-specific settings
- **validation rules**: naming conventions and standards

## <sequence>

1. **asset discovery**
   - scan directories
   - identify types
   - check dependencies
   - validate naming

2. **import pipeline**
   - configure settings
   - batch import
   - apply conventions
   - generate variants

3. **optimization**
   - process textures
   - generate lods
   - optimize materials
   - compress data

## <import>

### intelligent asset importer
```python
import unreal
import os
import json
from pathlib import Path

class AssetImportPipeline:
    """
    Intelligent asset import and processing
    """
    
    def __init__(self):
        self.asset_tools = unreal.AssetToolsHelpers.get_asset_tools()
        self.editor_asset = unreal.EditorAssetLibrary
        self.import_rules = self.load_import_rules()
        
    def smart_import(self, source_directory):
        """
        Intelligently import assets with type detection
        """
        import_report = {
            "meshes": [],
            "textures": [],
            "materials": [],
            "animations": [],
            "audio": [],
            "errors": []
        }
        
        # scan directory structure
        for root, dirs, files in os.walk(source_directory):
            for file in files:
                file_path = os.path.join(root, file)
                ext = Path(file).suffix.lower()
                
                try:
                    if ext in ['.fbx', '.obj', '.dae', '.abc']:
                        result = self.import_mesh(file_path)
                        import_report["meshes"].append(result)
                        
                    elif ext in ['.png', '.jpg', '.tga', '.exr', '.hdr']:
                        result = self.import_texture(file_path)
                        import_report["textures"].append(result)
                        
                    elif ext in ['.wav', '.mp3', '.ogg', '.flac']:
                        result = self.import_audio(file_path)
                        import_report["audio"].append(result)
                        
                    elif ext == '.bvh':
                        result = self.import_animation(file_path)
                        import_report["animations"].append(result)
                        
                except Exception as e:
                    import_report["errors"].append({
                        "file": file_path,
                        "error": str(e)
                    })
                    
        # auto-generate materials
        self.generate_materials_from_textures(import_report["textures"])
        
        return import_report
    
    def import_mesh(self, file_path):
        """
        Import and configure mesh assets
        """
        # detect mesh type from naming
        mesh_name = Path(file_path).stem
        is_skeletal = any(x in mesh_name.lower() for x in ['skel', 'char', 'anim'])
        
        # create import task
        task = unreal.AssetImportTask()
        task.filename = file_path
        task.destination_path = "/Game/Meshes"
        task.automated = True
        task.save = True
        
        # configure fbx options
        options = unreal.FbxImportUI()
        
        if is_skeletal:
            # skeletal mesh settings
            options.import_mesh = True
            options.import_as_skeletal = True
            options.skeletal_mesh_import_data.import_morph_targets = True
            options.skeletal_mesh_import_data.update_skeleton_reference_pose = True
            
            # animation settings
            options.import_animations = True
            options.anim_sequence_import_data.import_bone_tracks = True
            options.anim_sequence_import_data.remove_redundant_keys = True
            
        else:
            # static mesh settings
            options.import_mesh = True
            options.import_as_skeletal = False
            options.static_mesh_import_data.combine_meshes = True
            options.static_mesh_import_data.generate_lightmap_uv = True
            options.static_mesh_import_data.auto_generate_collision = True
            options.static_mesh_import_data.remove_degenerates = True
            
            # lod settings
            options.static_mesh_import_data.auto_generate_lods = True
            
        task.options = options
        
        # execute import
        self.asset_tools.import_asset_tasks([task])
        
        # post-import processing
        imported_asset = self.editor_asset.load_asset(
            f"/Game/Meshes/{mesh_name}"
        )
        
        if imported_asset:
            self.optimize_mesh(imported_asset)
            
        return {
            "name": mesh_name,
            "type": "skeletal" if is_skeletal else "static",
            "path": f"/Game/Meshes/{mesh_name}",
            "optimized": True
        }
    
    def import_texture(self, file_path):
        """
        Import and categorize textures
        """
        texture_name = Path(file_path).stem
        
        # detect texture type from naming convention
        texture_type = self.detect_texture_type(texture_name)
        
        # create import task
        task = unreal.AssetImportTask()
        task.filename = file_path
        task.destination_path = f"/Game/Textures/{texture_type}"
        task.automated = True
        task.save = True
        
        # configure texture settings
        factory = unreal.TextureFactory()
        
        # set compression based on type
        if texture_type == "normal":
            factory.compression_settings = unreal.TextureCompressionSettings.TC_NORMALMAP
            factory.srgb = False
        elif texture_type == "mask":
            factory.compression_settings = unreal.TextureCompressionSettings.TC_MASKS
            factory.srgb = False
        elif texture_type == "hdr":
            factory.compression_settings = unreal.TextureCompressionSettings.TC_HDR
            factory.srgb = False
        else:
            factory.compression_settings = unreal.TextureCompressionSettings.TC_DEFAULT
            factory.srgb = True
            
        task.factory = factory
        
        # import
        self.asset_tools.import_asset_tasks([task])
        
        return {
            "name": texture_name,
            "type": texture_type,
            "path": f"/Game/Textures/{texture_type}/{texture_name}"
        }
    
    def detect_texture_type(self, texture_name):
        """
        Detect texture type from naming convention
        """
        name_lower = texture_name.lower()
        
        # common suffixes
        if any(x in name_lower for x in ['_n', '_normal', '_nrm']):
            return "normal"
        elif any(x in name_lower for x in ['_d', '_diffuse', '_albedo', '_color']):
            return "diffuse"
        elif any(x in name_lower for x in ['_s', '_specular', '_spec']):
            return "specular"
        elif any(x in name_lower for x in ['_r', '_roughness', '_rough']):
            return "roughness"
        elif any(x in name_lower for x in ['_m', '_metallic', '_metal']):
            return "metallic"
        elif any(x in name_lower for x in ['_ao', '_occlusion', '_ambient']):
            return "ao"
        elif any(x in name_lower for x in ['_e', '_emissive', '_emission']):
            return "emissive"
        elif any(x in name_lower for x in ['_h', '_height', '_displacement']):
            return "height"
        elif any(x in name_lower for x in ['_mask', '_alpha']):
            return "mask"
        else:
            return "misc"
```

### material generation
```python
class MaterialGenerator:
    """
    Automatic material generation from textures
    """
    
    def generate_materials_from_textures(self, imported_textures):
        """
        Create materials from texture sets
        """
        # group textures by base name
        texture_sets = self.group_texture_sets(imported_textures)
        
        materials = []
        
        for base_name, texture_set in texture_sets.items():
            # create material
            material = self.create_pbr_material(base_name, texture_set)
            materials.append(material)
            
        return materials
    
    def group_texture_sets(self, textures):
        """
        Group related textures together
        """
        texture_sets = {}
        
        for texture in textures:
            # extract base name
            base_name = texture["name"]
            for suffix in ['_d', '_n', '_r', '_m', '_ao', '_e', '_h']:
                base_name = base_name.replace(suffix, '')
                
            if base_name not in texture_sets:
                texture_sets[base_name] = {}
                
            texture_sets[base_name][texture["type"]] = texture["path"]
            
        return texture_sets
    
    def create_pbr_material(self, name, texture_set):
        """
        Create physically based material
        """
        # create material asset
        material_factory = unreal.MaterialFactoryNew()
        material = self.asset_tools.create_asset(
            f"M_{name}",
            "/Game/Materials",
            unreal.Material,
            material_factory
        )
        
        # get material editor
        material_editor = unreal.MaterialEditingLibrary
        
        # create texture sample nodes
        nodes = {}
        y_position = 0
        
        for texture_type, texture_path in texture_set.items():
            texture_asset = self.editor_asset.load_asset(texture_path)
            
            if texture_asset:
                # create texture sample node
                node = material_editor.create_material_expression(
                    material,
                    unreal.MaterialExpressionTextureSample,
                    -400, y_position
                )
                node.texture = texture_asset
                nodes[texture_type] = node
                y_position += 200
                
        # connect nodes to material outputs
        if "diffuse" in nodes:
            material_editor.connect_material_property(
                nodes["diffuse"], "RGB",
                unreal.MaterialProperty.MP_BASE_COLOR
            )
            
        if "normal" in nodes:
            material_editor.connect_material_property(
                nodes["normal"], "RGB",
                unreal.MaterialProperty.MP_NORMAL
            )
            
        if "metallic" in nodes:
            material_editor.connect_material_property(
                nodes["metallic"], "R",
                unreal.MaterialProperty.MP_METALLIC
            )
            
        if "roughness" in nodes:
            material_editor.connect_material_property(
                nodes["roughness"], "R",
                unreal.MaterialProperty.MP_ROUGHNESS
            )
            
        if "ao" in nodes:
            material_editor.connect_material_property(
                nodes["ao"], "R",
                unreal.MaterialProperty.MP_AMBIENT_OCCLUSION
            )
            
        if "emissive" in nodes:
            material_editor.connect_material_property(
                nodes["emissive"], "RGB",
                unreal.MaterialProperty.MP_EMISSIVE_COLOR
            )
            
        # compile material
        material_editor.recompile_material(material)
        
        return f"/Game/Materials/M_{name}"
```

### asset optimization
```python
class AssetOptimizer:
    """
    Comprehensive asset optimization
    """
    
    def optimize_all_assets(self):
        """
        Optimize all project assets
        """
        optimization_report = {
            "textures": self.optimize_textures(),
            "meshes": self.optimize_meshes(),
            "materials": self.optimize_materials(),
            "animations": self.optimize_animations()
        }
        
        return optimization_report
    
    def optimize_textures(self):
        """
        Batch texture optimization
        """
        all_textures = self.editor_asset.list_assets("/Game/Textures")
        
        optimizations = []
        total_saved = 0
        
        for texture_path in all_textures:
            texture = self.editor_asset.load_asset(texture_path)
            
            if isinstance(texture, unreal.Texture2D):
                original_size = texture.source.get_size_on_disk()
                
                # optimize settings
                self.apply_texture_optimization(texture)
                
                # save and measure
                self.editor_asset.save_asset(texture_path)
                new_size = texture.source.get_size_on_disk()
                
                saved = original_size - new_size
                total_saved += saved
                
                optimizations.append({
                    "asset": texture_path,
                    "original": original_size,
                    "optimized": new_size,
                    "saved": saved
                })
                
        return {
            "count": len(optimizations),
            "total_saved": total_saved,
            "details": optimizations
        }
    
    def apply_texture_optimization(self, texture):
        """
        Apply optimal texture settings
        """
        # determine optimal max size
        source_width = texture.source.get_size_x()
        source_height = texture.source.get_size_y()
        
        # round down to power of 2
        import math
        max_size = min(
            2 ** math.floor(math.log2(max(source_width, source_height))),
            2048  # cap at 2k for most textures
        )
        
        texture.max_texture_size = max_size
        
        # streaming settings
        texture.never_stream = False
        texture.global_force_mip_levels_to_be_resident = False
        
        # compression
        if texture.compression_settings == unreal.TextureCompressionSettings.TC_DEFAULT:
            texture.compression_quality = unreal.TextureCompressionQuality.TCQ_DEFAULT
            
    def optimize_meshes(self):
        """
        Optimize all mesh assets
        """
        all_meshes = self.editor_asset.list_assets("/Game/Meshes")
        
        optimizations = []
        
        for mesh_path in all_meshes:
            mesh = self.editor_asset.load_asset(mesh_path)
            
            if isinstance(mesh, unreal.StaticMesh):
                # generate lods
                self.generate_mesh_lods(mesh)
                
                # optimize collision
                self.optimize_collision(mesh)
                
                # nanite conversion if applicable
                if self.should_use_nanite(mesh):
                    self.convert_to_nanite(mesh)
                    
                optimizations.append({
                    "mesh": mesh_path,
                    "lods": mesh.get_num_lods(),
                    "nanite": mesh.nanite_settings.enabled
                })
                
        return optimizations
    
    def should_use_nanite(self, mesh):
        """
        Determine if mesh should use nanite
        """
        # check triangle count
        tri_count = mesh.get_num_triangles()
        
        # use nanite for high-poly meshes
        return tri_count > 10000
    
    def convert_to_nanite(self, mesh):
        """
        Convert mesh to nanite
        """
        nanite_settings = mesh.nanite_settings
        nanite_settings.enabled = True
        nanite_settings.position_precision = 1.0
        nanite_settings.percent_triangles = 1.0
        
        # apply settings
        unreal.EditorStaticMeshLibrary.set_nanite_settings(
            mesh, nanite_settings
        )
```

### validation system
```python
class AssetValidation:
    """
    Asset validation and compliance
    """
    
    def validate_all_assets(self):
        """
        Comprehensive asset validation
        """
        validation_results = {
            "naming_conventions": self.check_naming_conventions(),
            "texture_sizes": self.check_texture_sizes(),
            "poly_counts": self.check_poly_counts(),
            "material_complexity": self.check_material_complexity(),
            "missing_assets": self.find_missing_references()
        }
        
        return validation_results
    
    def check_naming_conventions(self):
        """
        Validate asset naming
        """
        rules = {
            "StaticMesh": "SM_",
            "SkeletalMesh": "SK_",
            "Texture2D": "T_",
            "Material": "M_",
            "MaterialInstance": "MI_",
            "Blueprint": "BP_",
            "AnimationSequence": "AS_",
            "ParticleSystem": "PS_"
        }
        
        violations = []
        
        all_assets = self.editor_asset.list_assets("/Game")
        
        for asset_path in all_assets:
            asset = self.editor_asset.load_asset(asset_path)
            asset_name = Path(asset_path).name
            asset_type = asset.__class__.__name__
            
            if asset_type in rules:
                expected_prefix = rules[asset_type]
                if not asset_name.startswith(expected_prefix):
                    violations.append({
                        "asset": asset_path,
                        "type": asset_type,
                        "expected": expected_prefix,
                        "actual": asset_name
                    })
                    
        return violations
    
    def check_texture_sizes(self):
        """
        Check for oversized textures
        """
        oversized = []
        max_size = 4096
        
        textures = self.editor_asset.list_assets("/Game/Textures")
        
        for texture_path in textures:
            texture = self.editor_asset.load_asset(texture_path)
            
            if isinstance(texture, unreal.Texture2D):
                width = texture.source.get_size_x()
                height = texture.source.get_size_y()
                
                if width > max_size or height > max_size:
                    oversized.append({
                        "texture": texture_path,
                        "size": f"{width}x{height}",
                        "recommended": f"{max_size}x{max_size}"
                    })
                    
        return oversized
```

## <output>

### asset pipeline report
```
ASSET PIPELINE COMPLETE
=======================
Import Summary:
- Meshes: 156 imported (142 static, 14 skeletal)
- Textures: 523 imported (categorized by type)
- Materials: 89 generated
- Animations: 34 imported

Optimization Results:
 - Texture memory reduced: 847 MB → 512 MB (-40%)
 - LODs generated: 142 meshes
 - Nanite enabled: 23 high-poly meshes
 - Materials optimized: 89

Validation Report:
Warning: Naming violations: 12 assets
Warning: Oversized textures: 3 (>4K)
 - Poly counts: All within budget
 - Material complexity: Acceptable
 - Missing references: None

Storage Summary:
- Total assets: 802
- Disk usage: 3.2 GB
- Cooked size: 1.8 GB
- Compression: 44%

Performance Impact:
- Load time improved: -2.3s
- Draw calls reduced: -28%
- Memory usage optimized: -35%
```

## <components>

<use>@file:~/.halo/components/next-command.md</use>

## <next>

### asset workflows
- `/builder:unreal:python` - automate processing
- `/builder:unreal:build` - compile with assets
- `/3d-artist` - create new assets

---

*comprehensive asset pipeline management for unreal engine*
