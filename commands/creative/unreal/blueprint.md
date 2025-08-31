# builder:unreal:blueprint - visual scripting

comprehensive blueprint development for gameplay, ui, and automation with visual scripting best practices.

## <input>

- **blueprint type**: actor/component/interface/widget
- **functionality**: gameplay logic requirements
- **inheritance**: parent classes and interfaces
- **replication**: multiplayer considerations
- **optimization**: performance targets

## <sequence>

1. **blueprint architecture**
   - design class hierarchy
   - define interfaces
   - plan component structure
   - establish communication

2. **implementation**
   - create base classes
   - implement logic
   - wire events
   - configure properties

3. **optimization**
   - profile performance
   - reduce tick usage
   - optimize bindings
   - minimize casting

## <creation>

### blueprint generation
```python
import unreal

def create_gameplay_blueprint(name, parent_class=unreal.Actor):
    """
    Create optimized gameplay blueprint
    """
    # create blueprint factory
    factory = unreal.BlueprintFactory()
    factory.parent_class = parent_class
    
    # generate blueprint asset
    asset_tools = unreal.AssetToolsHelpers.get_asset_tools()
    blueprint = asset_tools.create_asset(
        asset_name=f"BP_{name}",
        package_path="/Game/Blueprints",
        asset_class=unreal.Blueprint,
        factory=factory
    )
    
    # get subsystem for component manipulation
    subsystem = unreal.get_engine_subsystem(unreal.SubobjectDataSubsystem)
    root_data = subsystem.k2_gather_subobject_data_for_blueprint(blueprint)[0]
    
    # add components
    components = [
        ("StaticMesh", unreal.StaticMeshComponent),
        ("Collision", unreal.BoxComponent),
        ("Audio", unreal.AudioComponent),
        ("Particle", unreal.ParticleSystemComponent)
    ]
    
    for comp_name, comp_class in components:
        comp_data, _ = subsystem.add_new_subobject(
            comp_class,
            root_data
        )
        subsystem.rename_subobject(comp_data, comp_name)
    
    return blueprint
```

### component blueprint
```python
def create_component_blueprint(name, functionality):
    """
    Create reusable component blueprint
    """
    factory = unreal.BlueprintFactory()
    factory.parent_class = unreal.ActorComponent
    
    blueprint = create_asset(
        f"BPC_{name}",
        "/Game/Blueprints/Components",
        factory
    )
    
    # add variables
    variables = {
        "Health": ("float", 100.0),
        "MaxHealth": ("float", 100.0),
        "IsActive": ("bool", True),
        "Tags": ("array", [])
    }
    
    for var_name, (var_type, default) in variables.items():
        add_blueprint_variable(blueprint, var_name, var_type, default)
    
    # add functions
    functions = [
        "Initialize",
        "UpdateState",
        "Cleanup"
    ]
    
    for func_name in functions:
        add_blueprint_function(blueprint, func_name)
    
    return blueprint
```

## <patterns>

### event-driven architecture
```python
# blueprint communication patterns
class BlueprintPatterns:
    @staticmethod
    def setup_event_dispatcher(blueprint):
        """
        Create event dispatcher for decoupled communication
        """
        dispatcher = unreal.EventDispatcher()
        dispatcher.name = "OnStateChanged"
        dispatcher.parameters = [
            ("NewState", "enum"),
            ("PreviousState", "enum")
        ]
        blueprint.add_event_dispatcher(dispatcher)
    
    @staticmethod
    def implement_interface(blueprint, interface_class):
        """
        Implement blueprint interface
        """
        blueprint.implemented_interfaces.append(interface_class)
        
        # implement required functions
        for func in interface_class.get_functions():
            implement_interface_function(blueprint, func)
    
    @staticmethod
    def create_state_machine(blueprint):
        """
        Setup state machine pattern
        """
        states = [
            "Idle",
            "Active", 
            "Cooldown",
            "Disabled"
        ]
        
        # create enum
        state_enum = create_enum("EGameplayState", states)
        
        # add state variable
        add_variable(blueprint, "CurrentState", state_enum)
        
        # create transition functions
        for state in states:
            add_function(blueprint, f"Enter{state}")
            add_function(blueprint, f"Exit{state}")
            add_function(blueprint, f"Update{state}")
```

### optimization techniques
```python
def optimize_blueprint(blueprint):
    """
    Apply blueprint optimization best practices
    """
    optimizations = []
    
    # disable tick where possible
    blueprint.set_editor_property("bCanEverTick", False)
    optimizations.append("Tick disabled")
    
    # use timers instead of tick
    if needs_periodic_update(blueprint):
        setup_timer_based_updates(blueprint)
        optimizations.append("Timer-based updates")
    
    # optimize bindings
    for binding in blueprint.get_bindings():
        if binding.is_pure:
            continue  # pure functions are ok
        
        # convert to cached value
        cache_binding_result(binding)
        optimizations.append(f"Cached binding: {binding.name}")
    
    # reduce casting
    for node in blueprint.get_nodes():
        if node.type == "Cast":
            if can_use_interface(node):
                replace_with_interface(node)
                optimizations.append(f"Replaced cast: {node.target}")
    
    # component activation
    for component in blueprint.get_components():
        if not component.always_needed:
            component.auto_activate = False
            optimizations.append(f"Lazy activation: {component.name}")
    
    return optimizations
```

## <widget>

### ui widget blueprint
```python
def create_ui_widget(name, widget_type="HUD"):
    """
    Create optimized ui widget blueprint
    """
    factory = unreal.WidgetBlueprintFactory()
    factory.parent_class = unreal.UserWidget
    
    widget = create_asset(
        f"WBP_{name}",
        "/Game/UI",
        factory
    )
    
    # add ui elements
    if widget_type == "HUD":
        add_hud_elements(widget)
    elif widget_type == "Menu":
        add_menu_elements(widget)
    elif widget_type == "Inventory":
        add_inventory_elements(widget)
    
    # setup bindings
    setup_ui_bindings(widget)
    
    # optimize for performance
    widget.set_editor_property("bIsFocusable", False)
    widget.set_editor_property("Visibility", "HitTestInvisible")
    
    return widget

def add_hud_elements(widget):
    """
    Add standard hud elements
    """
    elements = [
        ("HealthBar", "ProgressBar"),
        ("AmmoCounter", "TextBlock"),
        ("Minimap", "Image"),
        ("Crosshair", "Image")
    ]
    
    for element_name, element_type in elements:
        add_widget_element(widget, element_name, element_type)
```

## <multiplayer>

### replicated blueprint
```python
def setup_replication(blueprint):
    """
    Configure blueprint for multiplayer
    """
    # enable replication
    blueprint.set_editor_property("bReplicates", True)
    
    # setup replicated variables
    replicated_vars = [
        ("Health", "RepNotify"),
        ("Position", "Reliable"),
        ("State", "RepNotify")
    ]
    
    for var_name, rep_type in replicated_vars:
        var = blueprint.get_variable(var_name)
        var.replication = rep_type
        
        if rep_type == "RepNotify":
            # create onrep function
            add_function(blueprint, f"OnRep_{var_name}")
    
    # setup rpcs
    rpcs = [
        ("ServerFire", "Server", "Reliable"),
        ("MulticastExplosion", "Multicast", "Unreliable"),
        ("ClientNotification", "Client", "Reliable")
    ]
    
    for rpc_name, target, reliability in rpcs:
        func = add_function(blueprint, rpc_name)
        func.rpc_target = target
        func.rpc_reliability = reliability
```

## <debugging>

### blueprint debugging
```python
def add_debug_visualization(blueprint):
    """
    Add debug helpers to blueprint
    """
    # add debug variables
    debug_vars = [
        ("bShowDebug", "bool", False),
        ("DebugColor", "color", "(R=1,G=0,B=0,A=1)"),
        ("DebugDuration", "float", 2.0)
    ]
    
    for var_name, var_type, default in debug_vars:
        add_variable(blueprint, var_name, var_type, default)
    
    # add debug drawing
    debug_functions = """
    void DrawDebugInfo()
    {
        if (!bShowDebug) return;
        
        // draw debug sphere
        DrawDebugSphere(
            GetWorld(),
            GetActorLocation(),
            100.0f,
            12,
            DebugColor,
            false,
            DebugDuration
        );
        
        // print debug string
        UE_LOG(LogTemp, Warning, TEXT("Actor State: %s"), 
               *GetStateString());
    }
    """
    
    add_blueprint_code(blueprint, debug_functions)
```

## <output>

### blueprint report
```
BLUEPRINT CREATED
================
Name: BP_GameplayActor
Parent: AActor
Path: /Game/Blueprints/BP_GameplayActor

Components:
- StaticMeshComponent (Root)
- BoxComponent (Collision)
- AudioComponent
- ParticleSystemComponent

Variables:
- Health (Float, Replicated)
- MaxHealth (Float)
- CurrentState (Enum)
- Tags (Array<Name>)

Functions:
- BeginPlay (Override)
- Tick (Disabled)
- TakeDamage (Override)
- OnStateChanged (Event)

Optimizations Applied:
 - Tick disabled
 - Timer-based updates
 - Cached property bindings
 - Interface-based communication
 - Lazy component activation

Replication:
 - Replicated properties configured
 - RPCs implemented
 - Network optimization applied
```

## <components>

<use>@file:~/.halo/components/next-command.md</use>

## <next>

### workflow continuation
- `/builder:unreal:python` - add automation scripts
- `/builder:unreal:render` - setup visual effects
- `/builder:unreal:build` - compile blueprint project

---

*creates optimized blueprints with visual scripting best practices*
