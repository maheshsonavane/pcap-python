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