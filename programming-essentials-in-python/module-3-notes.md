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
range(start, stop, step)
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
## `for i in range()` imp:

```python

presidents = ["Washington", "Adams", "Jefferson", "Madison", "Monroe", "Adams", "Jackson"]
for i in range(len(presidents)):
    
    print("President {}: {}".format(i + 1, presidents[i]))
    # modifying the value of counter variable has no impact.
    i = 5.0
    i = "dsfafds"

i = 0
while i < len(presidents):
    print("President {}: {}".format(i + 1, presidents[i]))
    i += 1
    # TypeError: '<' not supported between instances of 'str' and 'int'
    i = "sfaadfasd" 
```

# Lists

- `ordered and mutable collection` of comma-separated items between square bracket.
- can be `indexed and updated`
- can be `nested`
- List elements and lists can be `deleted`
- can be `iterated` through using the for loop
- `len()` function may be used to check the list's length.
- can test if some items exist in a list or not using the keywords `in` and `not in`

```python

# function
result = function(arg)

# method
result = data.method(arg)

# Adding elements to a list: append() and insert()
# append returns [1, 2, 3, 4, 5]
myList = [] # creating an empty list
for i in range(5):
    myList.append(i + 1)
print(myList)

# insert returns [5, 4, 3, 2, 1]
myList = [] # creating an empty list
for i in range(5):
    myList.insert(0, i + 1)
print(myList)

# reversing a list
number =  [1,2,3,4,5,6]
number[0], number[5] = number[5], number[0]
number[1], number[4] = number[4], number[1]
number[2], number[3] = number[3], number[2]
print(number)

number =  [1,2,3,4,5,6]
length = len(number)
for i in range(len(number)//2):
    number[i], number[length - 1 - i] = number[length - 1 - i], number[i]

print(number)

# sort() method to sort elements of a list
lst.sort()

# reverse() method to sort elements of a list
lst.reverse()
```
## `Inner life of list`

`list2 = list1`
- copies the name of the array, not its contents. In effect, the two names `(list1 and list2)` identify the same location in the computer memory. Modifying one of them affects the other, and vice versa.

## `Slicing`:
- to copy a list or part of the list, you can do it by performing `slicing`
- can use negative indices to perform slices

```python
myList = [10, 8, 6, 4, 2]
newList = myList[1:3]
print(newList)
# ---> output : [8, 6]
# The newList list will have end - start (3 - 1 = 2) elements 
# the ones with indices equal to 1 and 2 (but not 3).

# If the start specifies an element lying further than the one described by the end (from the list's beginning point of view), the slice will be empty
myList = [10, 8, 6, 4, 2]
newList = myList[-1:1]
print(newList)
# The snippet's output is: [].

# del contents of list
myList = [10, 8, 6, 4, 2]
del myList[:]
print(myList) # returns [].

# del whole list
myList = [10, 8, 6, 4, 2]
del myList
print(myList) # error
```
## `Reversing Lists and Strings`:

```python
str1 = "ABCDE"
print(str1[::-1])

l1 = [10,20,30,40]
print(l1[::-1])

# can specify start as well
str1 = "ABCDE"
print(str1[:2:-1]) # returns ED
```
## `Adding list ?`

![adding-list](https://user-images.githubusercontent.com/45288730/67631245-2d9ff880-f8ad-11e9-9af3-53c426e00216.JPG)

## `Swapping variables ?`

![swapping-variables](https://user-images.githubusercontent.com/45288730/67631244-2d076200-f8ad-11e9-8c54-6155f62d5ca3.JPG)

## `Sorting list ?`

![sorting list](https://user-images.githubusercontent.com/45288730/67631580-e10aec00-f8b1-11e9-8eae-9a562ad16151.JPG)

# Lists in Lists

```python

# One dimensional array
row = [WHITE_PAWN for i in range(8)]
squares = [x ** 2 for x in range(10)]
twos = [2 ** i for i in range(8)]
odds = [x for x in squares if x % 2 != 0 ]

# Two dimensional array
# The inner part creates a row, and the outer part builds a list of rows.
board = [[EMPTY for i in range(8)] for j in range(8)]
lst = [[c for c in range(r)] for r in range(3)]
# gives [[], [0], [0, 1]]

```