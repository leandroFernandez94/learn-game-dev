# ViveCode Game — Learn Game Development Course

**A progressive, hands-on course building a 2D Metroid-style platformer shooter with Godot 4.2+, then transitioning to 3D fundamentals.**

This course is designed for experienced web developers with no game development background. Each lesson teaches core game development concepts, design patterns, and historical context while building a playable game step by step.

## 🎯 What You'll Build

- **2D Phase (Lessons 1-18)**: Complete Metroid-style exploration platformer with shooting, enemies, power-ups, and interconnected world
- **3D Phase (Lessons 19-22)**: Introduction to 3D game development, adapting 2D mechanics to 3D space

## 🚀 Getting Started

1. **Setup Your Environment**: Follow [SETUP.md](SETUP.md) to install Godot 4.2+ and configure VS Code
2. **Start with Lesson 00**: GDScript syntax primer for JavaScript developers
3. **Follow the Branch Strategy**: Each lesson uses two branches (see below)

## 📚 Branch Strategy

Each lesson follows a two-branch workflow:

### `lesson-{number}`

Initial implementation branch where you'll:

- Review the code I've created
- Test that everything works
- Debug and fix any issues
- Experiment with the implementation

### `lesson-{number}-finished`

Final learning branch where you'll:

- Ask questions about the lesson concepts
- Request code comments and explanations
- Review the completed lesson summary
- Understand the "why" behind each pattern

**Important**: Lesson branches remain separate and do NOT merge back to main. This allows you to jump to any lesson for reference.

## 📖 Course Curriculum

### Phase 0: Prerequisites

| Lesson | Topic           | Concepts                                            | Branch                      |
| ------ | --------------- | --------------------------------------------------- | --------------------------- |
| **00** | GDScript Primer | Syntax comparison JS→GDScript, signals, node access | `lesson-00-gdscript-primer` |

### Phase 1: Foundation (Lessons 1-4)

| Lesson | Topic                    | Concepts                                                 | Branch                          |
| ------ | ------------------------ | -------------------------------------------------------- | ------------------------------- |
| **01** | Game Loop & Scene System | `_process()`, `_physics_process()`, node hierarchy       | `lesson-01-game-loop`           |
| **02** | Input Handling           | InputMap, `Input.is_action_pressed()`, action buffering  | `lesson-02-input-handling`      |
| **03** | Basic Movement & Physics | CharacterBody2D, `move_and_slide()`, gravity, velocity   | `lesson-03-movement-physics`    |
| **04** | Collision Detection      | CollisionShape2D, collision layers/masks, area detection | `lesson-04-collision-detection` |

### Phase 2: Core Mechanics (Lessons 5-10)

| Lesson | Topic                  | Concepts                                           | Branch                           |
| ------ | ---------------------- | -------------------------------------------------- | -------------------------------- |
| **05** | Player State Machine   | Enums, match statements, state transitions         | `lesson-05-state-machine`        |
| **06** | Shooting & Projectiles | Area2D, object pooling, instancing scenes          | `lesson-06-shooting-projectiles` |
| **07** | Animation Systems      | AnimatedSprite2D, AnimationPlayer, blend trees     | `lesson-07-animation-systems`    |
| **08** | Camera Systems         | Camera2D, smoothing, position limits, room-locking | `lesson-08-camera-systems`       |
| **09** | Enemy AI Patterns      | Detection zones, patrol/chase behavior, timers     | `lesson-09-enemy-ai`             |
| **10** | Health & Damage        | Hit detection, invincibility frames, knockback     | `lesson-10-health-damage`        |

### Phase 3: World Building (Lessons 11-14)

| Lesson | Topic                   | Concepts                                               | Branch                         |
| ------ | ----------------------- | ------------------------------------------------------ | ------------------------------ |
| **11** | Tilemaps & Level Design | TileMap, collision layers, autotiling                  | `lesson-11-tilemaps`           |
| **12** | Room Transitions        | Scene loading, `change_scene_to_file()`, door triggers | `lesson-12-room-transitions`   |
| **13** | Power-ups & Abilities   | Global autoload, persistent state, gated progression   | `lesson-13-powerups-abilities` |
| **14** | UI/HUD Systems          | CanvasLayer, TextureProgressBar, Control nodes         | `lesson-14-ui-hud`             |

### Phase 4: Polish (Lessons 15-18)

| Lesson | Topic                    | Concepts                                        | Branch                        |
| ------ | ------------------------ | ----------------------------------------------- | ----------------------------- |
| **15** | Audio Integration        | AudioStreamPlayer2D, music system, audio buses  | `lesson-15-audio-integration` |
| **16** | Save Systems             | FileAccess, JSON serialization, ConfigFile      | `lesson-16-save-systems`      |
| **17** | Performance Optimization | Object pooling, VisibilityNotifier2D, culling   | `lesson-17-optimization`      |
| **18** | Particle Effects         | GPUParticles2D, custom materials, visual polish | `lesson-18-particle-effects`  |

### Phase 5: 3D Transition (Lessons 19-22)

| Lesson | Topic                | Concepts                                            | Branch                         |
| ------ | -------------------- | --------------------------------------------------- | ------------------------------ |
| **19** | 3D Fundamentals      | Node3D, CharacterBody3D, 3D scene structure         | `lesson-19-3d-fundamentals`    |
| **20** | 3D Movement & Camera | Camera3D orbit, mouse look, 3D character controller | `lesson-20-3d-movement-camera` |
| **21** | 3D Raycasting        | RayCast3D, ground detection, hitscan shooting       | `lesson-21-3d-raycasting`      |
| **22** | 3D Level Design      | MeshInstance3D, CSG primitives, 3D navigation       | `lesson-22-3d-level-design`    |

## 🎓 Learning Outcomes

By the end of this course, you'll understand:

### Core Concepts

- Game loops and frame-independent movement
- State machines and entity management
- Collision detection systems
- Input handling and buffering
- Camera systems and screen space

### Design Patterns

- Object pooling for performance
- Component-based architecture (Godot's scene system)
- Separation of concerns (scenes, scripts, resources)
- Event-driven programming with signals
- Singleton pattern (autoload scripts)

### Game-Specific Knowledge

- 2D platformer physics and feel
- Enemy AI behavior patterns
- Level design and gated progression
- Power-up systems and ability unlocks
- Metroidvania-style interconnected worlds
- Transitioning from 2D to 3D mechanics

### Historical Context

- How NES/SNES games handled technical limitations
- Evolution of scrolling and camera systems
- Classic Metroid design patterns
- Industry-standard optimization techniques

## 🛠️ Tech Stack

- **Engine**: Godot 4.2+ (open-source, cross-platform) — **Godot 4.5+ fully supported**
- **Language**: GDScript (Python-like, beginner-friendly)
- **Editor**: VS Code with godot-tools extension
- **Version Control**: Git with branch-per-lesson strategy
- **Assets**: Provided placeholder sprites, tiles, and audio

## 📂 Project Structure

```
vivecode-game/
├── README.md                    # This file
├── SETUP.md                     # Installation guide
├── project.godot                # Godot project config
├── .gitignore                   # Git ignore rules
├── .github/
│   └── copilot-instructions.md  # Course metadata for AI
├── assets/
│   └── starter-pack/            # Placeholder sprites, tiles, audio
│       ├── sprites/
│       ├── tiles/
│       └── audio/
├── scenes/                      # .tscn scene files
│   ├── player/
│   ├── enemies/
│   ├── levels/
│   └── ui/
├── scripts/                     # .gd script files
│   ├── player/
│   ├── enemies/
│   ├── systems/
│   └── autoload/
└── lessons/                     # Lesson documentation
    ├── SUMMARY_TEMPLATE.md      # Template for lesson summaries
    ├── 00-gdscript-primer/
    ├── 01-game-loop/
    └── ...
```

## 🎮 How to Use This Course

### For Each Lesson:

1. **Checkout the `lesson-XX` branch**

   ```bash
   git checkout lesson-XX-topic-name
   ```

2. **Open the project in Godot**
   - Review the scene files in `scenes/`
   - Read through the scripts in `scripts/`
   - Press F5 to run and test

3. **Experiment and debug**
   - Try modifying values
   - Break things intentionally
   - Fix any bugs you find

4. **Switch to `lesson-XX-finished` when ready**

   ```bash
   git checkout lesson-XX-topic-name-finished
   ```

5. **Study the final version**
   - Read inline comments
   - Review the lesson summary in `lessons/XX-topic/SUMMARY.md`
   - Ask questions about concepts
   - Note patterns for future reference

6. **Move to the next lesson**
   - Checkout `lesson-XX+1`
   - Each lesson builds on previous concepts

## 🤔 Getting Help

### During Development

- Each `-finished` branch includes detailed comments
- Lesson summaries explain the "why" behind patterns
- Historical context sections provide design rationale

### External Resources

- [Godot Documentation](https://docs.godotengine.org/en/stable/)
- [GDScript Style Guide](https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/gdscript_styleguide.html)
- [Godot Q&A](https://ask.godotengine.org/)

## 📝 Notes

- **No prior game development experience required**
- **Web development experience is assumed** (you know Git, basic programming concepts)
- **Each lesson is self-contained** but builds on previous lessons
- **Estimated time**: 2-3 hours per lesson (including experiments)
- **Total course**: 40-60 hours for complete mastery

## 🎯 After Completion

Once you finish Lesson 22, you'll have:

- ✅ A complete 2D Metroid-style platformer game
- ✅ Understanding of fundamental game dev concepts
- ✅ Experience with 3D game fundamentals
- ✅ Knowledge of industry-standard patterns
- ✅ Foundation to build your own games

**Next Steps**:

- Port your 2D game fully to 3D
- Create your own original game
- Contribute to open-source Godot projects
- Study advanced topics (shaders, networking, procedural generation)

## 🚦 Current Status

- ✅ Main branch setup complete
- ⏳ Lesson 00 (GDScript Primer) - Coming next
- ⏳ Lessons 01-22 - To be implemented

---

**Let's build something amazing!** 🎮✨

_Course created by GitHub Copilot for aspiring game developers from web development backgrounds._
