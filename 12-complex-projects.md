# Week 12: Complex Projects

## Learning Objectives
- Combine multiple techniques
- Plan complex drawings
- Create detailed scenes
- Use composition effectively
- Build layered artwork
- Design portfolio-quality pieces

---

## Table of Contents

- [Introduction](#introduction)
- [Project Planning](#project-planning)
- [Scene Composition](#scene-composition)
- [Complete Scene Examples](#complete-scene-examples)
- [Nature Scenes](#nature-scenes)
- [Abstract Compositions](#abstract-compositions)
- [Practice Exercises](#practice-exercises)
- [Challenge Project: Portfolio Piece](#challenge-project-portfolio-piece)
- [Code Organization](#code-organization)
- [Week 12 Checklist](#week-12-checklist)
- [Next Week Preview](#next-week-preview)
- [Additional Practice](#additional-practice)

---

## Introduction

This week brings together everything you've learned. You'll plan and execute complex projects that showcase your mastery of turtle graphics, combining shapes, patterns, colors, recursion, randomness, and mathematics into complete artworks.

---

## Project Planning

### Planning Checklist

Before starting a complex project:

1. **Concept**: What are you creating?
2. **Sketch**: Draw it on paper first
3. **Break Down**: List main components
4. **Functions**: Identify reusable functions needed
5. **Order**: Decide drawing sequence (background first!)
6. **Colors**: Choose color palette
7. **Test**: Create simplified version first

### Example Plan

**Project**: Forest Scene

**Components:**
- Sky (background)
- Sun/moon
- Mountains (background)
- Trees (various sizes)
- Ground/grass
- Flowers
- Birds (optional)

**Functions Needed:**
- `draw_sky()` - gradient background
- `draw_sun()` - circle with rays
- `draw_mountain()` - triangle
- `draw_tree()` - recursive tree
- `draw_flower()` - circle petals
- `draw_bird()` - V shape

---

## Scene Composition

### Layering Principle

Draw from **back to front**:
1. Background (sky)
2. Far elements (mountains, sun)
3. Middle elements (large trees)
4. Near elements (flowers, grass)
5. Foreground elements (birds, details)

### Example: Simple Scene

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=13)

# Layer 1: Sky
bgcolor('lightblue')

# Layer 2: Sun
penup()
# Navigate to sun position (-150, 100)
pendown()
color('yellow')
draw_circle(40)

# Layer 3: Ground
color('green')
width(100)
penup()
# Navigate to ground level
pendown()
forward(400)

# Layer 4: Tree
penup()
# Navigate to tree position
pendown()
draw_tree(80, 7)

# Layer 5: Flowers
# Draw multiple flowers
```

---

## Complete Scene Examples

### Beach Scene

```python
from ColabTurtle.Turtle import *
import math
import random
initializeTurtle(initial_speed=13)

def draw_circle(radius, steps=36):
    circumference = 2 * math.pi * radius
    step_length = circumference / steps
    step_angle = 360 / steps
    for i in range(steps):
        forward(step_length)
        right(step_angle)

def draw_wave(width, height):
    """Draw a simple wave"""
    for i in range(4):
        if i % 2 == 0:
            draw_arc(height, 180)
        else:
            draw_arc(height, -180)

def draw_palm_tree(trunk_height):
    """Draw a palm tree"""
    # Trunk
    color('brown')
    width(10)
    left(90)
    forward(trunk_height)
    width(2)

    # Fronds (leaves)
    color('green')
    for i in range(6):
        forward(trunk_height // 2)
        backward(trunk_height // 2)
        right(60)

    # Return
    right(90)
    backward(trunk_height)

def beach_scene():
    """Complete beach scene"""
    # Sky
    bgcolor('lightblue')

    # Sun
    penup()
    # Navigate to sun position
    pendown()
    color('yellow')
    draw_circle(50)

    # Ocean
    color('blue')
    width(60)
    penup()
    # Navigate to ocean level
    pendown()
    forward(400)

    # Beach/sand
    color('lightyellow')
    width(80)
    penup()
    # Navigate below ocean
    pendown()
    forward(400)

    # Palm trees
    positions = [(-150, -50), (150, -50)]
    for x, y in positions:
        penup()
        # Navigate to position
        pendown()
        draw_palm_tree(100)

    # Clouds
    color('white')
    cloud_positions = [(-180, 120), (0, 140), (180, 110)]
    for x, y in cloud_positions:
        penup()
        # Navigate and draw cloud (3 overlapping circles)
        pendown()

# Create scene
beach_scene()
```

### City Skyline

```python
from ColabTurtle.Turtle import *
import random
initializeTurtle(initial_speed=13)

def draw_rectangle(width, height):
    """Draw a rectangle"""
    for i in range(2):
        forward(width)
        left(90)
        forward(height)
        left(90)

def draw_building(width, height, window_rows, window_cols):
    """
    Draw a building with windows

    Parameters:
    -----------
    width : int
        Building width
    height : int
        Building height
    window_rows : int
        Number of window rows
    window_cols : int
        Number of window columns
    """
    # Building outline
    color('gray')
    draw_rectangle(width, height)

    # Windows
    window_width = width / (window_cols + 1)
    window_height = height / (window_rows + 1)

    for row in range(window_rows):
        for col in range(window_cols):
            # Calculate window position
            x_offset = window_width * (col + 1) - window_width / 4
            y_offset = window_height * (row + 1) - window_height / 4

            # Draw window
            penup()
            forward(x_offset)
            left(90)
            forward(y_offset)
            right(90)
            pendown()

            # Window (small square or just a dot)
            color(random.choice(['yellow', 'white', 'orange']))
            width(window_width / 2)
            forward(1)
            width(2)

            # Return to building base
            penup()
            left(90)
            backward(y_offset)
            right(90)
            backward(x_offset)
            pendown()

def city_skyline():
    """Draw a city skyline"""
    bgcolor('darkblue')

    # Stars
    color('white')
    for i in range(30):
        penup()
        x = random.randint(-250, 250)
        y = random.randint(50, 180)
        # Navigate to (x, y)
        pendown()
        width(2)
        forward(1)

    # Moon
    penup()
    # Navigate to moon position
    pendown()
    color('lightyellow')
    draw_circle(40)

    # Ground
    color('black')
    width(120)
    penup()
    # Navigate to ground level
    pendown()
    forward(500)

    # Buildings
    buildings = [
        (50, 120, 8, 3),
        (70, 180, 12, 4),
        (60, 100, 6, 3),
        (80, 200, 14, 5),
        (55, 140, 9, 3),
        (75, 160, 11, 4),
    ]

    penup()
    # Navigate to leftmost building position
    pendown()

    for width, height, rows, cols in buildings:
        draw_building(width, height, rows, cols)
        penup()
        forward(width + 5)
        pendown()

# Create skyline
city_skyline()
```

---

## Nature Scenes

### Forest Scene

```python
from ColabTurtle.Turtle import *
import random
initializeTurtle(initial_speed=13)

def draw_tree(branch_length, depth):
    """Recursive tree"""
    if depth == 0 or branch_length < 5:
        color('green')
        width(5)
        forward(1)
        width(2)
        return

    color('brown' if depth > 3 else 'darkgreen')
    width(depth // 2)
    forward(branch_length)

    right(random.randint(20, 30))
    draw_tree(branch_length * 0.7, depth - 1)

    left(random.randint(40, 60))
    draw_tree(branch_length * 0.7, depth - 1)

    right(random.randint(20, 30))
    backward(branch_length)
    width(2)

def draw_mountain(size):
    """Draw a mountain"""
    color('darkgray')
    left(60)
    forward(size)
    right(120)
    forward(size)
    left(60)

def draw_flower(petal_count, petal_size):
    """Simple flower"""
    for i in range(petal_count):
        color('pink')
        draw_circle(petal_size)
        right(360 / petal_count)

    color('yellow')
    draw_circle(petal_size / 2)

def forest_scene():
    """Complete forest scene"""
    # Sky
    bgcolor('lightblue')

    # Sun
    penup()
    # Navigate to sun position
    pendown()
    color('yellow')
    draw_circle(50)

    # Mountains (background)
    mountain_positions = [(-200, -100), (0, -100), (200, -100)]
    for x, y in mountain_positions:
        penup()
        # Navigate to position
        pendown()
        draw_mountain(100)

    # Ground
    color('green')
    width(80)
    penup()
    # Navigate to ground level
    pendown()
    forward(500)
    width(2)

    # Trees (various sizes and positions)
    tree_configs = [
        (-150, -20, 60, 6),
        (-50, -20, 80, 7),
        (100, -20, 70, 7),
        (200, -20, 65, 6),
    ]

    for x, y, length, depth in tree_configs:
        penup()
        # Navigate to position
        left(90)
        pendown()
        draw_tree(length, depth)
        right(90)

    # Flowers
    flower_positions = [(-120, -60), (-80, -65), (150, -58), (180, -62)]
    for x, y in flower_positions:
        penup()
        # Navigate to position
        pendown()
        draw_flower(6, 15)

# Create forest
forest_scene()
```

---

## Abstract Compositions

### Geometric Abstract Art

```python
from ColabTurtle.Turtle import *
import random
initializeTurtle(initial_speed=13)

def geometric_composition():
    """Create abstract geometric art"""
    bgcolor('black')

    shapes = ['circle', 'square', 'triangle', 'hexagon']
    colors = ['red', 'blue', 'cyan', 'yellow', 'magenta', 'white']

    # Large background shapes
    for i in range(5):
        penup()
        x = random.randint(-200, 200)
        y = random.randint(-150, 150)
        # Navigate to (x, y)
        pendown()

        shape = random.choice(shapes)
        color(random.choice(colors))
        width(3)

        size = random.randint(80, 150)

        if shape == 'circle':
            draw_circle(size // 2)
        elif shape == 'square':
            for j in range(4):
                forward(size)
                right(90)
        elif shape == 'triangle':
            for j in range(3):
                forward(size)
                right(120)
        elif shape == 'hexagon':
            for j in range(6):
                forward(size // 2)
                right(60)

    # Small foreground details
    width(1)
    for i in range(30):
        penup()
        x = random.randint(-250, 250)
        y = random.randint(-180, 180)
        # Navigate to (x, y)
        pendown()

        color(random.choice(colors))
        size = random.randint(10, 30)

        for j in range(random.choice([3, 4, 5, 6])):
            forward(size)
            right(360 / random.choice([3, 4, 5, 6]))

# Create composition
geometric_composition()
```

---

## Practice Exercises

### Exercise 1: Underwater Scene
Create an underwater scene with fish, coral, and bubbles.

**Components:**
- Blue gradient water background
- Sea floor
- Coral formations
- Fish (multiple sizes)
- Bubbles rising
- Seaweed

### Exercise 2: Space Scene
Draw a space scene with planets, stars, and a rocket.

### Exercise 3: Garden Scene
Create a garden with various flowers, butterflies, and a fence.

### Exercise 4: Weather Scene
Draw a scene showing specific weather (rain, snow, or storm).

### Exercise 5: Abstract Pattern Art
Create a large abstract pattern composition.

---

## Challenge Project: Portfolio Piece

Create a complex, portfolio-quality artwork.

**Requirements:**
- At least 7 different elements
- Uses at least 5 techniques from the course
- Well-planned composition
- Proper layering
- Color harmony
- Minimum 300 lines of code
- Clean, documented code
- Reusable functions

**Suggested Topics:**
1. Seasonal landscape (spring/summer/fall/winter)
2. Cultural scene (festival, celebration)
3. Fantasy world
4. Futuristic city
5. Natural phenomenon (aurora, eclipse, etc.)

**Example Structure:**
```python
from ColabTurtle.Turtle import *
import math
import random

# ============================================
# HELPER FUNCTIONS
# ============================================

def draw_circle(radius, steps=36):
    """Draw a circle"""
    circumference = 2 * math.pi * radius
    step_length = circumference / steps
    step_angle = 360 / steps
    for i in range(steps):
        forward(step_length)
        right(step_angle)

def draw_star(size, points=5):
    """Draw a star"""
    angle = 180 - (180 / points)
    for i in range(points):
        forward(size)
        right(angle)

# ... more helper functions

# ============================================
# COMPONENT FUNCTIONS
# ============================================

def draw_background():
    """Draw the background layer"""
    pass

def draw_far_elements():
    """Draw distant elements"""
    pass

def draw_middle_elements():
    """Draw middle-distance elements"""
    pass

def draw_near_elements():
    """Draw foreground elements"""
    pass

def draw_details():
    """Add final details"""
    pass

# ============================================
# MAIN COMPOSITION
# ============================================

def create_masterpiece():
    """Compose the complete artwork"""
    initializeTurtle(initial_speed=13)

    # Layer 1: Background
    draw_background()

    # Layer 2: Far elements
    draw_far_elements()

    # Layer 3: Middle elements
    draw_middle_elements()

    # Layer 4: Near elements
    draw_near_elements()

    # Layer 5: Details
    draw_details()

# Execute
create_masterpiece()
```

---

## Code Organization

### Best Practices

```python
# 1. Imports at top
from ColabTurtle.Turtle import *
import math
import random

# 2. Constants
CANVAS_WIDTH = 500
CANVAS_HEIGHT = 400
COLORS = ['red', 'blue', 'green']

# 3. Helper functions
def helper_function():
    pass

# 4. Component functions
def draw_component():
    pass

# 5. Main composition
def main():
    initializeTurtle(initial_speed=13)
    # ...

# 6. Execute
if __name__ == '__main__':
    main()
```

---

## Week 12 Checklist

By the end of this week, you should be able to:

- [ ] Plan complex projects
- [ ] Create detailed scenes
- [ ] Use proper layering
- [ ] Compose multiple elements
- [ ] Write organized code
- [ ] Build portfolio pieces
- [ ] Combine all learned techniques
- [ ] Create original artwork

---

## Next Week Preview

Week 13 is your **Final Project Week**! You'll:
- Plan and execute a capstone project
- Apply all skills learned
- Create presentation-ready work
- Build your portfolio
- Reflect on your journey

---

## Additional Practice

Plan and create:
1. A scene from your favorite book
2. A representation of a memory
3. A cultural celebration
4. A dream landscape
5. An original concept

You've got this! 🎨🐢
