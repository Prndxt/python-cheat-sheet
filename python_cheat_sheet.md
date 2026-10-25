# Introduction to Python: Cheat Sheet

## Overview

* Python basics: variables, operators, commands
* Conditional statements
* `while` and `for` loops
* Lists, tuples, sets and dictionaries

---

# Python Basics

> **Open a Jupyter notebook in VS Code to practice!**
>
> A notebook has two types of cells:
>
> | Type | Details |
> |---|---|
> | **Markdown** | Text and notes. Run a cell to see how it is rendered. |
> | **Code** | Python code, for example `print("Hello World")` |

> **Terminal commands**
> 1. Go to the folder of the exercise.
> 2. Run `uv sync` to install the required libraries.
> 3. Run `code .` to open the folder in VS Code.

#### Stop, restart and clear outputs

Long-running Python processes can be interrupted.

> In VS Code notebooks, use the notebook **toolbar** to interrupt or restart the kernel, clear outputs, or run all cells.

> Restarting the kernel clears the current Python session. This is useful to check that the notebook still runs correctly from top to bottom.

> **Select Kernel (environment)** → Python Environments → choose the environment of your project.

Assume: `name = "Alex"`, `x = 5`

| Command | Definition | Example | Result |
|---|---|---|---|
| `print(x)` | Print the value of `x` | `print(x)` | `5` |
| `print(2 + 3)` | Print the result of a calculation | `print(2 + 3)` | `5` |
| `print("hi, " + name)` | Join texts and print them | `print("hi, " + name)` | `hi, Alex` |
| `!pwd` | Jupyter only: run the terminal command `pwd` | `!pwd` | path of the current folder |
| `type(x)` | Show the type of a value: `int`, `float`, `str`, `bool`, `complex`, `list`, `tuple`, `set`, etc. | `type(x)` | `<class 'int'>` |
| `int(x)` | Convert to a whole number (cuts off decimals) | `int("4")`, `int(4.3)` | `4`, `4` |
| `float(x)` | Convert to a decimal number | `float("2.5")` | `2.5` |
| `str(x)` | Convert to text | `str(5)` | `"5"` |
| `bool(x)` | Convert to `True` / `False` | `bool("")`, `bool("hi")` | `False`, `True` |
| `len(x)` | Length of a string, list, etc. | `len(name)` | `4` |
| `f"text {x}"` | Insert variable values into a string | `f"hi, {name}"` | `"hi, Alex"` |
| `input("prompt")` | Read user input (always returned as a string) | `input("Name: ")`, user types Alex | `"Alex"` |

> Note: `int("4.3")` gives a `ValueError`. Convert to float first: `int(float("4.3"))` → `4`.

---

## Variables

| Variable | Definition |
|---|---|
| Naming rules | - Use lowercase letters (names are case-sensitive) <br> - Use underscores instead of spaces <br> - Numbers are allowed, but a name can't start with one <br> - Don't use built-in names such as `list`, `dict` or `str` |
| `x = 5` | Assign the value `5` to the name `x` |
| `x: float = 3.5` | Type hint only, not enforced by Python |
| `x, y = 1, 2` | Assign several variables in one line |
| `x = 1; y = 2` | Two statements in one line, separated by `;` |
| `x = y = 0` | Assign the same value to several names |
| `c = complex(5, 6)` | Create a complex number; `c` is `(5+6j)` |

---

## Operators

| Operator | Definition | Example | Result |
|---|---|---|---|
| Style rule | Leave a space on both sides of an operator | `10 + 3` | `13` |
| `+` | Add | `10 + 3` | `13` |
| `-` | Subtract | `10 - 3` | `7` |
| `*` | Multiply | `10 * 3` | `30` |
| `/` | Divide (result is always a float) | `10 / 3` | `3.333...` |
| `//` | Floor division | `10 // 3` | `3` |
| `%` | Remainder (modulo) | `10 % 3` | `1` |
| `**` | Power | `10 ** 3` | `1000` |
| `and` `or` `not` | Logical | `3 < 5 and 5 < 10` | `True` |
| `==` `!=` | Equal / not equal | `3 == 3` | `True` |
| `<` `>` `<=` `>=` | Comparison | `5 >= 5` | `True` |
| `+=` `-=` `*=` `/=` | Augmented assignment | `x += 3` <br> `x -= y - 5` | same as `x = x + 3` <br> same as `x = x - (y - 5)` |

### Useful number functions

| Function | Definition | Example | Result |
|---|---|---|---|
| `abs()` | Absolute value | `abs(-2)` | `2` |
| `min()` | Smallest value | `min(-2, 3, 5)` | `-2` |
| `max()` | Largest value | `max(-2, 3, 5)` | `5` |
| `round(x, n)` | Round to `n` decimal places | `round(3.141592, 2)` <br> `round(3.141592, 4)` | `3.14` <br> `3.1416` |

> **Long expressions:** put the operator at the **start** of each line, not at the end, and wrap the whole expression in parentheses `( )` so Python knows it continues on the next line.

```python
income = (
    gross_wages
    + taxable_interest
    + (dividends - qualified_dividends)
    - ira_deduction
    - student_loan_interest
)
```

> Note: **some operators also work on strings.**

```python
x = "My first string" + " " + "My second string"   # no automatic space
y = ("Repeating string" + " ") * 3                   # repeats the text 3 times
```

---

## Strings

> Access individual characters by their **index**. Python starts counting at 0.

```python
my_str_variable = "Test String"

my_str_variable[0]        # T   first character
my_str_variable[1]        # e
my_str_variable[-1]       # g   negative indexes count from the end
my_str_variable[-3]       # i

my_str_variable[1:3]      # es        the end index (3) is not included
my_str_variable[-6:-1]    # Strin
my_str_variable[:-3]      # Test Str

my_str_variable[::2]      # Ts tig    every 2nd character
my_str_variable[2:10:3]   # sSi       from 2 to 9, in steps of 3
```

### String methods

> Put a dot `.` after a value or variable to call one of its methods, e.g. `text.upper()`.

Assume: `text = "  hi, python programmers. "` (two spaces at the start, one at the end)

| Command | Definition | Example | Result |
|---|---|---|---|
| `string_name.strip()` | Remove spaces at both ends | `text.strip()` | `"hi, python programmers."` |
| `string_name.lower()` | All lowercase | `text.lower()` | `"  hi, python programmers. "` (no change, already lowercase) |
| `string_name.upper()` | All uppercase | `text.upper()` | `"  HI, PYTHON PROGRAMMERS. "` |
| `string_name.capitalize()` | First character uppercase, the rest lowercase | `text.strip().capitalize()` | `"Hi, python programmers."` |
| `string_name.replace("x", "y")` | Replace every `"x"` with `"y"` | `text.replace("hi", "bye")` | `"  bye, python programmers. "` |
| `string_name.split(" ")` | Split at each single space into a list | `text.split(" ")` | `['', '', 'hi,', 'python', 'programmers.', '']` |
| `string_name.split()` | Split at any whitespace, ignoring extra spaces | `text.split()` | `['hi,', 'python', 'programmers.']` |

> Note: methods return a **new** string; `text` itself does not change. To keep the result, assign it: `text = text.strip()`.

> Note: you can chain several methods with dot notation, e.g. `text.strip().upper()`.

> Note: double quotes let you use `'` inside the text.

```python
z = "With double quotes, I can use contractions: can't, won't, didn't, don't, etc."
```

### String formatting

> Insert values into a text. All four styles below print the same result: `Hello Alex`.

```python
my_name = "Alex"         # string
my_age = 28              # integer
greeting_msg = "Hello"

print("Hello" + " " + my_name)       # 1. + operator
print("Hello %s" % my_name)          # 2. % sign
print("Hello {}".format(my_name))    # 3. format()
print(f"Hello {my_name}")            # 4. f-string
# Result of all four: Hello Alex

print("{}, Alex".format(greeting_msg))    # {} fills placeholders in order
print("{0}, Alex".format(greeting_msg))   # {0} picks the argument by position (starts at 0)
# Result of both: Hello, Alex

# With several values:
print("My name is {} and I am {} years old".format(my_name, my_age))
print(f"My name is {my_name} and I am {my_age} years old")
# Result of both: My name is Alex and I am 28 years old
```

| # | Style | How it works |
|---|---|---|
| 1 | `+` operator | Joins strings; add the spaces yourself. Numbers need `str()` first |
| 2 | `%` sign | `%` marks where the value goes, followed by a letter for the type: `%s` string, `%d` whole number |
| 3 | `.format()` | `{}` marks where the value goes; the values are passed to `format()` |
| 4 | f-string | Put the variable directly inside `{}` after an `f` (the modern way) |

#### More on `.format()`

| Placeholder | Definition | Example | Result |
|---|---|---|---|
| `{}` | Fill in order | `"{} {}".format("a", "b")` | `a b` |
| `{0}` `{1}` | Pick by position (starts at 0) | `"{1} {0}".format("a", "b")` | `b a` |
| `{name}` | Pick by keyword | `"{n}".format(n="Alex")` | `Alex` |

---

# Conditional Statements: `if`

If a condition is `True`, the indented block below it runs. If it is `False`, the block is skipped.

```python
age = 70

if age > 5 and age < 18:    # a colon : ends each condition line
    msg = "child"
elif age < 40:              # "else if"; use as many as you need
    msg = "included"
else:
    msg = "excluded"

print(msg)                  # excluded
```

| Keyword | Definition | Example |
|---|---|---|
| `if` | Runs the block if the condition is `True` | `if age < 18:` |
| `elif` | Checked only if all earlier conditions were `False` | `elif age < 40:` |
| `else` | Runs if no condition was `True`; has no condition itself | `else:` |
| `pass` | Placeholder for an empty block | `if x: pass` |

**Short form (one line):**

```python
msg = "included" if age < 40 else "excluded"

if x > 10: print(x)
```

**Common mistakes:**
- Don't forget the `:` at the end of the condition line.
- `=` assigns, `==` compares. `if age = 40:` gives a `SyntaxError`.
- Use `elif`, not `else if`.
- Use `and` / `or` / `not`, not `&&` / `||` / `!`.
- Misaligned indentation or mixing tabs and spaces gives an `IndentationError`.

---

# `while` and `for` Loops

Loops repeat a block of code. As with `if`, a colon `:` ends the first line, and the block below must be indented (4 spaces).

## `while` loop

Repeats the block **as long as** the condition is `True`. Use it when you repeat until something changes.

```python
count = 1
while count < 3:          # runs as long as this condition is True
    print(count)          # 1, 2
    count += 1            # without this line, the loop never ends

my_str = "HELLO"
print(len(my_str))        # 5, the length of the string

i = 0
while i < len(my_str):    # prints HELLO vertically, one letter per line
    print(my_str[i])
    i += 1
```

## `for` loop

Repeats the block once for **each item**. Use it when you know what to loop over or how many times.

```python
for i in range(1, 4):     # 1, 2, 3 (the stop value 4 is not included)
    print("round", i)

for i in range(3):        # 0, 1, 2
    print(i)

my_list = [5, 8, 10]
for number in my_list:    # each item in the list
    print(number)

for ch in "hi":           # each character: h, i
    print(ch)

shopping_list = ["apple", "banana", "cherry"]
for fruit in shopping_list:   # each item in the list
    print(fruit)
```

| Command | Definition | Example | Result |
|---|---|---|---|
| `range(5)` | 0 up to 4 | `list(range(5))` | `[0, 1, 2, 3, 4]` |
| `range(start, stop)` | `start` up to `stop - 1` | `list(range(1, 4))` | `[1, 2, 3]` |
| `range(start, stop, step)` | Jump by `step` | `list(range(0, 10, 3))` | `[0, 3, 6, 9]` |
| `range(5, 0, -1)` | Count down | `list(range(5, 0, -1))` | `[5, 4, 3, 2, 1]` |

**Common mistakes:**
- `range(1, 10)` stops at 9. For 1 to 10, use `range(1, 11)`.
- A `while` loop whose condition never becomes `False` runs forever. Stop it with Ctrl+C (in Jupyter: the stop button).
- There is no C++-style `for (i = 0; i < n; i++)`. Use `for i in range(n):`.
- There is no `i++`. Use `i += 1`.

## Loops with lists and strings

```python
names = ["Max", "Moritz", "Monika"]

print(names[0])      # Max
print(names[1])      # Moritz
print(names[:1])     # ['Max']   a list with only position 0 (1 is not included)
print(names[1:])     # ['Moritz', 'Monika']

for name in names:
    initial = name[:1]     # round 1: name = "Max" → initial = "M"
    print(initial)         # M, M, M

for name in names:         # nested loop: one loop inside another
    for n in name:
        print(n.upper())
# round 1: name = "Max",    n = "M"
# round 2: name = "Max",    n = "a"
# round 3: name = "Max",    n = "x"
# round 4: name = "Moritz", n = "M"
# round 5: name = "Moritz", n = "o"  ...

my_str = "HELLO"
print(range(len(my_str)))    # range(0, 5), useful for double-checking
for i in range(len(my_str)): # prints HELLO vertically
    print(my_str[i])

my_name = "Alex"             # print every second letter of a name
for i in range(0, len(my_name), 2):
    print(my_name[i])        # A, e
```

## Loop control: `pass` vs `continue` vs `break`

> All three are used inside loops but behave differently. Example: what happens when `i == 3`?

| Keyword | Code | Output | What happens |
|---|---|---|---|
| `pass` | `if i == 3: pass` | `0 1 2 3 4 5 6 7 8 9` | Nothing is skipped; a placeholder that does nothing |
| `continue` | `if i == 3: continue` | `0 1 2 4 5 6 7 8 9` | 3 is skipped; jumps to the next round |
| `break` | `if i == 3: break` | `0 1 2` | The loop stops completely at 3 |

```python
# pass: nothing is skipped
for i in range(0, 10):
    if i == 3:
        pass
    print(i)        # 0 1 2 3 4 5 6 7 8 9

# continue: skip 3
for i in range(0, 10):
    if i == 3:
        continue
    print(i)        # 0 1 2 4 5 6 7 8 9

# break: stop at 3
for i in range(0, 10):
    if i == 3:
        break
    print(i)        # 0 1 2
```

Combined example, with a loop counter shown in the output:

```python
total, x = 0, 1
loop_counter = 1

while x <= 10:
    if x == 5:
        print(f"Loop {loop_counter}: skipped x = {x}, total = {total}")
        x += 1
        loop_counter += 1
        continue
    elif loop_counter == 9:
        print(f"Loop {loop_counter}: break out of the loop")
        break
    else:
        total += x
        print(f"Loop {loop_counter}: x = {x}, total = {total}")
        x += 1
    loop_counter += 1

print(f"Loop {loop_counter}: final x = {x}, final total = {total}")

# Loop 1: x = 1, total = 1
# Loop 2: x = 2, total = 3
# Loop 3: x = 3, total = 6
# Loop 4: x = 4, total = 10
# Loop 5: skipped x = 5, total = 10
# Loop 6: x = 6, total = 16
# Loop 7: x = 7, total = 23
# Loop 8: x = 8, total = 31
# Loop 9: break out of the loop
# Loop 9: final x = 9, final total = 31
```

---

# List vs Tuple vs Set

> All three store several items, but they differ in order and changeability:
> - **Lists** and **tuples** keep their items in order and use positions starting at 0.
> - **Sets** have no order and no positions, and don't allow duplicates.
> - **Lists** and **sets** can be changed; **tuples** cannot.

| | List | Tuple | Set |
|---|---|---|---|
| Brackets | `[ ]` | `( )` | `{ }` |
| Example | `names = ["Max", "Moritz"]` | `names = ("Max", "Moritz")` | `names = {"Max", "Moritz"}` |
| Changeable | Yes (mutable) | No (immutable) | Yes (mutable) |
| Ordered | Yes | Yes | No |
| Duplicates | Allowed | Allowed | Not allowed (removed automatically) |
| Change an item | `names[0] = "Tom"` works | `names[0] = "Tom"` gives `TypeError` | Not possible, no positions (remove and add instead) |
| Add an item | `names.append("Monika")` | Not possible | `names.add("Monika")` |
| Access an item | `names[0]` | `names[0]` | `names[0]` gives `TypeError` |
| Use when | Data changes (add, remove, edit) | Data should stay fixed (e.g. coordinates, days of the week) | Only unique items matter, or to remove duplicates |

> Note: a tuple with one item needs a trailing comma: `(5,)`. Without it, `(5)` is just the number 5.

```python
# list: can be changed
names = ["Max", "Moritz"]
names[0] = "Tom"
names.append("Monika")
print(names)            # ['Tom', 'Moritz', 'Monika']

# tuple: cannot be changed
point = (52.5, 13.4)
print(point[0])         # 52.5
point[0] = 10           # TypeError: 'tuple' object does not support item assignment

# set: can be changed, but no duplicates and no positions
colors = {"red", "green"}
colors.add("blue")
colors.add("red")       # already in the set, ignored
print(colors)           # {'red', 'green', 'blue'}  (order may differ)
print("red" in colors)  # True
colors[0]               # TypeError: 'set' object is not subscriptable
```

## List methods and operations

Assume: `names = ["Max", "Moritz", "Max"]` (each row starts from this list)

| Command | Definition | Example | Result |
|---|---|---|---|
| `list_name.append(item)` | Add an item to the end | `names.append("Monika")` | `['Max', 'Moritz', 'Max', 'Monika']` |
| `list_name.remove(item)` | Remove the **first** item with that value | `names.remove("Max")` | `['Moritz', 'Max']` |
| `list_name.count(item)` | Count how often an item appears (find duplicates) | `names.count("Max")` | `2` |
| `list(x)` | Convert a tuple, set, string or dictionary keys into a new list (on a list: makes a copy) | `list("Hi")` | `['H', 'i']` |
| `list(set(list_name))` | Remove duplicates by converting to a set and back | `list(set(names))` | `['Moritz', 'Max']` (order not guaranteed) |

Assume: `nums = [5, 2, 9, 1]`

| Command | Definition | Example | Result |
|---|---|---|---|
| `list_name.sort()` | Sort the list in place, ascending | `nums.sort()` | `nums` is now `[1, 2, 5, 9]` |
| `list_name.sort(reverse=True)` | Sort the list in place, descending | `nums.sort(reverse=True)` | `nums` is now `[9, 5, 2, 1]` |
| `sorted(list_name)` | Return a new sorted list; original unchanged | `sorted(nums)` | `[1, 2, 5, 9]` |
| `sorted(list_name, reverse=True)` | Return a new list sorted descending; original unchanged | `sorted(nums, reverse=True)` | `[9, 5, 2, 1]` |

> `enumerate()` lets you loop through a list or string and get each item **together with its index**.

```python
other_nums = [5, 2, 9, 1]
for index, value in enumerate(other_nums):
    print(index, value)     # 0 5, 1 2, 2 9, 3 1
```

## Set methods

> A set stores **unique** items inside curly brackets `{ }`. It has **no duplicates** and **no order**, so there are no positions (`s[0]` gives a `TypeError`).

```python
numbers = {1, 2, 2, 3, 3, 3}
print(numbers)              # {1, 2, 3}  (duplicates removed)
```

Assume: `s = {1, 2, 3}`

| Command | Definition | Example | Result |
|---|---|---|---|
| `set_name.add(item)` | Add an item (ignored if it already exists) | `s.add(4)` | `{1, 2, 3, 4}` |
| `set_name.remove(item)` | Remove an item (`KeyError` if missing) | `s.remove(1)` | `{2, 3}` |
| `set_name.discard(item)` | Remove an item (no error if missing) | `s.discard(10)` | `{1, 2, 3}` |
| `item in set_name` | Check if an item exists (fast) | `2 in s` | `True` |
| `len(set_name)` | Number of items | `len(s)` | `3` |
| `set(list_name)` | Convert a list to a set (removes duplicates) | `set([1, 1, 2])` | `{1, 2}` |

### Set operations

Assume: `a = {1, 2, 3}`, `b = {3, 4, 5}`

| Command | Definition | Result |
|---|---|---|
| `a \| b` or `a.union(b)` | Everything from both | `{1, 2, 3, 4, 5}` |
| `a & b` or `a.intersection(b)` | Only what is in both | `{3}` |
| `a - b` or `a.difference(b)` | In `a` but not in `b` | `{1, 2}` |

> **Empty set:** use `set()`. `{}` creates an empty **dictionary**, not a set.
> Set items must be unchangeable (numbers, strings, tuples), not lists.

---

## Dictionaries

> A dictionary stores data as **key: value** pairs inside curly brackets `{ }`. You look up a value by its key, not by a position as in a list.

```python
person = {"name": "Alex", "age": 28, "city": "Hamburg", "job": "Engineer"}

print(person["name"])               # Alex
print(person["job"])                # Engineer
print(person.get("city"))           # Hamburg  (key exists)
print(person.get("phone"))          # None     (key missing, no error)
```

Assume: `person = {"name": "Alex", "age": 28}` (each row starts from this dictionary)

| Command | Definition | Example | Result |
|---|---|---|---|
| `dict_name[key]` | Get the value of a key (`KeyError` if it doesn't exist) | `person["name"]` | `"Alex"` |
| `dict_name.get(key)` | Get the value of a key; `None` if missing (no error) | `person.get("phone")` | `None` |
| `dict_name.get(key, default)` | Same, but returns your default if missing | `person.get("phone", "unknown")` | `"unknown"` |
| `dict_name[key] = value` | Add a new pair, or change an existing one | `person["city"] = "Berlin"` | `{'name': 'Alex', 'age': 28, 'city': 'Berlin'}` |
| `del dict_name[key]` | Remove a pair | `del person["age"]` | `{'name': 'Alex'}` |
| `key in dict_name` | Check if a key exists | `"name" in person` | `True` |
| `dict_name.keys()` | All keys | `person.keys()` | `dict_keys(['name', 'age'])` |
| `dict_name.values()` | All values | `person.values()` | `dict_values(['Alex', 28])` |
| `dict_name.items()` | All key-value pairs | `person.items()` | `dict_items([('name', 'Alex'), ('age', 28)])` |
| `len(dict_name)` | Number of pairs | `len(person)` | `2` |

Looping through a dictionary:

```python
person = {"name": "Alex", "age": 28}

for key in person:                       # keys only
    print(key)                           # name, age

for key, value in person.items():        # keys and values
    print(key, value)                    # name Alex, then age 28
```

> **Rules:** keys must be unique (a repeated key overwrites the old value) and must be unchangeable types such as strings, numbers or tuples (not lists). Values can be anything.

---

## Summary: List vs Tuple vs Dictionary vs Set

| | List | Tuple | Dictionary | Set |
|---|---|---|---|---|
| Brackets | `[ ]` | `( )` | `{ }` | `{ }` |
| Example | `["a", "b"]` | `("a", "b")` | `{"name": "a"}` | `{"a", "b"}` |
| Ordered | Yes | Yes | Yes (insertion order, Python 3.7+) | No |
| Access by | Position | Position | Key | No access by position |
| Changeable | Yes | No | Yes | Yes |
| Duplicates | Allowed | Allowed | Keys must be unique | Not allowed |
| Use when | Data changes | Data stays fixed | Looking up values by name | Unique items, removing duplicates |

---

## Helpful References

* [Official Python tutorial](https://docs.python.org/3/tutorial/)
* [String methods (Python 3 docs)](https://docs.python.org/3/library/stdtypes.html#string-methods)
* [`%` formatting type letters (Python 3 docs)](https://docs.python.org/3/library/stdtypes.html#printf-style-string-formatting)
