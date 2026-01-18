# Week 11: Interactive Patterns

## Learning Objectives
- Create user-controlled designs
- Use random generation
- Build pattern generators
- Make configurable art
- Implement generative systems
- Design customizable functions

---

## Introduction

This week shifts focus to creating dynamic, unpredictable art using randomness and user parameters. You'll build pattern generators that create unique designs every time they run!

---

## Random Module Basics

### Random Numbers

```python
import random

# Random integer between 1 and 10
num = random.randint(1, 10)

# Random float between 0.0 and 1.0
decimal = random.random()

# Random choice from list
colors = ['red', 'blue', 'green', 'yellow']
color = random.choice(colors)

# Random sample (multiple choices without replacement)
selected = random.sample(colors, 2)

print(f"Random number: {num}")
print(f"Random decimal: {decimal:.2f}")
print(f"Random color: {color}")
print(f"Random sample: {selected}")
```

---

## Random Walks

### Simple Random Walk

```python
from ColabTurtle.Turtle import *
import random
initializeTurtle(initial_speed=13)

def random_walk(steps, step_size):
    """
    Perform a random walk

    Parameters:
    -----------
    steps : int
        Number of steps to take
    step_size : int
        Distance of each step
    """
    colors = ['red', 'blue', 'green', 'yellow', 'purple', 'orange']

    for i in range(steps):
        # Random color
        color(random.choice(colors))

        # Random direction (0, 90, 180, 270)
        direction = random.choice([0, 90, 180, 270])
        right(direction)

        # Move
        forward(step_size)

        # Reset heading
        left(direction)

# Perform random walk
random_walk(200, 10)
```

### Continuous Random Walk

```python
from ColabTurtle.Turtle import *
import random
initializeTurtle(initial_speed=13)

def continuous_random_walk(steps, step_size, max_turn):
    """Random walk with continuous turning"""
    colors = ['red', 'orange', 'yellow', 'green', 'blue', 'purple']

    for i in range(steps):
        # Random color
        color(colors[i % len(colors)])

        # Random turn
        turn_angle = random.randint(-max_turn, max_turn)
        right(turn_angle)

        # Move forward
        forward(step_size)

# Perform continuous random walk
continuous_random_walk(500, 5, 30)
```

---

## Random Shapes

### Random Polygons

```python
from ColabTurtle.Turtle import *
import random
initializeTurtle(initial_speed=13)

def random_polygon(max_sides, max_size):
    """Draw a polygon with random properties"""
    # Random properties
    sides = random.randint(3, max_sides)
    size = random.randint(20, max_size)
    color_choice = random.choice(['red', 'blue', 'green', 'yellow', 'purple', 'orange'])

    # Draw polygon
    color(color_choice)
    angle = 360 / sides

    for i in range(sides):
        forward(size)
        right(angle)

# Draw multiple random polygons
for i in range(10):
    penup()
    # Random position
    x = random.randint(-100, 100)
    y = random.randint(-100, 100)
    # Navigate to (x, y)
    pendown()

    random_polygon(8, 60)
```

### Random Stars

```python
from ColabTurtle.Turtle import *
import random
initializeTurtle(initial_speed=13)

def random_star():
    """Draw a star with random properties"""
    points = random.choice([5, 6, 7, 8])
    size = random.randint(30, 100)
    color_choice = random.choice(['red', 'yellow', 'white', 'orange', 'pink'])

    color(color_choice)
    angle = 180 - (180 / points)

    for i in range(points):
        forward(size)
        right(angle)

# Draw random stars
bgcolor('darkblue')
for i in range(15):
    penup()
    x = random.randint(-200, 200)
    y = random.randint(-200, 200)
    # Navigate to (x, y)
    pendown()

    random_star()
```

---

## Configurable Pattern Generators

### Customizable Spiral Generator

```python
from ColabTurtle.Turtle import *
import random
initializeTurtle(initial_speed=13)

def generate_spiral(start_size, growth_rate, angle, turns, color_scheme='rainbow'):
    """
    Generate a customizable spiral

    Parameters:
    -----------
    start_size : int
        Initial size
    growth_rate : float
        How much to grow each turn
    angle : int
        Turn angle (try 89, 90, 91, etc.)
    turns : int
        Number of turns
    color_scheme : str
        'rainbow', 'warm', 'cool', 'random'
    """
    # Color schemes
    schemes = {
        'rainbow': ['red', 'orange', 'yellow', 'green', 'blue', 'purple'],
        'warm': ['red', 'orange', 'yellow', 'pink'],
        'cool': ['blue', 'cyan', 'purple', 'lightblue'],
        'random': None  # Will use random each time
    }

    colors = schemes.get(color_scheme, schemes['rainbow'])
    size = start_size

    for i in range(turns):
        if color_scheme == 'random':
            color(random.choice(['red', 'orange', 'yellow', 'green', 'blue', 'purple', 'pink', 'cyan']))
        else:
            color(colors[i % len(colors)])

        forward(size)
        right(angle)
        size += growth_rate

# Try different configurations
generate_spiral(10, 2, 89, 100, 'rainbow')
```

### Pattern Factory

```python
from ColabTurtle.Turtle import *
import random
initializeTurtle(initial_speed=13)

def pattern_factory(pattern_type, **kwargs):
    """
    Generate different patterns based on type

    Parameters:
    -----------
    pattern_type : str
        'spiral', 'star_burst', 'circle_grid', 'random_walk'
    **kwargs : dict
        Additional parameters specific to each pattern
    """

    if pattern_type == 'spiral':
        size = kwargs.get('size', 10)
        turns = kwargs.get('turns', 50)
        angle = kwargs.get('angle', 89)

        for i in range(turns):
            forward(size)
            right(angle)
            size += 2

    elif pattern_type == 'star_burst':
        rays = kwargs.get('rays', 12)
        length = kwargs.get('length', 100)

        for i in range(rays):
            forward(length)
            backward(length)
            right(360 / rays)

    elif pattern_type == 'circle_grid':
        rows = kwargs.get('rows', 3)
        cols = kwargs.get('cols', 3)
        # Draw grid of circles

    elif pattern_type == 'random_walk':
        steps = kwargs.get('steps', 100)
        step_size = kwargs.get('step_size', 10)

        for i in range(steps):
            forward(step_size)
            right(random.randint(0, 360))

# Use pattern factory
pattern_factory('spiral', size=15, turns=40, angle=91)
```

---

## Randomized Fractals

### Random Tree

```python
from ColabTurtle.Turtle import *
import random
initializeTurtle(initial_speed=13)

def random_tree(branch_length, depth):
    """
    Draw a tree with random branching

    Parameters:
    -----------
    branch_length : int
        Length of branch
    depth : int
        Recursion depth
    """
    if depth == 0 or branch_length < 5:
        # Draw random colored leaves
        color(random.choice(['green', 'lightgreen', 'darkgreen', 'lime']))
        width(random.randint(3, 8))
        forward(1)
        width(2)
        return

    # Random branch properties
    left_angle = random.randint(15, 35)
    right_angle = random.randint(15, 35)
    left_shrink = random.uniform(0.6, 0.8)
    right_shrink = random.uniform(0.6, 0.8)

    # Branch color
    if depth > 3:
        color('brown')
    else:
        color('darkgreen')

    # Draw branch
    width(depth)
    forward(branch_length)

    # Right branch
    right(right_angle)
    random_tree(branch_length * right_shrink, depth - 1)

    # Left branch
    left(right_angle + left_angle)
    random_tree(branch_length * left_shrink, depth - 1)

    # Return
    right(left_angle)
    backward(branch_length)
    width(2)

# Draw random tree
bgcolor('lightblue')
left(90)
penup()
backward(150)
pendown()
random_tree(100, 8)
```

---

## Generative Art

### Random Abstract Art

```python
from ColabTurtle.Turtle import *
import random
initializeTurtle(initial_speed=13)

def generative_art(iterations):
    """Create random abstract art"""
    bgcolor('black')

    shapes = ['circle', 'square', 'triangle', 'line']
    colors = ['red', 'orange', 'yellow', 'cyan', 'blue', 'magenta', 'white']

    for i in range(iterations):
        # Random position
        penup()
        x = random.randint(-200, 200)
        y = random.randint(-200, 200)
        # Navigate to (x, y)
        pendown()

        # Random shape
        shape = random.choice(shapes)
        color(random.choice(colors))
        size = random.randint(20, 80)

        if shape == 'circle':
            # Draw circle
            pass
        elif shape == 'square':
            for j in range(4):
                forward(size)
                right(90)
        elif shape == 'triangle':
            for j in range(3):
                forward(size)
                right(120)
        elif shape == 'line':
            forward(size)

# Generate art
generative_art(50)
```

---

## Practice Exercises

### Exercise 1: Random Mandala Generator
Create a function that generates a different mandala each time.

```python
def random_mandala():
    """Generate random mandala"""
    layers = random.randint(3, 6)
    petals = random.choice([6, 8, 12])
    colors = random.sample(['red', 'blue', 'green', 'yellow', 'purple', 'orange'], 3)

    # Draw mandala with random parameters
```

### Exercise 2: Noise Pattern
Create a pattern using Perlin noise or random gradients.

### Exercise 3: Random City Skyline
Generate a different city skyline with each run.

### Exercise 4: Particle System
Simulate particles moving randomly from a center point.

### Exercise 5: Randomized Maze
Draw a simple maze with random walls.

---

## Advanced Examples

### Controlled Randomness

```python
from ColabTurtle.Turtle import *
import random
initializeTurtle(initial_speed=13)

def controlled_random_pattern(chaos_level):
    """
    Create pattern with controlled randomness

    Parameters:
    -----------
    chaos_level : float
        0.0 (ordered) to 1.0 (chaotic)
    """
    colors = ['red', 'blue', 'green', 'yellow']
    size = 50

    for i in range(36):
        color(colors[i % len(colors)])

        # Size varies by chaos level
        random_size = size + random.randint(-int(size * chaos_level), int(size * chaos_level))

        # Angle varies by chaos level
        base_angle = 10
        random_angle = base_angle + random.randint(-int(20 * chaos_level), int(20 * chaos_level))

        forward(random_size)
        right(random_angle)

# Try different chaos levels
controlled_random_pattern(0.3)  # Low chaos
# controlled_random_pattern(0.8)  # High chaos
```

### Weighted Random Choices

```python
from ColabTurtle.Turtle import *
import random
initializeTurtle(initial_speed=13)

def weighted_pattern():
    """Use weighted probabilities for choices"""

    # Weighted color choices (red is more likely)
    colors = ['red'] * 5 + ['blue'] * 2 + ['green'] * 1

    for i in range(100):
        color(random.choice(colors))
        forward(10)
        right(random.randint(0, 360))

weighted_pattern()
```

---

## Challenge Project: Generative Art System

Create a generative art system that produces unique art each time.

**Requirements:**
- At least 3 configurable parameters
- Use both randomness and user parameters
- Produces visually interesting results
- Different output each time
- Option to save "seeds" for reproducible results

**Example:**
```python
from ColabTurtle.Turtle import *
import random

def generative_system(seed=None, complexity=5, color_palette='rainbow', style='organic'):
    """
    Generative art system

    Parameters:
    -----------
    seed : int
        Random seed for reproducibility (None for random)
    complexity : int
        Level of detail (1-10)
    color_palette : str
        'rainbow', 'monochrome', 'warm', 'cool'
    style : str
        'organic', 'geometric', 'mixed'
    """

    # Set seed for reproducibility
    if seed is not None:
        random.seed(seed)

    initializeTurtle(initial_speed=13)
    bgcolor('black')

    # Color palettes
    palettes = {
        'rainbow': ['red', 'orange', 'yellow', 'green', 'blue', 'purple'],
        'monochrome': ['white', 'lightgray', 'gray'],
        'warm': ['red', 'orange', 'yellow', 'pink'],
        'cool': ['cyan', 'blue', 'purple', 'lightblue']
    }

    colors = palettes.get(color_palette, palettes['rainbow'])

    # Generate based on style
    iterations = complexity * 20

    if style == 'organic':
        # Curved, flowing patterns
        for i in range(iterations):
            color(random.choice(colors))
            forward(random.randint(10, 50))
            right(random.randint(-60, 60))

    elif style == 'geometric':
        # Sharp, angular patterns
        for i in range(iterations):
            color(random.choice(colors))
            sides = random.choice([3, 4, 5, 6])
            size = random.randint(20, 80)

            # Draw polygon
            for j in range(sides):
                forward(size)
                right(360 / sides)

            # Move to new position
            penup()
            forward(random.randint(20, 100))
            right(random.randint(0, 360))
            pendown()

    elif style == 'mixed':
        # Combination
        for i in range(iterations):
            color(random.choice(colors))

            if random.random() < 0.5:
                # Organic
                forward(random.randint(10, 50))
                right(random.randint(-60, 60))
            else:
                # Geometric
                for j in range(4):
                    forward(random.randint(20, 60))
                    right(90)

# Create generative art
generative_system(seed=42, complexity=7, color_palette='cool', style='organic')

# Run again with different seed for different result
# generative_system(seed=123, complexity=7, color_palette='cool', style='organic')
```

---

## Key Concepts Review

1. **Random Module:** Generate random numbers, choices, samples
2. **Random Walks:** Unpredictable movement patterns
3. **Configurable Functions:** User parameters control output
4. **Generative Art:** Algorithm-based art creation
5. **Seeds:** Reproducible randomness
6. **Controlled Chaos:** Balance between order and randomness

---

## Week 11 Checklist

By the end of this week, you should be able to:

- [ ] Use random number generation
- [ ] Create random walks
- [ ] Generate random shapes
- [ ] Build configurable pattern generators
- [ ] Implement generative art systems
- [ ] Control randomness levels
- [ ] Use seeds for reproducibility
- [ ] Design unique algorithmic art

---

## Next Week Preview

In Week 12, we'll learn to:
- Combine all techniques learned
- Plan complex projects
- Create detailed scenes
- Use composition effectively
- Build portfolio pieces

---

## Additional Practice

Create these generative systems:
1. A random landscape generator
2. A procedural flower garden
3. A constellation maker
4. An abstract expressionism generator
5. Your own unique generative art system

Embrace the chaos! 🎲🐢
