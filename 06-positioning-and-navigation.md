# Week 6: Positioning & Navigation

## Learning Objectives
- Navigate the canvas coordinate system
- Move to specific positions
- Create grid-based drawings
- Understand absolute vs relative positioning
- Build location-aware patterns

---

## Table of Contents

- [Introduction](#introduction)
- [Understanding the Coordinate System](#understanding-the-coordinate-system)
- [Manual Navigation](#manual-navigation)
- [Simpler Position Tracking](#simpler-position-tracking)
- [Grid-Based Drawing](#grid-based-drawing)
- [Coordinate-Based Patterns](#coordinate-based-patterns)
- [Checkerboard Pattern (Improved)](#checkerboard-pattern-improved)
- [Practice Exercises](#practice-exercises)
- [Advanced Positioning](#advanced-positioning)
- [Creating Graphs and Charts](#creating-graphs-and-charts)
- [Challenge Project: City Skyline](#challenge-project-city-skyline)
- [Key Concepts Review](#key-concepts-review)
- [Week 6 Checklist](#week-6-checklist)
- [Next Week Preview](#next-week-preview)
- [Additional Practice](#additional-practice)

---

## Introduction

So far, we've used relative positioning (forward, backward, left, right). This week, you'll learn to think about absolute positions on the canvas and navigate to specific coordinates.

---

## Understanding the Coordinate System

### Canvas Basics

```
         Y-axis (positive up)
              |
              |
     (-x, +y) | (+x, +y)
    ----------+---------- X-axis (positive right)
     (-x, -y) | (+x, -y)
              |
              |
        (Origin: 0, 0)
```

**Key Points:**
- Origin (0, 0) is typically at the center
- X increases to the right
- Y increases upward
- Turtle starts at origin, facing up (90°)

---

## Manual Navigation

### Moving to Specific Positions

Since ColabTurtle may not have a built-in `goto()`, we'll navigate manually:

```python
from ColabTurtle.Turtle import *
initializeTurtle()

def navigate_to(target_x, target_y, current_x=0, current_y=0, current_heading=90):
    """
    Navigate from current position to target position

    Headings: 0=Right, 90=Up, 180=Left, 270=Down
    """
    # Calculate displacement
    dx = target_x - current_x
    dy = target_y - current_y

    # Calculate distance
    import math
    distance = math.sqrt(dx**2 + dy**2)

    # Calculate target angle
    target_angle = math.degrees(math.atan2(dy, dx))

    # Calculate turn needed
    turn = target_angle - (current_heading - 90)

    # Normalize turn to -180 to 180
    while turn > 180:
        turn -= 360
    while turn < -180:
        turn += 360

    # Execute movement
    penup()
    if turn > 0:
        left(turn)
    else:
        right(abs(turn))
    forward(distance)
    pendown()

    return target_x, target_y, target_angle + 90

# Example usage
navigate_to(100, 50)
```

---

## Simpler Position Tracking

### Position Tracker Class

```python
from ColabTurtle.Turtle import *

class TurtleTracker:
    def __init__(self):
        self.x = 0
        self.y = 0
        self.heading = 90  # Start facing up

    def move_forward(self, distance):
        import math
        rad = math.radians(self.heading)
        self.x += distance * math.cos(rad)
        self.y += distance * math.sin(rad)
        forward(distance)

    def move_backward(self, distance):
        self.move_forward(-distance)
        backward(distance)

    def turn_right(self, angle):
        self.heading -= angle
        right(angle)

    def turn_left(self, angle):
        self.heading += angle
        left(angle)

    def get_position(self):
        return (self.x, self.y)

# Usage
initializeTurtle()
tracker = TurtleTracker()

tracker.move_forward(100)
print(f"Position: {tracker.get_position()}")
tracker.turn_right(90)
tracker.move_forward(50)
print(f"Position: {tracker.get_position()}")
```

---

## Grid-Based Drawing

### Simple Grid Function

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_grid(rows, cols, cell_size):
    """Draw a grid"""
    # Start position (top-left)
    penup()
    backward(cols * cell_size / 2)
    left(90)
    forward(rows * cell_size / 2)
    right(90)
    pendown()

    # Draw horizontal lines
    for i in range(rows + 1):
        forward(cols * cell_size)
        penup()
        backward(cols * cell_size)
        right(90)
        forward(cell_size)
        left(90)
        pendown()

    # Return to start
    penup()
    left(90)
    backward(cell_size)
    right(90)
    pendown()

    # Draw vertical lines
    for i in range(cols + 1):
        left(90)
        forward(rows * cell_size)
        penup()
        backward(rows * cell_size)
        right(90)
        forward(cell_size)
        pendown()

# Draw 5x5 grid
draw_grid(5, 5, 40)
```

---

## Coordinate-Based Patterns

### Placing Shapes at Specific Positions

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_square_at(x, y, size, color_name):
    """Draw a square at specific position (relative to start)"""
    penup()
    # Navigate to position (simplified)
    forward(x)
    left(90)
    forward(y)
    right(90)
    pendown()

    # Draw square
    color(color_name)
    for i in range(4):
        forward(size)
        right(90)

    # Return to origin
    penup()
    left(90)
    backward(y)
    right(90)
    backward(x)
    pendown()

# Draw squares at different positions
positions = [(0, 0), (100, 0), (0, 100), (100, 100)]
colors = ['red', 'blue', 'green', 'yellow']

for (x, y), col in zip(positions, colors):
    draw_square_at(x, y, 40, col)
```

---

## Checkerboard Pattern (Improved)

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_square(size):
    for i in range(4):
        forward(size)
        right(90)

def draw_checkerboard(rows, cols, cell_size):
    """Draw a checkerboard pattern"""
    colors = ['white', 'black']

    # Start at top-left
    start_x = -(cols * cell_size) / 2
    start_y = (rows * cell_size) / 2

    for row in range(rows):
        for col in range(cols):
            # Calculate position
            x = start_x + col * cell_size
            y = start_y - row * cell_size

            # Choose color
            color_index = (row + col) % 2
            color(colors[color_index])

            # Navigate and draw
            penup()
            # Manual navigation to (x, y)
            pendown()
            draw_square(cell_size)

# Draw 8x8 checkerboard
draw_checkerboard(8, 8, 30)
```

---

## Practice Exercises

### Exercise 1: Draw Stars at Corners
Place stars at the four corners of the canvas.

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_star(size):
    for i in range(5):
        forward(size)
        right(144)

corners = [(-150, 150), (150, 150), (150, -150), (-150, -150)]

for x, y in corners:
    penup()
    # Navigate to (x, y)
    pendown()
    draw_star(30)
```

### Exercise 2: Diagonal Line of Shapes
Draw shapes along a diagonal line from top-left to bottom-right.

### Exercise 3: Circle of Circles
Place circles around a larger circle's circumference.

### Exercise 4: Random Placement
Place shapes at random positions on the canvas.

```python
from ColabTurtle.Turtle import *
import random
initializeTurtle(initial_speed=13)

def draw_square(size):
    for i in range(4):
        forward(size)
        right(90)

# Draw 10 squares at random positions
for i in range(10):
    x = random.randint(-200, 200)
    y = random.randint(-200, 200)
    size = random.randint(20, 60)
    color_choice = random.choice(['red', 'blue', 'green', 'yellow', 'purple'])

    penup()
    # Navigate to (x, y)
    pendown()
    color(color_choice)
    draw_square(size)
```

### Exercise 5: Graph Function
Plot a mathematical function (e.g., y = x²) using turtle graphics.

---

## Advanced Positioning

### Cartesian Coordinate Helper

```python
from ColabTurtle.Turtle import *
import math

class CartesianTurtle:
    def __init__(self):
        initializeTurtle(initial_speed=13)
        self.x = 0
        self.y = 0
        self.heading = 90

    def goto(self, target_x, target_y):
        """Move to absolute position"""
        dx = target_x - self.x
        dy = target_y - self.y

        distance = math.sqrt(dx**2 + dy**2)
        target_angle = math.degrees(math.atan2(dy, dx))

        # Calculate turn
        turn_needed = target_angle - (self.heading - 90)

        # Normalize
        while turn_needed > 180:
            turn_needed -= 360
        while turn_needed < -180:
            turn_needed += 360

        # Execute
        if turn_needed > 0:
            left(turn_needed)
        else:
            right(abs(turn_needed))

        forward(distance)

        # Update state
        self.x = target_x
        self.y = target_y
        self.heading = target_angle + 90

    def goto_penup(self, target_x, target_y):
        """Move without drawing"""
        penup()
        self.goto(target_x, target_y)
        pendown()

# Usage
turtle = CartesianTurtle()
turtle.goto(100, 50)
turtle.goto(100, 100)
turtle.goto(0, 100)
turtle.goto(0, 0)
```

---

## Creating Graphs and Charts

### Simple Bar Chart

```python
from ColabTurtle.Turtle import *
initializeTurtle(initial_speed=13)

def draw_bar(height, bar_width, color_name):
    """Draw a vertical bar"""
    color(color_name)
    width(bar_width)
    forward(height)
    backward(height)
    width(2)

# Data
data = [50, 80, 120, 60, 100]
colors = ['red', 'blue', 'green', 'yellow', 'purple']
bar_width = 10
spacing = 20

# Position at bottom-left
penup()
backward(len(data) * spacing / 2)
right(90)
forward(150)
left(90)
pendown()

# Draw bars
for height, col in zip(data, colors):
    draw_bar(height, bar_width, col)
    penup()
    forward(spacing)
    pendown()
```

---

## Challenge Project: City Skyline

Create a city skyline with buildings at specific positions.

**Requirements:**
- At least 5 buildings of different heights
- Buildings positioned along a horizontal line
- Windows on buildings (grid pattern)
- Stars or moon in sky
- Optional: add clouds, sun, birds

**Example:**
```python
from ColabTurtle.Turtle import *
import random

def draw_rectangle(width, height, color_name='gray'):
    """Draw a filled rectangle outline"""
    color(color_name)
    for i in range(2):
        forward(width)
        left(90)
        forward(height)
        left(90)

def draw_building(width, height, window_rows, window_cols):
    """Draw a building with windows"""
    # Building body
    draw_rectangle(width, height, 'gray')

    # Windows
    window_width = width / (window_cols + 1)
    window_height = height / (window_rows + 1)

    for row in range(window_rows):
        for col in range(window_cols):
            penup()
            forward(window_width * (col + 1) - window_width/4)
            left(90)
            forward(window_height * (row + 1) - window_height/4)
            right(90)
            pendown()

            color('yellow')
            width(window_width / 2)
            forward(1)  # Draw window
            width(2)

            # Return
            penup()
            left(90)
            backward(window_height * (row + 1) - window_height/4)
            right(90)
            backward(window_width * (col + 1) - window_width/4)
            pendown()

def draw_skyline():
    """Draw a city skyline"""
    initializeTurtle(initial_speed=13)
    bgcolor('darkblue')

    # Ground line
    color('black')
    width(5)
    penup()
    backward(250)
    right(90)
    forward(100)
    left(90)
    pendown()
    forward(500)

    # Buildings
    buildings = [
        (60, 150, 5, 3),
        (80, 200, 7, 4),
        (50, 120, 4, 2),
        (70, 180, 6, 3),
        (90, 220, 8, 4),
    ]

    penup()
    backward(500)
    pendown()

    for width, height, rows, cols in buildings:
        draw_building(width, height, rows, cols)
        penup()
        forward(width + 10)
        pendown()

    # Moon
    color('white')
    penup()
    # Navigate to moon position
    pendown()
    width(40)
    forward(1)

# Run
draw_skyline()
```

---

## Key Concepts Review

1. **Coordinate System:** X-Y plane with origin at center
2. **Absolute Positioning:** Specific (x, y) coordinates
3. **Relative Positioning:** Movement from current position
4. **Navigation:** Moving to specific positions
5. **Grid Systems:** Organizing drawings in rows/columns
6. **Position Tracking:** Keeping track of turtle's location

---

## Week 6 Checklist

By the end of this week, you should be able to:

- [ ] Understand canvas coordinate system
- [ ] Navigate to specific positions manually
- [ ] Track turtle position programmatically
- [ ] Create grid-based patterns
- [ ] Place shapes at specific coordinates
- [ ] Build coordinate-aware drawings
- [ ] Create simple graphs and charts
- [ ] Design location-based compositions

---

## Next Week Preview

In Week 7, we'll learn to:
- Draw smooth circles and arcs
- Create star shapes
- Work with complex curves
- Generate spiral shapes
- Build advanced geometric patterns

---

## Additional Practice

Create these coordinate-based designs:
1. A connect-the-dots image
2. A constellation map
3. A floor plan layout
4. A game board (chess, tic-tac-toe)
5. A pixel art image using small squares

Master positioning! 📍🐢
