# Starter Asset Pack

This folder contains placeholder graphics and audio for the game development course. These simple assets allow you to focus on coding and game mechanics without worrying about art production.

## Contents

### Sprites (`sprites/`)
Simple colored shapes for rapid prototyping:
- `player.png` - 16x16px blue rectangle (player character)
- `enemy_walker.png` - 16x16px red circle (ground enemy)
- `enemy_flyer.png` - 16x16px orange triangle (flying enemy)
- `bullet_player.png` - 4x4px yellow circle (player projectile)
- `bullet_enemy.png` - 4x4px red circle (enemy projectile)
- `health_pickup.png` - 8x8px green cross (health restore)
- `powerup_missile.png` - 8x8px cyan diamond (weapon upgrade)
- `powerup_jump.png` - 8x8px purple star (jump ability)

### Tiles (`tiles/`)
Basic tileset for level construction:
- `tileset.png` - 16x16px grid with platform/wall variations
  - Gray: Solid platforms
  - Brown: Dirt/ground
  - Green: Grass
  - Dark gray: Background tiles

### Audio (`audio/`)
Simple sound effects (placeholder):
- `jump.wav` - Short blip sound
- `shoot.wav` - Quick beep
- `hit.wav` - Impact sound
- `pickup.wav` - Collect sound
- `enemy_hurt.wav` - Damage indicator
- `music_loop.ogg` - Simple background music (optional)

## Using These Assets

### In Godot:
1. Drag sprites directly onto nodes in the Scene panel
2. Set `Sprite2D.texture` to these images
3. Import the tileset into a `TileMap` node
4. Assign audio files to `AudioStreamPlayer` nodes

### Pixel Perfect Settings:
All sprites are designed at 16x16px base resolution. To maintain pixel-perfect rendering:
- Project settings: **Rendering → Textures → Canvas Textures → Default Texture Filter** = `Nearest`
- Already configured in `project.godot`

## Replacing Assets Later

These are intentionally simple! Once you understand the mechanics, you can:
- Create your own art in [Aseprite](https://www.aseprite.org/) or [Piskel](https://www.piskelapp.com/)
- Commission an artist
- Use free asset packs from [itch.io](https://itch.io/game-assets/free)
- Purchase assets from [Kenney](https://kenney.nl/) or other stores

The game logic remains the same—just swap the file references!

## License

These placeholder assets are released into the **public domain** (CC0). Use them however you want, no attribution required.

---

*Focus on the code. Make it beautiful later.* 🎨
