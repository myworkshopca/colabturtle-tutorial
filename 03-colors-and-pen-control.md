# Week 3: Colors & Pen Control

## Learning Objectives
- Work with colors effectively
- Control pen width
- Use background colors
- Create multi-colored patterns
- Understand color theory basics

---

## Introduction

Colors bring your turtle graphics to life! This week, you'll learn how to control not just what color the turtle draws with, but also the thickness of lines and the canvas background.

---

## Color Basics

### Setting Pen Color

```python
from ColabTurtle.Turtle import *
initializeTurtle()

# Set color before drawing
color('red')
forward(100)

color('blue')
right(90)
forward(100)
```

### Background Color

```python
from ColabTurtle.Turtle import *
initializeTurtle()

# Set background color (must be called after initialization)
bgcolor('lightyellow')

color('purple')
for i in range(4):
    forward(100)
    right(90)
```

---

## Available Color Names

### Basic Colors
```python
colors_basic = [
    'red', 'blue', 'green', 'yellow',
    'orange', 'purple', 'pink', 'brown',
    'black', 'white', 'gray'
]
```

### Extended Colors
```python
colors_extended = [
    'lightblue', 'darkblue', 'lightgreen', 'darkgreen',
    'lightyellow', 'lightgray', 'darkgray',
    'cyan', 'magenta', 'violet',
    'indigo', 'turquoise', 'salmon'
]
```

### Testing Colors

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

colors = ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet']

for i, col in enumerate(colors):
    color(col)
    forward(100)
    right(90 + i * 5)  # Slight angle change
```

---

## Pen Width Control

### Setting Pen Width

```python
from ColabTurtle.Turtle import *
initializeTurtle()

# Default width is usually 1-2 pixels
width(5)  # Set pen width to 5 pixels
forward(100)

width(10)  # Thicker line
right(90)
forward(100)
```

### Creating Lines of Different Thickness

```python
from ColabTurtle.Turtle import *
initializeTurtle()

widths = [1, 3, 5, 7, 9]

for w in widths:
    width(w)
    forward(100)
    penup()
    backward(100)
    right(90)
    forward(15)
    left(90)
    pendown()
```

---

## Combining Color and Width

### Rainbow Lines with Varying Width

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=10)

colors = ['red', 'orange', 'yellow', 'green', 'blue', 'purple']

for i, col in enumerate(colors):
    color(col)
    width(i + 2)  # Width increases: 2, 3, 4, 5, 6, 7
    forward(100)
    right(60)
```

---

## Creating Patterns

### Colorful Square Pattern

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

colors = ['red', 'blue', 'green', 'yellow']

for i in range(40):
    color(colors[i % 4])  # Cycle through colors
    forward(100)
    right(91)  # Slightly more than 90 degrees
```

### Spiral with Color Gradient

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

colors = ['red', 'orange', 'yellow', 'lightgreen', 'cyan', 'blue', 'purple']
distance = 10

for i in range(100):
    color(colors[i % len(colors)])
    forward(distance)
    right(89)
    distance += 1
```

---

## Creating a Color Wheel

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

colors = ['red', 'orange', 'yellow', 'green',
          'cyan', 'blue', 'purple', 'magenta']

for i in range(len(colors)):
    color(colors[i])
    width(5)
    forward(100)
    backward(100)
    right(360 / len(colors))
```

---

## Practice Exercises

### Exercise 1: Rainbow Square
Draw a square where each side is a different color and width.

```python
from ColabTurtle.Turtle import *
initializeTurtle()

colors = ['red', 'green', 'blue', 'yellow']
widths = [2, 4, 6, 8]

for i in range(4):
    color(colors[i])
    width(widths[i])
    forward(100)
    right(90)
```

### Exercise 2: Colorful Star
Draw a 5-pointed star with each line in a different color.

**Hint:** A star uses 36-degree angles or 144-degree angles depending on method.

### Exercise 3: Traffic Light
Create a vertical traffic light with three circles (red, yellow, green) and a black frame.

### Exercise 4: Color Gradient Line
Draw a line that changes color smoothly by drawing many short segments.

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

colors = ['red', 'orange', 'yellow', 'green', 'blue']

for i in range(100):
    color(colors[i % len(colors)])
    forward(2)
```

### Exercise 5: Colorful Spiral
Create a spiral that changes color as it grows.

---

## Advanced Example: Colorful Flower

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

bgcolor('lightgreen')
colors = ['red', 'pink', 'orange', 'yellow', 'purple', 'magenta']

# Draw 6 petals
for i in range(6):
    color(colors[i])
    width(3)

    # Draw petal (circle approximation)
    for j in range(36):
        forward(2)
        right(10)

    # Return to center and rotate
    left(360)
    right(60)

# Draw center
color('yellow')
width(20)
forward(1)  # Just a dot
```

---

## Creating Custom Patterns

### Checkerboard Pattern (Outline)

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

size = 40
colors = ['black', 'white']

for row in range(4):
    for col in range(4):
        # Choose color based on position
        color_index = (row + col) % 2
        color(colors[color_index])
        width(2)

        # Draw square
        for i in range(4):
            forward(size)
            right(90)

        # Move to next square
        penup()
        forward(size)
        pendown()

    # Move to next row
    penup()
    backward(size * 4)
    right(90)
    forward(size)
    left(90)
    pendown()
```

### Color Wave

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

colors = ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet']

for i in range(50):
    color(colors[i % len(colors)])
    width(3)
    forward(5)
    right(10)
```

---

## Background Color Ideas

### Sky Background
```python
bgcolor('lightblue')  # Sky
bgcolor('lightcyan')  # Light sky
bgcolor('deepskyblue')  # Deeper sky
```

### Nature Backgrounds
```python
bgcolor('lightgreen')  # Grass
bgcolor('lightyellow')  # Sand
bgcolor('lightcoral')  # Sunset
```

### Dark Backgrounds
```python
bgcolor('black')  # Night sky
bgcolor('darkblue')  # Ocean
bgcolor('darkgreen')  # Forest
```

---

## Challenge Project: Sunset Scene

Create a sunset scene with:
- Gradient sky background (multiple colored circles)
- Orange/red sun
- Simple landscape (ground line)
- Optional: birds, clouds, or trees

**Example:**
```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

# Background
bgcolor('lightyellow')

# Sun
color('orange')
width(50)
penup()
goto_position(0, 100)  # If goto is available, otherwise navigate manually
pendown()
forward(1)

# Ground
color('green')
width(5)
penup()
goto_position(-200, -100)  # Navigate to ground level
pendown()
forward(400)

# Add details...
```

---

## Key Concepts Review

1. **color()**: Sets the pen color for drawing
2. **bgcolor()**: Sets the canvas background color
3. **width()**: Controls the thickness of drawn lines
4. **Color Names**: String values like 'red', 'blue', 'lightgreen'
5. **Color Cycling**: Use modulo (%) to cycle through color lists

---

## Common Mistakes

### Mistake 1: Setting bgcolor Before initializeTurtle
```python
# ❌ Wrong
from ColabTurtle.Turtle import *
bgcolor('blue')  # Won't work!
initializeTurtle()

# ✅ Correct
from ColabTurtle.Turtle import *
initializeTurtle()
bgcolor('blue')
```

### Mistake 2: Misspelling Color Names
```python
# ❌ Wrong
color('lite blue')  # Spaces and wrong spelling

# ✅ Correct
color('lightblue')  # One word, correct spelling
```

### Mistake 3: Width Too Large
```python
# ❌ May look blocky
width(100)  # Too thick for most designs

# ✅ Better
width(5)   # Usually sufficient for emphasis
```

---

## Color Theory Basics

### Primary Colors
- **Red, Blue, Yellow** (traditional)
- **Red, Green, Blue** (digital/light-based)

### Complementary Colors (Opposite on color wheel)
- Red ↔ Green
- Blue ↔ Orange
- Yellow ↔ Purple

### Analogous Colors (Next to each other)
- Red, Orange, Yellow
- Blue, Purple, Magenta
- Green, Cyan, Blue

### Using Color Harmony
```python
# Analogous color scheme
warm_colors = ['red', 'orange', 'yellow']

# Complementary colors for contrast
contrast_colors = ['blue', 'orange']

# Monochromatic (shades of one color)
blue_shades = ['lightblue', 'blue', 'darkblue']
```

---

## Week 3 Checklist

By the end of this week, you should be able to:

- [ ] Set pen colors using color names
- [ ] Change background color
- [ ] Control pen width for thick/thin lines
- [ ] Create multi-colored patterns
- [ ] Cycle through color arrays
- [ ] Combine colors and widths effectively
- [ ] Apply basic color theory
- [ ] Create visually appealing designs

---

## Next Week Preview

In Week 4, we'll learn to:
- Create reusable functions for common shapes
- Use parameters to make functions flexible
- Build a personal shape library
- Organize code with proper structure
- Save and restore turtle state

---

## Additional Practice

Try creating these designs:
1. A rainbow with 7 colored arcs
2. A colorful mandala pattern
3. Your country's flag using turtle graphics
4. A stained glass window effect
5. A gradient from light to dark

Keep experimenting with colors! 🌈🐢
