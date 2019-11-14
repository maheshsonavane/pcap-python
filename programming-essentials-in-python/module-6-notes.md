# Class

Public and Private properties

- When any class component has a name starting with two underscores `(__)`, it becomes `private` - this means that it can be accessed only from within the class.

```python
# public
class Stack:
    def __init__(self):
        self.stackList = []

stackObject = Stack()
print(len(stackObject.stackList)) # returns 0



# private
class Stack:
    def __init__(self):
        self.__stackList = []

stackObject = Stack()
print(len(stackObject.__stackList)) # AttributeError: 'Stack' 
```

Subclass
- define a new subclass pointing to the class which will be used as the superclass.

```python
class AddingStack(Stack):
    pass
```

### `Overriding`


```python
class Stack:
    def __init__(self):
        self.__stackList = []

    def push(self, val):
        self.__stackList.append(val)

    def pop(self):
        val = self.__stackList[-1]
        del self.__stackList[-1]
        return val


class AddingStack(Stack):
    def __init__(self):
        Stack.__init__(self)
        self.__sum = 0

    def getSum(self):
        return self.__sum

    def push(self, val):
        self.__sum += val
        Stack.push(self, val)

    def pop(self):
        val = Stack.pop(self)
        self.__sum -= val
        return val


stackObject = AddingStack()
for i in range(5):
    stackObject.push(i)
print(stackObject.getSum())

for i in range(5):
    print(stackObject.pop())
```

# OOP Properties

### `Instance Variables`:

- modifying an instance variable of any object has no impact on all the remaining objects. 
- Instance variables are perfectly isolated from each other.

```python
class ExampleClass:
    def __init__(self, val = 1):
        self.first = val

    def setSecond(self, val):
        self.second = val


exampleObject1 = ExampleClass()
exampleObject2 = ExampleClass(2)

exampleObject2.setSecond(3)

exampleObject3 = ExampleClass(4)
exampleObject3.third = 5 
# exampleObject3 has been enriched with a property named third just on the fly, outside the class's code 
# this is possible and fully permissible.


print(exampleObject1.__dict__)
print(exampleObject2.__dict__)
print(exampleObject3.__dict__)

# Output
{'first': 1}
{'second': 3, 'first': 2}
{'third': 5, 'first': 4}

```

### `Class Variables`:

- a property which exists in just one copy and is stored outside any object.
- class variables aren't shown in an object's `__dict__` 
- Accessed using class name and dot notation i.e. `ExampleClass.__counter += 1`
- class variables exist even when no class instance (object) had been created.

```python
class ExampleClass:
    counter = 0 
    def __init__(self, val = 1):
        self.__first = val
        ExampleClass.counter += 1

exampleObject1 = ExampleClass()
exampleObject2 = ExampleClass(2)
exampleObject3 = ExampleClass(4)

print(exampleObject1.__dict__, exampleObject1.counter)
print(exampleObject2.__dict__, exampleObject2.counter)
print(exampleObject3.__dict__, exampleObject3.counter)

# Output
{'_ExampleClass__first': 1} 3
{'_ExampleClass__first': 2} 3
{'_ExampleClass__first': 4} 3
```

### `hasattr`
- function which is able to safely check if any object/class contains a specified property.
- can operate on classes too.

```python
class ExampleClass:
    def __init__(self, val):
        if val % 2 != 0:
            self.a = 1
        else:
            self.b = 1

exampleObject = ExampleClass(1)
print(exampleObject.a)

if hasattr(exampleObject, 'b'):
    print(exampleObject.b)


# operating on class

class ExampleClass:
    a = 1
    def __init__(self):
        self.b = 2

exampleObject = ExampleClass()

print(hasattr(exampleObject, 'b')) # True
print(hasattr(exampleObject, 'a')) # True
print(hasattr(ExampleClass, 'b')) # False
print(hasattr(ExampleClass, 'a')) # True
```
# OOP: Methods

## `Constructor`:

- cannot return a value, as it is designed to return a newly created object and nothing else;
- cannot be invoked directly either from the object or from inside the class

```python
class Classy:
    def __init__(self, value):
        self.var = value

obj1 = Classy("object")

print(obj1.var)
```

## `Key methods`

`__str__()` 
- describe s the object by returning string

`issubclass(ClassOne, ClassTwo)`
- The function returns True if ClassOne is a subclass of ClassTwo, and False otherwise
- each class is considered to be a subclass of itself.

`isinstance(objectName, ClassName)`
- whether it is an object of a certain class or not.
- objects can be considered as instance of all superclasses.

`objectOne `is` objectTwo`
- operator checks whether two variables (objectOne and objectTwo here) refer to the same object.

`super().__init__()` vs `ClassName.__init__(self)`


## `Class Methods`:

- must have `(self)` parameter.
- calling a private function:
    ```python
    obj = Classy()    
    obj._Classy__hidden()
    ```
- abstract method

    ![abstract-class](https://user-images.githubusercontent.com/45288730/68864154-11ec7d00-070a-11ea-8dae-802423065d54.PNG)


## `Built in Properties`:
- `__name__`
- `__dict__`
- `__module__`
- `__bases__`

### `Reflection & Introspection`
- `getattr(ObjectName,property)`
- `setattr(ObjectName,property,value)`

## `Inheritance`
- `Single inheritance`
    - simple
    - can be multi-level
- `Multiple inheritance`
    - <b>Diamond</b> problem may cause `MRO` (Method Resolution Error)
    - Subclass has more than one Super classes.
    - Python looks for object components in the following order:
        - inside the object itself;
        - in its superclasses, `from bottom to top`
        - if there is more than one class on a particular inheritance path, Python scans them from `left to right`.

- `Object composition`
    - Preferred over multiple inheritance.
    - `polymorphism` can be achieved better.
    - One Super class is used by more than one sub class.

`polymorphism`

- situation in `which the subclass is able to modify its superclass behavior (just like in the example) is called polymorphism`
- The method, redefined in any of the superclasses, thus changing the behavior of the superclass, is called `virtual`.

# Exceptions:

## `else` block:

- code labelled in this way is executed when (and only when) no exception has been raised inside the `try:` part.
    ```python
    def reciprocal(n):
        try:
            n = 1 / n
        except ZeroDivisionError:
            print("Division failed")
            return None
        else:
            print("Everything went fine")
            return n

    print(reciprocal(2))
    print(reciprocal(0))

    # Outputs
    Everything went fine
    0.5
    Division failed
    None
    ```

## `finally` block:

- always executed 

    ```python
    def reciprocal(n):
        try:
            n = 1 / n
        except ZeroDivisionError:
            print("Division failed")
            n = None
        else:
            print("Everything went fine")
        finally:
            print("It's time to say goodbye")
            return n

    print(reciprocal(2))
    print(reciprocal(0))

    # Outputs
    Everything went fine
    It's time to say good bye
    0.5
    Division failed
    It's time to say good bye
    None
    ```

## `args` property:

- property of `BaseException` class
- tuple designed to gather all arguments passed to the class constructor.
- don't count the `self` argument here.

    ```python
    try:
        raise Exception
    except Exception as e:
        print(e, e.__str__(), sep=' : ' ,end=' : ')
        print(e.args)

    try:
        raise Exception("my exception")
    except Exception as e:
        print(e, e.__str__(), sep=' : ', end=' : ')
        print(e.args)

    try:
        raise Exception("my", "exception")
    except Exception as e:
        print(e, e.__str__(), sep=' : ', end=' : ')
        print(e.args)
    
    #Output
     :  : ()
    my exception : my exception : ('my exception',)
    ('my', 'exception') : ('my', 'exception') : ('my', 'exception')
    ```

## `User Defined Exceptions`
- Created by defining your own, new exceptions as subclasses derived from predefined ones. 
- If you want to create an exception which will be utilized as a specialized case of any built-in exception, derive it from just this one. 

- If you want to build your own hierarchy, and don't want it to be closely connected to Python's exception tree, derive it from any of the top exception classes, like Exception

    ```python
    class PizzaError(Exception):
        def __init__(self, pizza, message):
            Exception.__init__(self, message)
            self.pizza = pizza


    class TooMuchCheeseError(PizzaError):
        def __init__(self, pizza, cheese, message):
            PizzaError.__init__(self, pizza, message)
            self.cheese = cheese

    def makePizza(pizza, cheese):
        if pizza not in ['margherita', 'capricciosa', 'calzone']:
            raise PizzaError(pizza, "no such pizza on the menu")
        if cheese > 100:
            raise TooMuchCheeseError(pizza, cheese, "too much cheese")
        print("Pizza ready!")


    for (pz, ch) in [('calzone', 0), ('margherita', 110), ('mafia', 20)]:
        try:
            makePizza(pz, ch)
        except TooMuchCheeseError as tmce:
            print(tmce, ':', tmce.cheese)
        except PizzaError as pe:
            print(pe, ':', pe.pizza)
    ```
# Generators / Iterators

- piece of specialized code able to produce a series of values, and to control the iteration process.

- iterator must provide two methods:
    - `__iter__()` which should return the object itself and which is invoked once.
    - `__next__()` which is intended to return the next value (first, second, and so on) of the desired series - it will be invoked by the for/in statements in order to pass through the next iteration; if there are no more values to provide, the method should raise the `StopIteration` exception.<br/><br/>

    ```python
    class Mahesh:
        def __init__(self, nn):
            #print("__init__")
            self.__n = nn
            self.__i = 0
            self.__p1 = self.__p2 = 1

        def __iter__(self):
            #print("__iter__")		
            return self

        def __next__(self):
            #print("__next__")				
            self.__i += 1
            if self.__i > self.__n:
                raise StopIteration
            if self.__i in [1, 2]:
                return 1
            ret = self.__p1 + self.__p2
            self.__p1, self.__p2 = self.__p2, ret
            return ret

    for i in Mahesh(10):
        print(i,sep=" ")
    ```

## `yield`:
- Turns the function into generator.
- function should not be invoked explicitly

    ```python
    def fun(n):
        for i in range(n):
            yield i

    for v in fun(5):
        print(v)
    ```

## `list comprehensions`:
```python
listOne = []

for ex in range(6):
    listOne.append(10 ** ex)


listTwo = [10 ** ex for ex in range(6)]

print(listOne)
print(listTwo)

## Outputs
[1, 10, 100, 1000, 10000, 100000]
[1, 10, 100, 1000, 10000, 100000]

## Example 2 - conditional instruction
lst = []

for x in range(10):
    lst.append(1 if x % 2 == 0 else 0)

print(lst)

lst2 = [1 if x % 2 ==0 else 0 for x in range(10)]
print(lst2)
## Outputs
[1, 0, 1, 0, 1, 0, 1, 0, 1, 0]
[1, 0, 1, 0, 1, 0, 1, 0, 1, 0]
```
## `turn any comprehension into a generator`:

- turn any comprehension into a generator.
- `[]` The brackets make a `comprehension`.
- `()` The parentheses make a `generator`.

    ```python
    lst = [1 if x % 2 == 0 else 0 for x in range(10)]
    genr = (1 if x % 2 == 0 else 0 for x in range(10))

    for v in lst:
        print(v, end=" ")
    print()

    for v in genr:
        print(v, end=" ")
    print()
    ```
## `lambda` - an anonymous function

`lambda parameters : expression`

    ```python
    two = lambda : 2 # anonymous parameterless function
    sqr = lambda x : x * x # one-parameter anonymous function
    pwr = lambda x, y : x ** y # takes two parameters

    for a in range(-2, 3):
        print(sqr(a), end=" ")
        print(pwr(a, two()))
    ```

`Whats the benefit`

![lambda functions2](https://user-images.githubusercontent.com/45288730/68836958-f9ae3b00-06d4-11ea-9484-d920557712f5.PNG)

`map(function, list)`

`map()` function applies the function passed by its first argument to all its second argument's elements, and returns an `iterator` delivering all subsequent function results.

- the second argument `list` may be any entity that can be iterated (e.g., a tuple, or just a generator)
- `map()` can accept more than two arguments.
    ```python
    list1 = [x for x in range(5)]
    list2 = list(map(lambda x: 2 ** x, list1))
    print(list2)
    for x in map(lambda x: x * x, list2):
        print(x, end=' ')
    print()
    ``` 
`filter()`

`filter()` function filters its second argument while being guided by directions flowing from the function specified as the first argument.

The elements which return `True` from the function pass the filter - the others are rejected.

```python
from random import seed, randint
seed()
data = [ randint(-10,10) for x in range(5) ]
filtered = list(filter(lambda x: x > 0 and x % 2 == 0, data))
print(data)
print(filtered)

# Output
[0, -5, -7, -10, 10]
[10]
``` 

## `closures`

- closure is a technique which allows the storing of values in spite of the fact that the context in which they have been created does not exist anymore
- Example - The function returned during the `outer()` invocation is a closure.

    ```python
    def outer(par):
        loc = par
        def inner():
            return loc
        return inner

    var = 1
    fun = outer(var)
    print(fun())

    ## Ex 2 - A closure has to be invoked in exactly the same way in which it has been declared
    
    def makeclosure(par):
        loc = par
        def power(p):
            return p ** loc
        return power

    fsqr = makeclosure(2)
    fcub = makeclosure(3)
    for i in range(5):
        print(i, fsqr(i), fcub(i))
    ```
# Files

```python
#windows only with escape character
name = "\\dir\\file" 
#windows + linux
name = "/dir/file" 
name = "/dir/file"
name = "c:/dir/file"
```


## `File Streams`

- default mode is `rt`.<br/><br/>

    ![modes](https://user-images.githubusercontent.com/45288730/68545849-734edc00-03ea-11ea-9f1f-c07212477e3c.JPG)

- `rt` - read 
  - the file must exist and readable.
- `wt` - write
    - if file doesn't exist it will be created 
    - if it exists, it will be truncated. (erased)
- `a` - append

    - if file doesn't exist, it will be created; 
    - if it exists the `file pointer` i.e virtual recording head will be set at the end of the file.
- `r+` - read and update
    - file must exist and has to be writeable.
    - both `read and write` operations are allowed for the stream.

- `w+` - write and update
    - if file doesn't exist, it will be created
    - the previous content of the file remains untouched;
    - both `read and write` operations are allowed for the stream.

- `x` - exclusive creation.
    - If the file already exists, the open() function will raise an exception.
    - You can also open a file for its exclusive creation

- `UnsupportedOperation`, which inherits `OSError` and `ValueError`, and comes from the `io` module.




## `bytearray`:

- Amorphous data is data which have no specific shape or form - they are just a series of bytes.
- specialized class Python uses to store amorphous data.
- mutable, 
- they're a subject of the len() function, 
- conventional indexing is possible
- `IMP` - you mustn't set any byte array elements with a value which is not an integer. violating this rule will cause a `TypeError` exception.
- not allowed to assign a value that doesn't come from the range `0` to `255` inclusive.
- 
```python
data = bytearray(100) # bytearray object able to store ten bytes.


data = bytearray(10)
print(data) # bytearray(b'\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00')
print(len(data)) #10
```
### `writing byetarray to file`

- The `write()` method returns a number of successfully written bytes.
    ```python
    from os import strerror
    data = bytearray(10)
    try:
        bf = open('file.bin', 'wb')
        bf.write(data)
        bf.close()
    except IOError as e:
        print("I/O error occurred:", strerr(e.errno))
    ```
### `readinto(b)` - read bytes from a stream
- Read bytes into a pre-allocated, writable bytes-like object b, and return the number of bytes read.

    ```python
    from os import strerror

    data = bytearray(10)

    try:
        bf = open('file.bin', 'rb')
        bf.readinto(data)
        bf.close()

        for b in data:
            print(hex(b), end=' ')
    except IOError as e:
        print("I/O error occurred:", strerr(e.errno))
    ```
### `read()` - read bytes from a stream
- Read all the contents of the file into the `memory.`
- don't use this kind of read if you're not sure that the file's contents will fit the available memory.


    ```python
    from os import strerror

    try:
        bf = open('file.bin', 'rb')
        data = bytearray(bf.read())
        bf.close()

        for b in data:
            print(hex(b), end=' ')

    except IOError as e:
        print("I/O error occurred:", strerr(e.errno))
    ```
### `read(n)` - read bytes from a stream
- If the read() method is invoked with an argument, it specifies the maximum number of bytes to be read.


    ```python
    try:
        bf = open('file.bin', 'rb')
        data = bytearray(bf.read(5))
        bf.close()

        for b in data:
            print(hex(b), end=' ')

    except IOError as e:
        print("I/O error occurred:", strerr(e.errno))
    ```

# Tasks

### `Character frequency histogram`:

Read file and count characters

```python
a -> 1
b -> 2
c -> 1
```
### `Character frequency histogram`:

Read file and count characters

```python
a -> 1
b -> 2
c -> 1
```


### Marks 

Read file and show marks for stduents

sample input file

```python

John	Smith	5
Anna	Boleyn	4.5
John	Smith	2
Anna	Boleyn	11
Andrew	Cox	1.5
```

sample output file

```python
Andrew Cox 	 1.5
Anna Boleyn 	 15.5
John Smith 	 7.0
```