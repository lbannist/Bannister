# Python *args and **kwargs Assignment Guide

## 🎯 Introduction: Flexible Function Parameters

Welcome to your *args and **kwargs assignment! These powerful Python features allow you to write functions that accept **any number of arguments**—making your code more flexible and reusable.

### The Problem They Solve

Imagine you're writing a calculator. With regular parameters, you can only add two numbers:

```python
def add(a, b):
    return a + b

result = add(5, 3)  # Works!
result = add(5, 3, 2)  # ❌ Error! Too many arguments
```

But what if you want to add 3, 5, or even 10 numbers? You'd need to write many different functions—or use ***args**!

```python
def add(*numbers):
    return sum(numbers)

result = add(5, 3)  # Works!
result = add(5, 3, 2)  # Works!
result = add(5, 3, 2, 8, 1)  # Also works!
```

### Understanding *args and **kwargs

| Feature | What It Does | Example |
|---------|-------------|---------|
| **`*args`** | Accepts any number of **positional** arguments | `func(1, 2, 3)` |
| **`**kwargs`** | Accepts any number of **keyword** arguments | `func(name="Bob", age=15)` |

**Think of it this way:**
- **`*args`** = "Arguments" → A tuple of values in order
- **`**kwargs`** = "Keyword Arguments" → A dictionary of name=value pairs

**The asterisks matter!**
- The `*` and `**` are what make the magic happen
- `args` and `kwargs` are just conventional names (you could use other names, but everyone uses these)

---

## 📋 Assignment Overview

Create a **Restaurant Order System** that uses *args and **kwargs to handle flexible menu items, toppings, and customizations.

**File name:** `[YourName]_Restaurant.py`

---

## 🏗️ Part 1: Understanding *args (Positional Arguments)

### What Are Positional Arguments?

Positional arguments are values passed **in order** without names:

```python
greet("Alice", "Bob", "Charlie")  # Order matters!
```

### How *args Works

The `*` collects all positional arguments into a **tuple**:

```python
def greet(*names):
    print(f"Type of names: {type(names)}")  # <class 'tuple'>
    print(f"Contents: {names}")  # ('Alice', 'Bob', 'Charlie')
    
    for name in names:
        print(f"Hello, {name}!")

greet("Alice", "Bob", "Charlie")
```

**Output:**
```
Type of names: <class 'tuple'>
Contents: ('Alice', 'Bob', 'Charlie')
Hello, Alice!
Hello, Bob!
Hello, Charlie!
```

### Task 1.1: Create calculate_total() Function

```python
def calculate_total(*prices):
    """
    FUNCTION - Calculates the total cost of menu items
    
    Parameters:
        *prices: Any number of prices (floats)
    
    Returns:
        total (float): Sum of all prices
    
    Example:
        calculate_total(5.99, 3.50, 2.25) → 11.74
    """
    # YOUR CODE HERE
    pass
```

**Requirements:**
- Accept any number of price arguments
- Calculate and return the sum
- Handle the case when no arguments are passed (return 0)

### Task 1.2: Create find_most_expensive() Function

```python
def find_most_expensive(*prices):
    """
    FUNCTION - Finds the highest price from menu items
    
    Parameters:
        *prices: Any number of prices (floats)
    
    Returns:
        highest (float): The maximum price, or 0 if no prices given
    
    Example:
        find_most_expensive(5.99, 12.50, 3.25) → 12.50
    """
    # YOUR CODE HERE
    pass
```

### Task 1.3: Create list_items() Function

```python
def list_items(*items):
    """
    FUNCTION - Prints a numbered list of menu items
    
    Parameters:
        *items: Any number of item names (strings)
    
    Returns:
        None (prints the list)
    
    Example:
        list_items("Burger", "Fries", "Shake")
        Output:
            1. Burger
            2. Fries
            3. Shake
    """
    # YOUR CODE HERE
    pass
```

---

## 🏗️ Part 2: Understanding **kwargs (Keyword Arguments)

### What Are Keyword Arguments?

Keyword arguments are values passed with **names** (like a dictionary):

```python
order_pizza(size="Large", cheese="Extra", peppers=True)
```

### How **kwargs Works

The `**` collects all keyword arguments into a **dictionary**:

```python
def order_pizza(**toppings):
    print(f"Type: {type(toppings)}")  # <class 'dict'>
    print(f"Contents: {toppings}")  # {'size': 'Large', 'cheese': 'Extra'}
    
    for key, value in toppings.items():
        print(f"{key}: {value}")

order_pizza(size="Large", cheese="Extra", peppers=True)
```

**Output:**
```
Type: <class 'dict'>
Contents: {'size': 'Large', 'cheese': 'Extra', 'peppers': True}
size: Large
cheese: Extra
peppers: True
```

### Task 2.1: Create customize_burger() Function

```python
def customize_burger(**options):
    """
    FUNCTION - Prints burger customizations
    
    Parameters:
        **options: Any number of customization options (keyword arguments)
    
    Returns:
        None (prints the customizations)
    
    Example:
        customize_burger(bun="Sesame", patty="Beef", cheese="Cheddar", bacon=True)
        Output:
            Burger Customizations:
            - bun: Sesame
            - patty: Beef
            - cheese: Cheddar
            - bacon: True
    """
    # YOUR CODE HERE
    pass
```

### Task 2.2: Create calculate_price_with_extras() Function

```python
def calculate_price_with_extras(base_price, **extras):
    """
    FUNCTION - Calculates total price including extra toppings
    
    Parameters:
        base_price (float): Starting price of the item
        **extras: Topping names and their prices
    
    Returns:
        total (float): Base price plus all extras
    
    Example:
        calculate_price_with_extras(8.99, cheese=1.50, bacon=2.00, avocado=1.75)
        → 14.24
    """
    # YOUR CODE HERE
    pass
```

### Task 2.3: Create print_order_summary() Function

```python
def print_order_summary(**order_details):
    """
    FUNCTION - Prints a formatted order summary
    
    Parameters:
        **order_details: Any details about the order (name, item, price, etc.)
    
    Returns:
        None (prints formatted summary)
    
    Example:
        print_order_summary(customer="Alice", item="Burger", price=8.99, table=5)
        Output:
            ===== ORDER SUMMARY =====
            Customer: Alice
            Item: Burger
            Price: $8.99
            Table: 5
    """
    # YOUR CODE HERE
    pass
```

---

## 🏗️ Part 3: Combining *args and **kwargs

### The Power of Combining Both

You can use both in the same function! **Order matters:**

```python
def order_meal(restaurant_name, *items, **details):
    """All three types of parameters!"""
    print(f"Ordering from: {restaurant_name}")  # Regular parameter
    print(f"Items: {items}")  # *args tuple
    print(f"Details: {details}")  # **kwargs dictionary

order_meal("Pizza Palace", "Pizza", "Salad", "Soda", 
           table=7, delivery=False, tip=5.00)
```

**Output:**
```
Ordering from: Pizza Palace
Items: ('Pizza', 'Salad', 'Soda')
Details: {'table': 7, 'delivery': False, 'tip': 5.0}
```

**Parameter Order Rules:**
1. Regular parameters (required)
2. `*args` (optional positional)
3. `**kwargs` (optional keyword)

### Task 3.1: Create place_order() Function

```python
def place_order(customer_name, *items, **preferences):
    """
    FUNCTION - Places a complete restaurant order
    
    Parameters:
        customer_name (str): Name of the customer
        *items: Any number of menu items ordered
        **preferences: Any number of special requests or details
    
    Returns:
        None (prints complete order)
    
    Example:
        place_order("Bob", "Burger", "Fries", "Shake", 
                    table=3, spicy=True, no_onions=True)
        Output:
            Customer: Bob
            Items ordered: Burger, Fries, Shake
            Special Requests:
              - table: 3
              - spicy: True
              - no_onions: True
    """
    # YOUR CODE HERE
    pass
```

### Task 3.2: Create calculate_group_bill() Function

```python
def calculate_group_bill(*prices, tip_percent=15, tax_percent=8):
    """
    FUNCTION - Calculates total bill with tax and tip
    
    Parameters:
        *prices: Any number of item prices
        tip_percent (int): Tip percentage (default 15%)
        tax_percent (int): Tax percentage (default 8%)
    
    Returns:
        dict: Dictionary with subtotal, tax, tip, and total
    
    Example:
        calculate_group_bill(12.99, 8.50, 15.75, tip_percent=20, tax_percent=10)
        → {'subtotal': 37.24, 'tax': 3.72, 'tip': 7.45, 'total': 48.41}
    """
    # YOUR CODE HERE
    pass
```

---

## 🏗️ Part 4: The Restaurant Class

Create a class that uses *args and **kwargs in its methods.

```python
class Restaurant:
    """A restaurant that handles flexible orders"""
    
    def __init__(self, name, cuisine_type):
        """
        Constructor
        
        Parameters:
            name (str): Restaurant name
            cuisine_type (str): Type of cuisine (Italian, Mexican, etc.)
        """
        self.__name = name
        self.__cuisine_type = cuisine_type
        self.__menu = {}  # Dictionary to store menu items
        self.__orders = []  # List to store orders
    
    def add_menu_items(self, **items):
        """
        METHOD - Adds items to the menu
        
        Parameters:
            **items: Item names as keys, prices as values
        
        Example:
            restaurant.add_menu_items(burger=8.99, fries=3.50, shake=4.25)
        """
        # YOUR CODE HERE
        pass
    
    def display_menu(self):
        """
        METHOD - Prints the full menu
        """
        # YOUR CODE HERE
        pass
    
    def take_order(self, customer_name, *items, **customizations):
        """
        METHOD - Records a customer order
        
        Parameters:
            customer_name (str): Customer's name
            *items: Menu items being ordered
            **customizations: Special requests
        
        Returns:
            order_number (int): The order number assigned
        """
        # YOUR CODE HERE
        pass
    
    def calculate_order_total(self, *item_names):
        """
        METHOD - Calculates total for specific items
        
        Parameters:
            *item_names: Names of items to calculate
        
        Returns:
            total (float): Sum of item prices
        """
        # YOUR CODE HERE
        pass
    
    def get_name(self):
        """Getter for restaurant name"""
        return self.__name
    
    def __str__(self):
        """String representation"""
        return f"{self.__name} - {self.__cuisine_type} Restaurant"
    
    def __repr__(self):
        """Detailed representation"""
        return f"Restaurant(name='{self.__name}', cuisine='{self.__cuisine_type}', menu_items={len(self.__menu)})"
```

---

## 🏗️ Part 5: Main Program with Menu

```python
def main():
    """Main program demonstrating *args and **kwargs"""
    
    print("=== PART 1: Testing *args Functions ===\n")
    
    # Test calculate_total
    total = calculate_total(5.99, 3.50, 12.99, 2.25)
    print(f"Total: ${total:.2f}")
    
    # Test find_most_expensive
    highest = find_most_expensive(5.99, 3.50, 12.99, 2.25)
    print(f"Most expensive: ${highest:.2f}")
    
    # Test list_items
    print("\nMenu Items:")
    list_items("Burger", "Pizza", "Salad", "Fries", "Shake")
    
    print("\n=== PART 2: Testing **kwargs Functions ===\n")
    
    # Test customize_burger
    customize_burger(bun="Brioche", patty="Beef", cheese="Cheddar", 
                     bacon=True, lettuce=True, tomato=True)
    
    # Test calculate_price_with_extras
    price = calculate_price_with_extras(8.99, cheese=1.50, bacon=2.00, avocado=1.75)
    print(f"\nTotal with extras: ${price:.2f}")
    
    # Test print_order_summary
    print()
    print_order_summary(customer="Alice", item="Deluxe Burger", 
                       price=14.24, table=5, time="12:30 PM")
    
    print("\n=== PART 3: Testing Combined *args and **kwargs ===\n")
    
    # Test place_order
    place_order("Bob", "Burger", "Fries", "Shake", 
                table=3, spicy=True, extra_sauce=True)
    
    # Test calculate_group_bill
    print()
    bill = calculate_group_bill(12.99, 8.50, 15.75, 9.25, tip_percent=20, tax_percent=10)
    print(f"Subtotal: ${bill['subtotal']:.2f}")
    print(f"Tax (10%): ${bill['tax']:.2f}")
    print(f"Tip (20%): ${bill['tip']:.2f}")
    print(f"Total: ${bill['total']:.2f}")
    
    print("\n=== PART 4: Testing Restaurant Class ===\n")
    
    # Create restaurant
    restaurant = Restaurant("Burger Haven", "American")
    print(restaurant)
    
    # Add menu items
    restaurant.add_menu_items(burger=8.99, cheeseburger=9.99, 
                             fries=3.50, onion_rings=4.25, 
                             shake=4.50, soda=2.00)
    
    # Display menu
    restaurant.display_menu()
    
    # Take orders
    order1 = restaurant.take_order("Charlie", "burger", "fries", "shake",
                                   no_pickles=True, extra_sauce=True)
    order2 = restaurant.take_order("Diana", "cheeseburger", "onion_rings", "soda",
                                   table=7, to_go=False)
    
    # Calculate order total
    total = restaurant.calculate_order_total("burger", "fries", "shake")
    print(f"\nCharlie's order total: ${total:.2f}")

if __name__ == "__main__":
    main()
```

---

## ✅ Requirements Checklist

### Part 1: *args Functions (20%)
- [ ] `calculate_total(*prices)` - sums all prices
- [ ] `find_most_expensive(*prices)` - returns highest price
- [ ] `list_items(*items)` - prints numbered list

### Part 2: **kwargs Functions (20%)
- [ ] `customize_burger(**options)` - prints all customizations
- [ ] `calculate_price_with_extras(base_price, **extras)` - adds extra costs
- [ ] `print_order_summary(**order_details)` - formats order info

### Part 3: Combined Functions (20%)
- [ ] `place_order(customer_name, *items, **preferences)` - complete order
- [ ] `calculate_group_bill(*prices, tip_percent, tax_percent)` - returns dict with breakdown

### Part 4: Restaurant Class (25%)
- [ ] Private variables for name, cuisine, menu, orders
- [ ] `add_menu_items(**items)` method
- [ ] `display_menu()` method
- [ ] `take_order(customer_name, *items, **customizations)` method
- [ ] `calculate_order_total(*item_names)` method
- [ ] `__str__()` and `__repr__()` dunders

### Part 5: Main Program (15%)
- [ ] Tests all Part 1 functions with different numbers of arguments
- [ ] Tests all Part 2 functions with various keyword arguments
- [ ] Tests all Part 3 functions with combined parameters
- [ ] Creates Restaurant object and tests all methods
- [ ] Demonstrates flexibility of *args and **kwargs

---

## 💡 Understanding Key Concepts

### Concept 1: *args Creates a Tuple

```python
def example(*args):
    print(type(args))  # <class 'tuple'>
    print(args[0])  # Access first element
    print(len(args))  # Number of arguments
    
    for arg in args:  # Loop through all
        print(arg)

example(1, 2, 3, 4, 5)
```

### Concept 2: **kwargs Creates a Dictionary

```python
def example(**kwargs):
    print(type(kwargs))  # <class 'dict'>
    print(kwargs['name'])  # Access by key
    print(len(kwargs))  # Number of key-value pairs
    
    for key, value in kwargs.items():  # Loop through all
        print(f"{key}: {value}")

example(name="Alice", age=15, grade="10th")
```

### Concept 3: Unpacking with * and **

You can also use `*` and `**` to **unpack** collections:

```python
# Unpacking a list with *
prices = [5.99, 3.50, 2.25]
total = calculate_total(*prices)  # Same as calculate_total(5.99, 3.50, 2.25)

# Unpacking a dictionary with **
options = {'bun': 'Sesame', 'cheese': 'Cheddar', 'bacon': True}
customize_burger(**options)  # Same as customize_burger(bun='Sesame', cheese='Cheddar', bacon=True)
```

### Concept 4: Default Values with **kwargs

```python
def greet(**kwargs):
    name = kwargs.get('name', 'Guest')  # Default to 'Guest'
    age = kwargs.get('age', 'unknown')  # Default to 'unknown'
    print(f"Hello {name}, age {age}!")

greet(name="Bob")  # age will be 'unknown'
greet(name="Alice", age=15)  # Both provided
```

---

## 🧪 Testing Your Program

### Test 1: *args Flexibility
```python
# Different numbers of arguments should all work
calculate_total(5.99)  # 1 argument
calculate_total(5.99, 3.50)  # 2 arguments
calculate_total(5.99, 3.50, 2.25, 12.99)  # 4 arguments
calculate_total()  # 0 arguments (should return 0)
```

### Test 2: **kwargs Flexibility
```python
# Different keyword arguments should all work
customize_burger(bun="Sesame")  # 1 option
customize_burger(bun="Sesame", cheese="Cheddar")  # 2 options
customize_burger(bun="Sesame", cheese="Cheddar", bacon=True, lettuce=True)  # Many options
customize_burger()  # 0 options (should handle gracefully)
```

### Test 3: Order Matters
```python
# ✅ CORRECT order
def test(regular, *args, **kwargs):
    pass

# ❌ WRONG order - will cause error
def test(*args, regular, **kwargs):  # Can't have required param after *args
    pass
```

### Test 4: Restaurant Class
```python
restaurant = Restaurant("Test", "American")

# Add various numbers of items
restaurant.add_menu_items(burger=8.99)
restaurant.add_menu_items(fries=3.50, shake=4.25, soda=2.00)

# Order with different numbers of items and customizations
restaurant.take_order("Alice", "burger")
restaurant.take_order("Bob", "burger", "fries", "shake", table=5)
restaurant.take_order("Charlie", "burger", "soda", spicy=True, no_onions=True, extra_sauce=True)
```

---

## 📊 Expected Output Example

```
=== PART 1: Testing *args Functions ===

Total: $24.73
Most expensive: $12.99

Menu Items:
1. Burger
2. Pizza
3. Salad
4. Fries
5. Shake

=== PART 2: Testing **kwargs Functions ===

Burger Customizations:
- bun: Brioche
- patty: Beef
- cheese: Cheddar
- bacon: True
- lettuce: True
- tomato: True

Total with extras: $14.24

===== ORDER SUMMARY =====
Customer: Alice
Item: Deluxe Burger
Price: $14.24
Table: 5
Time: 12:30 PM

=== PART 3: Testing Combined *args and **kwargs ===

Customer: Bob
Items ordered: Burger, Fries, Shake
Special Requests:
  - table: 3
  - spicy: True
  - extra_sauce: True

Subtotal: $46.49
Tax (10%): $4.65
Tip (20%): $9.30
Total: $60.44

=== PART 4: Testing Restaurant Class ===

Burger Haven - American Restaurant

===== MENU =====
burger: $8.99
cheeseburger: $9.99
fries: $3.50
onion_rings: $4.25
shake: $4.50
soda: $2.00

Order #1 placed for Charlie
Items: burger, fries, shake
Customizations: no_pickles, extra_sauce

Order #2 placed for Diana
Items: cheeseburger, onion_rings, soda
Customizations: table, to_go

Charlie's order total: $16.99
```

---

## ⚠️ Common Mistakes to Avoid

### Mistake 1: Wrong Parameter Order
```python
# ❌ WRONG
def example(**kwargs, *args):  # kwargs can't come before args!
    pass

# ✅ CORRECT
def example(*args, **kwargs):
    pass
```

### Mistake 2: Forgetting the Asterisks
```python
# ❌ WRONG - args is just a regular parameter name
def calculate_total(args):
    return sum(args)

calculate_total(1, 2, 3)  # Error! Takes 1 argument, got 3

# ✅ CORRECT - *args collects multiple arguments
def calculate_total(*args):
    return sum(args)

calculate_total(1, 2, 3)  # Works!
```

### Mistake 3: Modifying Tuple (args)
```python
def example(*args):
    args[0] = 100  # ❌ Error! Tuples are immutable
    
    # ✅ Convert to list first if you need to modify
    args_list = list(args)
    args_list[0] = 100
```

### Mistake 4: Not Handling Empty Cases
```python
# ❌ WRONG - crashes when no arguments given
def find_most_expensive(*prices):
    return max(prices)  # Error if prices is empty!

# ✅ CORRECT - handle empty case
def find_most_expensive(*prices):
    if len(prices) == 0:
        return 0
    return max(prices)
```

---

## 🚀 Extension Challenges (Optional)

### Challenge 1: Menu Search
Add a method to search menu items:
```python
def search_menu(self, *search_terms, max_price=None):
    """Returns items matching any search term and under max_price"""
    pass
```

### Challenge 2: Combo Deals
Create a function that applies discounts:
```python
def create_combo(*items, discount_percent=10, **extras):
    """Calculates combo price with discount and extras"""
    pass
```

### Challenge 3: Order History
Add method to filter orders:
```python
def get_orders(self, **filters):
    """
    Returns orders matching filters
    Example: get_orders(customer="Bob", table=5)
    """
    pass
```

---

## 📝 Submission Checklist

Before submitting, verify:
- [ ] File named: `[YourName]_Restaurant.py`
- [ ] All Part 1 functions work with varying numbers of arguments
- [ ] All Part 2 functions work with varying keyword arguments
- [ ] Part 3 functions combine both parameter types correctly
- [ ] Restaurant class uses private variables
- [ ] All methods properly use *args and/or **kwargs
- [ ] Main program tests all functions and methods
- [ ] Comments explain what *args and **kwargs do in each function
- [ ] Program runs without errors
- [ ] Output is clear and well-formatted

---

## 🎓 Key Learning Objectives

By completing this assignment, you'll master:

1. **`*args`**: Accepting variable numbers of positional arguments
2. **`**kwargs`**: Accepting variable numbers of keyword arguments
3. **Combining Both**: Using them together in the correct order
4. **Unpacking**: Using `*` and `**` to unpack collections
5. **Flexibility**: Writing functions that adapt to different inputs
6. **Dictionaries and Tuples**: Understanding how kwargs and args work internally
7. **Default Parameters**: Combining with *args and **kwargs
8. **Practical Applications**: Building real-world flexible APIs

---

## 📚 Quick Reference

### Syntax Summary
```python
# Only *args
def func1(*args):
    pass

# Only **kwargs
def func2(**kwargs):
    pass

# Both (order matters!)
def func3(*args, **kwargs):
    pass

# With regular parameters (order matters!)
def func4(required, *args, optional=default, **kwargs):
    pass
```

### When to Use What
- Use **`*args`** when: Number of positional arguments varies
- Use **`**kwargs`** when: You want named/optional parameters
- Use **both** when: Maximum flexibility needed
- Use **neither** when: Fixed number of parameters works fine

---

Good luck with your Restaurant Order System! 🍔🍕✨