# Literals

Types of literals:
- string literal - `print("2")` 
- numerical literal - integer - `print(2)`
- numerical literal - float - `print(2.0)`
- boolean literal - `print(True)`
- None literal - `print(None)`
```python

# integer literals
print(type(11111111)) # integer literal
print(type(11_111_111)) # integer literal introduced in Python 3.6

# integers - octal and hexadecimal numbers
print(0o123) # octal starts with 0o
print(0x123) # hex starts with 0x

# float literal
print(4.0)  
print(4.) 
print(0.4)
print(.4) 
print(3e10) # scientific notation
print(type(3E10)) # one more way to declare float
print(0.0000000000000000000001) # 1e-22 # till 3 zeros e.g. 0.0001

# String literal
print('I am "Mahesh Sonavane"') # using single quotes
print("I am \"Mahesh Sonavane\"") # using escape character

# Boolean literal
print(True > False) # returns True
print(True < False) # returns False
print(type(True)) # returns <class 'bool'>

# None literal. 
print(None) # used to represent the absence of a value. 
print(type(None)) # returns <class 'NoneType'>
```
# Operators

Operators Priority

![operators-priority](https://user-images.githubusercontent.com/45288730/67143194-e21c9780-f279-11e9-85ef-4baec185d605.JPG)

```python
print(2 ** 3) # exponentiation (power) operator
print(2 * 3) # multiplication operator
print(6 / 2) # division operator - result is always float.
'''
 integer division / floor division
    - the results are always rounded to lesser integer.
    - integer by integer division gives an integer result.  
    - All other cases produce floats.
'''
print(6 // 2) 
print(6. // -4) # returns -2.0 
print(6 // 4) # returns 1.0 

print(12 % 4.5) # remainder (modulo) operator gives 3.0
'''
How modulo operator works? 
    a. 12 // 4.5 gives 2.0; 
    b. 2.0 * 4.5 gives 9.0; 
    c. 12 - 9.0 gives 3.0
'''
print(-4 + 4) # addition gives 0
print(-4. + 8) # addition gives 4.0
print(-4 - 4) # subtraction gives -8
print(4. - 8) # subtraction gives -4.0
print(9 % 6 % 2) # left - sided binding gives result 1
print(2 ** 2 ** 3) # 256 - exponentiation operator uses right-sided binding.
```

# Variables

```python

# Python is case-sensitive
Import=10 # valid variable name import vs Import 
Adiós_Señora="d" # valid. can contain latin letters.

10t=110 # invalid. should not begin with letter.
Ex Rate=19.20 # invalid. should not contain space.
```

# Talk to Computer

## `input():` 
- result of the input() function is a `string`.

```python
print("Enter Value = ")
var  = input()
var  = input("Enter Value")

# Type casting
anything = float(input("Enter a number: "))
# or
anything = int(input("Enter a number: "))
something = anything ** 2.0
```
## `String comparisons`

- We can use ( > , < , <= , <= , == , !=  ) to compare two strings. Python compares string lexicographically i.e using ASCII value of the characters.

<b>Example</b>
Suppose you have `str1` as `"Mary"`  and `str2` as `"Mac"`. The first two characters from `str1`  and `str2` ( M and M ) are compared. As they are equal, the second two characters are compared. Because they are also equal, the third two characters (r and c ) are compared. And because r has greater ASCII value than c , `str1` is greater than `str2`.

<b>ASCII Table:</b>

- `0-9` is `048 to 057`
- `A-Z` is `65 to 90`
- `a-z` is `097 to 122`

## `String opertors:`

```python

# Concatenation (string + string)
a = "mahesh" + "sonavane"

''' 
Replication :
    string * number 
    number * string
'''
a = "mahesh" * 2
```
## `Type Conversion:`

```python
# int()
A = int(input("Enter Value for A"))
# float()
B = float(input("Enter Value for B"))
# str()
print("b = "+ str(B))
```
