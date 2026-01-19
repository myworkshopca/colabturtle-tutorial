# Week 4: Functions & Modularity

## Learning Objectives
- Create reusable drawing functions
- Use parameters for flexibility
- Build a library of shapes
- Understand function returns
- Save and restore turtle state

---

## Table of Contents

- [Introduction](#introduction)
- [Basic Function Structure](#basic-function-structure)
- [Functions with Multiple Parameters](#functions-with-multiple-parameters)
- [Building a Shape Library](#building-a-shape-library)
- [Default Parameters](#default-parameters)
- [Saving and Restoring Position](#saving-and-restoring-position)
- [Advanced Function Examples](#advanced-function-examples)
- [Practice Exercises](#practice-exercises)
- [Function Documentation](#function-documentation)
- [Challenge Project: Scene Builder](#challenge-project-scene-builder)
- [Key Concepts Review](#key-concepts-review)
- [Common Mistakes](#common-mistakes)
- [Week 4 Checklist](#week-4-checklist)
- [Next Week Preview](#next-week-preview)
- [Additional Practice](#additional-practice)

---

## Introduction

This week focuses on code organization and reusability. Functions allow you to write code once and use it many times with different parameters. This is essential for creating complex drawings efficiently.

---

## Basic Function Structure

### Simple Function

```python
from ColabTurtle.Turtle import *
initializeTurtle()

def draw_square():
    for i in range(4):
        forward(100)
        right(90)

# Use the function
draw_square()
```

### Function with Parameters

```python
from ColabTurtle.Turtle import *
initializeTurtle()

def draw_square(size):
    for i in range(4):
        forward(size)
        right(90)

# Use with different sizes
draw_square(50)
penup()
forward(150)
pendown()
draw_square(100)
```

---

## Functions with Multiple Parameters

### Square with Size and Color

```python
from ColabTurtle.Turtle import *
initializeTurtle()

def draw_square(size, color_name):
    color(color_name)
    for i in range(4):
        forward(size)
        right(90)

# Draw different squares
draw_square(50, 'red')
penup()
forward(150)
pendown()
draw_square(80, 'blue')
```

### Rectangle Function

```python
def draw_rectangle(width, height, color_name):
    color(color_name)
    for i in range(2):
        forward(width)
        right(90)
        forward(height)
        right(90)

# Use it
draw_rectangle(120, 60, 'green')
```

---

## Building a Shape Library

### Complete Shape Library

```python
from ColabTurtle.Turtle import *
initializeTurtle()

def draw_square(size, color_name='black'):
    """Draw a square of given size and color"""
    color(color_name)
    for i in range(4):
        forward(size)
        right(90)

def draw_triangle(size, color_name='black'):
    """Draw an equilateral triangle"""
    color(color_name)
    for i in range(3):
        forward(size)
        right(120)

def draw_hexagon(size, color_name='black'):
    """Draw a hexagon"""
    color(color_name)
    for i in range(6):
        forward(size)
        right(60)

def draw_circle_approx(radius, color_name='black', steps=36):
    """Draw a circle by approximating with small lines"""
    import math
    color(color_name)
    circumference = 2 * math.pi * radius
    step_length = circumference / steps
    step_angle = 360 / steps

    for i in range(steps):
        forward(step_length)
        right(step_angle)

def draw_star(size, color_name='black', points=5):
    """Draw a star with specified points"""
    color(color_name)
    angle = 180 - (180 / points)
    for i in range(points):
        forward(size)
        right(angle)
```

---

## Default Parameters

### Using Default Values

```python
def draw_polygon(sides, size, color_name='black', line_width=2):
    """Draw any regular polygon with defaults"""
    color(color_name)
    width(line_width)
    angle = 360 / sides

    for i in range(sides):
        forward(size)
        right(angle)

# Use with defaults
draw_polygon(6, 80)  # Black hexagon, width 2

# Use with custom values
draw_polygon(5, 100, 'red', 5)  # Red pentagon, width 5

# Use some defaults
draw_polygon(8, 60, 'blue')  # Blue octagon, width 2 (default)
```

---

## Saving and Restoring Position

### Manual Position Tracking

```python
from ColabTurtle.Turtle import *
initializeTurtle()

def draw_square_and_return(size, color_name):
    """Draw square and return to starting position"""
    color(color_name)

    # Draw square
    for i in range(4):
        forward(size)
        right(90)

    # Note: Turtle is already back at start after completing square

# Draw multiple squares from same point
draw_square_and_return(100, 'red')
draw_square_and_return(80, 'blue')
draw_square_and_return(60, 'green')
```

### Move, Draw, Return Pattern

```python
def draw_shape_at_offset(shape_func, x_offset, y_offset, *args):
    """Draw a shape at an offset position and return"""
    # Move to offset
    penup()
    forward(x_offset)
    right(90)
    forward(y_offset)
    left(90)
    pendown()

    # Draw shape
    shape_func(*args)

    # Return
    penup()
    left(90)
    backward(y_offset)
    right(90)
    backward(x_offset)
    pendown()

# Use it
draw_shape_at_offset(draw_square, 100, 0, 50, 'red')
draw_shape_at_offset(draw_triangle, 200, 0, 60, 'blue')
```

---

## Advanced Function Examples

### Concentric Shapes

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_concentric_squares(count, initial_size, size_step, colors):
    """Draw multiple squares inside each other"""
    size = initial_size

    for i in range(count):
        color(colors[i % len(colors)])
        draw_square(size, colors[i % len(colors)])

        # Move inward for next square
        penup()
        forward(size_step / 2)
        right(90)
        forward(size_step / 2)
        left(90)
        pendown()

        size -= size_step

# Use it
colors = ['red', 'orange', 'yellow', 'green', 'blue']
draw_concentric_squares(5, 200, 30, colors)
```

### Flower Function

```python
def draw_flower(petals, petal_size, petal_color, center_color):
    """Draw a flower with specified petals"""
    # Draw petals
    for i in range(petals):
        color(petal_color)
        draw_circle_approx(petal_size)
        right(360 / petals)

    # Draw center
    color(center_color)
    width(petal_size)
    forward(1)  # Draw a dot
    width(2)  # Reset width

# Use it
draw_flower(6, 30, 'pink', 'yellow')
```

---

## Practice Exercises

### Exercise 1: House Function
Create a function that draws a house with customizable size and colors.

```python
def draw_house(size, body_color, roof_color):
    """Draw a simple house"""
    # House body
    draw_square(size, body_color)

    # Roof
    color(roof_color)
    for i in range(3):
        forward(size)
        right(120)

    # Door (optional)
    # Window (optional)
```

### Exercise 2: Tree Function
Create a simple tree function with trunk and foliage.

```python
def draw_tree(trunk_height, trunk_color, foliage_size, foliage_color):
    """Draw a simple tree"""
    # Trunk (rectangle)
    color(trunk_color)
    width(10)
    forward(trunk_height)
    width(2)

    # Foliage (circle or triangle)
    color(foliage_color)
    draw_triangle(foliage_size, foliage_color)
```

### Exercise 3: Row of Shapes
Create a function that draws a row of shapes with spacing.

```python
def draw_row(shape_func, count, spacing, *shape_args):
    """Draw a row of shapes"""
    for i in range(count):
        shape_func(*shape_args)
        penup()
        forward(spacing)
        pendown()
```

### Exercise 4: Grid Function
Create a function to draw shapes in a grid pattern.

### Exercise 5: Custom Pattern Function
Design your own reusable pattern function.

---

## Function Documentation

### Using Docstrings

```python
def draw_polygon(sides, size, color_name='black'):
    """
    Draw a regular polygon.

    Parameters:
    -----------
    sides : int
        Number of sides (must be >= 3)
    size : int
        Length of each side in pixels
    color_name : str, optional
        Color of the polygon (default is 'black')

    Example:
    --------
    draw_polygon(6, 80, 'blue')  # Blue hexagon
    """
    color(color_name)
    angle = 360 / sides
    for i in range(sides):
        forward(size)
        right(angle)
```

---

## Challenge Project: Scene Builder

Create a complete scene using modular functions.

**Requirements:**
- At least 5 different shape functions
- At least 2 compound functions (functions that use other functions)
- Use default parameters
- Include docstrings
- Create a main function that composes the scene

**Example:**
```python
from ColabTurtle.Turtle import *
import math

def draw_square(size, color_name='black'):
    """Draw a square"""
    color(color_name)
    for i in range(4):
        forward(size)
        right(90)

def draw_triangle(size, color_name='black'):
    """Draw a triangle"""
    color(color_name)
    for i in range(3):
        forward(size)
        right(120)

def draw_circle_approx(radius, color_name='black', steps=36):
    """Draw a circle"""
    color(color_name)
    circumference = 2 * math.pi * radius
    step_length = circumference / steps
    step_angle = 360 / steps
    for i in range(steps):
        forward(step_length)
        right(step_angle)

def draw_house(size, body_color='brown', roof_color='red'):
    """Draw a house with square body and triangle roof"""
    draw_square(size, body_color)
    draw_triangle(size, roof_color)

def draw_tree(trunk_height, trunk_color='brown', foliage_color='green'):
    """Draw a simple tree"""
    # Trunk
    color(trunk_color)
    width(8)
    forward(trunk_height)
    width(2)

    # Foliage
    draw_circle_approx(trunk_height / 2, foliage_color)

    # Return
    backward(trunk_height)

def draw_sun(radius, color_name='yellow'):
    """Draw a sun with rays"""
    # Center circle
    draw_circle_approx(radius, color_name)

    # Rays
    for i in range(12):
        penup()
        forward(radius)
        pendown()
        forward(radius / 2)
        backward(radius / 2)
        penup()
        backward(radius)
        pendown()
        right(30)

def draw_scene():
    """Draw a complete landscape scene"""
    initializeTurtle(initial_speed=13)
    bgcolor('lightblue')

    # Sun
    penup()
    # Navigate to sun position
    left(90)
    forward(150)
    right(90)
    backward(100)
    pendown()
    draw_sun(30, 'yellow')

    # House
    penup()
    # Navigate to house position
    pendown()
    draw_house(80, 'brown', 'red')

    # Trees
    penup()
    # Navigate to tree positions
    pendown()
    draw_tree(60, 'brown', 'green')

    # Ground
    color('green')
    width(5)
    # Draw ground line...

# Run the scene
draw_scene()
```

---

## Key Concepts Review

1. **Functions**: Reusable blocks of code
2. **Parameters**: Input values that make functions flexible
3. **Default Parameters**: Optional values with defaults
4. **Docstrings**: Documentation for functions
5. **Modularity**: Breaking complex tasks into simple functions
6. **Composition**: Building complex shapes from simple functions

---

## Common Mistakes

### Mistake 1: Forgetting to Call Function
```python
# ❌ Wrong - function defined but not called
def draw_square(size):
    for i in range(4):
        forward(size)
        right(90)
# Nothing happens!

# ✅ Correct
def draw_square(size):
    for i in range(4):
        forward(size)
        right(90)

draw_square(100)  # Now it draws
```

### Mistake 2: Wrong Parameter Order
```python
def draw_rectangle(width, height, color_name):
    # ...

# ❌ Wrong
draw_rectangle('red', 100, 50)  # Color in wrong position

# ✅ Correct
draw_rectangle(100, 50, 'red')  # Correct order
```

### Mistake 3: Not Returning to Start
```python
# Consider if your function should return to start position
# or leave the turtle where it ends
```

---

## Week 4 Checklist

By the end of this week, you should be able to:

- [ ] Create functions with no parameters
- [ ] Create functions with multiple parameters
- [ ] Use default parameter values
- [ ] Write docstrings for functions
- [ ] Build a reusable shape library
- [ ] Compose complex drawings from simple functions
- [ ] Save and restore turtle position (manually)
- [ ] Organize code with proper structure

---

## Next Week Preview

In Week 5, we'll learn to:
- Create repeating patterns with loops
- Use nested loops for 2D patterns
- Generate circular and spiral patterns
- Create kaleidoscope effects
- Design tessellations

---

## Additional Practice

Build these function libraries:
1. Geometric shapes library (5+ shapes)
2. Nature library (tree, flower, cloud, sun)
3. Building library (house, building, door, window)
4. Transportation library (car, boat, plane - simple versions)

Keep building your toolkit! 🔧🐢
