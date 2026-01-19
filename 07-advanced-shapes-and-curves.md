# Week 7: Advanced Shapes

## Learning Objectives
- Draw smooth circles and arcs
- Create star shapes and polygrams
- Generate spiral shapes
- Work with curved paths
- Apply trigonometry to drawing

---

## Table of Contents

- [Introduction](#introduction)
- [Drawing Circles](#drawing-circles)
- [Drawing Arcs](#drawing-arcs)
- [Creating Star Shapes](#creating-star-shapes)
- [Spiral Shapes](#spiral-shapes)
- [Ellipses and Ovals](#ellipses-and-ovals)
- [Compound Curves](#compound-curves)
- [Practice Exercises](#practice-exercises)
- [Advanced Examples](#advanced-examples)
- [Challenge Project: Advanced Mandala](#challenge-project-advanced-mandala)
- [Key Concepts Review](#key-concepts-review)
- [Week 7 Checklist](#week-7-checklist)
- [Next Week Preview](#next-week-preview)
- [Additional Practice](#additional-practice)

---

## Introduction

This week moves beyond basic polygons to create smooth curves, stars, and spirals. You'll learn mathematical techniques to create beautiful organic and geometric shapes.

---

## Drawing Circles

### Circle Approximation Method

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=13)

def draw_circle(radius, steps=36):
    """
    Draw a circle by approximating with small line segments

    Parameters:
    -----------
    radius : int
        Radius of the circle
    steps : int
        Number of line segments (more = smoother)
    """
    circumference = 2 * math.pi * radius
    step_length = circumference / steps
    step_angle = 360 / steps

    for i in range(steps):
        forward(step_length)
        right(step_angle)

# Draw circles of different sizes
draw_circle(50)
penup()
forward(150)
pendown()
draw_circle(30, 72)  # Smoother circle with more steps
```

### Comparing Different Step Counts

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=13)

# Draw circles with different smoothness
step_counts = [6, 12, 24, 36, 72]
radius = 40

for steps in step_counts:
    draw_circle(radius, steps)
    penup()
    forward(radius * 2 + 20)
    pendown()
```

---

## Drawing Arcs

### Arc Function

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=13)

def draw_arc(radius, angle, steps=36):
    """
    Draw an arc (partial circle)

    Parameters:
    -----------
    radius : int
        Radius of the arc
    angle : int
        Total angle of the arc in degrees
    steps : int
        Number of segments per full circle
    """
    arc_length = 2 * math.pi * radius * (angle / 360)
    num_steps = int(steps * (angle / 360))
    step_length = arc_length / num_steps
    step_angle = angle / num_steps

    for i in range(num_steps):
        forward(step_length)
        right(step_angle)

# Draw various arcs
draw_arc(60, 180)  # Semicircle
penup()
forward(150)
pendown()
draw_arc(60, 90)   # Quarter circle
penup()
forward(150)
pendown()
draw_arc(60, 270)  # Three-quarter circle
```

---

## Creating Star Shapes

### 5-Pointed Star

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_star(size, points=5):
    """
    Draw a star shape

    Parameters:
    -----------
    size : int
        Length of each point
    points : int
        Number of points (must be >= 3)
    """
    angle = 180 - (180 / points)

    for i in range(points):
        forward(size)
        right(angle)

# Draw different stars
draw_star(100, 5)   # 5-pointed star
penup()
forward(200)
pendown()
draw_star(80, 7)    # 7-pointed star
```

### Star with Different Styles

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_star_outline(outer_radius, inner_radius, points=5):
    """Draw a star by connecting outer and inner points"""
    import math

    angle_step = 360 / (points * 2)

    for i in range(points * 2):
        # Alternate between outer and inner radius
        if i % 2 == 0:
            radius = outer_radius
        else:
            radius = inner_radius

        # Calculate next point
        angle_rad = math.radians(i * angle_step - 90)
        x = radius * math.cos(angle_rad)
        y = radius * math.sin(angle_rad)

        # Draw to point
        if i == 0:
            penup()
            # Navigate to first point
            pendown()
        else:
            # Draw line to next point
            pass

# Draw star
draw_star_outline(100, 40, 5)
```

---

## Spiral Shapes

### Archimedean Spiral

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_spiral(loops, spacing):
    """
    Draw an Archimedean spiral

    Parameters:
    -----------
    loops : int
        Number of complete loops
    spacing : int
        Distance between each loop
    """
    angle = 0
    distance = 0

    for i in range(360 * loops):
        forward(distance)
        right(1)
        distance += spacing / 360

# Draw spiral
draw_spiral(5, 10)
```

### Square Spiral (Revisited)

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_square_spiral(size_start, size_increment, turns):
    """Draw a square spiral"""
    size = size_start

    for i in range(turns):
        forward(size)
        right(90)
        size += size_increment

# Draw square spiral
draw_square_spiral(10, 5, 40)
```

### Triangular Spiral

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_triangle_spiral(size_start, size_increment, turns):
    """Draw a triangular spiral"""
    size = size_start

    for i in range(turns):
        forward(size)
        right(120)
        size += size_increment

# Draw triangular spiral
draw_triangle_spiral(10, 5, 30)
```

---

## Ellipses and Ovals

### Ellipse Approximation

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=13)

def draw_ellipse(width, height, steps=36):
    """
    Draw an ellipse

    Parameters:
    -----------
    width : int
        Width (horizontal diameter)
    height : int
        Height (vertical diameter)
    steps : int
        Number of segments
    """
    for i in range(steps):
        angle = (360 / steps) * i
        angle_rad = math.radians(angle)

        # Parametric equations for ellipse
        x = (width / 2) * math.cos(angle_rad)
        y = (height / 2) * math.sin(angle_rad)

        if i == 0:
            penup()
            # Navigate to first point
            pendown()

        # Draw small segment
        forward(2)
        # Adjust heading

# Draw ellipses
draw_ellipse(150, 80)
```

---

## Compound Curves

### Wave Pattern

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=13)

def draw_sine_wave(amplitude, wavelength, cycles):
    """
    Draw a sine wave

    Parameters:
    -----------
    amplitude : int
        Height of wave
    wavelength : int
        Length of one complete cycle
    cycles : int
        Number of complete cycles to draw
    """
    for i in range(wavelength * cycles):
        # Calculate y position
        angle = (360 / wavelength) * i
        y = amplitude * math.sin(math.radians(angle))

        # Move in small steps
        forward(1)
        # Adjust vertical position (approximate)
        if i > 0:
            prev_angle = (360 / wavelength) * (i - 1)
            prev_y = amplitude * math.sin(math.radians(prev_angle))
            diff = y - prev_y
            if diff > 0:
                left(1)
            else:
                right(1)

# Draw sine wave
draw_sine_wave(50, 60, 3)
```

### Heart Shape

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=13)

def draw_heart(size):
    """Draw a heart shape using arcs and lines"""
    # Left arc
    draw_arc(size / 2, 180)

    # Left diagonal
    right(45)
    forward(size * math.sqrt(2) / 2)

    # Right diagonal
    left(90)
    forward(size * math.sqrt(2) / 2)

    # Right arc
    left(45)
    draw_arc(size / 2, 180)

# Draw heart
color('red')
draw_heart(100)
```

---

## Practice Exercises

### Exercise 1: Olympic Rings
Draw the five Olympic rings with proper positioning and overlapping.

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=13)

colors = ['blue', 'yellow', 'black', 'green', 'red']
positions = [(-120, 0), (0, 0), (120, 0), (-60, -50), (60, -50)]

for pos, col in zip(positions, colors):
    color(col)
    width(5)
    penup()
    # Navigate to position
    pendown()
    draw_circle(40)
```

### Exercise 2: Flower with Circular Petals
Create a flower using overlapping circles as petals.

### Exercise 3: Spiral Galaxy
Draw a spiral galaxy using multiple curved arms.

### Exercise 4: Snowflake
Create a snowflake pattern with 6-fold symmetry using lines and curves.

### Exercise 5: Yin-Yang Symbol
Draw the yin-yang symbol using semicircles and small circles.

---

## Advanced Examples

### Rose Curve

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=13)

def draw_rose(petals, size):
    """
    Draw a rose curve (rhodonea curve)

    Parameters:
    -----------
    petals : int
        Number of petals (use even for proper rose)
    size : int
        Size of the rose
    """
    for angle in range(0, 360 * petals, 1):
        angle_rad = math.radians(angle)
        k = petals / 2  # Petal coefficient
        r = size * math.sin(k * angle_rad)

        if angle == 0:
            penup()
        else:
            pendown()

        # Move in small step
        forward(abs(r) / 50)
        right(1)

# Draw rose
draw_rose(8, 100)
```

### Lissajous Curve

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=13)

def draw_lissajous(a, b, size, steps=360):
    """
    Draw a Lissajous curve

    Parameters:
    -----------
    a, b : int
        Frequency parameters
    size : int
        Size of the curve
    steps : int
        Number of points to plot
    """
    for t in range(steps):
        t_rad = math.radians(t * 360 / steps)
        x = size * math.sin(a * t_rad)
        y = size * math.sin(b * t_rad)

        if t == 0:
            penup()
            # Navigate to first point
            pendown()

        # Draw to next point (approximate)
        forward(1)

# Draw Lissajous
draw_lissajous(3, 4, 80)
```

---

## Challenge Project: Advanced Mandala

Create a complex mandala using circles, arcs, stars, and spirals.

**Requirements:**
- At least 4 different shape types
- Radial symmetry (6, 8, or 12-fold)
- Multiple layers
- Color gradients or patterns
- Smooth curves throughout

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

def draw_petal(radius):
    """Draw a petal using two arcs"""
    draw_arc(radius, 60)
    left(120)
    draw_arc(radius, 60)
    left(120)

def draw_mandala():
    initializeTurtle(initial_speed=13)
    bgcolor('black')

    # Outer circles
    colors = ['purple', 'blue', 'cyan', 'white']
    for i, col in enumerate(colors):
        color(col)
        radius = 150 - i * 20
        draw_circle(radius)

    # Petals layer
    for i in range(12):
        color('pink')
        draw_petal(40)
        right(30)

    # Stars layer
    for i in range(8):
        color('yellow')
        draw_star(60, 5)
        right(45)

    # Center circle
    color('gold')
    draw_circle(30, 72)

# Create mandala
draw_mandala()
```

---

## Key Concepts Review

1. **Circle Approximation:** Use many small line segments
2. **Arc Drawing:** Partial circles with angle parameter
3. **Star Shapes:** Use external angles to create points
4. **Spirals:** Gradually increasing distance with rotation
5. **Parametric Curves:** Use mathematical formulas for complex shapes
6. **Smooth Drawing:** More steps = smoother curves

---

## Week 7 Checklist

By the end of this week, you should be able to:

- [ ] Draw smooth circles with variable smoothness
- [ ] Create arcs of any angle
- [ ] Draw stars with any number of points
- [ ] Generate various spiral types
- [ ] Draw ellipses and ovals
- [ ] Create compound curves
- [ ] Apply trigonometry to drawing
- [ ] Design complex curved patterns

---

## Next Week Preview

In Week 8, we'll learn to:
- Implement recursive functions
- Create fractal patterns
- Draw tree structures
- Generate Koch curves and snowflakes
- Explore L-systems

---

## Additional Practice

Create these curved designs:
1. A butterfly using circles and arcs
2. A Celtic knot pattern
3. A mandala with 8 layers
4. A mathematical rose curve
5. Your signature using smooth curves

Master the curves! 🌀🐢
