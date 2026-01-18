# GitHub Copilot Instructions — ViveCode Game Development Course

This file provides context and instructions for GitHub Copilot when assisting with this game development learning project.

## Project Overview

**Course Type**: Progressive game development tutorial using Godot 4.2+ and GDScript  
**Target Student**: Senior web developer with no game development experience  
**Learning Goal**: Build a 2D Metroid-style platformer shooter, then introduce 3D fundamentals  
**Branch Strategy**: Two branches per lesson (`lesson-XX` for implementation, `lesson-XX-finished` for final commented code with summary)

## Branch Workflow

### Implementation Branch: `lesson-{number}-{topic}`
- Contains working code for the lesson
- Used for testing and debugging
- May have minimal comments
- Student experiments here

### Finished Branch: `lesson-{number}-{topic}-finished`
- Based on implementation branch
- Includes comprehensive inline comments
- Contains `lessons/{number}-{topic}/SUMMARY.md` using the template
- Final, polished version for learning

**Important**: Branches do NOT merge back to main. They remain separate for reference.

## Curriculum Structure

### Phase 0: Prerequisites
- **Lesson 00**: GDScript Primer (15-minute syntax reference for JS developers)

### Phase 1: Foundation (Lessons 01-04)
- **Lesson 01**: Game Loop & Scene System
  - Concepts: `_process()`, `_physics_process()`, delta time, node hierarchy
  - Historical: NES game loops, fixed vs variable timesteps
  
- **Lesson 02**: Input Handling
  - Concepts: InputMap, `Input.is_action_pressed()`, input buffering, action events
  - Historical: NES controller reading, frame-perfect inputs
  
- **Lesson 03**: Basic Movement & Physics
  - Concepts: CharacterBody2D, `move_and_slide()`, velocity, acceleration, gravity
  - Historical: Super Mario Bros physics feel, Sonic momentum
  
- **Lesson 04**: Collision Detection
  - Concepts: CollisionShape2D, layers/masks, Area2D vs StaticBody2D
  - Historical: Early collision detection algorithms, tilemap collisions

### Phase 2: Core Mechanics (Lessons 05-10)
- **Lesson 05**: Player State Machine
  - Concepts: Enums, match statements, state transitions, state pattern
  - Historical: Fighting game state machines, Mega Man player states
  
- **Lesson 06**: Shooting & Projectiles
  - Concepts: Scene instancing, object pooling, Area2D for bullets
  - Historical: Contra bullet patterns, memory constraints driving pooling
  
- **Lesson 07**: Animation Systems
  - Concepts: AnimatedSprite2D, AnimationPlayer, frame timing, sprite sheets
  - Historical: Sprite animation on limited hardware, keyframe animation
  
- **Lesson 08**: Camera Systems
  - Concepts: Camera2D, smoothing, limits, room-locking, camera lag
  - Historical: Super Metroid camera lead, screen transitions vs scrolling
  
- **Lesson 09**: Enemy AI Patterns
  - Concepts: Detection zones, patrol behavior, state machines for NPCs, timers
  - Historical: Space Invaders patterns, Pac-Man ghost AI, predictable vs random
  
- **Lesson 10**: Health & Damage
  - Concepts: Hit detection, invincibility frames, knockback, damage numbers
  - Historical: Invincibility flashing (hardware sprite flicker), mercy invincibility

### Phase 3: World Building (Lessons 11-14)
- **Lesson 11**: Tilemaps & Level Design
  - Concepts: TileMap node, collision layers, autotiling, terrain sets
  - Historical: NES tilemap limitations, metatiles, CHR ROM
  
- **Lesson 12**: Room Transitions
  - Concepts: Scene loading, `change_scene_to_file()`, door triggers, screen scrolling
  - Historical: Metroid room flips, Zelda screen transitions, loading zones
  
- **Lesson 13**: Power-ups & Abilities
  - Concepts: Autoload singletons, persistent state, ability gates, collectibles
  - Historical: Metroid power-up progression, color-coded doors, sequence breaking
  
- **Lesson 14**: UI/HUD Systems
  - Concepts: CanvasLayer, TextureProgressBar, Control nodes, anchors/margins
  - Historical: HUD design on CRT screens, limited screen space

### Phase 4: Polish (Lessons 15-18)
- **Lesson 15**: Audio Integration
  - Concepts: AudioStreamPlayer2D, AudioBusLayout, music layers, sound effects
  - Historical: Chiptune music, limited audio channels, adaptive music
  
- **Lesson 16**: Save Systems
  - Concepts: FileAccess, JSON serialization, ConfigFile, save states
  - Historical: Battery-backed saves, passwords, EEPROM limitations
  
- **Lesson 17**: Performance Optimization
  - Concepts: Object pooling, VisibilityNotifier2D, culling, profiling
  - Historical: NES sprite limits, flickering, hardware constraints
  
- **Lesson 18**: Particle Effects
  - Concepts: GPUParticles2D, process materials, custom shaders
  - Historical: Sprite-based particles, explosion animations

### Phase 5: 3D Transition (Lessons 19-22)
- **Lesson 19**: 3D Fundamentals
  - Concepts: Node3D, CharacterBody3D, 3D transforms, coordinate systems
  - Transition: 2D scene graph → 3D scene graph, Z-axis considerations
  
- **Lesson 20**: 3D Movement & Camera
  - Concepts: Camera3D, mouse look, orbit camera, lerp smoothing
  - Transition: Adapting 2D movement to 3D space, Metroid Prime first-person
  
- **Lesson 21**: 3D Raycasting
  - Concepts: RayCast3D, collision masks, hitscan shooting, ground detection
  - Transition: 2D collision → 3D collision, raycasting vs area detection
  
- **Lesson 22**: 3D Level Design
  - Concepts: MeshInstance3D, CSG primitives, GridMap, spatial navigation
  - Transition: 2D tilemaps → 3D level geometry, environmental storytelling

## Code Style Guidelines

### GDScript Conventions
- Use `snake_case` for variables and functions
- Use `PascalCase` for class names
- Use `UPPER_CASE` for constants and enums
- Prefer explicit type hints: `var health: int = 100`
- Use `@export` for inspector-editable variables
- Use `@onready` for node references: `@onready var sprite: Sprite2D = $Sprite2D`

### Scene Organization
```
scenes/
├── player/
│   ├── player.tscn
│   └── player_bullet.tscn
├── enemies/
│   ├── enemy_walker.tscn
│   └── enemy_flyer.tscn
├── levels/
│   └── test_room.tscn
└── ui/
    └── hud.tscn
```

### Script Organization
```
scripts/
├── player/
│   └── player.gd
├── enemies/
│   ├── enemy_base.gd
│   └── enemy_walker.gd
├── systems/
│   ├── object_pool.gd
│   └── camera_controller.gd
└── autoload/
    ├── game_manager.gd
    └── player_data.gd
```

## Lesson Summary Template

Each `-finished` branch must include `lessons/{number}-{topic}/SUMMARY.md` following this structure:

```markdown
# Lesson {Number}: {Topic Name}

## Concepts Learned
- Bullet list of key concepts
- What you implemented in this lesson
- Core game dev principles demonstrated

## Key Code Patterns
- Important code snippets with explanations
- Reusable patterns you'll use again
- Godot-specific idioms

## Historical Context
- How classic games solved similar problems
- Hardware constraints that shaped design
- Evolution of this technique

## Common Pitfalls
- Mistakes beginners make
- How to debug common issues
- Performance considerations

## Try This
- 3-5 exercises to extend the lesson
- Variations to experiment with
- Challenges to test understanding
```

## Teaching Philosophy

### For Web Developers
- **Relate to familiar concepts**: Compare signals to events, scenes to components, autoload to singletons
- **Leverage existing skills**: GDScript syntax is similar to Python but thinking is like modular JS
- **Highlight differences**: No async/await patterns, different memory model, frame-based vs event-driven
- **Show the "why"**: Explain game-specific patterns (object pooling, fixed timestep) that web devs don't typically encounter

### Progressive Complexity
- **Start simple**: Each lesson adds ONE major concept
- **Build incrementally**: New lessons extend previous work
- **Test thoroughly**: Each implementation branch should run without errors
- **Document clearly**: Finished branches explain every non-obvious line

### Historical Context
- **Show evolution**: How did NES games handle this? SNES? Modern games?
- **Explain constraints**: Why do these patterns exist? What problems did they solve?
- **Connect to classics**: Reference specific games (Metroid, Mega Man, Castlevania)
- **Keep it brief**: 2-3 paragraphs per topic, not a history lesson

## When Helping With Code

### For Implementation Branches (`lesson-XX`)
- Write clean, working code
- Minimal comments (only for non-obvious logic)
- Focus on functionality
- Test that it runs in Godot

### For Finished Branches (`lesson-XX-finished`)
- Add comprehensive inline comments
- Explain the "why" not just the "what"
- Reference previous lessons when using prior concepts
- Create detailed SUMMARY.md using the template
- Highlight patterns that will reappear later

### When Student Asks Questions
- Reference the specific lesson branch
- Relate to web dev concepts when possible
- Provide code examples
- Suggest experiments to deepen understanding
- Point to relevant Godot documentation

## Asset Guidelines

### Placeholder Assets (starter-pack/)
- **Sprites**: Simple colored rectangles/circles
  - Player: 16x16px, blue rectangle
  - Enemy: 16x16px, red circle
  - Bullet: 4x4px, yellow circle
  - Tiles: 16x16px, gray/brown/green variations

- **Audio**: Simple placeholder sounds
  - Jump: Short blip
  - Shoot: Quick beep
  - Hit: Impact sound
  - Music: Simple loop (optional)

- **Purpose**: Focus on code/mechanics, not art. Students can replace later.

## Debugging Tips to Share

### Common Godot Gotchas
- Forgetting to set collision layers/masks
- Not calling `super()` in `_ready()` when extending classes
- Using `_process()` instead of `_physics_process()` for physics
- Forgetting to free queued nodes with `queue_free()`
- Not checking for `null` before accessing node references

### Performance Tips
- Use object pooling for frequently spawned objects
- Disable `_process()` on inactive nodes
- Use VisibilityNotifier2D for off-screen culling
- Avoid `get_node()` in loops, cache references
- Profile with Godot's built-in profiler

## Course Completion Criteria

### 2D Game (Lesson 18)
Student should have:
- ✅ Playable character with run, jump, shoot
- ✅ Multiple enemy types with AI
- ✅ 3+ interconnected rooms
- ✅ Health and damage system
- ✅ At least 2 power-ups that unlock new abilities
- ✅ Working save/load system
- ✅ HUD with health/ammo display
- ✅ Audio for effects and music

### 3D Fundamentals (Lesson 22)
Student should understand:
- ✅ 3D coordinate system and transforms
- ✅ Character controller in 3D space
- ✅ 3D camera controls
- ✅ Raycasting for interactions
- ✅ Basic 3D level creation
- ✅ Differences between 2D and 3D architecture

## Repository Metadata

- **Engine**: Godot 4.2+ (4.2.0.stable or higher)
- **Language**: GDScript (Godot's built-in scripting language)
- **Platform**: macOS (but cross-platform compatible)
- **License**: MIT (for course code, student owns their game)
- **Estimated Time**: 40-60 hours for complete course
- **Prerequisites**: Web development experience, basic programming knowledge

## Success Metrics

A lesson is successful when the student can:
1. **Explain** the concept in their own words
2. **Implement** the pattern without looking at the code
3. **Debug** common issues independently
4. **Extend** the concept with their own variations
5. **Connect** it to similar web dev concepts

---

*This file helps GitHub Copilot provide contextual, educational assistance throughout the course. Update as curriculum evolves.*
