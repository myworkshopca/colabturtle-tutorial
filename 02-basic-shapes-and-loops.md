# Week 2: Basic Shapes

## Learning Objectives
- Draw basic geometric shapes
- Use loops for repetitive patterns
- Understand angles and distances
- Control drawing speed and colors

---

## Introduction

This week, we'll move beyond simple lines to create complete shapes. You'll learn how to use loops to make your code more efficient and discover how to add colors to make your drawings more interesting.

---

## Drawing a Square

### Method 1: Without Loops

```python
from ColabTurtle.Turtle import *
initializeTurtle()

# Draw a square (100x100 pixels)
forward(100)
right(90)
forward(100)
right(90)
forward(100)
right(90)
forward(100)
right(90)
```

**Problem:** Repetitive code!

### Method 2: With a For Loop

```python
from ColabTurtle.Turtle import *
initializeTurtle()

# Draw a square using a loop
for i in range(4):
    forward(100)
    right(90)
```

**Much better!** This is more efficient and easier to modify.

---

## Understanding Angles

For regular polygons (shapes with equal sides and angles):
- **Square:** 4 sides, turn 360/4 = 90 degrees
- **Triangle:** 3 sides, turn 360/3 = 120 degrees
- **Pentagon:** 5 sides, turn 360/5 = 72 degrees
- **Hexagon:** 6 sides, turn 360/6 = 60 degrees

**Formula:** Turn angle = 360 / number_of_sides

---

## Drawing Different Shapes

### Triangle (Equilateral)

```python
from ColabTurtle.Turtle import *
initializeTurtle()

# Draw a triangle
for i in range(3):
    forward(100)
    right(120)
```

### Pentagon

```python
from ColabTurtle.Turtle import *
initializeTurtle()

# Draw a pentagon
for i in range(5):
    forward(80)
    right(72)
```

### Hexagon

```python
from ColabTurtle.Turtle import *
initializeTurtle()

# Draw a hexagon
for i in range(6):
    forward(70)
    right(60)
```

---

## Adding Colors

### Basic Color Command

```python
from ColabTurtle.Turtle import *
initializeTurtle()

# Set color before drawing
color('red')
for i in range(4):
    forward(100)
    right(90)
```

### Available Colors

Common color names you can use:
- `'red'`, `'blue'`, `'green'`, `'yellow'`
- `'orange'`, `'purple'`, `'pink'`, `'brown'`
- `'black'`, `'white'`, `'gray'`
- `'cyan'`, `'magenta'`

### Multi-Colored Square

```python
from ColabTurtle.Turtle import *
initializeTurtle()

colors = ['red', 'blue', 'green', 'yellow']

for i in range(4):
    color(colors[i])
    forward(100)
    right(90)
```

---

## Controlling Speed

### Speed Command

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=10)

# Speed values: 1 (slowest) to 13 (fastest)
speed(5)  # Medium speed

for i in range(4):
    forward(100)
    right(90)
```

**Speed Values:**
- `1` - Very slow (good for learning)
- `5` - Medium speed
- `10` - Fast
- `13` - Maximum speed (instant)

---

## Drawing Rectangles

```python
from ColabTurtle.Turtle import *
initializeTurtle()

# Rectangle: 150 wide x 100 tall
width = 150
height = 100

forward(width)
right(90)
forward(height)
right(90)
forward(width)
right(90)
forward(height)
right(90)
```

### Rectangle with Loop

```python
from ColabTurtle.Turtle import *
initializeTurtle()

width = 150
height = 100

for i in range(2):
    forward(width)
    right(90)
    forward(height)
    right(90)
```

---

## Creating a Function for Any Polygon

```python
from ColabTurtle.Turtle import *
initializeTurtle()

def draw_polygon(sides, length):
    angle = 360 / sides
    for i in range(sides):
        forward(length)
        right(angle)

# Draw different polygons
draw_polygon(3, 100)  # Triangle
penup()
forward(150)
pendown()
draw_polygon(5, 80)   # Pentagon
penup()
forward(150)
pendown()
draw_polygon(8, 60)   # Octagon
```

---

## Practice Exercises

### Exercise 1: Colorful Triangle
Draw a triangle where each side is a different color.

```python
from ColabTurtle.Turtle import *
initializeTurtle()

colors = ['red', 'green', 'blue']
for i in range(3):
    color(colors[i])
    forward(100)
    right(120)
```

### Exercise 2: Side-by-Side Shapes
Draw a square, triangle, and hexagon next to each other.

**Hint:** Use `penup()` and `forward()` to move between shapes.

### Exercise 3: Nested Squares
Draw 3 squares of different sizes, one inside the other.

```python
from ColabTurtle.Turtle import *
initializeTurtle()

sizes = [150, 100, 50]
colors = ['red', 'blue', 'green']

for size, col in zip(sizes, colors):
    color(col)
    for i in range(4):
        forward(size)
        right(90)
    # Move to center for next square
    penup()
    forward(25)
    right(90)
    forward(25)
    left(90)
    pendown()
```

### Exercise 4: Pentagon in Different Colors
Draw a pentagon where each side has a different color.

### Exercise 5: Create a House Shape
Draw a simple house using a square (body) and triangle (roof).

```python
from ColabTurtle.Turtle import *
initializeTurtle()

# Draw house body (square)
color('brown')
for i in range(4):
    forward(100)
    right(90)

# Draw roof (triangle)
color('red')
for i in range(3):
    forward(100)
    right(120)
```

---

## Advanced Example: Rainbow Hexagon

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=10)

colors = ['red', 'orange', 'yellow', 'green', 'blue', 'purple']

for i in range(6):
    color(colors[i])
    forward(80)
    right(60)
```

---

## Challenge Project: Geometric Art

Create a composition using at least 4 different shapes with different colors.

**Requirements:**
- Use at least 4 different polygon types
- Each shape should be a different color
- Shapes should be positioned in an interesting layout
- Use functions to avoid code repetition
- Add comments explaining your design

**Example:**
```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_polygon(sides, length, color_name):
    color(color_name)
    angle = 360 / sides
    for i in range(sides):
        forward(length)
        right(angle)

# Create a pattern
draw_polygon(4, 100, 'red')    # Square

penup()
forward(150)
pendown()
draw_polygon(3, 100, 'blue')   # Triangle

penup()
backward(75)
left(90)
forward(130)
right(90)
pendown()
draw_polygon(6, 60, 'green')   # Hexagon

penup()
forward(150)
pendown()
draw_polygon(8, 50, 'orange')  # Octagon
```

---

## Key Concepts Review

1. **For Loops:** Repeat actions efficiently
2. **Polygon Formula:** Turn angle = 360 / sides
3. **Color Command:** `color('color_name')` sets pen color
4. **Speed Control:** Values 1-13, where 13 is fastest
5. **Functions:** Create reusable shape drawing code

---

## Common Mistakes

### Mistake 1: Wrong Angle for Polygon
```python
# ❌ Wrong - using interior angle
for i in range(6):
    forward(80)
    right(120)  # Wrong angle for hexagon!

# ✅ Correct - using exterior angle
for i in range(6):
    forward(80)
    right(60)   # 360/6 = 60
```

### Mistake 2: Forgetting to Reset Position
```python
# When drawing multiple shapes, remember to reposition
draw_polygon(4, 100, 'red')
# ❌ Next shape will start where the last one ended

draw_polygon(4, 100, 'red')
penup()
forward(150)  # ✅ Move between shapes
pendown()
draw_polygon(3, 100, 'blue')
```

---

## Week 2 Checklist

By the end of this week, you should be able to:

- [ ] Draw regular polygons (3-8 sides)
- [ ] Use `for` loops for repetitive drawing
- [ ] Apply colors to your drawings
- [ ] Control drawing speed
- [ ] Create functions for reusable shapes
- [ ] Calculate turn angles for any polygon
- [ ] Position multiple shapes on the canvas
- [ ] Create simple multi-shape compositions

---

## Next Week Preview

In Week 3, we'll learn to:
- Work with RGB color values
- Control pen width for thick lines
- Fill shapes with solid colors
- Create gradient effects
- Build more complex color patterns

---

## Additional Practice

Try recreating these patterns:
1. A row of 5 different colored squares
2. A traffic light (3 circles in red, yellow, green)
3. A simple robot face using squares and triangles
4. An Olympic rings pattern (5 connected circles)

Keep practicing! 🎨🐢
