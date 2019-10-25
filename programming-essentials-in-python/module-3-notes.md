# Boolean

Operators Priority

![operators-priority-2](https://user-images.githubusercontent.com/45288730/67576636-f962f580-f74f-11e9-8783-e6fffaaecf83.JPG)

```python
# == operator
2 == 2 # returns True
2 == 2. # return True. python converts integer to 2 and compares.

# != operator
2 != 1 # returns True

# Comparison operators
ans = 2 > 4
print(ans) # returns False
```
# Conditions and conditional execution

```python

# code it in a more comprehensive form - if any of the if-elif-else branches contains just one instruction
if number1 > number2: larger_number = number1
else: larger_number = number2
```

# Loops

```python
# multi line printing
print(
"""
Hello
Mahesh
"""
)

# range() function for loops
range(100) # gives range from 0 to 99
range(2,8) # gives range from 2 to 7
range(2, 8, 3) # gives step range like 2, 5

# while loop and the else branch
i = 1
while i < 5:
    print(i)
    i += 1
else:
    print("else:", i)

# for loop and the else branch
for i in range(6):
    print(i)
else:
    print("else:", i)
```
