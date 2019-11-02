# Modules

## `importing module`:

<b>1. import module:</b>

- `import moduleName` instruction may be located anywhere in your code, but it must be placed <b>before the first use of any of the module's entities.</b>

- `Namespace` - Inside a certain namespace, each name must remain unique. Python imports `module` contents, i.e., all the names defined in the module become known, but they don't enter your code's namespace. 

    <b>Example:</b><br/><br/>
    ```python
    import math
    print(math.pi) # accessing module contents

    pi = 2 # namespace of this variable is different
    print(2) # returns 2
    ```

- `math.pi` - using this qualification is `compulsory` if a module has been imported by the import module instruction. It doesn't matter if any of the names from your code and from the module's namespace are in conflict or not.

<b>2. from math import pi, sin</b>

- `Namespace` - Inside a certain namespace, each name must remain unique. Python imports `module` contents, i.e., all the names defined in the module become known, but they don't enter your code's namespace. 

    <b>Example:</b><br/><br/>
    ```python
    from math import sin, pi
    pi = 3.14	# redefine the meaning of pi - in effect, they supersede the original (imported) definitions within the code's namespace;

    def sin(x):
        if 2 * x == pi:
            return 0.99999999
        else:
            return None	# line 07

    print(sin(pi/2))	# line 09


    from math import sin, pi	# line 12

    print(sin(pi/2))	# imported symbols supersede their previous definitions within the namespace; and returns 1.0
    ```
<b>3. from math import *</b>
<b>4. import module as alias</b>

## `Working with Standard Modules`:

### `dir(module)`:
- alphabetically sorted list containing all entities' names available in the module.

```python
import math
for name in dir(math):
    print(name, end="\t")

dir(math)
```

### `random`: 

<b>choice and sample</b>
```python
from random import choice, sample
lst = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print(choice(lst))
print(sample(lst, 5))
print(sample(lst, 10))
```
output of the program is not predictable. 
```
4
[3, 1, 8, 9, 10]
[10, 8, 5, 1, 6, 4, 3, 9, 7, 2]
```

### `platform module`
```python
from platform import platform
print(platform())
print(platform(1))
print(platform(0, 1))
```

# Packages

![packages](https://user-images.githubusercontent.com/45288730/67940611-7c22ff00-fbed-11e9-86a9-21a7f3295593.JPG)

## `What happens when we import module`:

- When Python imports a module for the first time, it translates its contents into a somewhat `compiled shape`. The file doesn't contain `machine code` - it's internal Python `semi-compiled code`, ready to be executed by `Python's interpreter`.

- As effect of this, python compiled file (PYC) is created under `pycache` folder. Every subsequent import will go quicker than interpreting the source text from scratch.

- When a module is imported, its content is `implicitly executed by Python`.

- Python creates a variable called `__name__`.
    - when you run a file directly, its `__name__` variable is set to `__main__`;
    - when a file is imported as a module, its `__name__` variable is set to the file's name (excluding .py)
<br/>

    ```
    Imagine the following context:

    - there is a module named mod1;
    - there is a module named mod2 which contains the import mod1 instruction;
    - there is a main file containing the import mod1 and import mod2 instructions.

    At first glance, you may think that mod1 will be imported twice 
    Fortunately, only the first import occurs. 
    Python remembers the imported modules and silently omits all subsequent imports.
    ```

## `how Python searches for modules`:

![moduleimportspath](https://user-images.githubusercontent.com/45288730/67944026-e25f5000-fbf4-11e9-9357-bae249dc41f7.JPG)

`__init__.py`: Package initialization

![packageinit](https://user-images.githubusercontent.com/45288730/67945786-33714300-fbf9-11e9-9c52-c205c5e667a4.JPG)

# Exceptions

- Python 3 defines `63 built-in` exceptions, and all of them form a tree-shaped hierarchy.

    ![exception-hie](https://user-images.githubusercontent.com/45288730/68067868-c5e32500-fd66-11e9-8949-251a51661e06.JPG)

    <br/>
    - Example - Below all there snippets produces same output.

    ```python
    # Detail Level
    try:
        y = 1 / 0
    except ZeroDivisionError:
        print("Oooppsss...")

    print("THE END.")

    # Generic Level
    try:
        y = 1 / 0
    except ArithmeticError:
        print("Oooppsss...")

    print("THE END.")

    # More Generic Level
    try:
        y = 1 / 0
    except Exception:
        print("Oooppsss...")

    print("THE END.")
    ```
- the order of the branches matters!
- don't put more general exceptions before more concrete ones;
- this will make the latter one unreachable and useless;
- moreover, it will make your code messy and inconsistent;
- Python won't generate any error messages regarding this issue.


    ```python
    try:
        y = 1 / 0
    except ArithmeticError:
        print("Arithmetic problem!")
    except ZeroDivisionError:
        print("Zero Division!")

    print("THE END.")

    # The exception is the same, but the more general exception is now listed first
    # it will catch all zero divisions too.
    # It also means that there's no chance that any exception hits the ZeroDivisionError branch. 
    # This branch is now completely unreachable.

    ```
- handle two or more exceptions 
    ```python
    try:
        :
    except (exc1, exc2):
        :
    ```
- Exception handling in Functions

    ![exception-handling-in-functions](https://user-images.githubusercontent.com/45288730/68067978-c8467e80-fd68-11e9-9180-219087e34a6d.JPG)

- Raising exceptions: `raise exception` v `raise`

    ```python
    # Option 1 - raise exception

    def badFun(n):
        raise ZeroDivisionError

    try:
        badFun(0)
    except ArithmeticError:
        print("What happened? An error?")
    print("THE END.")

    # Option 2 - raise 
    def badFun(n):
    try:
        return n / 0
    except:
        print("I did it again!")
        raise # to be used inside the except branch only.

    try:
        badFun(0)
    except ArithmeticError:
        print("I see!")

    print("THE END.")
    ```
- `assert` instruction
    a concrete exception raised by the assert instruction when its argument evaluates to `False`, `None`, `0`, or an empty string.

    ```python
    import math

    x = float(input("Enter a number: "))
    assert x >= 0.0

    x = math.sqrt(x)

    print(x)
    ```

# Strings - immutable sequences

```python
# multiline strings 
multiLine = '''Line #1
Line #2'''
print(len(multiLine))
multiLine = """Line #1
Line #2"""
print(len(multiLine))

# ord() - know a specific character's ASCII/UNICODE code point value
ch1 = 'a' 
ch2 = ' ' # space
print(ord(ch1)) # 97
print(ord(ch2)) # 32

# chr() - takes a code point and returns its character.
print(chr(97)) # a
print(chr(945)) # α
```

### `Sequence operations` 
- Iterating
- Slicing 
- checking character in string `in` and `not in`
- min()
- `immutable` - not allowed to use the `del`, `append()`,`insert()` instructions on string.

```python
exampleString = 'silly walks'
for ch in exampleString:
    print(ch, end=' ')
print()

alpha = "abdefg"
print(alpha[1:3]) # bd
print("f" not in alpha) # True

print(min("aAbByYzZ")) # gives A because ACSII code point is is less

print("dsfds".index("d")) # index of the first occurrence of "d"-->0

# count() and list()
print(list("abcabc"))
print("abcabc".count("b"))
```


### `String methods`

```python

# capitalize()
print("Alpha".capitalize())
print('ALPHA'.capitalize())
print(' Alpha'.capitalize())
print('123'.capitalize())
print("αβγδ".capitalize(

# center()
print('[' + 'Beta'.center(2) + ']')
print('[' + 'Beta'.center(4) + ']')
print('[' + 'Beta'.center(6) + ']')
print('[' + 'gamma'.center(20, '*') + ']')

# endswith()
t = "zeta"
print(t.endswith("a"))
print(t.endswith("A"))
print(t.endswith("et"))
print(t.endswith("eta"))

# find() 
t = 'theta'
print(t.find('eta'))
print(t.find('et'))
print(t.find('the'))
print(t.find('ha'))
txt = """A variation of the ordinary lorem ipsum
text has been used in typesetting since the 1960s 
or earlier, when it was popularized by advertisements 
for Letraset transfer sheets. It was introduced to 
the Information Age in the mid-1980s by the Aldus Corporation, 
which employed it in graphics and word-processing templates
for its desktop publishing program PageMaker (from Wikipedia)"""

fnd = txt.find('the')
while fnd != -1:
    print(fnd)
    fnd = txt.find('the', fnd + 1)

print('kappa'.find('a', 1, 4)) # 1
print('kappa'.find('a', 2, 4)) # -1 

# isalnum()
t = 'Six lambdas'
print(t.isalnum()) # False 
t = 'ΑβΓδ'
print(t.isalnum()) # True
t = '20E1'
print(t.isalnum()) # True

# isalpha() and isdigit()

print("Moooo".isalpha()) # True
print('Mu40'.isalpha()) # False

print('2018'.isdigit()) # True
print("Year2019".isdigit()) # False

# join()
print(",".join(["omicron", "pi", "rho"]))

# lstrip()
print("[" + " tau ".lstrip() + "]") # [tau]
print("www.cisco.com".lstrip("w.")) # cisco.com
print("pythoninstitute.org".lstrip(".org")) # pythoninstitute.org

# replace()
print("www.netacad.com".replace("netacad.com", "pythoninstitute.org"))
print("This is it!".replace("is", "are"))
print("Apple juice".replace("juice", ""))
print("This is it!".replace("is", "are", 1))
print("This is it!".replace("is", "are", 2))


# my own split function
def mysplit(strng):
    if strng.isspace() or strng == '':
        return []
    a = []
    temp = ""
    for i in strng.strip():
        if not i.isspace():
            temp += i
        else: 
            a.append(temp)
            temp = ""
    a.append(temp)
    return a

print(mysplit("To be or not to be, this is a question"))
print(mysplit("To be or not to be,this is a question"))
print(mysplit("   "))
print(mysplit(" abc "))
print(mysplit(""))
```


### `String comparisons`

```python
'10' == 10 # False
'10' != 10 # True
'10' == 1 # Flase
'10' != 1 # True
'10' > 10 # TypeError exception
```