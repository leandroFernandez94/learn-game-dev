# Lesson 0: GDScript Primer for JavaScript Developers

> **Branch**: `lesson-00-gdscript-primer-finished`  
> **Prerequisites**: JavaScript/TypeScript experience  
> **Estimated Time**: 15-20 minutes

## Concepts Learned

- **GDScript syntax fundamentals**: Variables, types, functions, and control flow in GDScript vs JavaScript
- **Godot-specific features**: Signals, node access with `$`, `@export` and `@onready` decorators
- **Type system**: Optional static typing with explicit type hints and type inference
- **Object-oriented patterns**: How GDScript extends node types rather than standalone classes
- **Async handling**: Using `await` with signals instead of promises
- **Common gotchas**: Differences in equality, null checking, and truthiness from JavaScript

### What You Learned

- How to declare variables with proper type hints using `:` and `:=`
- Function syntax with `func` keyword and return type annotations
- Control flow with `if/elif/else` and the powerful `match` statement
- Array and Dictionary operations with `.append()` and `.size()`
- Signal system for event-driven programming
- Node tree navigation with `$` shorthand and `get_node()`
- Export variables for Inspector integration with `@export`

## Key Code Patterns

### Pattern 1: Type-Safe Variable Declaration

**Purpose**: Catch bugs early with explicit typing while maintaining readability

```gdscript
# Type inference with := (recommended for clarity)
var player_name := "Hero"  # String inferred
var health := 100          # int inferred
var speed := 5.5           # float inferred

# Explicit types (best for function parameters and complex types)
var health: int = 100
var velocity: Vector2 = Vector2.ZERO
var enemies: Array[Node2D] = []

# Constants (always typed, UPPER_CASE convention)
const MAX_HEALTH: int = 100
const GRAVITY: float = 980.0
```

**Key Takeaways**:
- Use `:=` for simple assignments where type is obvious
- Use explicit types for function signatures and public APIs
- Constants use `const` and UPPER_CASE naming
- Similar to TypeScript but syntax is slightly different

### Pattern 2: Function Signatures with Return Types

**Purpose**: Document function behavior and enable type checking

```gdscript
# No return value (void)
func take_damage(amount: int) -> void:
    health -= amount
    if health <= 0:
        die()

# Return value with type
func calculate_damage(base_damage: int, multiplier: float) -> int:
    return int(base_damage * multiplier)

# Default parameters
func heal(amount: int = 10) -> void:
    health = min(health + amount, MAX_HEALTH)

# Multiple return values using Array
func get_stats() -> Array:
    return [health, max_health, speed]
```

**Key Takeaways**:
- Always specify return type with `-> Type`
- Use `-> void` when function doesn't return
- Default parameters work like JavaScript
- No tuple unpacking; use Arrays for multiple returns

### Pattern 3: Match Statement (Enhanced Switch)

**Purpose**: Pattern matching for cleaner control flow than switch/case

```gdscript
# Simple matching
match player_state:
    PlayerState.IDLE:
        play_idle_animation()
    PlayerState.RUNNING:
        play_run_animation()
    PlayerState.JUMPING:
        play_jump_animation()
    _:  # Default case (underscore)
        print("Unknown state")

# Pattern matching with values
match health:
    0:
        die()
    var n when n < 30:  # Guard condition
        show_low_health_warning()
    var n when n >= 100:
        health = 100  # Cap at max
    _:
        pass  # Normal health range

# Matching arrays/tuples
match [input_x, input_y]:
    [0, 0]:
        state = "idle"
    [_, 0]:  # Any X, Y is 0
        state = "moving_horizontal"
    [0, _]:  # X is 0, any Y
        state = "moving_vertical"
    _:
        state = "moving_diagonal"
```

**Key Takeaways**:
- More powerful than JavaScript's `switch`
- No `break` needed (doesn't fall through)
- Can match patterns, not just values
- Guard conditions with `when` clause

### Pattern 4: Signal-Based Events

**Purpose**: Type-safe, editor-integrated event system

```gdscript
# Define signals at class level
signal health_changed(new_health: int, old_health: int)
signal died
signal power_up_collected(power_up_type: String)

# Emit signals when events occur
func take_damage(amount: int) -> void:
    var old_health = health
    health -= amount
    health_changed.emit(health, old_health)  # Godot 4.x syntax
    
    if health <= 0:
        died.emit()

# In another script, connect to signals
func _ready():
    # Connect using method reference
    player.health_changed.connect(_on_player_health_changed)
    player.died.connect(_on_player_died)

# Callback functions (convention: prefix with _on_)
func _on_player_health_changed(new_health: int, old_health: int) -> void:
    health_bar.value = new_health
    if new_health < old_health:
        play_hurt_sound()

func _on_player_died() -> void:
    game_over_screen.show()
```

**Key Takeaways**:
- Signals are like events but type-safe and editor-visible
- Define with `signal` keyword at top of script
- Emit with `.emit()` method (Godot 4.x)
- Connect with `.connect(method_reference)`
- Convention: callback methods start with `_on_`

### Pattern 5: Node References with @onready

**Purpose**: Safely reference child nodes after scene tree is ready

```gdscript
extends CharacterBody2D

# @onready ensures node exists before assignment
@onready var sprite: Sprite2D = $Sprite2D
@onready var collision: CollisionShape2D = $CollisionShape2D
@onready var animation_player: AnimationPlayer = $AnimationPlayer

# Path navigation (../ for parent, / for children)
@onready var hud: CanvasLayer = $"../HUD"
@onready var health_label: Label = $"../HUD/HealthLabel"

# Alternative: get_node() longhand
@onready var sprite: Sprite2D = get_node("Sprite2D")

func _ready():
    # Nodes are guaranteed to be assigned here
    sprite.modulate = Color.BLUE
    animation_player.play("idle")
```

**Key Takeaways**:
- `@onready` delays assignment until `_ready()` is called
- `$NodeName` is shorthand for `get_node("NodeName")`
- Always use `@onready` when caching node references
- Type hint node references for autocomplete
- Similar to React's `useRef` but for scene tree

### Godot-Specific Idioms

- **Lifecycle methods**: `_init()` (constructor), `_ready()` (component mounted), `_process()` (update loop)
- **Node paths**: Use `$` for children, `../` for parent, `get_tree()` for scene root
- **Groups**: Tag nodes with groups using editor, retrieve with `get_tree().get_nodes_in_group("enemies")`
- **Yield/Await**: Use `await signal_name` to wait for events (replaces `yield` from Godot 3.x)
- **Export variables**: `@export` makes variables editable in Inspector (unique to game engines)

## Historical Context

### Evolution of Game Scripting Languages

**Early Era (1980s-1990s)**: Games were written entirely in assembly or C. No scripting layer existed—every behavior was hardcoded. This made iteration slow and required programmers for all content changes.

**Scripting Revolution (Late 1990s)**: Games like Quake introduced QuakeC, separating game logic from engine code. This allowed:
- Faster iteration (no recompilation)
- Modding communities (Half-Life's impact)
- Non-programmers could create content

**Modern Era (2000s-2020s)**:
- **Lua**: Became industry standard (World of Warcraft, Roblox) for lightweight embedding
- **Python**: Used in Blender, Panda3D for its readability
- **C#**: Unity's choice, bringing full .NET features
- **JavaScript**: Used in web games (Phaser, Three.js) and Node.js game servers

### Why GDScript Exists

**Godot's Philosophy**: Rather than embedding an existing language, Godot created GDScript specifically for game development:

1. **Tight Engine Integration**: Direct access to Godot's node system without bindings
2. **Editor Integration**: Properties appear in Inspector automatically with `@export`
3. **Performance Balance**: Faster than Python, good enough for most games (C++ available for bottlenecks)
4. **Low Learning Curve**: Python-like syntax familiar to many developers
5. **Debugging**: Built-in debugger integrated with editor

**Compared to Unity's C#**: C# is more powerful but requires understanding .NET framework. GDScript sacrifices some features for simplicity and editor integration.

**Compared to Unreal's Blueprints**: GDScript is text-based while Blueprints are visual. Text is faster for experienced programmers but less accessible to artists.

### Signal Pattern Origins

The **signal/slot pattern** comes from Qt framework (1995):
- **Problem**: Tight coupling between UI and logic
- **Solution**: Signals declare "something happened", slots subscribe without knowing the source
- **Impact**: Became standard in game engines (Unity's Events, Unreal's Delegates)

Godot's signals are particularly elegant because they're:
- **First-class language feature** (not library code)
- **Editor-visible** (can connect in Inspector, not just code)
- **Type-safe** (unlike string-based event systems)

This pattern allows loose coupling—critical for complex games where many systems need to react to player actions without directly referencing each other.

## Common Pitfalls

### Pitfall 1: Forgetting Type Hints

**Problem**: Untyped code loses autocomplete and catches fewer bugs

```gdscript
# Bad: No type hints
var player
var health = 100

func get_player():
    return player  # What type is this?

# Editor can't provide autocomplete or warnings
```

**Why It Happens**: Coming from JavaScript where typing is optional (or nonexistent)

**Solution**: Add type hints everywhere

```gdscript
# Good: Explicit types
var player: CharacterBody2D
var health: int = 100

func get_player() -> CharacterBody2D:
    return player

# Now editor knows player has .velocity, .move_and_slide(), etc.
```

### Pitfall 2: Using camelCase Instead of snake_case

**Problem**: GDScript convention is snake_case; mixing styles is inconsistent

```gdscript
# Bad: JavaScript habits
var playerHealth = 100
var maxHealth = 100

func takeDamage(damageAmount):
    playerHealth -= damageAmount
```

**Why It Happens**: Muscle memory from JavaScript/TypeScript

**Solution**: Use snake_case for everything except class names

```gdscript
# Good: GDScript convention
var player_health: int = 100
var max_health: int = 100

func take_damage(damage_amount: int) -> void:
    player_health -= damage_amount

# Class names use PascalCase
class_name PlayerController
```

### Pitfall 3: Accessing Nodes Before _ready()

**Problem**: Nodes aren't available until scene tree is built

```gdscript
# Bad: Accessing nodes too early
extends Node2D

var sprite = $Sprite2D  # ERROR: Sprite2D doesn't exist yet!

func _init():
    sprite.modulate = Color.RED  # CRASH: sprite is null
```

**Why It Happens**: Not understanding Godot's lifecycle (coming from immediate DOM access in web dev)

**Solution**: Use `@onready` or access nodes in `_ready()`

```gdscript
# Good: Wait until ready
extends Node2D

@onready var sprite: Sprite2D = $Sprite2D

func _ready():
    sprite.modulate = Color.RED  # Safe: _ready() called after tree is built
```

### Pitfall 4: Confusing == with === (They're the Same!)

**Problem**: Expecting JavaScript's strict equality semantics

```gdscript
# GDScript only has ==, no ===
if health == "100":  # This is false (int vs String)
    pass

# JS developers expect === for strict comparison
# But GDScript == is already strict (checks type)
```

**Why It Happens**: JavaScript's quirky `==` behavior trains you to always use `===`

**Solution**: Use `==` and know it's already strict

```gdscript
# Good: == is type-safe in GDScript
if health == 100:  # Correct
    pass

if health == "100":  # False (int != String)
    pass

# For null checks, be explicit
if player != null:
    player.move()
```

### Pitfall 5: Expecting Array Methods Like .map() and .filter()

**Problem**: GDScript arrays don't have functional methods

```gdscript
# Bad: Trying JavaScript array methods
var double_values = numbers.map(func(x): return x * 2)  # NO MAP METHOD!
var evens = numbers.filter(func(x): return x % 2 == 0)  # NO FILTER!
```

**Why It Happens**: Modern JavaScript relies heavily on array methods

**Solution**: Use for loops or manual implementations

```gdscript
# Good: Use for loops
var doubled = []
for num in numbers:
    doubled.append(num * 2)

var evens = []
for num in numbers:
    if num % 2 == 0:
        evens.append(num)

# Or create helper functions
func map_array(arr: Array, callback: Callable) -> Array:
    var result = []
    for item in arr:
        result.append(callback.call(item))
    return result
```

### Debugging Tips

- **Print debugging**: Use `print()`, `print_debug()`, or `push_warning()` for messages
- **Breakpoints**: Click line number gutter in editor to set breakpoints
- **Remote debugging**: Run game with debugger attached (F5 in editor)
- **Type errors**: Most caught at parse time if using type hints
- **Node not found**: Check node paths with `print($NodePath)` to see what exists
- **Signal not firing**: Use `print()` in emit location to verify execution

## Try This

### Exercise 1: Convert JavaScript Code to GDScript ⭐

**Goal**: Translate the following JavaScript class to GDScript

```javascript
class Enemy {
    constructor(health, speed) {
        this.health = health || 100;
        this.speed = speed || 5.0;
        this.isAlive = true;
    }
    
    takeDamage(amount) {
        this.health -= amount;
        if (this.health <= 0) {
            this.die();
        }
    }
    
    die() {
        this.isAlive = false;
        console.log("Enemy died!");
    }
}
```

**Expected Outcome**: A GDScript class extending Node with proper types and conventions

<details>
<summary>Solution</summary>

```gdscript
extends Node
class_name Enemy

var health: int = 100
var speed: float = 5.0
var is_alive: bool = true

func _init(initial_health: int = 100, initial_speed: float = 5.0):
    health = initial_health
    speed = initial_speed

func take_damage(amount: int) -> void:
    health -= amount
    if health <= 0:
        die()

func die() -> void:
    is_alive = false
    print("Enemy died!")
```
</details>

### Exercise 2: Implement a Signal System ⭐⭐

**Goal**: Create a simple health system with signals

**Requirements**:
- Define signals for `health_changed` and `died`
- Implement `take_damage()` and `heal()` methods
- Emit appropriate signals
- Create a listener that prints messages

**Hints**:
- Start with a basic Node script
- Use `signal` keyword at top of class
- Remember to emit with parameters
- Test by calling methods in `_ready()`

**Expected Outcome**: Console output showing health changes and death message

<details>
<summary>Solution</summary>

```gdscript
extends Node

signal health_changed(new_health: int)
signal died

var health: int = 100
var max_health: int = 100

func _ready():
    # Connect to our own signals for testing
    health_changed.connect(_on_health_changed)
    died.connect(_on_died)
    
    # Test the system
    take_damage(30)
    heal(20)
    take_damage(200)  # Should trigger death

func take_damage(amount: int) -> void:
    health -= amount
    health = max(0, health)  # Clamp to 0
    health_changed.emit(health)
    
    if health <= 0:
        died.emit()

func heal(amount: int) -> void:
    health += amount
    health = min(max_health, health)  # Clamp to max
    health_changed.emit(health)

func _on_health_changed(new_health: int) -> void:
    print("Health changed to: ", new_health)

func _on_died() -> void:
    print("Player has died!")
```
</details>

### Exercise 3: Match Statement Practice ⭐⭐

**Goal**: Create a state machine using `match`

**Requirements**:
- Create an enum for player states (IDLE, RUNNING, JUMPING, FALLING)
- Use `match` to handle state transitions
- Print different messages for each state
- Implement a function that cycles through states

**Hints**:
- `enum PlayerState { IDLE, RUNNING, JUMPING, FALLING }`
- Use `match current_state:` for state handling
- Remember the `_:` default case

**Expected Outcome**: Clean state management with match patterns

### Exercise 4: Type-Safe Dictionary ⭐⭐⭐

**Goal**: Create a typed inventory system

**Requirements**:
- Create a Dictionary to store items (String keys, int quantities)
- Implement `add_item()`, `remove_item()`, `has_item()` methods
- Handle edge cases (removing more than you have, etc.)
- Add type hints throughout

**Challenge**: Make it more robust than the weakly-typed version

### Exercise 5: Research GDScript Callables 📚

**Goal**: Understand how GDScript handles function references

**Research Topics**:
- What is a `Callable` in GDScript?
- How does it differ from JavaScript's functions as first-class objects?
- When would you use `Callable.call()` vs direct invocation?
- Look at Godot docs for signal connections with Callables

**Deliverable**: Write a short explanation (3-4 sentences) and a code example

## Connecting to Web Development

| Game Dev Concept | Web Dev Equivalent | Key Differences |
|------------------|-------------------|-----------------|
| GDScript | TypeScript | More focused syntax, built for one engine |
| Signals | Event listeners | Type-safe, editor-integrated, bi-directional |
| Node tree | DOM/Component tree | Fixed hierarchy, no virtual DOM, explicit refs |
| `@export` | Component props | Inspector-editable, not reactive |
| `@onready` | `useRef`/`componentDidMount` | Guarantees node availability |
| `_process()` | `requestAnimationFrame` | Called automatically every frame |
| `_physics_process()` | None (game-specific) | Fixed timestep for consistent physics |
| Scenes | React components | Reusable, composable, instantiable |
| Autoload singletons | Redux/Context | Global state, persistent across scenes |
| `match` | `switch` with superpowers | Pattern matching, no fall-through |

## What's Next

**In the next lesson** (`lesson-01-game-loop`), you'll learn:
- Godot's scene and node system architecture
- The game loop: `_process()` vs `_physics_process()`
- Delta time and frame-independent movement
- Creating your first interactive scene

**Looking Ahead**: By Lesson 4, you'll have a moving character with physics and collision!

## Additional Resources

- [Official GDScript Basics](https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/gdscript_basics.html)
- [GDScript Style Guide](https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/gdscript_styleguide.html)
- [GDScript Reference](https://docs.godotengine.org/en/stable/classes/class_@gdscript.html)
- [Signals Documentation](https://docs.godotengine.org/en/stable/getting_started/step_by_step/signals.html)

---

## Summary Checklist

By completing this lesson, you should be able to:

- [x] Declare variables with proper type hints using `:` and `:=`
- [x] Write functions with parameter and return types
- [x] Use `match` statements for pattern-based control flow
- [x] Define and emit custom signals
- [x] Access child nodes with `$` and `@onready`
- [x] Explain the difference between `_init()` and `_ready()`
- [x] Understand when to use `@export` for Inspector integration
- [x] Convert simple JavaScript classes to GDScript

**Completion Time**: ~15-20 minutes (reference), 30-45 minutes (with exercises)  
**Difficulty**: Beginner (reference material)  
**Fun Factor**: Foundational knowledge—pays off immediately! 📚

---

*This summary was generated for Lesson 0 of the ViveCode Game Development Course. See [README.md](../../README.md) for the complete curriculum.*
