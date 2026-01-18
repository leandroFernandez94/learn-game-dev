# Setup Guide — Game Development Course

This guide will help you set up your macOS development environment for creating games with Godot 4.2+ and VS Code.

**Note**: This course is designed for Godot 4.2+. Godot 4.5 (or any 4.x version) works perfectly!

## Prerequisites

- macOS (you're all set!)
- Basic command line knowledge
- Git installed (you already have this)
- ~500MB disk space for Godot

## Step 1: Install Godot 4.2+

### Option A: Homebrew (Recommended)

If you have Homebrew installed:

```bash
brew install --cask godot
```

This installs the latest stable version of Godot 4.

### Option B: Direct Download

1. Visit [godotengine.org/download/macos](https://godotengine.org/download/macos/)
2. Download **Godot 4.x Standard** (4.2, 4.5, or later - not .NET version unless you want C# support)
3. Open the `.dmg` file and drag Godot to Applications
4. First launch: Right-click Godot → Open (to bypass macOS security)

### Verify Installation

Open Terminal and run:

```bash
# If installed via Homebrew
godot --version

# If installed via direct download, you may need to add it to PATH or use:
/Applications/Godot.app/Contents/MacOS/Godot --version
```

You should see output like: `4.2.x.stable.official` or `4.5.x.stable.official` (any 4.x version works)

## Step 2: Import the Project

### Using Godot Project Manager

1. Open Godot (you'll see the Project Manager window)
2. Click **Import**
3. Click **Browse** and navigate to this folder: `/Users/leandrofernandez/Documents/projects/vivecode-game`
4. Select the folder (Godot will detect the `project.godot` file)
5. Click **Import & Edit**

**Note**: We use "Import" instead of "New Project" because the `project.godot` file already exists in your repo with pre-configured settings (input mappings, collision layers, etc.).

**Important**: You need to have a project open to access Editor Settings in the next step!

## Step 3: Configure VS Code

### Install Godot Tools Extension

1. Open VS Code
2. Go to Extensions (⌘+Shift+X)
3. Search for "godot-tools" (by geequlim)
4. Click Install

### Configure VS Code as External Editor in Godot

**Note**: Make sure you have the vivecode-game project open in Godot first!

1. In Godot, go to **Editor → Editor Settings** (or press **⌘+,**)
2. Navigate to **Text Editor → External**
3. Check **Use External Editor**
4. Set **Exec Path** to:
   ```
   /usr/local/bin/code
   ```
   (Or find it with: `which code` in Terminal)
5. Set **Exec Flags** to:
   ```
   {project} --goto {file}:{line}:{col}
   ```

### Enable GDScript Language Server

1. In Godot: **Editor → Editor Settings** (or press **⌘+,**)
2. Navigate to **Network → Language Server**
3. Check **Enable** and **Use Thread**
4. Set **Remote Host** to `127.0.0.1`
5. Set **Remote Port** to `6005`

In VS Code:

1. Open Settings (⌘+,)
2. Search for "godot"
3. Set **Godot_tools: Editor Path** to:
   - Homebrew: `/Applications/Godot.app`
   - Direct: `/Applications/Godot.app`

### Project Structure

Godot will create:

```
vivecode-game/
├── project.godot          # Project configuration
├── .godot/                # Build cache (git ignored)
├── assets/                # We'll add art, audio here
├── scenes/                # .tscn scene files
├── scripts/               # .gd script files
└── lessons/               # Lesson documentation
```

## Step 4: Verify Setup

### Test GDScript in VS Code

1. In Godot, create a new scene: **Scene → New Scene**
2. Add a **Node** (root node)
3. Click the script icon next to the node
4. Choose **Create**
5. Save as `scripts/test.gd`
6. Right-click the script in FileSystem → **Open in External Editor**

VS Code should open with:

- Syntax highlighting
- Autocomplete (type `func` and press Tab)
- Error checking

### Test Running the Game

1. In Godot, press **F5** (or play button)
2. Select **main.tscn** when prompted (create it if needed)
3. You should see an empty game window

If you see the game window, you're ready to code!

## Step 5: Git Configuration

### Add .gitignore

The project already has (or will have) a `.gitignore` file. Ensure it contains:

```
# Godot build files
.godot/
.import/
export.cfg
export_presets.cfg

# Godot private files
*.translation

# Mono (if using C#)
.mono/
data_*/

# macOS
.DS_Store
```

### Initialize Repository

If not already initialized:

```bash
cd /Users/leandrofernandez/Documents/projects/vivecode-game
git init
git add .
git commit -m "Initial commit - main branch setup"
```

## Troubleshooting

### VS Code not opening from Godot

- Check the **Exec Path** is correct
- Try using `code` command: Install via VS Code Command Palette → "Shell Command: Install 'code' command in PATH"

### Autocomplete not working

- Ensure Language Server is enabled in Godot settings
- Restart VS Code
- Check Output panel (View → Output) → Select "Godot Tools"

### Godot won't open (macOS security)

- Right-click Godot.app → Open (first time only)
- System Settings → Privacy & Security → Allow Godot

## What's Next?

You're ready to start learning! Proceed to:

- **Lesson 00**: GDScript Primer for JavaScript Developers
- Check the main [README.md](README.md) for the full course structure

## Useful Resources

- [Godot Documentation](https://docs.godotengine.org/en/stable/)
- [GDScript Reference](https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/gdscript_basics.html)
- [Godot Community](https://godotengine.org/community)

---

**Ready to build games!** 🎮
