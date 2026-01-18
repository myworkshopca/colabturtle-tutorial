# Week 10: Mathematical Art

## Learning Objectives
- Use mathematical functions in art
- Create parametric designs
- Generate Lissajous curves
- Work with trigonometry (sine, cosine)
- Apply golden ratio and Fibonacci
- Create mathematical visualizations

---

## Introduction

Mathematics and art have been connected for centuries. This week, you'll use mathematical functions to create beautiful patterns, from simple sine waves to complex parametric curves. Discover how numbers can become visual beauty!

---

## Trigonometry Basics

### Sine and Cosine Review

```python
import math

# Sine function: oscillates between -1 and 1
# sin(0°) = 0, sin(90°) = 1, sin(180°) = 0, sin(270°) = -1

angle_degrees = 45
angle_radians = math.radians(angle_degrees)
sine_value = math.sin(angle_radians)
cosine_value = math.cos(angle_radians)

print(f"sin(45°) = {sine_value:.2f}")
print(f"cos(45°) = {cosine_value:.2f}")
```

---

## Sine Wave

### Drawing a Sine Wave

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
        Height of the wave
    wavelength : int
        Length of one complete cycle in pixels
    cycles : int
        Number of complete cycles
    """
    total_points = wavelength * cycles
    prev_y = 0

    for x in range(total_points):
        # Calculate y position using sine
        angle = (x / wavelength) * 360
        y = amplitude * math.sin(math.radians(angle))

        # Calculate movement
        dx = 1
        dy = y - prev_y

        # Move turtle
        if dy > 0:
            left(math.degrees(math.atan(dy / dx)))
            forward(math.sqrt(dx**2 + dy**2))
        elif dy < 0:
            right(math.degrees(math.atan(abs(dy) / dx)))
            forward(math.sqrt(dx**2 + dy**2))
        else:
            forward(dx)

        prev_y = y

# Draw sine wave
color('blue')
draw_sine_wave(50, 80, 3)
```

### Multiple Waves

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=13)

def simple_wave_approximation(amplitude, wavelength, cycles, color_name):
    """Simplified wave drawing"""
    color(color_name)

    for i in range(cycles * 360):
        y = amplitude * math.sin(math.radians(i))

        # Approximate by moving forward and adjusting angle slightly
        forward(wavelength / 360)

        if i > 0:
            prev_y = amplitude * math.sin(math.radians(i - 1))
            diff = y - prev_y

            if diff > 0:
                left(0.5)
            elif diff < 0:
                right(0.5)

# Draw multiple waves at different positions
waves = [
    (30, 60, 3, 'red'),
    (40, 60, 3, 'blue'),
    (50, 60, 3, 'green')
]

for amp, wl, cyc, col in waves:
    penup()
    # Reposition for next wave
    pendown()
    simple_wave_approximation(amp, wl, cyc, col)
```

---

## Circular Motion

### Point Moving in Circle

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=13)

def plot_circle_parametric(radius, points=36):
    """Plot circle using parametric equations"""
    prev_x, prev_y = 0, 0

    for i in range(points + 1):
        # Parametric equations for circle
        angle = (i / points) * 360
        angle_rad = math.radians(angle)

        x = radius * math.cos(angle_rad)
        y = radius * math.sin(angle_rad)

        if i == 0:
            # Move to first point
            penup()
            forward(x)
            left(90)
            forward(y)
            right(90)
            pendown()
        else:
            # Draw to next point
            dx = x - prev_x
            dy = y - prev_y
            distance = math.sqrt(dx**2 + dy**2)
            forward(distance)

        prev_x, prev_y = x, y

plot_circle_parametric(100)
```

---

## Lissajous Curves

### Basic Lissajous Curve

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=13)

def draw_lissajous(a, b, delta, size, steps=360):
    """
    Draw a Lissajous curve

    Parameters:
    -----------
    a, b : int
        Frequency parameters
    delta : float
        Phase shift
    size : int
        Size of the curve
    steps : int
        Number of points to plot
    """
    prev_x, prev_y = None, None

    penup()

    for t in range(steps + 1):
        # Parametric equations for Lissajous
        t_normalized = t / steps
        angle = t_normalized * 2 * math.pi

        x = size * math.sin(a * angle + delta)
        y = size * math.sin(b * angle)

        if prev_x is None:
            # First point - navigate to it
            forward(x)
            left(90)
            forward(y)
            right(90)
            pendown()
        else:
            # Calculate distance and draw
            dx = x - prev_x
            dy = y - prev_y
            dist = math.sqrt(dx**2 + dy**2)

            if dist > 0:
                # Calculate angle to next point
                target_angle = math.degrees(math.atan2(dy, dx))
                # Adjust turtle heading
                # ... (simplified movement)
                forward(dist)

        prev_x, prev_y = x, y

# Draw Lissajous curves
color('purple')
draw_lissajous(3, 2, 0, 80)
```

### Lissajous Gallery

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=13)

# Draw different Lissajous curves
params = [
    (1, 2, 0, 'red'),
    (3, 2, 0, 'blue'),
    (3, 4, math.pi/2, 'green'),
    (5, 4, 0, 'purple')
]

for a, b, delta, col in params:
    penup()
    # Reposition
    pendown()
    color(col)
    draw_lissajous(a, b, delta, 60, 360)
```

---

## Fibonacci Spiral

### Fibonacci Squares

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=10)

def fibonacci_spiral(n):
    """Draw Fibonacci spiral using squares"""
    a, b = 0, 1
    colors = ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet']

    for i in range(n):
        color(colors[i % len(colors)])

        # Draw square
        size = b * 10
        for j in range(4):
            forward(size)
            right(90)

        # Move and rotate for next square
        right(90)

        # Next Fibonacci number
        a, b = b, a + b

# Draw Fibonacci spiral
fibonacci_spiral(10)
```

---

## Golden Ratio

### Golden Spiral

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=13)

def golden_spiral(size, angle, iterations):
    """Draw a spiral using golden ratio"""
    phi = 1.618033988749895  # Golden ratio

    for i in range(iterations):
        forward(size)
        right(angle)
        size *= phi / (phi + 1)  # Shrink by golden ratio

# Draw golden spiral
color('gold')
golden_spiral(100, 89, 50)
```

### Golden Rectangle

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=10)

def golden_rectangle(width):
    """Draw golden rectangle"""
    phi = 1.618033988749895
    height = width / phi

    # Draw rectangle
    color('gold')
    width(3)

    for i in range(2):
        forward(width)
        right(90)
        forward(height)
        right(90)

golden_rectangle(200)
```

---

## Parametric Curves

### Rose Curve

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=13)

def rose_curve(k, size, steps=360):
    """
    Draw a rose curve (rhodonea curve)

    Parameters:
    -----------
    k : float
        Number of petals (if odd) or 2*k petals (if even)
    size : int
        Size of the rose
    steps : int
        Number of points
    """
    prev_x, prev_y = None, None
    penup()

    for t in range(steps * abs(int(k)) + 1):
        angle = (t / steps) * 2 * math.pi
        r = size * math.cos(k * angle)

        x = r * math.cos(angle)
        y = r * math.sin(angle)

        if prev_x is None:
            # Navigate to first point
            forward(x)
            left(90)
            forward(y)
            right(90)
            pendown()
        else:
            # Draw to next point
            dx = x - prev_x
            dy = y - prev_y
            dist = math.sqrt(dx**2 + dy**2)
            forward(dist)

        prev_x, prev_y = x, y

# Draw rose curves
colors = ['red', 'pink', 'purple']
k_values = [3, 4, 7]

for k, col in zip(k_values, colors):
    penup()
    # Reposition
    pendown()
    color(col)
    rose_curve(k, 80)
```

---

## Practice Exercises

### Exercise 1: Cosine Wave
Draw a cosine wave and compare it to a sine wave.

### Exercise 2: Superposition
Draw two sine waves with different frequencies and show their sum.

### Exercise 3: Spiral of Squares
Create a spiral where each turn has a square, using Fibonacci sizes.

### Exercise 4: Harmonograph
Simulate a harmonograph drawing by combining multiple sine functions.

### Exercise 5: Custom Parametric Curve
Design your own parametric equations and draw the result.

---

## Advanced Examples

### Multiple Frequency Patterns

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=13)

def harmonic_pattern(frequencies, amplitudes, colors, steps=360):
    """Draw pattern combining multiple frequencies"""

    for freq, amp, col in zip(frequencies, amplitudes, colors):
        color(col)
        penup()
        # Reset to start position
        pendown()

        for i in range(steps):
            angle = (i / steps) * 360 * freq
            y = amp * math.sin(math.radians(angle))

            forward(1)
            # Adjust height

# Draw harmonic patterns
frequencies = [1, 2, 3]
amplitudes = [30, 20, 10]
colors = ['red', 'blue', 'green']

harmonic_pattern(frequencies, amplitudes, colors)
```

### Spirograph Simulation

```python
from ColabTurtle.Turtle import *
import math
initializeTurtle(initial_speed=13)

def spirograph(R, r, d, steps=720):
    """
    Simulate a spirograph

    Parameters:
    -----------
    R : int
        Radius of fixed circle
    r : int
        Radius of rolling circle
    d : int
        Distance of pen from center of rolling circle
    """
    prev_x, prev_y = None, None
    penup()

    for t in range(steps):
        angle = math.radians(t)

        # Spirograph parametric equations
        x = (R - r) * math.cos(angle) + d * math.cos((R - r) / r * angle)
        y = (R - r) * math.sin(angle) - d * math.sin((R - r) / r * angle)

        if prev_x is None:
            # First point
            forward(x)
            left(90)
            forward(y)
            right(90)
            pendown()
        else:
            # Draw to next point
            dx = x - prev_x
            dy = y - prev_y
            dist = math.sqrt(dx**2 + dy**2)
            forward(dist)

        prev_x, prev_y = x, y

# Draw spirograph
color('blue')
spirograph(100, 30, 50, 720)
```

---

## Challenge Project: Mathematical Art Gallery

Create a gallery of mathematical curves.

**Requirements:**
- At least 5 different mathematical curves
- Each labeled (if possible)
- Different colors
- Organized layout
- Include: sine wave, Lissajous, rose curve, spiral, Fibonacci

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

def math_gallery():
    initializeTurtle(initial_speed=13)
    bgcolor('black')

    # Gallery layout: 2x3 grid
    # Each curve in a different position

    # 1. Sine wave (top-left)
    penup()
    # Navigate
    pendown()
    color('cyan')
    draw_sine_wave(30, 60, 2)

    # 2. Lissajous (top-middle)
    penup()
    # Navigate
    pendown()
    color('magenta')
    draw_lissajous(3, 2, 0, 40)

    # 3. Rose curve (top-right)
    penup()
    # Navigate
    pendown()
    color('yellow')
    rose_curve(5, 50)

    # 4. Fibonacci spiral (bottom-left)
    penup()
    # Navigate
    pendown()
    color('green')
    fibonacci_spiral(7)

    # 5. Golden spiral (bottom-middle)
    penup()
    # Navigate
    pendown()
    color('gold')
    golden_spiral(80, 89, 40)

    # 6. Spirograph (bottom-right)
    penup()
    # Navigate
    pendown()
    color('red')
    spirograph(60, 20, 30, 360)

# Create gallery
math_gallery()
```

---

## Key Concepts Review

1. **Trigonometry:** Sine and cosine for oscillating patterns
2. **Parametric Equations:** x(t) and y(t) define curves
3. **Lissajous Curves:** Combining different frequencies
4. **Golden Ratio:** φ ≈ 1.618, found in nature
5. **Fibonacci Sequence:** 0, 1, 1, 2, 3, 5, 8, 13, 21...
6. **Mathematical Beauty:** Numbers create visual patterns

---

## Week 10 Checklist

By the end of this week, you should be able to:

- [ ] Draw sine and cosine waves
- [ ] Create Lissajous curves
- [ ] Generate rose curves
- [ ] Draw Fibonacci spirals
- [ ] Apply golden ratio
- [ ] Use parametric equations
- [ ] Combine mathematical functions
- [ ] Create mathematical visualizations

---

## Next Week Preview

In Week 11, we'll learn to:
- Create user-controlled designs
- Use random generation
- Build pattern generators
- Make configurable art
- Implement generative systems

---

## Additional Practice

Create these mathematical patterns:
1. A superposition of 3 sine waves
2. A cardioid curve
3. An Archimedean spiral
4. A hypotrochoid
5. Your own mathematical discovery

Embrace the beauty of math! 📐🐢
