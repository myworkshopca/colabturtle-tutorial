# Week 5: Patterns & Loops

## Learning Objectives
- Create repeating patterns
- Use nested loops effectively
- Generate circular and spiral patterns
- Create kaleidoscope effects
- Understand pattern mathematics

---

## Table of Contents

- [Introduction](#introduction)
- [Simple Repeating Patterns](#simple-repeating-patterns)
- [Circular Patterns](#circular-patterns)
- [Spiral Patterns](#spiral-patterns)
- [Nested Loop Patterns](#nested-loop-patterns)
- [Rotational Patterns](#rotational-patterns)
- [Geometric Patterns](#geometric-patterns)
- [Practice Exercises](#practice-exercises)
- [Advanced Patterns](#advanced-patterns)
- [Mathematical Patterns](#mathematical-patterns)
- [Challenge Project: Mandala Creator](#challenge-project-mandala-creator)
- [Pattern Design Tips](#pattern-design-tips)
- [Key Concepts Review](#key-concepts-review)
- [Common Mistakes](#common-mistakes)
- [Week 5 Checklist](#week-5-checklist)
- [Next Week Preview](#next-week-preview)
- [Additional Practice](#additional-practice)

---

## Introduction

Patterns are everywhere in nature and art. This week, you'll learn to create beautiful repeating patterns using loops. By combining rotation with repetition, you can create stunning visual effects.

---

## Simple Repeating Patterns

### Line of Squares

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_square(size):
    for i in range(4):
        forward(size)
        right(90)

# Draw 5 squares in a row
for i in range(5):
    draw_square(50)
    penup()
    forward(70)
    pendown()
```

### Alternating Colors

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

colors = ['red', 'blue']

for i in range(10):
    color(colors[i % 2])
    draw_square(40)
    penup()
    forward(50)
    pendown()
```

---

## Circular Patterns

### Circle of Squares

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_square(size):
    for i in range(4):
        forward(size)
        right(90)

# Draw 12 squares in a circle
for i in range(12):
    draw_square(50)
    right(360 / 12)  # 30 degrees
```

### Circle of Triangles

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_triangle(size):
    for i in range(3):
        forward(size)
        right(120)

# Draw 12 triangles in a circle
for i in range(12):
    draw_triangle(60)
    right(30)
```

---

## Spiral Patterns

### Square Spiral

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

size = 10
for i in range(50):
    forward(size)
    right(90)
    size += 5  # Increase size each iteration
```

### Colorful Spiral

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

colors = ['red', 'orange', 'yellow', 'green', 'blue', 'purple']
size = 5

for i in range(100):
    color(colors[i % len(colors)])
    forward(size)
    right(91)  # Slightly more than 90
    size += 2
```

---

## Nested Loop Patterns

### Grid of Squares

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_square(size):
    for i in range(4):
        forward(size)
        right(90)

# Draw 4x4 grid
square_size = 40
spacing = 50

for row in range(4):
    for col in range(4):
        draw_square(square_size)

        # Move to next column
        penup()
        forward(spacing)
        pendown()

    # Move to next row
    penup()
    backward(spacing * 4)
    right(90)
    forward(spacing)
    left(90)
    pendown()
```

### Checkerboard Pattern

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_square(size, fill_color):
    color(fill_color)
    for i in range(4):
        forward(size)
        right(90)

size = 40
colors = ['black', 'white']

for row in range(4):
    for col in range(4):
        color_index = (row + col) % 2
        draw_square(size, colors[color_index])

        penup()
        forward(size)
        pendown()

    penup()
    backward(size * 4)
    right(90)
    forward(size)
    left(90)
    pendown()
```

---

## Rotational Patterns

### Flower Pattern

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=13)

def draw_circle_approx(radius, steps=36):
    circumference = 2 * math.pi * radius
    step_length = circumference / steps
    step_angle = 360 / steps
    for i in range(steps):
        forward(step_length)
        right(step_angle)

# Draw 8 petals in a circle
for i in range(8):
    color('pink')
    draw_circle_approx(40)
    right(45)

# Draw center
color('yellow')
width(20)
forward(1)
```

### Mandala Pattern

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

colors = ['red', 'orange', 'yellow', 'green', 'blue', 'purple']

# Multiple layers
for layer in range(3):
    for i in range(18):
        color(colors[i % len(colors)])
        forward(100 - layer * 20)
        backward(100 - layer * 20)
        right(20)
```

---

## Geometric Patterns

### Star Burst

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

# Draw many lines from center
for i in range(36):
    color('blue')
    forward(100)
    backward(100)
    right(10)
```

### Spirograph Effect

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

colors = ['red', 'blue', 'green', 'orange', 'purple', 'cyan']

for i in range(360):
    color(colors[i % len(colors)])
    forward(i)
    right(59)  # Try different angles: 59, 91, 121, etc.
```

---

## Practice Exercises

### Exercise 1: Rainbow Circles
Draw 7 concentric circles, each in a different rainbow color.

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=13)

colors = ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet']

for i, col in enumerate(colors):
    color(col)
    radius = 20 + i * 10
    draw_circle_approx(radius)
    # Reposition for next circle
```

### Exercise 2: Hexagon Grid
Create a honeycomb pattern with hexagons.

### Exercise 3: Spiral of Squares
Create a spiral where each turn has a square instead of a line.

### Exercise 4: Rotating Triangles
Draw 12 triangles rotating around a center point, each in a different color.

### Exercise 5: Complex Mandala
Create a multi-layered mandala with at least 3 different patterns.

---

## Advanced Patterns

### Fibonacci Spiral (Approximation)

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_square(size):
    for i in range(4):
        forward(size)
        right(90)

# Fibonacci sequence
a, b = 1, 1
for i in range(10):
    draw_square(b * 10)
    right(90)
    a, b = b, a + b
```

### Kaleidoscope Pattern

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_pattern():
    colors = ['red', 'orange', 'yellow']
    for i in range(3):
        color(colors[i])
        forward(80)
        right(120)

# Repeat pattern in circle
for i in range(12):
    draw_pattern()
    right(30)
```

### Wave Pattern

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

# Create wave effect
for i in range(20):
    forward(20)
    right(30)
    forward(20)
    left(60)
    forward(20)
    right(30)
```

---

## Mathematical Patterns

### Polygons Inscribed in Circle

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_polygon(sides, size):
    angle = 360 / sides
    for i in range(sides):
        forward(size)
        right(angle)

# Draw polygons from 3 to 8 sides
colors = ['red', 'orange', 'yellow', 'green', 'blue', 'purple']
for sides in range(3, 9):
    color(colors[(sides - 3) % len(colors)])
    draw_polygon(sides, 60)
```

### Golden Spiral Approximation

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

# Golden ratio approximation
size = 5
for i in range(60):
    forward(size)
    right(89)
    size += 0.618  # Golden ratio
```

---

## Challenge Project: Mandala Creator

Create a function that generates customizable mandalas.

**Requirements:**
- Function with parameters: layers, petals, colors
- At least 3 different pattern types
- Smooth transitions between layers
- Color gradients

**Example:**
```python
from ColabTurtle.Turtle import *
import math

def draw_circle_approx(radius, steps=36):
    circumference = 2 * math.pi * radius
    step_length = circumference / steps
    step_angle = 360 / steps
    for i in range(steps):
        forward(step_length)
        right(step_angle)

def draw_petal(size):
    """Draw a single petal shape"""
    for i in range(2):
        draw_circle_approx(size, 36)
        left(90)

def draw_mandala(layers=3, petals=8, colors=None):
    """
    Draw a customizable mandala

    Parameters:
    -----------
    layers : int
        Number of concentric layers
    petals : int
        Number of petals per layer
    colors : list
        List of colors to use
    """
    if colors is None:
        colors = ['red', 'orange', 'yellow', 'green', 'blue', 'purple']

    initializeTurtle(initial_speed=13)
    bgcolor('black')

    # Draw each layer
    for layer in range(layers, 0, -1):
        radius = layer * 30

        # Draw petals in circle
        for i in range(petals):
            color(colors[i % len(colors)])

            # Draw petal
            draw_circle_approx(radius, 36)

            # Rotate for next petal
            right(360 / petals)

    # Draw center
    color('yellow')
    width(20)
    forward(1)

# Create mandala
draw_mandala(4, 12, ['red', 'pink', 'orange', 'yellow', 'white'])
```

---

## Pattern Design Tips

1. **Start Simple:** Begin with basic repeating shapes
2. **Add Rotation:** Rotate slightly after each iteration
3. **Vary Size:** Increase or decrease size progressively
4. **Color Cycling:** Use modulo to cycle through colors
5. **Experiment with Angles:** Small angle changes create interesting effects
6. **Layer Patterns:** Combine multiple pattern types
7. **Use Symmetry:** Repeat patterns at regular intervals

---

## Key Concepts Review

1. **Repetition:** Use loops to repeat patterns
2. **Rotation:** Combine rotation with repetition for circular patterns
3. **Nested Loops:** Create 2D grids and complex patterns
4. **Incremental Change:** Gradually modify size, angle, or color
5. **Modulo Operator:** Cycle through arrays with `i % length`
6. **Symmetry:** Regular intervals create balanced designs

---

## Common Mistakes

### Mistake 1: Wrong Rotation Angle
```python
# ❌ For 12 items in a circle
for i in range(12):
    draw_shape()
    right(12)  # Wrong! Should be 360/12 = 30

# ✅ Correct
for i in range(12):
    draw_shape()
    right(360 / 12)  # 30 degrees
```

### Mistake 2: Not Returning to Center
```python
# For circular patterns, make sure shape returns to center
# Or move back to center after drawing
```

### Mistake 3: Grid Positioning Errors
```python
# Remember to reset position after each row
# Use backward() to return to start of row
```

---

## Week 5 Checklist

By the end of this week, you should be able to:

- [ ] Create linear repeating patterns
- [ ] Generate circular patterns
- [ ] Draw spirals (square, circular)
- [ ] Use nested loops for 2D patterns
- [ ] Create kaleidoscope effects
- [ ] Design mandalas
- [ ] Apply mathematical patterns
- [ ] Combine multiple pattern types

---

## Next Week Preview

In Week 6, we'll learn to:
- Navigate to specific coordinates
- Use absolute positioning
- Create grid-based drawings
- Implement coordinate systems
- Build location-aware patterns

---

## Additional Practice

Create these patterns:
1. A spiral galaxy effect
2. A flower garden (multiple flowers arranged in pattern)
3. A geometric tessellation
4. An Islamic art-inspired pattern
5. Your own original mandala design

Keep creating beautiful patterns! 🌸🐢
