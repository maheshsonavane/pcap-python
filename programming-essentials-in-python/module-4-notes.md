# Functions

- Don't invoke a function which is not known at the moment of invocation. Python reads your code from `top to bottom`.<br>
    <b>Example:</b> below codes gives error `NameError: name 'message' is not defined`<br/><br/>
    ```python

    print("We start here.")
    message()
    print("We end here.")

    def message():
        print("Enter a value: ")
    ```
- You mustn't have a function and a variable of the same name.<br/>
    <b>Example:</b> Assigning a value to the name `message` causes Python to forget its previous role. The function named `message` becomes unavailable.<br/><br/>
    
    ```python
    def message():
        print("Enter a value: ")

    message = 1
    ```
- You're free to `mix your code with functions` - you're not obliged to put all your functions at the top of your source file.<br/>
    <b>Example:</b> Below code is valid
    ```python
    print("We start here.")

    def message():
        print("Enter a value: ")

    message()

    print("We end here.")
    ```
- Types of functions:
    - built-in functions 
    - functions from `pre-installed modules`
    - user-defined functions
    - `[lambda]` functions

# Parameterized Functions

- `parameters` live inside functions (this is their natural environment)
- `arguments` exist outside functions, and are carriers of values passed to corresponding parameters.
- Mixing positional and keyword arguments is allowed but `positional arguments mustn't follow keyword arguments.`<br/><br/>

    <b>Example:</b><br/><br/>
    ```python
    def subtra(a, b):
    print(a - b)

    subtra(5, b=2)    # outputs: 3
    subtra(a=5, 2)    # Syntax Error
    ```

## `shadowing mechanism:`

- It's legal, and possible, to have a variable named the same as a function's parameter.<br/>
<b>Example:</b> <br/><br/>
    ```python
    def message(number):
        print("Enter a number:", number)

    number = 1234
    message(1)
    print(number)
    ```
    - A situation like this activates a mechanism called shadowing:
        - parameter x shadows any variable of the same name, but...
        - ... only inside the function defining the parameter.

# Returning a result from a function

##  `return:`
- `return` without an expression
    - immediate termination of the function's execution, and an instant return (hence the name) to the point of invocation.
- `return` with an expression
    1. immediate termination of the function's execution.
    2. evaluate the expression's value and will return (hence the name once again) it as the function's result.

- function returns a value, and we ignore it. we are allowed to ignore the function's result.
    <b>Example</b>
    ```python
    def boringFunction():
        print("'Boredom Mode' ON.")
        return 123

    print("This lesson is interesting!)
    boringFunction()
    print("This lesson is boring...")
    ```
- if a function doesn't return a certain value using a return expression clause, it is assumed that it implicitly returns `None`.

# Scopes in Python

## `local`:
- A variable that exists outside a function has a scope inside the function body (Example 1) unless the function defines a variable of the same name.
<b>Example</b><br/><br/>
    ```python
    var = 2

    def multByVar(x):
        return x * var

    print(multByVar(7))    # outputs: 14
    ```
## `global`:

- Using this keyword `inside a function` with the name (or names separated with commas) of a variable(s), forces Python to refrain from creating a new variable inside the function - the one accessible from outside will be used instead. <br/><br/>
    ```python
    def myFunction():
        global var
        var = 2
        print("Do I know that variable?", var)

    var = 5
    myFunction()
    print(var)
    ```
## `function interaction with its arguments`:
- changing the parameter's value doesn't propagate outside the function. function receives the `argument's value`, not the `argument` itself. This is true for `scalars`.
    <b>Example</b><br/><br/>
    ```python
    def myFunction(n):
        print("I got", n)
        n += 1
        print("I have", n)

    var = 1
    myFunction(var)
    print(var)
    ```
- if the argument is a `list`, then changing the value of the corresponding parameter doesn't affect the list.
    <b>Example</b><br/><br/>
    ```python
    def myFunction(myList1):
        print(myList1)
        myList1 = [0, 1]

    myList2 = [2, 3]
    myFunction(myList2)
    print(myList2)
    ```
    Output:

    ```
    [2, 3]
    [2, 3]
    ```
- if you change a list identified by the parameter `(note: the list, not the parameter!)`, the list will reflect the change.
    <b>Example</b><br/><br/>
    ```python
    def myFunction(myList1):
        print(myList1)
        del myList1[0]

    myList2 = [2, 3]
    myFunction(myList2)
    print(myList2)
    ```
    Output:

    ```
    [2, 3]
    [3]
    ```
# Tuples -immutable sequence type

- the `len()` function accepts tuples, and returns the number of elements contained inside;
- the `+` operator can join tuples together
- the `*` operator can multiply tuples, just like lists;
- the `in` and `not in` operators work in the same way as in lists.
- tuple's elements can be `variables`, not only `literals`. Moreover, they can be `expressions` if they're on the right side of the assignment operator.<br/><br/>

    ```python
    # creating tuples
    tuple1 = (1, 2, 4, 8)
    tuple2 = 1., .5, .25, .125
    emptyTuple = ()
    oneElementTuple1 = (1, )
    oneElementTuple2 = 1.,  # comma is imp
    ```
# Dictionary

- not a `sequence type` (but can be easily adapted to sequence processing) and it is `mutable`.
- each key must be `unique` - it's not possible to have more than one key of the same value;
- keys are case-sensitive
- a key may be data of `any type`: it may be a number (integer or float), or even a string;
- the `len()` function works for dictionaries, too - it returns the numbers of key-value elements in the dictionary;
- a dictionary is a `one-way tool` - if you have an English-French dictionary, you can look for French equivalents of English terms, but not vice versa.
- dictionaries are not lists - they `don't preserve the order of their data`.
- In Python 3.6x dictionaries have become ordered collections by default.
- The order in which a dictionary stores its data is completely out of your control.

## `Browsing Dictionaries`

- `keys()`: returns a list built of all the keys gathered within the dictionary. <br/><br/>

    ```python
    dict = {"cat" : "chat", "dog" : "chien", "horse" : "cheval"}

    for key in dict.keys():
        print(key, "->", dict[key]
    ```
- `items()`: returns a list of tuples where each tuple is a key-value pair. <br/><br/>

    ```python
    dict = {"cat" : "chat", "dog" : "chien", "horse" : "cheval"}

    for english, french in dict.items():
        print(english, "->", french)
    ```
- `values()`: returns a list of values. <br/><br/>

    ```python
    dict = {"cat" : "chat", "dog" : "chien", "horse" : "cheval"}

    for french in dict.values():
        print(french)
    ```

## `modifying and adding values`

```python

# modify value of key
dict = {"cat" : "chat", "dog" : "chien", "horse" : "cheval"}
dict['cat'] = 'minou'
print(dict)

# add new key
dict = {"cat" : "chat", "dog" : "chien", "horse" : "cheval"}
dict['swan'] = 'cygne'
print(dict)

# remove key
dict = {"cat" : "chat", "dog" : "chien", "horse" : "cheval"}
del dict['dog']
print(dict)

# remove the last item in a dictionary
dict = {"cat" : "chat", "dog" : "chien", "horse" : "cheval"}
dict.popitem()
print(dict)    # outputs: {'cat' : 'chat', 'dog' : 'chien'}

# samples - copy vs assignment
a = {1:'one',2:'two',3:'threw'}
b = a # assignment
b.popitem()
print(b)
print(a)

a = {1:'one',2:'two',3:'threw'}
b = a.copy() # copy
b.popitem()
print(b)
print(a)
```

`note` - In the older versions of Python, i.e., before 3.6.7, the `popitem()` method removes a random item from a dictionary.

# Extra:

- `tuple()` function: You can also create a tuple using a Python built-in function called tuple(). This is particularly useful when you want to convert a certain iterable (e.g., a list, range, string, etc.) to a tuple
- `list() function: By the same fashion, when you want to convert an iterable to a list, you can use a Python built-in function called list()
