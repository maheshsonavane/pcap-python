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

### ``