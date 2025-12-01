

# AMCS1034 Software Development Fundamentals - Course Notes

## Chapter 1: Software Development Fundamentals

### Computing Disciplines
- The Association for Computing Machinery (ACM) defines five major computing disciplines:
  1. **Computer Engineering (CE)**: Focuses on hardware-software integration
  2. **Computer Science (CS)**: Focuses on theory, algorithms, and computation
  3. **Information Systems (IS)**: Focuses on information generation and use
  4. **Information Technology (IT)**: Focuses on infrastructure and reliability
  5. **Software Engineering (SE)**: Focuses on creating robust software

### Algorithms
- An algorithm is a finite sequence of well-defined instructions that solves a problem
- Features of algorithms:
  - Finite number of instructions
  - Each instruction is well-defined
  - Eventually halts with a solution
  - Solves a general class of problems

### Information Processing
- Data vs. Information:
  - Data: Raw, unorganized facts
  - Information: Processed, organized data presented in context
- IPO Model (Input-Process-Output):
  - Input: Raw data
  - Process: Transformation using algorithms
  - Output: Information

### Software Development Life Cycle (SDLC)
- Stages of SDLC:
  1. Planning: Estimate resources, cost, and size
  2. Requirement Gathering: Collect detailed requirements from client
  3. Analysis: Analyze requirements and clarify specifications
  4. Design: Create software architecture and approach
  5. Development: Translate design into code (longest phase)
  6. Testing: Verify software works as expected
  7. Deployment: Release product to client
  8. Maintenance: Ongoing support and updates

### SDLC Models
- Waterfall Model: Sequential flow from one phase to the next
- Prototype Model: Creates working model early for feedback
- Incremental Model: Develops and delivers in parts

### Python Programming
- Why Python?
  1. Popularity: Consistently ranked in top programming languages
  2. Continuous Support: Large community of volunteer developers
  3. Code Readability: Clean, simple syntax
  4. Simpler Code: Express concepts in fewer lines
  5. Flexibility: Used by major companies (Google, NASA, Facebook)
  6. Free and Open Source: Available at no cost
  7. Extensive Libraries: Rich collection of modules

---

## Chapter 2B: Problem Solving with Flowchart

### Solution Design vs. Coding
- Solution design precedes coding in the SDLC
- Importance of early design:
  - Reduces costs of fixing errors
  - Mistakes found earlier are cheaper to correct

### Flowchart
- Visual representation of an algorithm or workflow
- Common flowchart symbols:
  - Start/End: Oval shapes
  - Input/Output: Parallelograms
  - Process: Rectangles
  - Connector: Circles

### Control Structures
1. **Sequence**: Instructions executed one after another
2. **Selection**: Decision-making between alternatives
3. **Loop**: Repetition of instructions

### Problem-Solving Examples
- Temperature conversion: Celsius to Fahrenheit
- Finding highest and second-highest scores from a list

---

## Chapter 3A: Selection

### Boolean Types and Values
- Boolean data type has two values: True and False
- Internally represented as 1 (True) and 0 (False)

### Relational Operators
- Comparison operators:
  - `==` (equal)
  - `!=` (not equal)
  - `>` (greater than)
  - `<` (less than)
  - `>=` (greater than or equal)
  - `<=` (less than or equal)

### Selection Statements
1. **One-Way if**:
   ```python
   if condition:
       statement
   ```

2. **Two-Way if-else**:
   ```python
   if condition:
       statement1
   else:
       statement2
   ```

3. **Nested if**:
   ```python
   if condition1:
       if condition2:
           statement
   ```

4. **Multi-Way if-elif-else**:
   ```python
   if condition1:
       statement1
   elif condition2:
       statement2
   else:
       statement3
   ```

### Logical Operators
- `and`: True only if both operands are True
- `or`: True if at least one operand is True
- `not`: Negates the operand

### Switch Case (Python 3.10+)
```python
match variable:
    case value1 | value2:
        statement1
    case value3:
        statement2
    case _:
        default_statement
```

---

## Chapter 3B: Loop

### Loop Types
1. **Count-controlled loops**: Execute a predetermined number of times
2. **Event-controlled loops**: Continue until a condition changes

### For Loop
```python
for item in sequence:
    statement
```

- Range function:
  - `range(stop)`: 0 to stop-1
  - `range(start, stop)`: start to stop-1
  - `range(start, stop, step)`: start to stop-1 with increments

### While Loop
```python
while condition:
    statement
    update_statement
```

### Augmented Assignment Operators
- `+=`, `-=`, `*=`, `/=`, `%=`, etc.
- Example: `x += 1` is equivalent to `x = x + 1`

### Nested Loops
- Loops inside other loops
- Each iteration of outer loop triggers complete inner loop

### Break and Continue
- `break`: Exits the loop immediately
- `continue`: Skips the rest of current iteration

### Do-While Simulation
```python
while True:
    statement
    if exit_condition:
        break
```

---

## Chapter 4A: String Processing

### String Basics
- Sequence of characters enclosed in quotes
- No separate character type in Python
- Empty string: `""` or `''`

### String Operations
- Concatenation: `+` operator
- Repetition: `*` operator
- Length: `len(string)`
- Indexing: `string[index]`
- Slicing: `string[start:end:step]`

### String Methods
- `upper()`, `lower()`: Change case
- `strip()`: Remove whitespace
- `find()`, `replace()`: Search and replace
- `split()`: Split into list
- `join()`: Join list into string

### String Formatting
- Old style: `%` operator
  ```python
  "Value: %.2f" % value
  ```
- New style: `format()` method
  ```python
  "Value: {:.2f}".format(value)
  ```

### String Representation
- ASCII: American Standard Code for Information Interchange
- Unicode: Universal encoding for all languages
- UTF-8: Variable-length Unicode encoding

---

## Chapter 4B: Exception Handling

### Exception Types
- Errors that disrupt normal program flow
- Common exceptions:
  - `ZeroDivisionError`: Division by zero
  - `ValueError`: Invalid value
  - `IndexError`: Out-of-range index
  - `FileNotFoundError`: File doesn't exist

### Handling Exceptions
```python
try:
    # Code that might raise exception
except ExceptionType:
    # Handle specific exception
except (Exception1, Exception2):
    # Handle multiple exceptions
except:
    # Handle any exception
else:
    # Execute if no exception
finally:
    # Always execute
```

### Raising Exceptions
```python
raise ExceptionType("Error message")
```

---

## Chapter 4C: Text File Processing

### File Paths
- Windows: `C:\\Users\\User\\file.txt` or `r"C:\Users\User\file.txt"`
- Linux/Mac: `/home/user/file.txt`

### File Operations
```python
# Opening files
file = open("filename.txt", "mode")  # r, w, a, r+, etc.

# Reading
content = file.read()           # Entire file
line = file.readline()         # Single line
lines = file.readlines()        # List of lines

# Writing
file.write("text")             # String
file.writelines(list_of_strings) # List of strings

# Closing
file.close()
```

### Context Manager
```python
with open("filename.txt", "mode") as file:
    # File operations
    # Automatically closed after block
```

### File Manipulation
- `os.rename(old, new)`: Rename file
- `os.remove(file)`: Delete file
- `shutil.copy(src, dst)`: Copy file
- `shutil.move(src, dst)`: Move file

---

## Chapter 5A: Lists

### List Basics
- Ordered, mutable sequence of elements
- Created with square brackets: `list = [1, 2, 3]`
- Can contain mixed types: `[1, "two", 3.0]`

### List Operations
- Concatenation: `list1 + list2`
- Repetition: `list * n`
- Indexing: `list[index]`
- Slicing: `list[start:end:step]`
- Membership: `item in list`

### List Methods
- `append(item)`: Add to end
- `extend(list)`: Extend with list
- `insert(index, item)`: Insert at position
- `remove(item)`: Remove first occurrence
- `pop(index)`: Remove and return item
- `sort()`: Sort in place
- `reverse()`: Reverse in place

### List Comprehensions
```python
new_list = [expression for item in iterable if condition]
# Example: squares = [x**2 for x in range(10)]
```

### Copying Lists
- Assignment creates reference: `list2 = list1` (same object)
- Shallow copy: `list2 = list1.copy()` or `list1[:]`
- Deep copy: `import copy; list2 = copy.deepcopy(list1)`

---

## Chapter 5B: Tuples, Sets and Dictionaries

### Tuples
- Ordered, immutable sequence
- Created with parentheses: `tuple = (1, 2, 3)`
- Single element: `(1,)` (comma required)
- Unpacking: `a, b = (1, 2)`

### Sets
- Unordered collection of unique elements
- Created with braces: `set = {1, 2, 3}`
- Set operations:
  - Union: `set1 | set2` or `set1.union(set2)`
  - Intersection: `set1 & set2` or `set1.intersection(set2)`
  - Difference: `set1 - set2` or `set1.difference(set2)`
  - Symmetric difference: `set1 ^ set2` or `set1.symmetric_difference(set2)`

### Dictionaries
- Key-value pairs
- Created with braces: `dict = {"key": "value"}`
- Access: `dict["key"]` or `dict.get("key", default)`
- Methods:
  - `keys()`: Return keys
  - `values()`: Return values
  - `items()`: Return key-value pairs
  - `update(other_dict)`: Merge dictionaries

---

## Chapter 6: Functions

### Function Definition
```python
def function_name(parameters):
    """Docstring"""
    # Function body
    return value  # Optional
```

### Function Parameters
- Positional arguments: Match by position
- Keyword arguments: Match by name
- Default parameters: `def func(param=default_value)`
- Variable arguments: `*args` (tuple), `**kwargs` (dict)

### Return Values
- Single value: `return value`
- Multiple values: `return value1, value2` (returns tuple)
- No explicit return: Returns `None`

### Scope and Lifetime
- Local scope: Variables defined inside function
- Global scope: Variables defined outside all functions
- `global` keyword: Modify global variable inside function
- `nonlocal` keyword: Modify variable in enclosing function

### Anonymous Functions
```python
lambda arguments: expression
# Example: add = lambda x, y: x + y
```

### Function Abstraction
- Benefits:
  - Code reusability
  - Improved readability
  - Easier debugging
  - Modular design

### Stepwise Refinement
- Top-down design approach
- Break complex problems into smaller subproblems
- Implement functions gradually from general to specific