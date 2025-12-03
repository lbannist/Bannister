# Python Decorators Assignment Guide

## 🎯 Introduction: Understanding Closures and Decorators

Welcome to your Decorators assignment! Before we dive into decorators, you need to understand **closures**—a concept that makes decorators possible.

### What is a Closure?

A **closure** is when an inner function "remembers" variables from its outer function, even after the outer function has finished running.

**Think of it like this:**
- Imagine you write a secret message in a locked box
- You give the box to your friend
- Even though you're not there anymore, your friend can still open the box and read your message
- The box (inner function) "remembers" the message (variable) you put in it

```python
def outer_func():
    message = 'Hi'  # This variable...
    
    def inner_func():
        print(message)  # ...is remembered here!
    
    return inner_func

my_func = outer_func()  # outer_func finishes, but...
my_func()  # ...inner_func still remembers 'message'!
# Output: Hi
```

### Why Closures Matter

Closures let inner functions access variables from their enclosing scope. This is the foundation for decorators!

### What is a Decorator?

A **decorator** is a way to modify or enhance a function's behavior **without changing its source code**. It's like adding features to your phone with a case—the phone stays the same, but you add functionality around it.

**Common uses for decorators:**
- Logging when functions run
- Timing how long functions take
- Checking if a user is authorized
- Validating input data
- Caching results

---

## 📋 Assignment Overview

Create a **Game Achievement System** that uses closures and decorators to track player actions, timing, and achievements.

**File name:** `[YourName]_Decorators.py`

---

## 🏗️ Part 1: Understanding Closures

### Basic Closure (No Parameters)

```python
def create_greeting():
    """
    FUNCTION - Demonstrates basic closure
    The inner function remembers 'message' even after outer function finishes
    """
    message = "Welcome, Player!"
    
    def greet():
        print(message)  # Accesses variable from outer scope
    
    return greet

# Usage:
my_greeting = create_greeting()  # my_greeting is now the inner function
print(my_greeting.__name__)  # Output: greet
my_greeting()  # Output: Welcome, Player!
```

### Task 1.1: Create score_tracker() Closure

```python
def score_tracker(player_name):
    """
    FUNCTION - Creates a closure that tracks a player's score
    
    Parameters:
        player_name (str): The player's name
    
    Returns:
        inner function that adds points and prints current score
    
    Example:
        player1 = score_tracker("Alice")
        player1(10)  # "Alice earned 10 points! Total: 10"
        player1(5)   # "Alice earned 5 points! Total: 15"
    """
    total_score = 0  # This variable is "closed over"
    
    def add_points(points):
        nonlocal total_score  # Allows modifying outer scope variable
        # YOUR CODE HERE
        pass
    
    return add_points
```

**Requirements:**
- Create a closure that remembers the player's name and total score
- The inner function should accept points to add
- Print: `"[player_name] earned [points] points! Total: [total_score]"`
- Use `nonlocal` keyword to modify total_score

### Task 1.2: Create level_system() Closure

```python
def level_system(starting_level=1):
    """
    FUNCTION - Creates a closure that manages player levels
    
    Parameters:
        starting_level (int): Initial level (default 1)
    
    Returns:
        inner function that levels up and displays current level
    
    Example:
        player_level = level_system(5)
        player_level()  # "Level Up! Now at level 6"
        player_level()  # "Level Up! Now at level 7"
    """
    # YOUR CODE HERE
    pass
```

**Requirements:**
- Inner function increments level by 1 each time it's called
- Print: `"Level Up! Now at level [current_level]"`
- Remember the level between function calls

---

## 🏗️ Part 2: Basic Decorators

### Understanding Decorator Syntax

A decorator wraps a function to add functionality:

```python
def my_decorator(original_func):
    """Decorator that adds behavior before/after original function"""
    
    def wrapper_func():
        print("Before the function runs")
        original_func()  # Run the original function
        print("After the function runs")
    
    return wrapper_func

# Method 1: Manual decoration
def display():
    print("Function is running")

decorated_display = my_decorator(display)
decorated_display()

# Method 2: Using @ syntax (preferred)
@my_decorator
def display():
    print("Function is running")

display()  # Automatically decorated!
```

**Output:**
```
Before the function runs
Function is running
After the function runs
```

### Task 2.1: Create @announce Decorator

```python
def announce(original_func):
    """
    DECORATOR - Announces when a game action happens
    
    Prints a message before and after the function runs
    
    Example:
        @announce
        def jump():
            print("Player jumps!")
        
        jump()
        # Output:
        # ===== ACTION START =====
        # Player jumps!
        # ===== ACTION COMPLETE =====
    """
    def wrapper_func():
        print("===== ACTION START =====")
        # YOUR CODE HERE
        pass
    
    return wrapper_func
```

**Requirements:**
- Print `"===== ACTION START ======"` before function runs
- Execute the original function
- Print `"===== ACTION COMPLETE ======"` after function runs

### Task 2.2: Create @track_calls Decorator

```python
def track_calls(original_func):
    """
    DECORATOR - Counts how many times a function is called
    
    Example:
        @track_calls
        def attack():
            print("Player attacks!")
        
        attack()  # "Call #1 to attack"
        attack()  # "Call #2 to attack"
        attack()  # "Call #3 to attack"
    """
    count = 0  # Closure variable to track calls
    
    def wrapper_func():
        nonlocal count
        count += 1
        print(f"Call #{count} to {original_func.__name__}")
        # YOUR CODE HERE
        pass
    
    return wrapper_func
```

**Requirements:**
- Track number of times function is called
- Print: `"Call #[count] to [function_name]"`
- Execute the original function
- Remember count between calls (closure!)

---

## 🏗️ Part 3: Decorators with Parameters

### The Challenge with Parameters

When the decorated function has parameters, the wrapper must accept them too:

```python
def my_decorator(original_func):
    def wrapper_func(*args, **kwargs):  # Accept any arguments
        print("Before function")
        result = original_func(*args, **kwargs)  # Pass them along
        print("After function")
        return result
    
    return wrapper_func

@my_decorator
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet("Alice")  # Works!
greet("Bob", greeting="Hi")  # Also works!
```

### Task 3.1: Create @log_action Decorator

```python
def log_action(original_func):
    """
    DECORATOR - Logs game actions with their arguments
    
    Example:
        @log_action
        def collect_item(item_name, quantity):
            print(f"Collected {quantity} {item_name}(s)")
        
        collect_item("gold coin", 5)
        # Output:
        # [LOG] Calling collect_item with args: ('gold coin', 5), kwargs: {}
        # Collected 5 gold coin(s)
        # [LOG] collect_item completed
    """
    def wrapper_func(*args, **kwargs):
        print(f"[LOG] Calling {original_func.__name__} with args: {args}, kwargs: {kwargs}")
        # YOUR CODE HERE
        pass
    
    return wrapper_func
```

**Requirements:**
- Print log message with function name, args, and kwargs before running
- Execute original function with all arguments
- Print completion message after
- Return the result of the original function

### Task 3.2: Create @validate_positive Decorator

```python
def validate_positive(original_func):
    """
    DECORATOR - Ensures all numeric arguments are positive
    
    Example:
        @validate_positive
        def add_health(amount):
            print(f"Added {amount} health")
        
        add_health(10)   # Works: "Added 10 health"
        add_health(-5)   # Error: "Error: All arguments must be positive numbers"
    """
    def wrapper_func(*args, **kwargs):
        # Check if all numeric args are positive
        for arg in args:
            if isinstance(arg, (int, float)) and arg <= 0:
                print("Error: All arguments must be positive numbers")
                return None
        
        # YOUR CODE HERE - also check kwargs
        pass
    
    return wrapper_func
```

**Requirements:**
- Check all arguments (both args and kwargs) that are numbers
- If any number is ≤ 0, print error and return None
- If all valid, execute original function

---

## 🏗️ Part 4: Class-Based Decorators

### Why Use Classes for Decorators?

Sometimes decorators need to maintain state or have complex behavior. Classes make this easier.

```python
class CountCalls:
    """Class-based decorator to count function calls"""
    
    def __init__(self, original_func):
        self.original_func = original_func
        self.count = 0
    
    def __call__(self, *args, **kwargs):
        """This method runs when the decorated function is called"""
        self.count += 1
        print(f"Call {self.count} to {self.original_func.__name__}")
        return self.original_func(*args, **kwargs)

@CountCalls
def jump():
    print("Player jumps!")

jump()  # Call 1 to jump
jump()  # Call 2 to jump
```

### Task 4.1: Create TimerDecorator Class

```python
import time

class TimerDecorator:
    """
    CLASS DECORATOR - Times how long a function takes to execute
    
    Example:
        @TimerDecorator
        def load_level():
            time.sleep(0.1)  # Simulate loading
            print("Level loaded!")
        
        load_level()
        # Output:
        # Level loaded!
        # [TIMER] load_level took 0.1001 seconds
    """
    
    def __init__(self, original_func):
        """Store the original function"""
        # YOUR CODE HERE
        pass
    
    def __call__(self, *args, **kwargs):
        """Execute with timing"""
        # YOUR CODE HERE
        # Hint: Use time.time() before and after function call
        pass
```

**Requirements:**
- Store original function in `__init__`
- In `__call__`, record start time using `time.time()`
- Execute original function
- Record end time and calculate duration
- Print: `"[TIMER] [function_name] took [duration] seconds"`
- Return result of original function

### Task 4.2: Create AchievementTracker Class

```python
class AchievementTracker:
    """
    CLASS DECORATOR - Tracks achievements and unlocks them after certain calls
    
    Example:
        @AchievementTracker(milestone=3, achievement="Hat Trick")
        def score_goal():
            print("GOAL!")
        
        score_goal()  # GOAL!
        score_goal()  # GOAL!
        score_goal()  # GOAL! + "🏆 Achievement Unlocked: Hat Trick"
    """
    
    def __init__(self, milestone, achievement):
        """
        Store the milestone and achievement name
        Note: original_func is NOT passed here!
        """
        self.milestone = milestone
        self.achievement = achievement
        self.count = 0
    
    def __call__(self, original_func):
        """
        This is called when @AchievementTracker(args) decorates a function
        Returns the actual wrapper
        """
        def wrapper(*args, **kwargs):
            self.count += 1
            result = original_func(*args, **kwargs)
            
            # YOUR CODE HERE
            # Check if count == milestone, print achievement
            
            return result
        
        return wrapper
```

**Requirements:**
- Accept milestone number and achievement name in `__init__`
- Track how many times function is called
- When count reaches milestone, print: `"🏆 Achievement Unlocked: [achievement_name]"`
- Note: This is a decorator WITH parameters (different pattern!)

---

## 🏗️ Part 5: Chained Decorators

### Stacking Multiple Decorators

You can apply multiple decorators to one function. **Order matters!**

```python
@decorator1
@decorator2
@decorator3
def my_func():
    pass

# Equivalent to:
my_func = decorator1(decorator2(decorator3(my_func)))
# Bottom decorator wraps first, top decorator wraps last
```

### Task 5.1: Create @requires_permission Decorator

```python
def requires_permission(permission_level):
    """
    DECORATOR FACTORY - Checks if player has required permission
    
    Example:
        current_permission = 5  # Global variable
        
        @requires_permission(3)
        def enter_area():
            print("Entering restricted area")
        
        enter_area()  # If current_permission >= 3, works
                      # Otherwise: "Access Denied! Requires level 3 permission"
    """
    def decorator(original_func):
        def wrapper(*args, **kwargs):
            # YOUR CODE HERE
            # Check global variable 'current_permission'
            # Compare to permission_level
            pass
        
        return wrapper
    return decorator
```

**Requirements:**
- Check if `current_permission` (global variable) >= `permission_level`
- If yes: execute function
- If no: print `"Access Denied! Requires level [permission_level] permission"`

### Task 5.2: Demonstrate Chained Decorators

```python
# Create a function with multiple decorators stacked

@TimerDecorator
@log_action
@announce
def boss_battle(boss_name, difficulty):
    """
    Function with 3 decorators chained
    
    This should:
    1. Time the function (TimerDecorator)
    2. Log the action (log_action)
    3. Announce start/complete (announce)
    4. Execute the actual battle
    """
    print(f"Fighting {boss_name} on {difficulty} difficulty!")
    time.sleep(0.5)  # Simulate battle
    print(f"Defeated {boss_name}!")

# Test it:
boss_battle("Dragon", "Hard")
```

**Requirements:**
- Stack at least 3 decorators on one function
- Observe the order of execution
- Comment explaining which decorator runs first/last

---

## 🏗️ Part 6: Main Program

```python
# Global permission level for Task 5.1
current_permission = 5


def main():
    """Main program demonstrating all decorator concepts"""
    
    print("=== PART 1: Closures ===\n")
    
    # Test score_tracker
    player1 = score_tracker("Alice")
    player1(10)
    player1(5)
    player1(3)
    
    print()
    
    # Test level_system
    level_up = level_system(1)
    level_up()
    level_up()
    level_up()
    
    print("\n=== PART 2: Basic Decorators ===\n")
    
    @announce
    def jump():
        print("Player jumps!")
    
    jump()
    print()
    
    @track_calls
    def attack():
        print("Player attacks!")
    
    attack()
    attack()
    attack()
    
    print("\n=== PART 3: Decorators with Parameters ===\n")
    
    @log_action
    def collect_item(item_name, quantity):
        print(f"Collected {quantity} {item_name}(s)")
    
    collect_item("gold coin", 5)
    collect_item("health potion", 3)
    
    print()
    
    @validate_positive
    def add_health(amount):
        print(f"Added {amount} health")
    
    add_health(10)
    add_health(-5)  # Should show error
    
    print("\n=== PART 4: Class-Based Decorators ===\n")
    
    @TimerDecorator
    def load_level():
        time.sleep(0.1)
        print("Level loaded!")
    
    load_level()
    
    print()
    
    @AchievementTracker(milestone=3, achievement="Triple Threat")
    def score_goal():
        print("GOAL!")
    
    score_goal()
    score_goal()
    score_goal()  # Achievement unlocks here
    
    print("\n=== PART 5: Chained Decorators ===\n")
    
    @requires_permission(3)
    def enter_vault():
        print("Entering vault...")
    
    enter_vault()  # Should work (current_permission = 5)
    
    print()
    
    # Test boss battle with chained decorators
    boss_battle("Dragon", "Hard")
    
    print("\n=== PART 6: Permission System ===\n")
    
    global current_permission
    current_permission = 2  # Lower permission
    
    @requires_permission(5)
    def admin_area():
        print("Welcome to admin area")
    
    admin_area()  # Should be denied


if __name__ == "__main__":
    main()
```

---

## ✅ Requirements Checklist

### Part 1: Closures (15%)
- [ ] `score_tracker()` - closure that remembers player name and score
- [ ] `level_system()` - closure that remembers and increments level
- [ ] Both use `nonlocal` keyword correctly

### Part 2: Basic Decorators (20%)
- [ ] `@announce` - prints before/after messages
- [ ] `@track_calls` - counts function calls using closure
- [ ] Both return wrapper function

### Part 3: Decorators with Parameters (20%)
- [ ] `@log_action` - logs function calls with arguments
- [ ] `@validate_positive` - validates numeric arguments
- [ ] Both use `*args` and `**kwargs`
- [ ] Both return result of original function

### Part 4: Class-Based Decorators (20%)
- [ ] `TimerDecorator` - class decorator that times execution
- [ ] `AchievementTracker` - class decorator with parameters
- [ ] Both use `__init__` and `__call__` dunders
- [ ] TimerDecorator uses `import time` inside class

### Part 5: Chained Decorators (15%)
- [ ] `@requires_permission` - decorator factory with parameter
- [ ] `boss_battle()` - function with 3+ stacked decorators
- [ ] Comment explaining decorator execution order

### Part 6: Main Program (10%)
- [ ] Tests all closures and decorators
- [ ] Demonstrates various use cases
- [ ] Clean, formatted output
- [ ] Comments explain what's being tested

---

## 💡 Understanding Key Concepts

### Concept 1: Closures Remember Variables

```python
def outer():
    count = 0  # This variable...
    
    def inner():
        nonlocal count  # ...is remembered here
        count += 1
        return count
    
    return inner

counter = outer()
print(counter())  # 1
print(counter())  # 2
print(counter())  # 3 - still remembers!
```

### Concept 2: Decorators Are Just Functions

```python
# These are equivalent:
@my_decorator
def func():
    pass

# Same as:
def func():
    pass
func = my_decorator(func)
```

### Concept 3: Decorator with Parameters (Decorator Factory)

```python
# Without parameters:
@decorator
def func():
    pass

# With parameters:
@decorator(param1, param2)
def func():
    pass

# The second one needs an extra layer:
def decorator(param1, param2):  # Accepts parameters
    def actual_decorator(func):  # Accepts function
        def wrapper(*args, **kwargs):  # Accepts function's args
            # Use param1, param2, and call func
            pass
        return wrapper
    return actual_decorator
```

### Concept 4: Order of Chained Decorators

```python
@decorator_a
@decorator_b
def func():
    pass

# Execution order:
# 1. decorator_b wraps func first (inner)
# 2. decorator_a wraps the result (outer)
# When called: decorator_a → decorator_b → func
```

---

## 🧪 Testing Your Program

### Test 1: Closure Memory
```python
# Create two independent closures
player1 = score_tracker("Alice")
player2 = score_tracker("Bob")

player1(10)  # Alice: 10
player2(5)   # Bob: 5
player1(5)   # Alice: 15 (remembered previous!)
player2(3)   # Bob: 8 (independent from Alice!)
```

### Test 2: Decorator Stacking Order
```python
@announce  # Runs LAST (outermost)
@log_action  # Runs SECOND
@track_calls  # Runs FIRST (innermost)
def test():
    print("Function runs")

# When test() is called:
# 1. announce prints "ACTION START"
# 2. log_action prints logging info
# 3. track_calls prints call count
# 4. test() executes
# 5. track_calls completes
# 6. log_action completes  
# 7. announce prints "ACTION COMPLETE"
```

### Test 3: Class Decorator State
```python
@TimerDecorator
def slow_func():
    time.sleep(1)

@TimerDecorator
def fast_func():
    time.sleep(0.1)

# Each decorated function has its OWN timer instance
slow_func()  # Times this independently
fast_func()  # Times this independently
```

---

## 📊 Expected Output Example

```
=== PART 1: Closures ===

Alice earned 10 points! Total: 10
Alice earned 5 points! Total: 15
Alice earned 3 points! Total: 18

Level Up! Now at level 2
Level Up! Now at level 3
Level Up! Now at level 4

=== PART 2: Basic Decorators ===

===== ACTION START =====
Player jumps!
===== ACTION COMPLETE =====

Call #1 to attack
Player attacks!
Call #2 to attack
Player attacks!
Call #3 to attack
Player attacks!

=== PART 3: Decorators with Parameters ===

[LOG] Calling collect_item with args: ('gold coin', 5), kwargs: {}
Collected 5 gold coin(s)
[LOG] collect_item completed
[LOG] Calling collect_item with args: ('health potion', 3), kwargs: {}
Collected 3 health potion(s)
[LOG] collect_item completed

Added 10 health
Error: All arguments must be positive numbers

=== PART 4: Class-Based Decorators ===

Level loaded!
[TIMER] load_level took 0.1001 seconds

GOAL!
GOAL!
GOAL!
🏆 Achievement Unlocked: Triple Threat

=== PART 5: Chained Decorators ===

Entering vault...

===== ACTION START =====
[LOG] Calling boss_battle with args: ('Dragon', 'Hard'), kwargs: {}
Fighting Dragon on Hard difficulty!
Defeated Dragon!
[LOG] boss_battle completed
===== ACTION COMPLETE =====
[TIMER] boss_battle took 0.5002 seconds

=== PART 6: Permission System ===

Access Denied! Requires level 5 permission
```

---

## ⚠️ Common Mistakes to Avoid

### Mistake 1: Forgetting to Return Wrapper
```python
# ❌ WRONG
def my_decorator(func):
    def wrapper():
        func()
    # Missing return!

# ✅ CORRECT
def my_decorator(func):
    def wrapper():
        func()
    return wrapper  # Must return wrapper!
```

### Mistake 2: Not Using *args, **kwargs
```python
# ❌ WRONG - Only works for functions with no parameters
def decorator(func):
    def wrapper():
        return func()
    return wrapper

# ✅ CORRECT - Works for any function
def decorator(func):
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    return wrapper
```

### Mistake 3: Forgetting nonlocal
```python
# ❌ WRONG - Creates new local variable
def counter():
    count = 0
    def increment():
        count = count + 1  # Error! count referenced before assignment
    return increment

# ✅ CORRECT
def counter():
    count = 0
    def increment():
        nonlocal count  # Modifies outer count
        count += 1
    return increment
```

### Mistake 4: Wrong Order for Decorator Factory
```python
# ❌ WRONG
def decorator(func):  # Missing parameter layer
    def wrapper(param):
        # Can't access param here!
        return func()
    return wrapper

# ✅ CORRECT - Decorator factory
def decorator(param):  # Accept parameter
    def actual_decorator(func):  # Accept function
        def wrapper(*args, **kwargs):  # Accept function's args
            # Can use param here!
            return func(*args, **kwargs)
        return wrapper
    return actual_decorator
```

---

## 🚀 Extension Challenges (Optional)

### Challenge 1: Retry Decorator
Create a decorator that retries a function if it fails:
```python
@retry(max_attempts=3)
def unstable_network_call():
    # Might fail, will retry up to 3 times
    pass
```

### Challenge 2: Cache Decorator
Create a decorator that caches function results:
```python
@cache
def expensive_calculation(n):
    # Result is cached, only calculated once per input
    pass
```

### Challenge 3: Rate Limiter
Create a decorator that limits how often a function can be called:
```python
@rate_limit(calls_per_second=2)
def api_call():
    # Can only be called twice per second
    pass
```

---

## 📝 Submission Checklist

Before submitting, verify:
- [ ] File named: `[YourName]_Decorators.py`
- [ ] All closures use `nonlocal` correctly
- [ ] All decorators return wrapper functions
- [ ] Decorators with parameters use decorator factory pattern
- [ ] Class decorators use `__init__` and `__call__`
- [ ] `TimerDecorator` includes `import time` at top of file
- [ ] Chained decorators demonstrate execution order
- [ ] Main program tests all features
- [ ] Comments explain decorator concepts
- [ ] Output is clear and well-formatted

---

## 🎓 Key Learning Objectives

By completing this assignment, you'll master:

1. **Closures**: Inner functions that remember outer variables
2. **`nonlocal` Keyword**: Modifying variables from outer scope
3. **Basic Decorators**: Wrapping functions to add functionality
4. **`@` Syntax**: Clean decorator application
5. **`*args, **kwargs`**: Handling any function signature
6. **Decorator Factories**: Decorators that accept parameters
7. **Class Decorators**: Using classes instead of functions
8. **Chained Decorators**: Stacking multiple decorators
9. **Practical Applications**: Logging, timing, validation, permissions

---

## 📚 Quick Reference

### Closure Pattern
```python
def outer(param):
    variable = param
    
    def inner():
        nonlocal variable  # If modifying
        # Use variable here
        pass
    
    return inner
```

### Basic Decorator Pattern
```python
def decorator(func):
    def wrapper(*args, **kwargs):
        # Before function
        result = func(*args, **kwargs)
        # After function
        return result
    return wrapper
```

### Decorator Factory Pattern
```python
def decorator_with_params(param):
    def decorator(func):
        def wrapper(*args, **kwargs):
            # Use param and call func
            return func(*args, **kwargs)
        return wrapper
    return decorator
```

### Class Decorator Pattern
```python
class Decorator:
    def __init__(self, func):
        self.func = func
    
    def __call__(self, *args, **kwargs):
        # Decorator logic
        return self.func(*args, **kwargs)
```

---

Good luck with your Game Achievement System! 🎮🏆✨