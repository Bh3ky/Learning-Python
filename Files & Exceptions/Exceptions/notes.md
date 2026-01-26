## Exceptions

- Python use special objects called exceptions to manage errors that arise during a program's execution. 
- exceptions are handled with `try-except` blocks. 

1. **Handling the ZeroDivisionError Exception**

```python
print(5/0)
```

- get a traceback
```
Traceback (most recent call last):  File "division_calculator.py", line 1, in <module>    print(5/0)          ~^~
1 ZeroDivisionError: division by zero (exception object)
```

- sometimes when we think an error may occur, we can write `try-except` block to handle the exception that might be raised.
    - basically, we tell Python to try running the code and if the code results in a particular kind of exception we tell it what to do. 
- code snippet:

```python
try:
    print(5/0)
except ZeroDivisionError:
    print("You cannot divide by zero!")
```

---

#### Using Exceptions to Prevent Crashes

- handling errors correctly is especially important when the program has got more works to do after the errors.
- this happens often in programs that prompt users for input. if the program responds to invalid input appropriately, it can prompt for more valid input instead of crashing. 

```python
print("Give me two numbers, and I'll divide them.")
print("Enter 'q' to quit.")

while True:
    first_number = input("\nFirst number: ")
    if first_number == 'q':
        break
    second_number = input("Second number: ")
    if second_number == 'q':
        break

    try:
        answer = int(first_number) / int(second_number)
    except ZeroDivisionError:
        print("You can't divide by 0!")
    else:
        print(answer)
```


#### Handling the FileNotFoundError Exception

- we can also use `try-except` block to handle missing files.
- Note: we write an except block that matches the error.

```python
from pathlib import Path

path = Path('alice.txt')
try:
    contents = path.read_text(encoding='utf-8')
except FileNotFoundError:
    print(f"Sorry, the file {path} does not exist.")
```

#### Analyzing Text

```python
from pathlib import Path

path = Path('alice.txt')
try:
    contents = path.read_text(encoding='utf-8')
except FileNotFoundError:
    print(f"Sorry, the file {path} does not exist.")

else:
    # count the approximate number of words in the file:
    words = contents.split()
    num_words = len(words)
    print(f"The file {path} has about {num_words} words.")
```

#### Working with Multiple Files

- write a short loop to count the words in any text we want to analyse.
- we store the names of files we want to analyse in a list and then call `count_words()` for each file in the list