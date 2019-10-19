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
print(0.0000000000000000000001) # 1e-22

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
