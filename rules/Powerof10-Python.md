# The Power of 10: Rules for Developing Safety-Critical Code (Adaptation for Python Programming)

- [The Power of 10: Rules for Developing Safety-Critical Code (Adaptation for Python Programming)](#the-power-of-10-rules-for-developing-safety-critical-code-adaptation-for-python-programming)
  - [1. **Restrict control flow to very simple constructs**](#1-restrict-control-flow-to-very-simple-constructs)
  - [2. **Give all loops a fixed upper bound**](#2-give-all-loops-a-fixed-upper-bound)
  - [3. **Do not use dynamic memory allocation after initialization**](#3-do-not-use-dynamic-memory-allocation-after-initialization)
  - [4. **No function should be longer than a single sheet of paper**](#4-no-function-should-be-longer-than-a-single-sheet-of-paper)
  - [5. **The density of assertions in code should be at least two assertions per function**](#5-the-density-of-assertions-in-code-should-be-at-least-two-assertions-per-function)
  - [6. **Declare all data objects at the smallest possible level of scope**](#6-declare-all-data-objects-at-the-smallest-possible-level-of-scope)
  - [7. **Every calling function must check the return value of non-void functions, and every called function must check the validity of all parameters provided by the caller**](#7-every-calling-function-must-check-the-return-value-of-non-void-functions-and-every-called-function-must-check-the-validity-of-all-parameters-provided-by-the-caller)
  - [8. **Limit the use of the preprocessor to file inclusions and simple macro definitions**](#8-limit-the-use-of-the-preprocessor-to-file-inclusions-and-simple-macro-definitions)
  - [9. **Restrict the use of pointers**](#9-restrict-the-use-of-pointers)
  - [10. **All code must be compiled with all compiler warnings enabled at the most pedantic level available**](#10-all-code-must-be-compiled-with-all-compiler-warnings-enabled-at-the-most-pedantic-level-available)

## 1. **Restrict control flow to very simple constructs**

**Original rule:** Do not use `goto`, `setjmp`, or `longjmp` statements, nor direct or indirect recursion.

**Python adaptation:** Use only simple control flow structures like `if`, `for`, and `while`. Avoid recursion for simpler clarity and analysis.

:warning: Example to avoid :warning:

```python
def recursive_sum(list):
    if not list:
        return 0
    return list[0] + recursive_sum(list[1:])

# Usage example
my_list = [1, 2, 3, 4, 5]
result = recursive_sum(my_list)
print(f"The sum is: {result}")
```

:heavy_check_mark: Recommended example :heavy_check_mark:

```python
def iterative_sum(list):
    sum = 0
    for element in list:
        sum += element
    return sum

# Usage example
my_list = [1, 2, 3, 4, 5]
result = iterative_sum(my_list)
print(f"The sum is: {result}")
```

| :warning: Example to avoid :warning: | :heavy_check_mark: Recommended example :heavy_check_mark: |
|--|--|
| **Risk of stack overflow:** Deep recursion can lead to stack overflow for very large lists. | **Avoids stack overflow:** Using loops avoids the risk of stack overflow associated with recursion. |
| **Difficulty in analysis and debugging:** Recursion can be difficult to follow and debug, especially for less experienced developers. | **Ease of analysis and debugging:** `for` loops and simple control structures are easier to understand, follow, and debug. |
| **Less efficient:** Recursion involves repeated function calls, which can be less efficient compared to an iterative loop. | **Performance:** Iterative loops are generally more efficient than recursion for simple tasks like summing the elements of a list. |

## 2. **Give all loops a fixed upper bound**

**Original rule:** It must be trivially possible for a checking tool to statically prove that the loop cannot exceed a predefined upper bound.

**Python adaptation:** Add an explicit limit to all loops with a variable number of iterations.

:warning: Example to avoid :warning:

```python
def find_element_without_limit(list, element):
    i = 0
    while i < len(list):
        if list[i] == element:
            return i
        i += 1
    return -1

# Usage example
my_list = [3, 5, 7, 9, 11]
element_to_find = 7
result = find_element_without_limit(my_list, element_to_find)
print(f"The element {element_to_find} is found at index {result}.")
```

:heavy_check_mark: Recommended example :heavy_check_mark:

```python
def find_element_with_limit(list, element):
    max_iterations = len(list)
    i = 0
    
    while i < max_iterations:
        if list[i] == element:
            return i
        i += 1

    return -1  # Returns -1 if the element is not found

# Usage example
my_list = [3, 5, 7, 9, 11]
element_to_find = 7
result = find_element_with_limit(my_list, element_to_find)
print(f"The element {element_to_find} is found at index {result}.")
```

| :warning: Example to avoid :warning: | :heavy_check_mark: Recommended example :heavy_check_mark: |
|--|--|
| **Implicit dependency on loop condition:** The loop condition implicitly depends on the length of the list, making static analysis difficult. | **Explicit limit:** By defining `max_iterations`, it is clear to static analysis tools and code readers that the loop will never exceed the number of elements in the list. |
| **No explicit limit:** There is no fixed limit defined for the iterations, which can potentially cause infinite loops if the condition is poorly defined. | **Clarity and safety:** The explicit limit makes the code safer and more predictable, avoiding unexpected infinite loops or overflows. |
|  | **Readability:** The explicit limit makes the code easier to understand and maintain. |

## 3. **Do not use dynamic memory allocation after initialization**

**Original rule:** Avoid the use of `malloc` and garbage collectors.

**Python adaptation:** Avoid creating large objects or dynamically allocating memory after initialization. Use predefined data structures.

:warning: Example to avoid :warning:

```python
def process_data(data):
    # Dynamic memory allocation
    results = []
    for item in data:
        results.append(item * 2)
    return results

# Usage example
data = [1, 2, 3, 4, 5]
print(process_data(data))  # Prints: [2, 4, 6, 8, 10]
```

:heavy_check_mark: Recommended example :heavy_check_mark:

```python
def process_data(data):
    # Fixed memory allocation
    results = [0] * len(data)
    for i in range(len(data)):
        results[i] = data[i] * 2
    return results

# Usage example
data = [1, 2, 3, 4, 5]
print(process_data(data))  # Prints: [2, 4, 6, 8, 10]
```

| :warning: Example to avoid :warning: | :heavy_check_mark: Recommended example :heavy_check_mark: |
|--|--|
| **Dynamic memory allocation:** The `results` list is dynamically allocated during runtime, which can lead to unpredictable memory usage. | **Predictable memory allocation:** By pre-allocating memory for `results`, we know exactly how much memory will be used. |
| **Unpredictable performance:** Dynamic growth of the list can result in frequent memory reallocations and impact performance. | **Improved performance:** Fixed allocation avoids frequent reallocations and improves performance. |

## 4. **No function should be longer than a single sheet of paper**

**Original rule:** Limit functions to approximately 60 lines of code.

**Python adaptation:** Break down complex functions into smaller functions, each performing a specific task.

:warning: Example to avoid :warning:

```python
def process_and_analyze_data(data):
    # Data cleaning
    cleaned_data = []
    for item in data:
        if item is not None and item != '':
            cleaned_data.append(item.strip())

    # Data analysis
    total = 0
    num_elements = len(cleaned_data)
    for item in cleaned_data:
        total += int(item)

    average = total / num_elements if num_elements > 0 else 0

    # Report generation
    report = f"Number of elements: {num_elements}\nTotal: {total}\nAverage: {average}"
    
    return report

# Usage example
data = ["10", "20", None, "30", " 40 ", ""]
print(process_and_analyze_data(data))
```

:heavy_check_mark: Recommended example :heavy_check_mark:

```python
def clean_data(data):
    cleaned_data = []
    for item in data:
        if item is not None and item != '':
            cleaned_data.append(item.strip())
    return cleaned_data

def analyze_data(cleaned_data):
    total = 0
    num_elements = len(cleaned_data)
    for item in cleaned_data:
        total += int(item)
    average = total / num_elements if num_elements > 0 else 0
    return num_elements, total, average

def generate_report(num_elements, total, average):
    report = f"Number of elements: {num_elements}\nTotal: {total}\nAverage: {average}"
    return report

def process_and_analyze_data(data):
    cleaned_data = clean_data(data)
    num_elements, total, average = analyze_data(cleaned_data)
    report = generate_report(num_elements, total, average)
    return report

# Usage example
data = ["10", "20", None, "30", " 40 ", ""]
print(process_and_analyze_data(data))
```

| :warning: Example to avoid :warning: | :heavy_check_mark: Recommended example :heavy_check_mark: |
|--|--|
| **Too long function:** The function contains multiple distinct tasks (cleaning, analysis, report generation) and becomes difficult to read and maintain. | **Short and specific functions:** Each function performs a specific task, making the code more readable and easier to understand. |
| **Difficulty in debugging:** Errors are harder to identify and isolate in a long function. | **Ease of debugging:** Errors are easier to identify and fix because each function has a clear and limited responsibility. |
|  | **Reusability:** Smaller functions can be reused in other parts of the program if needed. |

## 5. **The density of assertions in code should be at least two assertions per function**

**Original rule:** Use assertions to check for abnormal conditions that should never occur in real execution.

**Python adaptation:** Use assertions to check preconditions and postconditions of functions.

:warning: Example to avoid :warning:

```python
def process_list(list, value_to_add):
    """
    Processes a list by adding a value to each element.

    Parameters:
        list (list): List of integers to process
        value_to_add (int): Value to add to each element of the list

    Returns:
        new_list (list): New list with the value added to each element
    """

    # No preconditions
    new_list = [i + value_to_add for i in list]

    # No postconditions
    return new_list

# Usage example
my_list = [1, 2, 3, 4]
value = 5
result = process_list(my_list, value)
print(f"List after processing: {result}")
```

:heavy_check_mark: Recommended example :heavy_check_mark:

```python
def process_list(list, value_to_add):
    """
    Processes a list by adding a value to each element.

    Parameters:
        list (list): List of integers to process
        value_to_add (int): Value to add to each element of the list

    Returns:
        new_list (list): New list with the value added to each element
    """

    # Preconditions
    assert isinstance(list, list), "Input must be a list."
    assert all(isinstance(i, int) for i in list), "All elements in the list must be integers."
    assert isinstance(value_to_add, int), "The value to add must be an integer."

    new_list = [i + value_to_add for i in list]

    # Postconditions
    assert len(new_list) == len(list), "The length of the new list must be equal to the original list."
    assert all(isinstance(i, int) for i in new_list), "All elements in the new list must be integers."

    return new_list

# Usage example
try:
    my_list = [1, 2, 3, 4]
    value = 5
    result = process_list(my_list, value)
    print(f"List after processing: {result}")
except AssertionError as e:
    print(f"Error: {e}")
```

:white_check_mark: Incorrect usage example :white_check_mark:

```python
try:
    my_list = [1, 2, 3, 'four']  # One element is not an integer
    value = 5
    result = process_list(my_list, value)
    print(f"List after processing: {result}")
except AssertionError as e:
    print(f"Error: {e}")
```

| :warning: Example to avoid :warning: | :heavy_check_mark: Recommended example :heavy_check_mark: |
|--|--|
| **No precondition checks:** There is no verification that `list` is indeed a list, that its elements are integers, or that `value_to_add` is an integer. This can lead to unexpected errors if the inputs are incorrect. | **Early error detection:** Assertions help detect errors as soon as they occur, before incorrect values propagate further into the program. |
| **No postcondition checks:** There is no verification that the length of `new_list` is correct or that its elements are integers. This can result in incorrect or unexpected results without being detected. | **Code documentation:** Assertions serve as living documentation by specifying expectations and invariants directly in the code. |
| **Difficulty in debugging:** Without assertions, the program will fail with an error when executing `new_list = [i + value_to_add for i in list]` because `'four'` cannot be added with an integer, but the error message will be less clear and it will be harder to diagnose the issue. ```TypeError: unsupported operand type(s) for +: 'str' and 'int'``` | **Simplified debugging:** Assertions help isolate issues by providing clear and specific error messages when conditions are not met. ```Error: All elements in the list must be integers.```|

## 6. **Declare all data objects at the smallest possible level of scope**

**Original rule:** Limit the scope of variables to avoid unintended side effects.

**Python adaptation:** Use local variables as much as possible and minimize the use of global variables.

:warning: Example to avoid :warning:

```python
# Using global variables

# Global variable
global_counter = 0

def increment_counter(value):
    global global_counter
    global_counter += value

def decrement_counter(value):
    global global_counter
    global_counter -= value

def display_counter():
    global global_counter
    print(f"Counter: {global_counter}")

# Usage example
increment_counter(5)
display_counter()  # Prints: Counter: 5
decrement_counter(2)
display_counter()  # Prints: Counter: 3
```

:heavy_check_mark: Recommended example :heavy_check_mark:

```python
# Using local variables and classes to encapsulate state

class Counter:
    def __init__(self):
        self.counter = 0

    def increment(self, value):
        self.counter += value

    def decrement(self, value):
        self.counter -= value

    def display(self):
        print(f"Counter: {self.counter}")

# Usage example
my_counter = Counter()
my_counter.increment(5)
my_counter.display()  # Prints: Counter: 5
my_counter.decrement(2)
my_counter.display()  # Prints: Counter: 3
```

| :warning: Example to avoid :warning: | :heavy_check_mark: Recommended example :heavy_check_mark: |
|--|--|
| **Side effects:** Using the global variable `global_counter` means that any modification to this variable can have unintended side effects elsewhere in the program. This makes the behavior of the program hard to predict. | **Isolation of state:** By encapsulating the state within a class (`Counter`), each instance of the class has its own independent state. This avoids unintended side effects. |
| **Reduced readability and maintainability:** It becomes difficult to track where and how `global_counter` is modified, especially in larger and more complex programs. | **Readability and maintainability:** The code is clearer and easier to follow because the state is managed locally within the class. |
| **Difficult unit testing:** Testing functions that use global variables can be complicated because global variables need to be properly initialized and cleaned up between tests. | **Easy unit testing:** Testing the methods of the `Counter` class is simpler because each test can create a new instance of the class without interfering with other tests. |

## 7. **Every calling function must check the return value of non-void functions, and every called function must check the validity of all parameters provided by the caller**

**Original rule:** Check the return value of all functions and the validity of parameters.

**Python adaptation:** Always check return values and validate input parameters.

:warning: Example to avoid :warning:

```python
def open_file(file_name):
    try:
        file = open(file_name, 'r')
        content = file.read()
        file.close()
        return content
    except FileNotFoundError:
        return None

def process_file(file_name):
    content = open_file(file_name)
    processed_content = content.upper()  # This line can fail if `content` is `None`
    return processed_content

# Usage example
result = process_file('example.txt')
print(result)
```

:heavy_check_mark: Recommended example :heavy_check_mark:

```python
def open_file(file_name):
    """
    Opens a file and reads its content.

    Parameters:
        file_name (str): The name of the file to open

    Returns:
        content (str): The content of the file or None if the file does not exist
    """
    # Validate input parameters
    assert isinstance(file_name, str), "The file name must be a string."

    try:
        with open(file_name, 'r') as file:
            content = file.read()
        return content
    except FileNotFoundError:
        return None

def process_file(file_name):
    """
    Processes a file by checking that the content is correctly read.

    Parameters:
        file_name (str): The name of the file to process

    Returns:
        processed_content (str): The processed content of the file or an error message
    """
    content = open_file(file_name)

    # Check the return value
    if content is None:
        return "Error: The file does not exist."
    else:
        # Perform processing on the file content
        processed_content = content.upper()  # Example of simple processing
        return processed_content

# Usage example
result = process_file('example.txt')
print(result)
```

| :warning: Example to avoid :warning: | :heavy_check_mark: Recommended example :heavy_check_mark: |
|--|--|
| **No parameter validation:** `open_file` does not validate that `file_name` is a string. | **Parameter validation:** In `open_file`, there is an assertion to validate that `file_name` is indeed a string (`assert isinstance(file_name, str)`). |
| **No return value checking:** `process_file` directly uses `content` without checking if it is `None`. If `open_file` returns `None` (for example, if the file does not exist), the call to `content.upper()` will fail with an `AttributeError`. | **Return value checking:** In `process_file`, the return value of `open_file` is checked. If the content is `None`, an error message is returned. |
| **Risk of silent errors:** If `open_file` fails, `content` will be `None`, and the error will not be reported to the caller. | **Error handling:** By checking the return value of `open_file`, the program can properly handle cases where the file does not exist or cannot be opened. |

## 8. **Limit the use of the preprocessor to file inclusions and simple macro definitions**

**Original rule:** Limit the use of the preprocessor to file inclusions and simple macro definitions.

**Python adaptation:** Limit the use of external modules and conditional imports. Avoid excessive use of macros and code generators.

:warning: Example to avoid :warning:

```python
import os
import subprocess

def list_files(directory):
    """
    Lists the files in a given directory.

    Parameters:
        directory (str): The directory path

    Returns:
        list: A list of file names in the directory, or an empty list if the directory does not exist
    """
    # Excessive use of subprocess to list files
    if os.path.isdir(directory):
        result = subprocess.run(['ls', directory], stdout=subprocess.PIPE)
        return result.stdout.decode('utf-8').split('\n')
    else:
        return []

# Usage example
directory_path = './documents'
files = list_files(directory_path)
print(f"Files in directory '{directory_path}': {files}")
```

:heavy_check_mark: Recommended example :heavy_check_mark:

```python
import os

def list_files(directory):
    """
    Lists the files in a given directory.

    Parameters:
        directory (str): The directory path

    Returns:
        list: A list of file names in the directory, or an empty list if the directory does not exist
    """
    # Validate input parameter is a string
    assert isinstance(directory, str), "The directory must be a string."

    # Make judicious use of an external module (os)
    if os.path.isdir(directory):
        return os.listdir(directory)
    else:
        return []

def read_file(file_path):
    """
    Reads the content of a given file.

    Parameters:
        file_path (str): The file path to read

    Returns:
        str: The content of the file, or an empty string if the file does not exist
    """
    # Validate input parameter is a string
    assert isinstance(file_path, str), "The file path must be a string."

    # Make judicious use of an external module (os)
    if os.path.isfile(file_path):
        with open(file_path, 'r') as file:
            return file.read()
    else:
        return ""

# Usage example
directory_path = './documents'
files = list_files(directory_path)
print(f"Files in directory '{directory_path}': {files}")

file_path = './documents/example.txt'
content = read_file(file_path)
print(f"Content of file '{file_path}': {content}")
```

| :warning: Example to avoid :warning: | :heavy_check_mark: Recommended example :heavy_check_mark: |
|--|--|
| **Excessive use of external modules:** Using `subprocess` to list files in a directory, when it can be done more simply and efficiently with `os.listdir`. | **Limited use of external modules:** The `os` module is used to check for the existence of a directory (`os.path.isdir`) and to list files in a directory (`os.listdir`). The `os` module is also used to check for the existence of a file (`os.path.isfile`) and to read the file's content using a `with` block to safely handle the file. |
|  | **Parameter validation:** The `list_files` and `read_file` functions validate their parameters to ensure they are of string type (`assert isinstance(directory, str)` and `assert isinstance(file_path, str)`). |
| **Unnecessary complexity:** Using `subprocess.run` to execute a system command `ls` is excessive and introduces unnecessary complexity, which can also pose security issues. | **Simple design:** The functions are designed in a simple and straightforward manner, focusing on a specific task without using complex constructs or generated code. |

## 9. **Restrict the use of pointers**

**Original rule:** Use at most one level of dereferencing.

**Python adaptation:** Avoid the use of complex references and multiple levels of indirection. Use simple data structures and direct access.

:warning: Example to avoid :warning:

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None
        self.previous = None  # Unnecessary additional reference

class DoublyLinkedList:
    def __init__(self):
        self.head = None
        self.tail = None  # Unnecessary additional reference

    def append(self, value):
        new_node = Node(value)
        if self.head is None:
            self.head = new_node
            self.tail = new_node  # Unnecessary additional reference
        else:
            current = self.head
            while current.next:
                current = current.next
            current.next = new_node
            new_node.previous = current  # Unnecessary additional reference
            self.tail = new_node  # Unnecessary additional reference

    def display(self):
        values = []
        current = self.head
        while current:
            values.append(current.value)
            current = current.next
        print(" -> ".join(map(str, values)))

# Usage example
doubly_linked_list = DoublyLinkedList()
doubly_linked_list.append(1)
doubly_linked_list.append(2)
doubly_linked_list.append(3)
doubly_linked_list.display()
```

:heavy_check_mark: Recommended example :heavy_check_mark:

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def append(self, value):
        new_node = Node(value)
        if self.head is None:
            self.head = new_node
        else:
            current = self.head
            while current.next:
                current = current.next
            current.next = new_node

    def find(self, value):
        current = self.head
        while current:
            if current.value == value:
                return current
            current = current.next
        return None

    def display(self):
        values = []
        current = self.head
        while current:
            values.append(current.value)
            current = current.next
        print(" -> ".join(map(str, values)))

# Usage example
linked_list = LinkedList()
linked_list.append(1)
linked_list.append(2)
linked_list.append(3)
linked_list.display()

node = linked_list.find(2)
if node:
    print(f"Node with value {node.value} found.")
else:
    print("Node not found.")
```

| :warning: Example to avoid :warning: | :heavy_check_mark: Recommended example :heavy_check_mark: |
|--|--|
| **Unnecessary complexity:** The structure is complicated by additional references (`previous`, `tail`), making the code harder to read. | **Simplicity and readability:** The data structure is simple with only one reference (`next`). |
| **Maintenance difficulty:** The additional references require extra attention during modifications, increasing the risk of errors. | **Ease of maintenance:** Modifications are straightforward to make and understand. |
| **Reduced performance:** The additional references and management of the doubly linked list can slow down operations and increase memory consumption. | **Memory efficiency/performance:** Fewer references mean more efficient memory usage. Operations are faster due to the simplicity of the references. |

## 10. **All code must be compiled with all compiler warnings enabled at the most pedantic level available**

**Original rule:** All code must be compiled without warnings and analyzed daily with at least one static code analyzer.

**Python adaptation:** Use static analysis tools like `pylint`, `flake8`, `mypy`, `black` or `ruff` and ensure your code generates no warnings.

[![linting: pylint](https://img.shields.io/badge/linting-pylint-yellowgreen)](https://github.com/pylint-dev/pylint)
[flake8 GitHub Repository](https://www.github.com/PyCQA/flake8)
[mypy GitHub Repository](https://github.com/python/mypy)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![Linting: Ruff](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/charliermarsh/ruff/main/assets/badge/v2.json)](https://github.com/astral-sh/ruff)

These adaptations of NASA rules in Python aim to ensure code quality, readability, and maintainability while adhering to principles of critical software development.
