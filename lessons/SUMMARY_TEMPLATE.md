# Lesson {Number}: {Topic Name}

> **Branch**: `lesson-{number}-{topic-name}-finished`  
> **Prerequisites**: Lesson {previous number}  
> **Estimated Time**: {X} hours

## Concepts Learned

<!-- List the key concepts and skills taught in this lesson -->

- **Core concept 1**: Brief explanation
- **Core concept 2**: Brief explanation
- **Core concept 3**: Brief explanation
- Godot-specific API or node types introduced
- Game development patterns demonstrated
- Programming techniques applied

### What You Implemented

<!-- Concrete list of what the student built -->

- Feature or system 1
- Feature or system 2
- Code structure or pattern 3

## Key Code Patterns

<!-- Important code snippets with detailed explanations -->

### Pattern 1: {Pattern Name}

**Purpose**: Explain what this pattern accomplishes and when to use it

```gdscript
# Example code snippet
func example_function() -> void:
    # Detailed comment explaining each step
    var result = some_operation()
    # Why we do this specific thing
    return result
```

**Key Takeaways**:

- Why this pattern is useful
- Common use cases
- How it relates to web dev patterns (if applicable)

### Pattern 2: {Pattern Name}

**Purpose**: Explain what this pattern accomplishes

```gdscript
# Another code example
```

**Key Takeaways**:

- Important points about this pattern

### Godot-Specific Idioms

<!-- Highlight Godot conventions used in this lesson -->

- **Node access with `$`**: How and when to use it vs `get_node()`
- **Signals**: How they compare to events in web development
- **@export vs @onready**: When to use each decorator
- Other Godot conventions introduced

## Historical Context

<!-- 2-3 paragraphs connecting modern patterns to game development history -->

### How Classic Games Solved This Problem

{Describe how NES, SNES, or other classic games handled this concept}

Example: "In the original Metroid (1986), room transitions used a simple screen-flip technique because the NES could only hold one screen's worth of tiles in VRAM at a time. This hardware limitation shaped the iconic 'flipping' transition that became a signature of the series..."

### Evolution of the Technique

{Explain how the approach evolved with better hardware}

Example: "Super Metroid (1994) introduced smooth scrolling between rooms, taking advantage of the SNES's Mode 7 capabilities and larger memory..."

### Modern Applications

{Connect to how modern games use this pattern}

Example: "Today, games like Hollow Knight and Ori use seamless streaming to load adjacent rooms, but many indie devs still use discrete room transitions for artistic choice and technical simplicity..."

## Common Pitfalls

<!-- List mistakes beginners often make and how to avoid/fix them -->

### Pitfall 1: {Common Mistake}

**Problem**: Describe what goes wrong

**Why It Happens**: Explain the root cause

**Solution**: How to fix it

```gdscript
# Bad example (what NOT to do)
func bad_approach():
    pass

# Good example (correct way)
func good_approach():
    pass
```

### Pitfall 2: {Common Mistake}

**Problem**: Description

**Solution**: Fix

### Debugging Tips

- Specific debugging techniques for this lesson's concepts
- How to use Godot's debugger for this particular system
- Console/print debugging strategies
- Performance profiling if relevant

## Try This

<!-- 3-5 hands-on exercises to extend learning -->

### Exercise 1: {Easy Modification} ⭐

**Goal**: {What to accomplish}

**Steps**:

1. Modify X in the code
2. Test by doing Y
3. Observe the result

**Expected Outcome**: {What should happen}

### Exercise 2: {Medium Challenge} ⭐⭐

**Goal**: {What to accomplish}

**Hints**:

- You'll need to use {concept from this lesson}
- Reference the {pattern} we learned above
- Don't forget to {important consideration}

**Expected Outcome**: {What should happen}

### Exercise 3: {Advanced Extension} ⭐⭐⭐

**Goal**: {What to accomplish}

**Challenge**: This requires combining concepts from this lesson with {previous lesson}

**Hints**:

- Think about how {concept} could apply here
- You may need to research {Godot API feature}

**Expected Outcome**: {What should happen}

### Exercise 4: {Creative Variation} 🎨

**Goal**: Make it your own!

**Ideas**:

- Change the aesthetic (colors, sizes, effects)
- Add a twist to the mechanic
- Combine with a different game genre

### Exercise 5: {Research Challenge} 📚

**Goal**: Deep dive into a related concept

**Research Topics**:

- Read Godot documentation on {topic}
- Investigate how {game title} implemented {feature}
- Study the difference between {approach A} and {approach B}

**Deliverable**: Write a paragraph explaining what you learned

## Connecting to Web Development

<!-- Help web developers relate game concepts to familiar territory -->

| Game Dev Concept    | Web Dev Equivalent    | Key Differences                             |
| ------------------- | --------------------- | ------------------------------------------- |
| Godot Signals       | Event listeners       | Typed, editor-connected, no capturing phase |
| Scene instancing    | Component composition | Tree-based, not virtual DOM                 |
| @export variables   | Component props       | Inspector-editable, not reactive            |
| Autoload singletons | Global state managers | Persistent across scenes                    |

## What's Next

**In the next lesson** (`lesson-{next-number}-{next-topic}`), you'll learn:

- Next major concept
- How it builds on this lesson
- Why it's important for the game

**Looking Ahead**: By Lesson {milestone number}, you'll have {major feature} fully working.

## Additional Resources

<!-- Optional: Links to relevant documentation and tutorials -->

- [Godot Docs: {Relevant Topic}](https://docs.godotengine.org/...)
- [GDScript Reference: {Feature}](https://docs.godotengine.org/...)
- Video tutorial recommendation (if particularly helpful)
- Community examples or case studies

---

## Summary Checklist

By completing this lesson, you should be able to:

- [ ] Explain {core concept 1} in your own words
- [ ] Implement {pattern/system} without referring to code
- [ ] Debug common issues with {feature}
- [ ] Identify when to use {technique} vs alternatives
- [ ] Connect {concept} to classic game design examples

**Completion Time**: ~{X} hours (including exercises)  
**Difficulty**: {Beginner/Intermediate/Advanced}  
**Fun Factor**: {How satisfying is this to implement} 🎮

---

_This summary was generated for Lesson {number} of the ViveCode Game Development Course. See [README.md](../../README.md) for the complete curriculum._
