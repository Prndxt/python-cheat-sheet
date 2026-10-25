# Functions

A function is a reusable block of code. **Define** it once with `def`, then **call** it as often as you like.

## Defining and calling a function

> Python has no built-in `average()` function, so we can write our own:

```python
def average(a, b, c):              # define: a, b, c are parameters
    """
    Calculate the average of 3 numbers.
    """                            # this text is the docstring
    return (a + b + c) / 3         # return sends the result back

help(average)                      # shows the function name and its docstring

result = average(20, 30, 40)       # call: 20, 30, 40 are arguments
print(result)                      # 30.0
```

| Term | Meaning |
|---|---|
| `def` | Keyword that starts a function definition |
| Parameter | The name in the definition, e.g. `a` in `def average(a, b, c)` |
| Argument | The actual value passed in the call, e.g. `20` in `average(20, 30, 40)` |
| Docstring | Text in triple quotes right below `def`; describes what the function does |
| `return` | Sends a value back to where the function was called |

---

## Default values

A parameter can have a default value. If no argument is passed for it, the default is used.

```python
def add(a=0, b=0, c=0):
    return a + b + c

result = add(20, 30)      # no value for c, so c = 0
print(result)             # 50
```

> **Rule:** parameters **with** a default value must come **after** parameters **without** one. Python fills parameters from left to right, so a parameter without a default can't come after one that has a default.

```python
def my_func1(var1="Hello", var2):       # wrong: SyntaxError
def my_func2(var1, var2="Hello"):       # correct
def my_func3(var1, var2=35):            # correct
def my_func4(var1=35, var2):            # wrong: SyntaxError
def my_func5(var1=35, var2="Hello"):    # correct (both have defaults)
def my_func6(var1, var2):               # correct (no defaults)

# Summary: parameters with default values always go at the end.
```

---

## Positional and keyword arguments

```python
def introduce(name, age, city):
    print(f"{name} is {age} years old and lives in {city}.")

# Positional: values must be in the same order as the parameters
introduce("Max", 30, "Berlin")

# Keyword: name the parameter, then the order doesn't matter
introduce(age=27, name="Tom", city="Berlin")

# Mixed: positional first, then keyword
introduce("Jack", city="Berlin", age=25)

# Wrong: a positional argument after a keyword argument
introduce(name="Anna", 25, "Berlin")
# SyntaxError: positional argument follows keyword argument
```

> **Rule:** positional arguments must come **before** keyword arguments. Once you use a keyword argument, every argument after it must also be a keyword argument.

---

## `return` vs `print`

```python
# With return: the value comes back and can be saved
def greeting(name, course):
    return f"Hi {name}, from the {course} course"

result = greeting("Alex", "Python")
print(result)            # Hi Alex, from the Python course


# With print: the value is only shown on screen
def greeting(name, course):
    print(f"Hi {name}, from the {course} course")

greeting("Alex", "Python")    # Hi Alex, from the Python course

result = greeting("Alex", "Python")   # still prints the text...
print(result)                        # ...but result is None (nothing was returned)
```

| | `return` | `print` |
|---|---|---|
| What it does | Gives the value back so you can save or reuse it | Only shows the value on screen |
| Saved in a variable | The returned value | `None` |
| Use when | The result is needed later in the code | You only want to display something |

> Note: `return` works a bit like `break` in a loop. As soon as Python reaches `return`, it leaves the function immediately; any code after it in the function is not run.

---

## Variable scope

A variable created **inside** a function is **local**: it exists only while the function runs and can't be used outside of it. A variable with the same name outside the function is a separate variable.

```python
x = "outside"

def my_function():
    x = "inside"          # local variable, a different x
    print(x)              # inside

my_function()
print(x)                  # outside (unchanged)
```

| Where it is created | Name | Can be used |
|---|---|---|
| Inside a function | Local variable | Only inside that function |
| Outside, at the top level | Global variable | Everywhere (can be read inside functions) |

```python
def my_function():
    y = 5

my_function()
print(y)                  # NameError: name 'y' is not defined
```

> **Note:** changing a variable outside the function doesn't affect a local variable with the same name. Every time the function is called, its local variable starts again with the value set inside the function.

```python
y = 100

def my_function():
    y = 5                 # local y, always starts as 5
    print(y)

y = 200                   # changes only the outside y
my_function()             # 5    (the inside y is not affected)
print(y)                  # 200
```

> Parameters are local too: `a`, `b` and `c` in `def average(a, b, c)` exist only inside the function.

---

## Review example

Two functions working together on a list of dictionaries:

```python
def calculate_average(scores):
    """
    Calculate the average of a list of scores.
    """
    return sum(scores) / len(scores)

def get_grade(average):
    """
    Return the letter grade for an average score.
    """
    if average >= 90:
        return "A"
    elif average >= 80:
        return "B"
    elif average >= 70:
        return "C"
    elif average >= 60:
        return "D"
    else:
        return "F"

students = [                                    # a list of dictionaries
    {"name": "Max",  "score": [95, 85, 90]},
    {"name": "Tom",  "score": [90, 99, 95]},
    {"name": "Jack", "score": [60, 40, 100]},
]

for student in students:
    average = calculate_average(student["score"])
    grade = get_grade(average)
    print(f"{student['name']} has an average score of {average:.2f} and a grade of {grade}")

# Max has an average score of 90.00 and a grade of A
# Tom has an average score of 94.67 and a grade of A
# Jack has an average score of 66.67 and a grade of D
```

> `{average:.2f}` formats the number with 2 decimal places.

---

## Importing functions (modules)

> Every Python file is a **module**. Put your functions in one file, then `import` that file in another one (e.g. `main.py`). Both files must be in the same folder.

> To run it from the terminal (inside that folder): `python3 main.py`

**File 1: `my_math.py`** (the functions)

```python
def add(a, b):
    return a + b

def average(a, b, c):
    return (a + b + c) / 3
```

**File 2: `main.py`** (uses the functions)

```python
import my_math

print(my_math.add(2, 3))              # 5
print(my_math.average(20, 30, 40))    # 30.0
```

| Import style | Code | How to call |
|---|---|---|
| Whole file | `import my_math` | `my_math.add(2, 3)` |
| Whole file with a short name | `import my_math as mm` | `mm.add(2, 3)` |
| Only certain functions | `from my_math import add, average` | `add(2, 3)` |

**Common mistakes:**
- Write the file name **without** `.py` in the import: `import my_math`, not `import my_math.py`.
- `ModuleNotFoundError` means Python can't find the file: check the spelling and that both files are in the same folder.
- In a Jupyter notebook, the `.py` file must be in the same folder as the notebook.
