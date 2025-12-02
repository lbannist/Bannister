# Python OOP Calculator Assignment Guide

## 🎯 Introduction

Welcome to your Object-Oriented Programming calculator project! In this assignment, you'll explore one of the fundamental concepts in Python programming: **the difference between functions and methods**.

While both functions and methods perform operations and can return results, they work in distinctly different ways. Understanding this difference is crucial as you develop your skills in object-oriented programming.

**Think of it this way:**
- A **function** is like a standalone tool in your toolbox—you pick it up and use it whenever you need it
- A **method** is like a feature built into a machine—you access it through the machine itself

## 📚 Understanding Functions vs Methods

### What is a Function?

A **function** is an independent block of code that:
- Lives on its own (not attached to any object)
- Is called directly by name
- Works with data you pass to it as arguments
- Returns a result without changing any object's state

**Example:**
```python
def add(a, b):
    return a + b

result = add(5, 3)  # Called directly
```

### What is a Method?

A **method** is a function that:
- Belongs to a class (lives inside it)
- Is called on an object using dot notation
- Can access and modify the object's internal data
- Works as part of an object's behavior

**Example:**
```python
class Calculator:
    def add(self, a, b):
        return a + b

my_calc = Calculator()  # Create an object
result = my_calc.add(5, 3)  # Called on the object
```

### Key Differences Summary

| Aspect | Function | Method |
|--------|----------|--------|
| **How to call** | `add(5, 3)` | `calculator.add(5, 3)` |
| **Where it lives** | Outside any class | Inside a class |
| **First parameter** | Whatever you choose | Always `self` |
| **Access to object data** | No | Yes |
| **Independence** | Completely standalone | Tied to an object |

---

## 🎯 Assignment Overview

Create a calculator program that uses **both functions and methods** to perform at least 6 different calculations.

---

## 📋 Step-by-Step Implementation Guide

### **Step 1: Set Up Your File Structure**

Create a file named: `Calculator_[YourName].py`

### **Step 2: Create Standalone Functions**

These are **functions** (not methods) because they don't belong to a class.

```python
# FUNCTIONS - Called directly, not on an object

def add_function(num1, num2):
    """This is a FUNCTION - adds two numbers"""
    return num1 + num2

def subtract_function(num1, num2):
    """This is a FUNCTION - subtracts num2 from num1"""
    return num1 - num2

# Add more functions here (multiply, divide, etc.)
```

### **Step 3: Create a Calculator Class with Methods**

These are **methods** because they belong to a class and are called on objects.

```python
# CLASS with METHODS - Called on an object

class Calculator:
    """Calculator class containing various calculation methods"""
    
    def __init__(self):
        """Constructor - initializes the calculator"""
        self.name = "Basic Calculator"
    
    def add_method(self, num1, num2):
        """This is a METHOD - adds two numbers"""
        return num1 + num2
    
    def power_method(self, base, exponent):
        """This is a METHOD - raises base to the power of exponent"""
        return base ** exponent
    
    # Add more methods here
```

### **Step 4: Build the Menu Loop**

Create a main program that:
1. Displays menu options
2. Gets user choice
3. Validates input
4. Calls appropriate function/method
5. Displays result
6. Loops until user exits

```python
def main():
    """Main program loop"""
    calc = Calculator()  # Create calculator object
    
    while True:
        print("\n=== CALCULATOR MENU ===")
        print("1. Add (using function)")
        print("2. Subtract (using function)")
        print("3. Multiply (using method)")
        print("4. Power (using method)")
        print("5. Hypotenuse (your choice)")
        print("6. Divide (your choice)")
        print("Type 'exit' to quit")
        
        choice = input("\nEnter your choice: ").lower()
        
        # Check for exit
        if choice == 'exit':
            print("Thank you for using the calculator!")
            break
        
        # Validate input
        if choice not in ['1', '2', '3', '4', '5', '6']:
            print("Invalid choice. Please try again.")
            continue
        
        # Get numbers from user and perform calculation
        # (You'll implement this part)
```

---

## ✅ Requirements Checklist

- [ ] **At least 6 calculations** implemented
- [ ] **Mix of functions and methods** (not all the same)
- [ ] **Clear comments** explaining which are functions vs methods
- [ ] **User input validation** (handle invalid choices)
- [ ] **Menu loop** continues until user types "exit"
- [ ] **Each calculation asks for appropriate input** using `input()`
- [ ] **Results displayed** in the main program
- [ ] **Debug print statements commented out** (not deleted)
- [ ] **Proper file naming**: `Calculator_[YourName].py`

---

## 💡 Suggested Calculations

### Required (at least 6):
1. **Add** - sum of two numbers
2. **Subtract** - difference of two numbers
3. **Multiply** - product of two numbers
4. **Divide** - quotient (handle division by zero!)
5. **Hypotenuse** - `√(a² + b²)` for right triangle
6. **Power** - raise base to exponent

### Optional (for extra challenge):
7. **BEDMAS calculator** - handles order of operations
8. **Bracket handler** - evaluates expressions with parentheses

---

## 🔍 Testing Your Program

Test with these scenarios:
- Valid menu choices (1-6)
- Invalid menu choices (7, abc, -1)
- Division by zero
- Negative numbers
- Decimal numbers
- Typing "exit" to quit

---

## 📝 Commenting Guide

Use comments to explain:
- **What type it is**: "This is a FUNCTION" or "This is a METHOD"
- **What it does**: Brief description of the calculation
- **Parameters**: What inputs it expects
- **Return value**: What it gives back

Example:
```python
def calculate_hypotenuse(side_a, side_b):
    """
    This is a FUNCTION - calculates the hypotenuse of a right triangle
    Parameters: side_a (float), side_b (float)
    Returns: hypotenuse length (float)
    """
    return (side_a**2 + side_b**2)**0.5
```

---

## 🚀 Getting Started Tips

1. **Start simple**: Get the menu working with just 2 calculations first
2. **Test frequently**: Run your program after adding each new feature
3. **Comment as you go**: Don't wait until the end to add comments
4. **Handle errors**: Think about what could go wrong (invalid input, division by zero)
5. **Use meaningful names**: `calculate_hypotenuse` is better than `calc_h`

---

## 🎓 Key Learning Objectives

By completing this assignment, you'll understand:
- The difference between functions and methods
- How to create and use classes in Python
- Object-oriented programming basics
- User input validation
- Program control flow with loops
- Code organization and documentation

Good luck with your calculator! 🧮