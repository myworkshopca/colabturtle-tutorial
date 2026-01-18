# Week 9: Animation Basics

## Learning Objectives
- Create animated drawings
- Control drawing speed dynamically
- Show step-by-step processes
- Create growing patterns
- Build progressive animations
- Implement time-based effects

---

## Introduction

Animation brings your turtle graphics to life! This week, you'll learn to create drawings that change over time, showing the drawing process, creating growing patterns, and building dynamic visual effects.

---

## Speed Control

### Dynamic Speed Changes

```python
from ColabTurtle.Turtle import *
initializeTurtle()

def animated_square(size):
    """Draw a square with changing speed"""
    speeds = [1, 3, 5, 7]

    for i in range(4):
        speed(speeds[i])
        forward(size)
        right(90)

animated_square(100)
```

### Gradual Speed Increase

```python
from ColabTurtle.Turtle import *
initializeTurtle()

def accelerating_spiral(turns):
    """Spiral that gets faster as it grows"""
    size = 5

    for i in range(turns):
        # Speed increases with iteration
        current_speed = min(1 + i // 10, 13)
        speed(current_speed)

        forward(size)
        right(90)
        size += 2

accelerating_spiral(100)
```

---

## Growing Patterns

### Growing Square

```python
from ColabTurtle.Turtle import *
initializeTurtle()

def growing_square(max_size, step):
    """Draw squares that grow from small to large"""
    size = step

    while size <= max_size:
        for i in range(4):
            forward(size)
            right(90)
        size += step

        # Reposition for next square
        penup()
        backward(step / 2)
        right(90)
        forward(step / 2)
        left(90)
        pendown()

growing_square(150, 10)
```

### Growing Circle

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=10)

def draw_circle(radius, steps=36):
    circumference = 2 * math.pi * radius
    step_length = circumference / steps
    step_angle = 360 / steps
    for i in range(steps):
        forward(step_length)
        right(step_angle)

def growing_circles(max_radius, step, colors):
    """Draw circles growing from center"""
    radius = step

    while radius <= max_radius:
        color(colors[(radius // step) % len(colors)])
        draw_circle(radius)
        radius += step

# Draw growing circles
colors = ['red', 'orange', 'yellow', 'green', 'blue', 'purple']
growing_circles(100, 15, colors)
```

---

## Progressive Drawing

### Step-by-Step Flower

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle()

def draw_circle(radius, steps=36):
    circumference = 2 * math.pi * radius
    step_length = circumference / steps
    step_angle = 360 / steps
    for i in range(steps):
        forward(step_length)
        right(step_angle)

def animated_flower(petals, petal_radius, delay_factor=1):
    """Draw flower one petal at a time"""
    colors = ['red', 'pink', 'orange', 'yellow', 'purple', 'magenta']

    for i in range(petals):
        # Slower speed for each petal
        speed(3 * delay_factor)

        color(colors[i % len(colors)])
        draw_circle(petal_radius)
        right(360 / petals)

    # Draw center
    speed(5 * delay_factor)
    color('yellow')
    draw_circle(petal_radius / 2)

animated_flower(6, 40, 1)
```

### Building a House

```python
from ColabTurtle.Turtle import *
initializeTurtle()

def animated_house(size):
    """Draw a house step by step"""

    # Base - slow
    speed(3)
    color('brown')
    for i in range(4):
        forward(size)
        right(90)

    # Roof - medium speed
    speed(5)
    color('red')
    for i in range(3):
        forward(size)
        right(120)

    # Door - fast
    speed(8)
    color('darkbrown')
    penup()
    forward(size / 3)
    pendown()
    for i in range(2):
        forward(size / 3)
        right(90)
        forward(size / 2)
        right(90)

animated_house(100)
```

---

## Rotating Animations

### Spinning Square

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=5)

def spinning_squares(count, size, rotation):
    """Draw squares that rotate around center"""
    colors = ['red', 'orange', 'yellow', 'green', 'blue', 'purple']

    for i in range(count):
        color(colors[i % len(colors)])

        # Draw square
        for j in range(4):
            forward(size)
            right(90)

        # Rotate for next square
        right(rotation)

spinning_squares(18, 80, 20)
```

### Spiraling Triangles

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=10)

def spiraling_triangles(count):
    """Draw triangles in a spiral pattern"""
    colors = ['red', 'blue', 'green']
    size = 30

    for i in range(count):
        color(colors[i % len(colors)])

        # Draw triangle
        for j in range(3):
            forward(size)
            right(120)

        # Rotate and grow
        right(15)
        size += 2

spiraling_triangles(24)
```

---

## Color Transitions

### Fading Colors

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def color_transition_spiral(turns):
    """Spiral with transitioning colors"""
    colors = ['red', 'orange', 'yellow', 'green', 'cyan', 'blue', 'purple', 'magenta']
    size = 5

    for i in range(turns):
        color(colors[(i // 10) % len(colors)])
        forward(size)
        right(89)
        size += 0.5

color_transition_spiral(200)
```

### Rainbow Wave

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def rainbow_wave(waves):
    """Create a rainbow wave pattern"""
    colors = ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet']

    for i in range(360 * waves):
        color(colors[(i // 20) % len(colors)])
        forward(2)

        # Create wave motion
        if i % 40 < 20:
            left(1)
        else:
            right(1)

rainbow_wave(3)
```

---

## Practice Exercises

### Exercise 1: Growing Tree
Animate a tree that grows from a seed to full size.

```python
from ColabTurtle.Turtle import *
initializeTurtle()

def growing_tree(max_length, growth_rate, depth):
    """Tree that grows over time"""
    for current_length in range(10, max_length, growth_rate):
        draw_tree_frame(current_length, depth)
        # Clear and redraw (if supported)

def draw_tree_frame(length, depth):
    if depth == 0:
        return
    forward(length)
    right(20)
    draw_tree_frame(length * 0.7, depth - 1)
    left(40)
    draw_tree_frame(length * 0.7, depth - 1)
    right(20)
    backward(length)
```

### Exercise 2: Pulsing Star
Create a star that grows and shrinks repeatedly.

### Exercise 3: Spiraling Colors
Create a spiral where colors transition smoothly.

### Exercise 4: Animated Mandala
Build a mandala one layer at a time.

### Exercise 5: Drawing Animation
Simulate handwriting by drawing slowly.

---

## Advanced Examples

### Firework Effect

```python
from ColabTurtle.Turtle import *
import random
initializeTurtle(initial_speed=10)

def firework(x, y, num_sparks=12):
    """Draw a firework burst at position"""
    colors = ['red', 'orange', 'yellow', 'white', 'pink']

    # Move to position
    penup()
    # Navigate to (x, y)
    pendown()

    # Draw sparks
    for i in range(num_sparks):
        color(random.choice(colors))
        length = random.randint(30, 80)

        # Draw spark
        forward(length)
        backward(length)

        # Rotate for next spark
        right(360 / num_sparks)

# Draw multiple fireworks
positions = [(0, 100), (-100, 50), (100, 80), (0, -50)]
for pos in positions:
    firework(pos[0], pos[1], random.randint(8, 16))
```

### Blooming Flower

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle()

def draw_circle(radius, steps=36):
    circumference = 2 * math.pi * radius
    step_length = circumference / steps
    step_angle = 360 / steps
    for i in range(steps):
        forward(step_length)
        right(step_angle)

def blooming_flower(petals, max_radius, steps):
    """Flower that blooms gradually"""
    colors = ['pink', 'lightpink', 'hotpink', 'deeppink']

    for radius in range(5, max_radius, max_radius // steps):
        for i in range(petals):
            color(colors[i % len(colors)])
            draw_circle(radius)
            right(360 / petals)

blooming_flower(6, 40, 8)
```

---

## Clearing and Redrawing

### Frame-Based Animation (Conceptual)

```python
from ColabTurtle.Turtle import *

def animate_moving_square(frames):
    """Conceptual frame-based animation"""
    size = 50
    x = -100

    for frame in range(frames):
        # Clear screen (if supported in ColabTurtle)
        # clear()

        # Reinitialize
        # initializeTurtle(initial_speed=13)

        # Move to current position
        penup()
        # Navigate to (x + frame * 5, 0)
        pendown()

        # Draw square
        for i in range(4):
            forward(size)
            right(90)

# Note: ColabTurtle may not support clearing and redrawing
```

---

## Challenge Project: Animated Scene

Create an animated scene that builds over time.

**Requirements:**
- At least 5 different elements
- Elements appear in sequence
- Different speeds for different elements
- Color transitions
- Final composition is complete scene

**Example:**
```python
from ColabTurtle.Turtle import *
import math

def draw_circle(radius, steps=36):
    circumference = 2 * math.pi * radius
    step_length = circumference / steps
    step_angle = 360 / steps
    for i in range(steps):
        forward(step_length)
        right(step_angle)

def animated_scene():
    initializeTurtle(initial_speed=1)
    bgcolor('lightblue')

    # Phase 1: Draw ground (slow)
    speed(2)
    color('green')
    width(50)
    penup()
    # Navigate to ground position
    pendown()
    forward(400)

    # Phase 2: Draw sun (medium)
    speed(5)
    color('yellow')
    width(2)
    penup()
    # Navigate to sun position
    pendown()
    draw_circle(40)

    # Phase 3: Draw tree trunk (slow)
    speed(3)
    color('brown')
    width(10)
    penup()
    # Navigate to tree position
    pendown()
    forward(80)

    # Phase 4: Draw tree foliage (fast)
    speed(10)
    color('green')
    draw_circle(40)

    # Phase 5: Draw flowers (very fast)
    speed(13)
    colors = ['red', 'pink', 'purple', 'yellow']
    for i in range(5):
        penup()
        # Navigate to flower position
        pendown()
        color(colors[i % len(colors)])
        draw_circle(10)

    # Phase 6: Draw clouds (fast)
    speed(10)
    color('white')
    # Draw multiple overlapping circles for clouds

animated_scene()
```

---

## Timing and Pacing

### Variable Speed Pattern

```python
from ColabTurtle.Turtle import *
initializeTurtle()

def rhythm_pattern():
    """Create a pattern with rhythmic speed changes"""
    # Fast-slow-fast-slow pattern
    speeds = [10, 2, 10, 2, 10, 2, 10, 2]
    colors = ['red', 'blue', 'green', 'yellow', 'orange', 'purple', 'cyan', 'magenta']

    size = 20

    for i in range(len(speeds)):
        speed(speeds[i])
        color(colors[i])

        for j in range(4):
            forward(size)
            right(90)

        right(45)
        size += 10

rhythm_pattern()
```

---

## Key Concepts Review

1. **Speed Control:** Use `speed()` to control drawing pace
2. **Progressive Building:** Add elements one at a time
3. **Growing Patterns:** Increase size over iterations
4. **Color Transitions:** Change colors gradually
5. **Rotation Animation:** Rotate shapes around center
6. **Timing:** Control when elements appear

---

## Week 9 Checklist

By the end of this week, you should be able to:

- [ ] Control drawing speed dynamically
- [ ] Create growing patterns
- [ ] Build progressive animations
- [ ] Implement color transitions
- [ ] Create rotating animations
- [ ] Pace elements for visual effect
- [ ] Design animated sequences
- [ ] Build complete animated scenes

---

## Next Week Preview

In Week 10, we'll learn to:
- Use mathematical functions in art
- Create parametric designs
- Generate Lissajous curves
- Work with trigonometry
- Apply golden ratio and Fibonacci

---

## Additional Practice

Create these animations:
1. A clock with moving hands
2. A bouncing ball (simulated)
3. A loading spinner
4. An animated wave
5. Your own animated story

Bring it to life! 🎬🐢
