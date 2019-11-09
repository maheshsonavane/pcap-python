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

### `Constructor`:

- cannot return a value, as it is designed to return a newly created object and nothing else;
- cannot be invoked directly either from the object or from inside the class

```python
class Classy:
    def __init__(self, value):
        self.var = value

obj1 = Classy("object")

print(obj1.var)
```






`__init__(self,[optional parameters])`
`__str__(self)`
`issubclass(ClassOne, ClassTwo)`
- The function returns True if ClassOne is a subclass of ClassTwo, and False otherwise
- each class is considered to be a subclass of itself.

`isinstance(objectName, ClassName)`
- whether it is an object of a certain class or not.

`objectOne `is` objectTwo`

- operator checks whether two variables (objectOne and objectTwo here) refer to the same object.

`super().__init__(name)`

`Multiple inheritance`
- occurs when a class has more than one superclass
- Python looks for object components in the following order:
    - inside the object itself;
    - in its superclasses, `from bottom to top`
    - if there is more than one class on a particular inheritance path, Python scans them from `left to right`.

`polymorphism`

- situation in `which the subclass is able to modify its superclass behavior (just like in the example) is called polymorphism`
- The method, redefined in any of the superclasses, thus changing the behavior of the superclass, is called `virtual`.


# Generators 

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

- `yield`:
    - Turns the function into generator.

    ```python
    def fun(n):
        for i in range(n):
            yield i

    for v in fun(5):
        print(v)
    ```
    