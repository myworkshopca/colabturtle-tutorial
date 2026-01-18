# Week 1: Introduction & Setup

## Learning Objectives
- Understand what turtle graphics is
- Set up ColabTurtle in Google Colab
- Learn basic movement commands
- Control the pen (up/down)

---

## What is Turtle Graphics?

Turtle graphics is a method of programming vector graphics using a relative cursor (the "turtle") on a Cartesian coordinate system. Imagine a turtle carrying a pen that can move forward, backward, turn left, turn right, and lift/lower its pen to draw.

**History:** Created in 1967 as part of the Logo programming language by Seymour Papert, turtle graphics was designed to teach programming concepts to children.

---

## Setup ColabTurtle

### Installation

```python
# Install ColabTurtle package
!pip install ColabTurtle
```

### Import and Initialize

```python
from ColabTurtle.Turtle import *

# Initialize the turtle canvas
initializeTurtle()
```

**Note:** You must call `initializeTurtle()` before using any turtle commands in Google Colab.

---

## Basic Commands

### Movement Commands

| Command | Description | Example |
|---------|-------------|---------|
| `forward(distance)` | Move forward by distance pixels | `forward(100)` |
| `backward(distance)` | Move backward by distance pixels | `backward(50)` |
| `right(angle)` | Turn right by angle degrees | `right(90)` |
| `left(angle)` | Turn left by angle degrees | `left(45)` |

### Pen Control

| Command | Description | Example |
|---------|-------------|---------|
| `penup()` | Lift the pen (stop drawing) | `penup()` |
| `pendown()` | Lower the pen (start drawing) | `pendown()` |

---

## Example 1: Drawing a Line

```python
from ColabTurtle.Turtle import *
initializeTurtle()

# Draw a horizontal line
forward(100)
```

**Output:** A horizontal line 100 pixels long

---

## Example 2: Drawing an L-Shape

```python
from ColabTurtle.Turtle import *
initializeTurtle()

# Draw vertical line
forward(100)

# Turn right 90 degrees
right(90)

# Draw horizontal line
forward(100)
```

**Output:** An L-shaped line

---

## Example 3: Moving Without Drawing

```python
from ColabTurtle.Turtle import *
initializeTurtle()

# Draw first line
forward(50)

# Lift pen and move
penup()
forward(50)

# Put pen down and draw again
pendown()
forward(50)
```

**Output:** Two separate line segments with a gap

---

## Example 4: Creating a Path

```python
from ColabTurtle.Turtle import *
initializeTurtle()

# Create a zigzag path
forward(50)
right(45)
forward(50)
left(90)
forward(50)
right(45)
forward(50)
```

---

## Practice Exercises

### Exercise 1: Draw a Plus Sign (+)
Draw a plus sign by moving forward, backward, turning, and drawing again.

**Hint:**
```python
from ColabTurtle.Turtle import *
initializeTurtle()

# Vertical line
forward(50)
backward(100)
forward(50)

# Horizontal line
penup()
right(90)
forward(50)
pendown()
backward(100)
```

### Exercise 2: Draw a T-Shape
Create a T-shape using forward, backward, and turn commands.

### Exercise 3: Draw the Letter "L"
Draw a capital letter L that is 100 pixels tall and 60 pixels wide.

### Exercise 4: Draw Your Initials
Create a simple version of your initials using straight lines only.

### Exercise 5: Create a Staircase
Draw a 3-step staircase pattern.

---

## Key Concepts Review

1. **Turtle Starts at Center:** The turtle begins at coordinates (0, 0) facing up/north
2. **Angles:** 0° = Up, 90° = Right, 180° = Down, 270° = Left
3. **Pen State:** Pen is down by default (drawing mode)
4. **Distance:** Measured in pixels
5. **Relative Movement:** All movements are relative to current position and direction

---

## Common Mistakes

### Mistake 1: Forgetting to Initialize
```python
# ❌ Wrong
from ColabTurtle.Turtle import *
forward(100)  # Error!

# ✅ Correct
from ColabTurtle.Turtle import *
initializeTurtle()
forward(100)
```

### Mistake 2: Confusing Left/Right
```python
# Remember: left() and right() are turns, not movements
right(90)  # Turns 90 degrees clockwise
left(90)   # Turns 90 degrees counter-clockwise
```

### Mistake 3: Negative Distances
```python
# Use backward() instead of negative forward()
forward(-50)  # May not work as expected
backward(50)  # ✅ Correct way
```

---

## Challenge Project: Draw Your Initials

Create a complete program that draws your initials (first and last name) using only the commands learned this week.

**Requirements:**
- Use at least 5 `forward()` or `backward()` commands
- Use at least 3 turn commands (`left()` or `right()`)
- Use `penup()` and `pendown()` to move between letters
- Add comments explaining each major step

**Example for initials "JD":**
```python
from ColabTurtle.Turtle import *
initializeTurtle()

# Draw J
forward(80)
backward(40)
right(90)
forward(40)
left(90)
forward(20)
left(90)
forward(20)

# Move to draw D
penup()
left(90)
forward(60)
right(90)
pendown()

# Draw D
forward(80)
right(90)
forward(30)
# ... continue
```

---

## Week 1 Checklist

By the end of this week, you should be able to:

- [ ] Install and import ColabTurtle
- [ ] Initialize the turtle canvas
- [ ] Move the turtle forward and backward
- [ ] Turn the turtle left and right
- [ ] Control the pen (up/down)
- [ ] Draw simple shapes using straight lines
- [ ] Understand basic turtle coordinate system
- [ ] Debug simple drawing errors

---

## Next Week Preview

In Week 2, we'll learn to:
- Draw complete shapes (squares, rectangles, triangles)
- Use `for` loops to simplify repetitive code
- Add colors to our drawings
- Control drawing speed

---

## Additional Resources

- [ColabTurtle GitHub](https://github.com/tolgaatam/ColabTurtle)
- [Python Turtle Documentation](https://docs.python.org/3/library/turtle.html) (standard library reference)

Happy coding! 🐢
