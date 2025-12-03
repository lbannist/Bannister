# Python OOP Geometry with Dunders Assignment Guide

## 🎯 Introduction: Understanding Encapsulation and Dunders

Welcome to your Geometry assignment! This project introduces you to **encapsulation**—one of the core principles of Object-Oriented Programming. Encapsulation means protecting data within a class from being accidentally modified from outside the class.

### Why Encapsulation Matters

Imagine you're building a banking app. You wouldn't want anyone to directly change someone's account balance like this:

```python
# BAD - Anyone can change the balance!
account.balance = 1000000  # Instant millionaire!
```

Instead, you want controlled access through methods:

```python
# GOOD - Controlled through methods
account.deposit(100)  # Must follow rules
account.withdraw(50)  # Can check for sufficient funds
```

### Python's Approach: Naming Conventions

Unlike Java or C++ which use `public`, `private`, and `protected` keywords, Python uses **naming conventions with underscores**:

| Convention | Meaning | Example |
|------------|---------|---------|
| `name` | **Public** - accessible anywhere | `self.radius` |
| `_name` | **Protected** - internal use, but accessible | `self._radius` |
| `__name` | **Private** - strongly discouraged from outside | `self.__radius` |

**Important Note:** Python's privacy is based on *convention*, not enforcement. Even "private" variables can technically be accessed (through name mangling), but **in this course we maintain proper practice** ✅

### What Are Dunders?

**"Dunders"** (double-underscores) are special methods in Python that start and end with `__`. They're fundamental to how Python objects work:

- `__init__`: Constructor - runs when you create an object
- `__str__`: Returns a user-friendly string representation
- `__repr__`: Returns a detailed string for debugging
- `__del__`: Destructor - runs when object is deleted

You'll use these immediately in your first real classes!

---

## 📋 Assignment Overview

Create a geometry program with three classes that demonstrate:
- Multiple constructors (using default parameters)
- Private instance variables
- Essential dunder methods
- Encapsulation principles

**File name:** `[YourName]_OOP_Geometry.py`

---

## 🏗️ Class Requirements

### **Class 1: Circle**

#### Private Instance Variables (use `__` prefix):
- `__name` (string): The circle's name
- `__radius` (float): The radius in meters
- `__height` (float): The height in meters (0 for flat circles)

#### Constructor Methods:

Python doesn't support multiple constructors like Java, but we can simulate them using **default parameters**:

```python
class Circle:
    """A class representing a circle or cylinder"""
    
    def __init__(self, name, radius, height=0):
        """
        Constructor - Creates a Circle or Cylinder
        
        Parameters:
            name (str): Name of the shape
            radius (float): Radius in meters
            height (float): Height in meters (default=0 for flat circle)
        
        When height=0: Creates a flat circle
        When height>0: Creates a cylinder
        """
        self.__name = name
        self.__radius = radius
        self.__height = height
```

**Usage Examples:**
```python
# First constructor style: flat circle (height defaults to 0)
manhole = Circle("Man Hole", 0.5)

# Second constructor style: cylinder (height specified)
tower = Circle("Tower of Pisa", 20, 80)
```

#### Required Methods:

**1. `get_name(self)` - Getter Method**
```python
def get_name(self):
    """Returns the name of the shape"""
    return self.__name
```

**2. `print_area(self)` - Calculate and Display Area**
- If height is 0 (flat circle): Area = πr²
- If height > 0 (cylinder): Area = 2πr² + 2πrh (two ends + curved surface)
- Use 3.14 for π
- Print format: `"The [name]'s surface area is [area] square meters"`

**3. `print_circumference(self)` - Calculate and Display Circumference**
- Formula: C = 2πr
- Use 3.14 for π
- Print format: `"The [name]'s circumference is [circumference] meters"`

**4. `print_volume(self)` - Calculate and Display Volume**
- If height is 0: Print `"The [name] is not a cylinder. Volume cannot be computed."`
- If height > 0: Calculate V = πr²h and print `"The [name] is a cylinder. It has a volume of [volume] cubic meters"`

**5. `__str__(self)` - Dunder for String Representation**
```python
def __str__(self):
    """Returns user-friendly string when print() is called"""
    shape_type = "cylinder" if self.__height > 0 else "circle"
    return f"{self.__name} (a {shape_type} with radius {self.__radius}m)"
```

**6. `__repr__(self)` - Dunder for Detailed Representation**
```python
def __repr__(self):
    """Returns detailed string for debugging"""
    return f"Circle(name='{self.__name}', radius={self.__radius}, height={self.__height})"
```

---

### **Class 2: Rectangle**

#### Private Instance Variables (use `__` prefix):
- `__name` (string): The rectangle's name
- `__width` (float): Width in meters
- `__length` (float): Length in meters
- `__height` (float): Height in meters (0 for flat rectangles)

#### Constructor Method:

```python
class Rectangle:
    """A class representing a rectangle or rectangular prism"""
    
    def __init__(self, name, width, length, height=0):
        """
        Constructor - Creates a Rectangle or Rectangular Prism
        
        Parameters:
            name (str): Name of the shape
            width (float): Width in meters
            length (float): Length in meters
            height (float): Height in meters (default=0 for flat rectangle)
        
        When height=0: Creates a flat rectangle
        When height>0: Creates a rectangular prism (like a box)
        """
        self.__name = name
        self.__width = width
        self.__length = length
        self.__height = height
```

**Usage Examples:**
```python
# First constructor style: flat rectangle
paper = Rectangle("Paper", 0.216, 0.28)

# Second constructor style: rectangular prism
printer = Rectangle("Printer", 0.36, 0.32, 0.24)
```

#### Required Methods:

**1. `get_name(self)` - Getter Method**

**2. `print_area(self)` - Calculate and Display Surface Area**
- If height is 0 (flat): Area = width × length
- If height > 0 (prism): Area = 2(wl + wh + lh)
- Print format: `"The [name]'s surface area is [area] square meters"`

**3. `print_perimeter(self)` - Calculate and Display Base Perimeter**
- Formula: P = 2(width + length)
- Print format: `"The [name]'s perimeter is [perimeter] meters"`

**4. `print_volume(self)` - Calculate and Display Volume**
- Formula: V = width × length × height
- If height is 0: Volume will be 0
- Print format: `"The [name]'s volume is [volume] cubic meters"`

**5. `__str__(self)` and `__repr__(self)` - Dunder Methods**

Similar to Circle class, create user-friendly and detailed representations.

---

### **Class 3: GeometryMain**

This is your main program that creates objects and tests all functionality.

```python
def main():
    """Main program to test Circle and Rectangle classes"""
    
    # Create list to store all shapes
    shapes = []
    
    # Create circles
    manhole = Circle("Man Hole", 0.5)  # Flat circle
    tower = Circle("Tower of Pisa", 20, 80)  # Cylinder
    
    shapes.append(manhole)
    shapes.append(tower)
    
    # Create rectangles
    paper = Rectangle("Paper", 0.216, 0.28)  # Flat rectangle
    printer = Rectangle("Printer", 0.36, 0.32, 0.24)  # Prism
    
    shapes.append(paper)
    shapes.append(printer)
    
    # Print all shape details
    print("=== ALL SHAPES ===\n")
    for shape in shapes:
        print(f"{shape.get_name()} has the following properties:")
        shape.print_area()
        
        if isinstance(shape, Circle):
            shape.print_circumference()
        elif isinstance(shape, Rectangle):
            shape.print_perimeter()
        
        shape.print_volume()
        print()  # Blank line
    
    # Test __str__ dunder
    print("\n=== TESTING __str__ DUNDER ===")
    for shape in shapes:
        print(shape)  # This calls __str__
    
    # Test __repr__ dunder
    print("\n=== TESTING __repr__ DUNDER ===")
    for shape in shapes:
        print(repr(shape))  # This calls __repr__
    
    # Search functionality
    search_shapes(shapes)

if __name__ == "__main__":
    main()
```

---

## 🔍 Search Functionality

Implement a search function that allows users to find shapes by name:

```python
def search_shapes(shape_list):
    """
    FUNCTION - Searches for a shape by name
    Parameter: shape_list (list of Circle and Rectangle objects)
    """
    while True:
        print("\n=== SHAPE SEARCH ===")
        search_name = input("Enter shape name to search (or 'exit' to quit): ").strip()
        
        if search_name.lower() == 'exit':
            break
        
        found = False
        for shape in shape_list:
            if shape.get_name().lower() == search_name.lower():
                print(f"\n✓ Found: {shape}")
                print(f"\n{shape.get_name()} has the following properties:")
                shape.print_area()
                
                if isinstance(shape, Circle):
                    shape.print_circumference()
                elif isinstance(shape, Rectangle):
                    shape.print_perimeter()
                
                shape.print_volume()
                found = True
                break
        
        if not found:
            print(f"✗ Shape '{search_name}' not found in collection.")
```

---

## 📊 Expected Output Example

```
=== ALL SHAPES ===

Man Hole has the following properties:
The Man Hole's surface area is 0.785 square meters
The Man Hole's circumference is 3.14 meters
The Man Hole is not a cylinder. Volume cannot be computed.

Tower of Pisa has the following properties:
The Tower of Pisa's surface area is 12566.4 square meters
The Tower of Pisa's circumference is 125.6 meters
The Tower of Pisa is a cylinder. It has a volume of 100480.0 cubic meters

Paper has the following properties:
The Paper's surface area is 0.06048 square meters
The Paper's perimeter is 0.992 meters
The Paper's volume is 0.0 cubic meters

Printer has the following properties:
The Printer's surface area is 0.4608 square meters
The Printer's perimeter is 1.36 meters
The Printer's volume is 0.027648 cubic meters

=== TESTING __str__ DUNDER ===
Man Hole (a circle with radius 0.5m)
Tower of Pisa (a cylinder with radius 20m)
Paper (a rectangle with width 0.216m and length 0.28m)
Printer (a rectangular prism with width 0.36m and length 0.32m)

=== TESTING __repr__ DUNDER ===
Circle(name='Man Hole', radius=0.5, height=0)
Circle(name='Tower of Pisa', radius=20, height=80)
Rectangle(name='Paper', width=0.216, length=0.28, height=0)
Rectangle(name='Printer', width=0.36, length=0.32, height=0.24)

=== SHAPE SEARCH ===
Enter shape name to search (or 'exit' to quit): tower of pisa

✓ Found: Tower of Pisa (a cylinder with radius 20m)

Tower of Pisa has the following properties:
The Tower of Pisa's surface area is 12566.4 square meters
The Tower of Pisa's circumference is 125.6 meters
The Tower of Pisa is a cylinder. It has a volume of 100480.0 cubic meters
```

---

## ✅ Requirements Checklist

### Circle Class (30%)
- [ ] Three private instance variables: `__name`, `__radius`, `__height`
- [ ] Constructor with default parameter for height
- [ ] `get_name()` method
- [ ] `print_area()` method (handles both circle and cylinder)
- [ ] `print_circumference()` method
- [ ] `print_volume()` method (handles flat circles appropriately)
- [ ] `__str__()` dunder method
- [ ] `__repr__()` dunder method

### Rectangle Class (20%)
- [ ] Four private instance variables: `__name`, `__width`, `__length`, `__height`
- [ ] Constructor with default parameter for height
- [ ] `get_name()` method
- [ ] `print_area()` method (handles both rectangle and prism)
- [ ] `print_perimeter()` method
- [ ] `print_volume()` method
- [ ] `__str__()` dunder method
- [ ] `__repr__()` dunder method

### GeometryMain (30%)
- [ ] Creates Man Hole circle (flat, radius 0.5m)
- [ ] Creates Tower of Pisa cylinder (radius 20m, height 80m)
- [ ] Creates Paper rectangle (flat, 0.216m × 0.28m)
- [ ] Creates Printer prism (0.36m × 0.32m × 0.24m)
- [ ] Stores all shapes in single list
- [ ] Uses loop to print all shape properties
- [ ] Tests `__str__` dunder by printing objects
- [ ] Tests `__repr__` dunder using `repr()`
- [ ] Uses `isinstance()` to identify shape type

### Search Functionality (10%)
- [ ] Prompts user for shape name
- [ ] Searches through list
- [ ] Prints all properties if found
- [ ] Handles "not found" cases gracefully
- [ ] Loop allows multiple searches
- [ ] Case-insensitive search

### Code Quality (10%)
- [ ] Proper use of private variables (`__` prefix)
- [ ] Comprehensive comments and docstrings
- [ ] File named correctly: `[YourName]_OOP_Geometry.py`
- [ ] Clean, readable code structure
- [ ] No direct access to private variables from main

---

## 💡 Understanding Key Concepts

### 1. Default Parameters (Simulating Multiple Constructors)

Python doesn't have method overloading like Java, but default parameters achieve the same goal:

```python
# In Java, you'd need two separate constructors:
# Circle(String name, double radius)
# Circle(String name, double radius, double height)

# In Python, use default parameters:
def __init__(self, name, radius, height=0):
    # Works for both cases!
```

### 2. Private Variables with Name Mangling

When you use `__variable`, Python performs "name mangling":

```python
class Circle:
    def __init__(self, name, radius):
        self.__radius = radius  # Private

# Outside the class:
c = Circle("Test", 5)
print(c.__radius)  # ❌ AttributeError!
print(c._Circle__radius)  # ⚠️ Technically works but DON'T DO THIS!
```

**Best Practice:** Use getter/setter methods to access private variables:

```python
def get_radius(self):
    return self.__radius

def set_radius(self, radius):
    if radius > 0:  # Can add validation!
        self.__radius = radius
```

### 3. The `isinstance()` Function

Use `isinstance()` to check what type of object you have:

```python
if isinstance(shape, Circle):
    shape.print_circumference()  # Only circles have this
elif isinstance(shape, Rectangle):
    shape.print_perimeter()  # Only rectangles have this
```

### 4. `__str__` vs `__repr__`

**`__str__`**: For end users (readable)
```python
print(circle)  # "Man Hole (a circle with radius 0.5m)"
```

**`__repr__`**: For developers (unambiguous)
```python
print(repr(circle))  # "Circle(name='Man Hole', radius=0.5, height=0)"
```

**Pro Tip:** `__repr__` should ideally let you recreate the object:
```python
circle = eval(repr(circle))  # Should work!
```

---

## 🧪 Testing Your Program

### Test 1: Circle Calculations
- **Man Hole** (r=0.5, h=0):
  - Area = πr² = 3.14 × 0.5² = **0.785 m²**
  - Circumference = 2πr = 2 × 3.14 × 0.5 = **3.14 m**
  - Volume = Not a cylinder

- **Tower of Pisa** (r=20, h=80):
  - Area = 2πr² + 2πrh = 2(3.14)(20²) + 2(3.14)(20)(80) = **12,566.4 m²**
  - Circumference = 2πr = 2 × 3.14 × 20 = **125.6 m**
  - Volume = πr²h = 3.14 × 20² × 80 = **100,480 m³**

### Test 2: Rectangle Calculations
- **Paper** (w=0.216, l=0.28, h=0):
  - Area = wl = 0.216 × 0.28 = **0.06048 m²**
  - Perimeter = 2(w+l) = 2(0.216 + 0.28) = **0.992 m**
  - Volume = **0 m³**

- **Printer** (w=0.36, l=0.32, h=0.24):
  - Area = 2(wl + wh + lh) = 2(0.1152 + 0.0864 + 0.0768) = **0.5568 m²**
  - Perimeter = 2(0.36 + 0.32) = **1.36 m**
  - Volume = wlh = 0.36 × 0.32 × 0.24 = **0.027648 m³**

### Test 3: Dunder Methods
```python
# Test __str__
print(manhole)  # Should be user-friendly

# Test __repr__
print(repr(manhole))  # Should show all details

# Test that print() uses __str__
for shape in shapes:
    print(shape)  # Calls __str__ automatically
```

### Test 4: Encapsulation
```python
# This should NOT work (and you shouldn't do it):
try:
    print(manhole.__radius)  # Should raise AttributeError
except AttributeError:
    print("✓ Private variable is protected!")

# This SHOULD work:
print(manhole.get_name())  # Uses getter method
```

---

## 🚀 Extension Challenges (Optional)

### Challenge 1: Add Validation
Prevent invalid shapes:
```python
def __init__(self, name, radius, height=0):
    if radius <= 0:
        raise ValueError("Radius must be positive!")
    if height < 0:
        raise ValueError("Height cannot be negative!")
    # ... set variables
```

### Challenge 2: Add More Dunders
Implement comparison dunders:
```python
def __eq__(self, other):
    """Check if two circles are equal"""
    if not isinstance(other, Circle):
        return False
    return self.__radius == other.__radius

def __lt__(self, other):
    """Check if this circle is smaller"""
    return self.__radius < other.__radius
```

### Challenge 3: Add Setter Methods
Create setters with validation:
```python
def set_radius(self, radius):
    """Setter for radius with validation"""
    if radius > 0:
        self.__radius = radius
    else:
        print("Error: Radius must be positive")
```

### Challenge 4: Create a Sphere Class
Extend your program with a new shape!

---

## ⚠️ Common Mistakes to Avoid

### Mistake 1: Accessing Private Variables Directly
```python
# ❌ WRONG - Don't do this!
print(circle.__radius)

# ✅ CORRECT - Use getter method
print(circle.get_radius())
```

### Mistake 2: Forgetting `self` Parameter
```python
# ❌ WRONG
def print_area():
    return 3.14 * radius ** 2

# ✅ CORRECT
def print_area(self):
    return 3.14 * self.__radius ** 2
```

### Mistake 3: Printing Inside Methods That Should Return
```python
# ❌ WRONG for get_name()
def get_name(self):
    print(self.__name)

# ✅ CORRECT
def get_name(self):
    return self.__name
```

### Mistake 4: Not Using `isinstance()` Before Method Calls
```python
# ❌ WRONG - Will crash if shape is Rectangle
for shape in shapes:
    shape.print_circumference()  # Rectangles don't have this!

# ✅ CORRECT
for shape in shapes:
    if isinstance(shape, Circle):
        shape.print_circumference()
```

---

## 📝 Submission Checklist

Before submitting, verify:
- [ ] File named: `[YourName]_OOP_Geometry.py`
- [ ] All private variables use `__` prefix
- [ ] Both classes have `__str__` and `__repr__`
- [ ] All calculations are correct (verify with calculator)
- [ ] Search function works with case-insensitive input
- [ ] Comments explain all major sections
- [ ] No direct access to private variables from main
- [ ] Program runs without errors
- [ ] Output matches expected format

---

## 🎓 Key Learning Objectives

By completing this assignment, you'll master:

1. **Encapsulation**: Protecting data with private variables
2. **Dunder Methods**: `__init__`, `__str__`, `__repr__`
3. **Default Parameters**: Simulating multiple constructors
4. **Type Checking**: Using `isinstance()` effectively
5. **Single List Design**: Storing different object types together
6. **Getter Methods**: Controlled access to private data
7. **Python Conventions**: Understanding `_` and `__` naming
8. **Name Mangling**: How Python implements privacy

---

## 📚 Reference: Public vs Protected vs Private

| Type | Syntax | Accessible From | Use Case |
|------|--------|----------------|----------|
| **Public** | `self.name` | Anywhere | Public API, frequently accessed |
| **Protected** | `self._name` | Class & subclasses | Internal use, inheritance |
| **Private** | `self.__name` | Class only (name mangled) | Strong encapsulation needed |

**Remember:** In this course, we maintain proper practice by not accessing private variables from outside the class! ✅

---

Good luck with your Geometry program! 📐✨