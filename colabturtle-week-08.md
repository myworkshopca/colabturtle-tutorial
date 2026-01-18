# Week 8: Recursion & Fractals

## Learning Objectives
- Understand recursive functions
- Create fractal patterns
- Draw tree structures
- Generate Koch curves
- Implement Sierpinski triangles
- Explore L-systems basics

---

## Introduction

Recursion is when a function calls itself. This powerful technique is perfect for creating fractals - infinitely complex patterns that are self-similar at different scales. This week unlocks a whole new level of turtle graphics!

---

## Understanding Recursion

### Basic Recursive Function

```python
def countdown(n):
    """Simple recursive countdown"""
    if n <= 0:  # Base case
        print("Done!")
    else:
        print(n)
        countdown(n - 1)  # Recursive call

countdown(5)
# Output: 5, 4, 3, 2, 1, Done!
```

### Recursive Drawing Concept

```python
from ColabTurtle.Turtle import *
initializeTurtle()

def draw_recursive_line(length, depth):
    """Draw a line that splits into smaller lines"""
    if depth == 0:  # Base case
        forward(length)
    else:  # Recursive case
        draw_recursive_line(length / 2, depth - 1)
        left(60)
        draw_recursive_line(length / 2, depth - 1)
        right(120)
        draw_recursive_line(length / 2, depth - 1)
        left(60)

draw_recursive_line(100, 3)
```

---

## Fractal Trees

### Simple Binary Tree

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_tree(branch_length, angle=25, depth=3):
    """
    Draw a recursive fractal tree

    Parameters:
    -----------
    branch_length : int
        Length of the current branch
    angle : int
        Angle of branching
    depth : int
        Recursion depth (number of levels)
    """
    if depth == 0 or branch_length < 5:  # Base case
        return

    # Draw branch
    forward(branch_length)

    # Right sub-tree
    right(angle)
    draw_tree(branch_length * 0.7, angle, depth - 1)

    # Left sub-tree
    left(angle * 2)
    draw_tree(branch_length * 0.7, angle, depth - 1)

    # Return to starting position
    right(angle)
    backward(branch_length)

# Position turtle and draw tree
left(90)
penup()
backward(150)
pendown()
draw_tree(80, 25, 7)
```

### Tree with Color Gradients

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_colored_tree(branch_length, depth, max_depth):
    """Draw tree with color changing by depth"""
    if depth == 0 or branch_length < 5:
        return

    # Color based on depth
    if depth > max_depth / 2:
        color('brown')
        width(depth)
    else:
        color('green')
        width(2)

    forward(branch_length)

    # Right branch
    right(20)
    draw_colored_tree(branch_length * 0.75, depth - 1, max_depth)

    # Left branch
    left(40)
    draw_colored_tree(branch_length * 0.75, depth - 1, max_depth)

    # Return
    right(20)
    backward(branch_length)

# Draw tree
bgcolor('lightblue')
left(90)
penup()
backward(150)
pendown()
draw_colored_tree(100, 10, 10)
```

---

## Koch Curve

### Koch Curve (Snowflake Edge)

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def koch_curve(length, depth):
    """
    Draw a Koch curve

    Parameters:
    -----------
    length : int
        Length of the curve
    depth : int
        Recursion depth (0 = straight line)
    """
    if depth == 0:
        forward(length)
    else:
        length /= 3.0
        koch_curve(length, depth - 1)
        left(60)
        koch_curve(length, depth - 1)
        right(120)
        koch_curve(length, depth - 1)
        left(60)
        koch_curve(length, depth - 1)

# Draw Koch curve
koch_curve(300, 4)
```

### Koch Snowflake

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def koch_snowflake(length, depth):
    """Draw a complete Koch snowflake (3 sides)"""
    for i in range(3):
        koch_curve(length, depth)
        right(120)

# Draw snowflake
penup()
backward(150)
left(90)
backward(50)
right(90)
pendown()

color('cyan')
bgcolor('darkblue')
koch_snowflake(300, 4)
```

---

## Sierpinski Triangle

### Sierpinski Triangle

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_triangle(size):
    """Draw an equilateral triangle"""
    for i in range(3):
        forward(size)
        left(120)

def sierpinski(size, depth):
    """
    Draw Sierpinski triangle

    Parameters:
    -----------
    size : int
        Size of the triangle
    depth : int
        Recursion depth
    """
    if depth == 0:
        draw_triangle(size)
    else:
        # Draw three smaller triangles
        sierpinski(size / 2, depth - 1)

        penup()
        forward(size / 2)
        pendown()

        sierpinski(size / 2, depth - 1)

        penup()
        backward(size / 2)
        left(60)
        forward(size / 2)
        right(60)
        pendown()

        sierpinski(size / 2, depth - 1)

        # Return to start
        penup()
        left(60)
        backward(size / 2)
        right(60)
        pendown()

# Draw Sierpinski triangle
color('blue')
sierpinski(200, 4)
```

---

## Dragon Curve

### Dragon Curve

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def dragon_curve(length, depth, direction=1):
    """
    Draw a dragon curve

    Parameters:
    -----------
    length : int
        Length of each segment
    depth : int
        Recursion depth
    direction : int
        1 for right, -1 for left
    """
    if depth == 0:
        forward(length)
    else:
        dragon_curve(length, depth - 1, 1)
        right(90 * direction)
        dragon_curve(length, depth - 1, -1)

# Draw dragon curve
color('red')
dragon_curve(5, 12, 1)
```

---

## Hilbert Curve

### Hilbert Curve

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def hilbert(length, depth, angle):
    """
    Draw Hilbert curve

    Parameters:
    -----------
    length : int
        Length of each segment
    depth : int
        Recursion depth
    angle : int
        Turning angle (90 or -90)
    """
    if depth == 0:
        return

    right(angle)
    hilbert(length, depth - 1, -angle)
    forward(length)
    left(angle)
    hilbert(length, depth - 1, angle)
    forward(length)
    hilbert(length, depth - 1, angle)
    left(angle)
    forward(length)
    hilbert(length, depth - 1, -angle)
    right(angle)

# Draw Hilbert curve
color('purple')
hilbert(10, 5, 90)
```

---

## Practice Exercises

### Exercise 1: Asymmetric Tree
Create a tree where left and right branches have different angles and lengths.

```python
def asymmetric_tree(length, left_angle, right_angle, depth):
    if depth == 0:
        return

    forward(length)

    right(right_angle)
    asymmetric_tree(length * 0.6, left_angle, right_angle, depth - 1)

    left(right_angle + left_angle)
    asymmetric_tree(length * 0.8, left_angle, right_angle, depth - 1)

    right(left_angle)
    backward(length)
```

### Exercise 2: Barnsley Fern
Research and implement the Barnsley Fern fractal.

### Exercise 3: Recursive Spirals
Create a spiral made of smaller spirals.

### Exercise 4: Fractal Mountain Range
Use recursion to create a mountain silhouette.

### Exercise 5: Custom Fractal
Design your own unique fractal pattern.

---

## Advanced Examples

### Colorful Fractal Tree

```python
from ColabTurtle.Turtle import *
import random
initializeTurtle(initial_speed=13)

def colorful_tree(length, depth, colors):
    """Tree with random colors"""
    if depth == 0 or length < 5:
        # Draw leaves
        color(random.choice(['green', 'lightgreen', 'darkgreen']))
        width(5)
        forward(1)
        width(2)
        return

    # Branch color
    color(colors[min(depth, len(colors) - 1)])
    width(max(1, depth // 2))

    forward(length)

    # Random angles
    angle1 = random.randint(15, 35)
    angle2 = random.randint(15, 35)

    right(angle1)
    colorful_tree(length * 0.7, depth - 1, colors)

    left(angle1 + angle2)
    colorful_tree(length * 0.7, depth - 1, colors)

    right(angle2)
    backward(length)

# Draw colorful tree
bgcolor('lightblue')
brown_shades = ['brown', 'chocolate', 'sienna']
left(90)
penup()
backward(150)
pendown()
colorful_tree(100, 12, brown_shades)
```

### Fractal Plant with Leaves

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_leaf():
    """Draw a simple leaf"""
    color('green')
    begin_fill_if_available()  # If supported
    for i in range(2):
        forward(10)
        right(90)
        forward(5)
        right(90)
    end_fill_if_available()

def plant(length, depth):
    """Draw fractal plant with leaves"""
    if depth == 0:
        draw_leaf()
        return

    # Stem
    color('green')
    width(depth)
    forward(length)

    # Left branch
    left(30)
    plant(length * 0.6, depth - 1)

    # Right branch
    right(60)
    plant(length * 0.6, depth - 1)

    # Return
    left(30)
    backward(length)

# Draw plant
bgcolor('lightyellow')
left(90)
penup()
backward(150)
pendown()
plant(100, 8)
```

---

## Challenge Project: Fractal Art Gallery

Create a program that displays multiple fractals in one image.

**Requirements:**
- At least 4 different fractal types
- Each positioned in a different quadrant
- Different colors for each
- Adjustable recursion depth
- Labels for each fractal (if possible)

**Example:**
```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def koch_curve(length, depth):
    if depth == 0:
        forward(length)
    else:
        length /= 3.0
        koch_curve(length, depth - 1)
        left(60)
        koch_curve(length, depth - 1)
        right(120)
        koch_curve(length, depth - 1)
        left(60)
        koch_curve(length, depth - 1)

def draw_tree(length, depth):
    if depth == 0:
        return
    forward(length)
    right(20)
    draw_tree(length * 0.7, depth - 1)
    left(40)
    draw_tree(length * 0.7, depth - 1)
    right(20)
    backward(length)

def sierpinski_line(length, depth):
    if depth == 0:
        forward(length)
    else:
        sierpinski_line(length / 3, depth - 1)
        left(60)
        sierpinski_line(length / 3, depth - 1)
        right(120)
        sierpinski_line(length / 3, depth - 1)
        left(60)
        sierpinski_line(length / 3, depth - 1)

def fractal_gallery():
    bgcolor('black')

    # Fractal 1: Koch curve (top-left)
    penup()
    # Navigate to position
    pendown()
    color('cyan')
    koch_curve(100, 3)

    # Fractal 2: Tree (top-right)
    penup()
    # Navigate to position
    pendown()
    color('green')
    left(90)
    draw_tree(50, 6)

    # Fractal 3: Dragon curve (bottom-left)
    penup()
    # Navigate to position
    pendown()
    color('red')
    dragon_curve(5, 10, 1)

    # Fractal 4: Sierpinski (bottom-right)
    penup()
    # Navigate to position
    pendown()
    color('yellow')
    sierpinski_line(100, 4)

# Create gallery
fractal_gallery()
```

---

## Understanding Recursion Depth

### Depth Comparison

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

# Draw trees with different depths side by side
depths = [3, 4, 5, 6]
start_x = -200

for depth in depths:
    penup()
    # Navigate to position
    pendown()

    left(90)
    draw_tree(60, depth)
    right(90)

    # Move to next position
    start_x += 120
```

---

## Key Concepts Review

1. **Recursion:** Function calling itself
2. **Base Case:** Condition to stop recursion
3. **Recursive Case:** Function calls itself with modified parameters
4. **Fractals:** Self-similar patterns at different scales
5. **Depth:** Number of recursive levels
6. **Return Path:** Backtracking to original position

---

## Common Mistakes

### Mistake 1: Missing Base Case
```python
# ❌ Infinite recursion!
def bad_tree(length):
    forward(length)
    bad_tree(length * 0.5)  # Never stops!

# ✅ Correct
def good_tree(length, depth):
    if depth == 0:  # Base case
        return
    forward(length)
    good_tree(length * 0.5, depth - 1)
```

### Mistake 2: Not Returning to Start
```python
# ✅ Remember to backtrack
def tree(length, depth):
    if depth == 0:
        return
    forward(length)
    # ... branches ...
    backward(length)  # Return to start!
```

### Mistake 3: Stack Overflow
```python
# Be careful with depth
# Depth > 15 may cause issues
draw_tree(100, 20)  # ⚠️ May be too deep
```

---

## Week 8 Checklist

By the end of this week, you should be able to:

- [ ] Understand recursive function structure
- [ ] Implement base and recursive cases
- [ ] Draw fractal trees
- [ ] Create Koch curves and snowflakes
- [ ] Generate Sierpinski triangles
- [ ] Implement dragon and Hilbert curves
- [ ] Adjust recursion depth
- [ ] Design custom fractals

---

## Next Week Preview

In Week 9, we'll learn to:
- Create animations
- Control drawing speed dynamically
- Show step-by-step processes
- Create growing patterns
- Build interactive animations

---

## Additional Practice

Create these fractals:
1. A fern using L-systems
2. A fractal coastline
3. A Mandelbrot set visualization (simplified)
4. A recursive maze
5. Your own fractal design

Embrace the recursion! 🌳🐢
