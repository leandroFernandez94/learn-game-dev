# GDScript Primer for JavaScript Developers

> **⏱️ Estimated time**: 15 minutes  
> **Branch**: `lesson-00-gdscript-primer`

A quick reference guide to GDScript syntax for developers coming from JavaScript/TypeScript backgrounds.

## Quick Overview

GDScript is:
- **Python-inspired** syntax (whitespace matters!)
- **Statically typed** (optional, but recommended)
- **Built for Godot** (not a general-purpose language)
- **JIT compiled** (faster than Python, slower than C++)

## Variables & Types

### JavaScript
```javascript
// Untyped
let health = 100;
const maxHealth = 100;
var speed = 5.5;

// TypeScript
let health: number = 100;
const maxHealth: number = 100;
```

### GDScript
```gdscript
# Untyped (inferred)
var health = 100
var max_health = 100  # Use snake_case, not camelCase
var speed = 5.5

# Explicitly typed (recommended)
var health: int = 100
var max_health: int = 100
var speed: float = 5.5

# Type inference with :=
var player_name := "Hero"  # String inferred
var is_alive := true       # bool inferred

# Constants (UPPER_CASE by convention)
const MAX_HEALTH: int = 100
const SPEED: float = 5.5
```

**Key Differences**:
- No `let`, `const`, or `var` distinction—only `var` and `const`
- No semicolons (they're optional but not used)
- Type hints use `:` after variable name
- Use `snake_case` not `camelCase`

## Functions

### JavaScript
```javascript
// Regular function
function takeDamage(amount) {
    this.health -= amount;
}

// Arrow function
const heal = (amount) => {
    this.health += amount;
    return this.health;
};

// TypeScript
function takeDamage(amount: number): void {
    this.health -= amount;
}
```

### GDScript
```gdscript
# Basic function
func take_damage(amount):
    health -= amount

# With type hints (recommended)
func take_damage(amount: int) -> void:
    health -= amount

# With return value
func heal(amount: int) -> int:
    health += amount
    return health

# Default parameters
func take_damage(amount: int = 10) -> void:
    health -= amount

# Multiple return values (using Array)
func get_position_and_health() -> Array:
    return [position, health]
```

**Key Differences**:
- Use `func` keyword, not `function`
- Return type comes after `->` at end of signature
- No arrow functions—only `func` declarations
- Indentation defines scope (like Python)
- No curly braces `{}`

## Classes & Objects

### JavaScript
```javascript
class Player {
    constructor(name) {
        this.name = name;
        this.health = 100;
    }
    
    takeDamage(amount) {
        this.health -= amount;
    }
}

const player = new Player("Hero");
```

### GDScript
```gdscript
# In Godot, scripts extend nodes
extends CharacterBody2D

# Class variables (properties)
var player_name: String = "Hero"
var health: int = 100

# Constructor
func _init():
    # Called when object is created
    pass

# Ready is like componentDidMount/useEffect
func _ready():
    # Called when node enters scene tree
    print("Player ready!")

# Methods
func take_damage(amount: int) -> void:
    health -= amount

# To instantiate (in another script):
# var player = Player.new()  # Usually you use scene instancing instead
```

**Key Differences**:
- Scripts `extend` a node type (not standalone classes)
- No `this` keyword—just use variable names directly
- `_init()` is constructor, `_ready()` is like lifecycle hook
- `class_name` keyword to register class globally

## Control Flow

### JavaScript
```javascript
// If/else
if (health > 50) {
    console.log("Healthy");
} else if (health > 0) {
    console.log("Hurt");
} else {
    console.log("Dead");
}

// Switch
switch (state) {
    case "idle":
        idle();
        break;
    case "running":
        run();
        break;
    default:
        break;
}

// Ternary
const status = health > 0 ? "alive" : "dead";
```

### GDScript
```gdscript
# If/elif/else (note: elif not else if)
if health > 50:
    print("Healthy")
elif health > 0:
    print("Hurt")
else:
    print("Dead")

# Match (more powerful than switch)
match state:
    "idle":
        idle()
    "running":
        run()
    _:  # Default case uses underscore
        pass

# Ternary (same syntax)
var status = "alive" if health > 0 else "dead"

# Match with patterns
match [x, y]:
    [0, 0]:
        print("Origin")
    [0, _]:
        print("On Y axis")
    [_, 0]:
        print("On X axis")
    _:
        print("Somewhere else")
```

**Key Differences**:
- `elif` not `else if`
- `match` is more powerful than `switch`
- No `break` needed in `match`
- Default case uses `_` underscore

## Loops

### JavaScript
```javascript
// For loop
for (let i = 0; i < 10; i++) {
    console.log(i);
}

// For...of
for (const item of items) {
    console.log(item);
}

// While
while (running) {
    update();
}

// forEach
enemies.forEach(enemy => {
    enemy.update();
});
```

### GDScript
```gdscript
# For loop with range
for i in range(10):
    print(i)  # 0 to 9

for i in range(5, 10):
    print(i)  # 5 to 9

for i in range(0, 10, 2):
    print(i)  # 0, 2, 4, 6, 8 (step by 2)

# For each in array
for item in items:
    print(item)

# While loop
while running:
    update()

# No forEach method—use for loop
for enemy in enemies:
    enemy.update()
```

**Key Differences**:
- `for x in range(n)` instead of `for (let i = 0; i < n; i++)`
- No `forEach`, `map`, `filter` methods—use loops or list comprehensions
- `break` and `continue` work the same

## Arrays & Dictionaries

### JavaScript
```javascript
// Arrays
const items = [1, 2, 3];
items.push(4);
items.pop();
console.log(items[0]);
console.log(items.length);

// Objects
const player = {
    name: "Hero",
    health: 100
};
console.log(player.name);
console.log(player["health"]);

// Destructuring
const [first, second] = items;
const { name, health } = player;
```

### GDScript
```gdscript
# Arrays (typed and untyped)
var items = [1, 2, 3]
var typed_items: Array[int] = [1, 2, 3]

items.append(4)      # Same as push
items.pop_back()     # Remove last
print(items[0])      # First element
print(items.size())  # Length (not .length)

# Dictionaries (like objects)
var player = {
    "name": "Hero",
    "health": 100
}
print(player["name"])
print(player.get("health", 0))  # With default value

# Typed Dictionary
var typed_player: Dictionary = {"name": "Hero"}

# No destructuring syntax in GDScript
var first = items[0]
var second = items[1]
```

**Key Differences**:
- `.append()` instead of `.push()`
- `.size()` instead of `.length`
- Dictionaries need string keys in quotes
- No destructuring assignment
- No spread operator `...`

## Signals (Events)

### JavaScript
```javascript
// Event listener
button.addEventListener('click', handleClick);

// Custom event
class Player extends EventEmitter {
    takeDamage(amount) {
        this.health -= amount;
        this.emit('damaged', amount);
    }
}

player.on('damaged', (amount) => {
    console.log(`Took ${amount} damage`);
});
```

### GDScript
```gdscript
# Define custom signal
signal health_changed(new_health)
signal died

# Emit signal
func take_damage(amount: int) -> void:
    health -= amount
    health_changed.emit(health)  # Godot 4.x syntax
    
    if health <= 0:
        died.emit()

# Connect to signal (in another script)
func _ready():
    player.health_changed.connect(_on_player_health_changed)
    player.died.connect(_on_player_died)

func _on_player_health_changed(new_health: int) -> void:
    print("Health is now: ", new_health)

func _on_player_died() -> void:
    print("Player died!")
```

**Key Differences**:
- Signals are first-class language feature (not library)
- Define with `signal` keyword
- Emit with `signal_name.emit(args)`
- Connect with `signal_name.connect(callback_function)`
- Type-safe and editor-integrated

## Node Access

### JavaScript/React
```javascript
// DOM/React refs
const sprite = document.querySelector('#sprite');
const spriteRef = useRef(null);

// Component children
this.props.children
```

### GDScript
```gdscript
# Access child nodes by name
@onready var sprite = $Sprite2D
@onready var collision = $CollisionShape2D

# Longer form (same as above)
@onready var sprite = get_node("Sprite2D")

# Access by path
@onready var health_label = $"../UI/HealthLabel"

# Find by group
var enemies = get_tree().get_nodes_in_group("enemies")

# Parent access
var parent_node = get_parent()
```

**Key Differences**:
- `$NodeName` is shorthand for `get_node("NodeName")`
- `@onready` ensures node is ready before assignment
- Node paths use `/` like file paths
- No virtual DOM—direct node tree access

## Async/Await (Signals Instead)

### JavaScript
```javascript
async function loadData() {
    const data = await fetch('/api/data');
    return data.json();
}

setTimeout(() => {
    console.log("Delayed");
}, 1000);
```

### GDScript
```gdscript
# Use await with signals (Godot 4.x)
func load_data():
    var http_request = HTTPRequest.new()
    add_child(http_request)
    http_request.request("https://api.example.com/data")
    await http_request.request_completed
    # Continue after signal

# Wait for timeout
func delayed_action():
    await get_tree().create_timer(1.0).timeout
    print("Delayed")

# Await animation
func play_animation():
    animation_player.play("jump")
    await animation_player.animation_finished
    print("Animation done")
```

**Key Differences**:
- `await` works with signals, not promises
- No `async` keyword—just use `await`
- Use timers instead of `setTimeout`
- More explicit about what you're waiting for

## Common Gotchas

### 1. Equality Operators
```javascript
// JavaScript
if (x === y)  // Strict equality
if (x == y)   // Loose equality
```

```gdscript
# GDScript
if x == y:    # Only one equality operator
    pass
# No === or !== operators
```

### 2. Boolean Values
```javascript
// JavaScript
if (value)  // Truthy check
```

```gdscript
# GDScript - More strict
if value != null and value != 0:  # Explicit check needed
    pass

# Or use is
if value:  # Works but more strict than JS
    pass
```

### 3. Null Checking
```javascript
// JavaScript
const name = player?.name ?? "Unknown";
```

```gdscript
# GDScript
var name = player.name if player else "Unknown"

# Or
var name = player.name if player != null else "Unknown"
```

### 4. String Interpolation
```javascript
// JavaScript
const message = `Player ${name} has ${health} HP`;
```

```gdscript
# GDScript
var message = "Player %s has %d HP" % [name, health]

# Or in Godot 4.x
var message = str("Player ", name, " has ", health, " HP")
```

## Export Decorator (Inspector Variables)

### GDScript Only Feature
```gdscript
# Make variables editable in Godot Inspector
@export var speed: float = 5.0
@export var max_health: int = 100
@export var player_name: String = "Hero"

# Export with range
@export_range(0, 100) var health: int = 100
@export_range(0, 10, 0.5) var speed: float = 5.0

# Export node reference
@export var target: Node2D

# Export file path
@export_file var config_path: String
@export_file("*.json") var data_path: String

# Export color
@export var player_color: Color = Color.BLUE
```

**No JavaScript equivalent** — this is editor integration!

## Summary Table

| Concept | JavaScript | GDScript |
|---------|-----------|----------|
| Variables | `let`, `const` | `var`, `const` |
| Functions | `function`, `=>` | `func` |
| Types | Optional (TS) | Optional (recommended) |
| Classes | `class` | `extends` |
| This | `this` | (implicit) |
| Null | `null`, `undefined` | `null` |
| Booleans | `true`, `false` | `true`, `false` |
| Equality | `===`, `==` | `==` |
| Logic | `&&`, `||`, `!` | `and`, `or`, `not` |
| If/Else | `if`, `else if` | `if`, `elif` |
| Switch | `switch/case` | `match` |
| For Loop | `for (;;)` | `for in range()` |
| Arrays | `[]`, `.push()` | `[]`, `.append()` |
| Objects | `{}` | `{}` (Dictionary) |
| Events | Listeners | Signals |
| Async | `async/await` | `await signals` |
| Comments | `//`, `/* */` | `#`, `""" """` |

## What's Next?

Now that you understand GDScript syntax, you're ready to start building! 

**Next**: Proceed to `lesson-01-game-loop` to learn about Godot's scene system and game loop fundamentals.

## Quick Reference Card

```gdscript
# Variables
var health: int = 100
var speed := 5.0  # Inferred
const MAX_HEALTH: int = 100

# Functions
func take_damage(amount: int) -> void:
    health -= amount

# Control Flow
if health > 0:
    print("Alive")
elif health == 0:
    print("Dead")

match state:
    "idle":
        idle()
    _:
        default()

# Loops
for i in range(10):
    print(i)

for enemy in enemies:
    enemy.update()

# Arrays & Dictionaries
var items: Array[int] = [1, 2, 3]
var data: Dictionary = {"name": "Hero"}

# Signals
signal health_changed(new_health)
health_changed.emit(100)

# Node Access
@onready var sprite = $Sprite2D

# Export
@export var speed: float = 5.0
```

---

**Time spent**: 15 minutes  
**Difficulty**: Reference Material  
**Ready for**: Lesson 01 - Game Loop & Scene System
