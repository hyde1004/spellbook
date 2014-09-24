###### Reference : http://www.codecademy.com/tracks/python

#### Python Syntax

##### Multi-Line Comments
``` python
"""Sipping from your cup 'til it runneth over,
Holy Grail.
"""
```
#### Strings & Console Output

##### Escaping characters
``` python
'There\'s a snake in my boot!'
```
##### String methods
 - `len()`
 - `lower()`
 - `upper()`
 - `str()`

```python
"Ryan".lower()
"Ryan".upper()
str(3.14)
len("roar")
```
##### String Formatting with `%`
``` python
print "The %s who %s %s!" % ("Knights", "say", "Ni")
# This will print "The Knights who say Ni!"
```
#### Date and Time

##### Getting the Current Date and Time

``` python
from datetime import datetime

now = datetime.now()
print now
```
##### Extracting Information

``` python
from datetime import datetime
now = datetime.now()

current_year = now.year
current_month = now.month
current_day = now.day
```

##### Pretty Time

``` python
from datetime import datetime
now = datetime.now()

print '%s:%s:%s' % (now.hour, now.minute, now.second)
```
#### Conditionals & Control Flow

##### And
 - 1 < 2 `and` 2 < 3 is True
 - 1 < 2 `and` 2 > 3 is False

##### This and That (or This, But Not That!)
Boolean operators aren't just evaluated from left to right. Just like with arithmetic operators, there's an order of operations for boolean operators:
 - `not` is evaluated first
 - `and` is evaluated next
 - `or` is evaluated last

##### The Big If
``` python
if this_might_be_true():
    print "This really is true."
elif that_might_be_true():
    print "That is true."
else:
    print "None of the above."
```

#### PygLatin

##### Input!
``` python
name = raw_input("What's your name?")
print name
```

##### Check Yourself... Some More
``` python
x = "J123"
x.isalpha()  # False
```

#### Functions

##### Generic Imports 
``` python
# Ask Python to print sqrt(25) on line 3.
import math

print math.sqrt(25)
```

##### Function Imports
``` python
from module import function

print sqrt(25)
```

##### Universal Imports
``` python
from module import *
```

##### Here Be Dragons

``` python
import math            # Imports the math module
everything = dir(math) # Sets everything to a list of things from math
print everything       # Prints 'em all!
```

``` text
['__doc__', '__name__', '__package__', 'acos', 'acosh', 'asin', 'asinh', 'atan', 'atan2', 'atanh', 'ceil', 'copysign', 'cos', 'cosh', 'degrees', 'e', 'erf', 'erfc', 'exp', 'expm1', 'fabs', 'factorial', 'floor', 'fmod', 'frexp', 'fsum', 'gamma', 'hypot', 'isinf', 'isnan', 'ldexp', 'lgamma', 'log', 'log10', 'log1p', 'modf', 'pi', 'pow', 'radians', 'sin', 'sinh', 'sqrt', 'tan', 'tanh', 'trunc']
None
```

##### On Beyond Strings

``` python
def biggest_number(*args):
    print max(args)
    return max(args)
    
biggest_number(-10, -5, 5, 10)    
```

##### Built-in Functions

``` python
maximum = max(1, 1.1, -3.2)
print maximum

minimum = min(-100, 0, 44, 100.3)
print minimum

absolute = abs(-42)
print absolute

print type(4)     # <type 'int'>
print type(4.2)   # <type 'float'>
print type('hello') # <type 'str'>
```

#### Python Lists and Dictionaries

##### Introduction to Lists
Lists are a datatype you can use to store a collection of different pieces of information as a sequence under a single variable name.

##### Late Arrivals & List Length
``` python
letters = ['a', 'b', 'c']
letters.append('d')
print len(letters)
print letters
```

##### List Slicing
``` python
suitcase = ["sunglasses", "hat", "passport", "laptop", "suit", "shoes"]

first  = suitcase[0:2]  # The first and second items (index zero and one)
middle = suitcase[2:4]  # Third and fourth items (index two and three)
last   = suitcase[4:6]  # The last two items (index four and five)
```

##### Slicing Lists and Strings
``` python
animals = "catdogfrog"
cat  = animals[:3]   # The first three characters of animals
dog  = animals[3:6]              # The fourth through sixth characters
frog = animals[6:]              # From the seventh character to the end
```

##### Maintaining Order
``` python
animals = ["ant", "bat", "cat"]
print animals.index("bat")

animals.insert(1, "dog")
print animals
```

##### For One and All

``` python
my_list = [1,9,3,8,5,7]

for number in my_list:
    # Your code here
    print 2 * number
```

##### More with 'for'

``` python
animals = ["cat", "ant", "bat"]
animals.sort()

for animal in animals:
    print animal
```

##### This Next Part is Key

``` python
# Assigning a dictionary with three key-value pairs to residents:
residents = {'Puffin' : 104, 'Sloth' : 105, 'Burmese Python' : 106}

print residents['Puffin'] # Prints Puffin's room number

# Your code here!
print residents['Sloth']
print residents['Burmese Python']
```

##### New Entries
``` python
dict_name[new_key] = new_value
```

##### Changing Your Mind

``` python
del dict_name[key_name]

dict_name[key] = new_value
```

##### Remove a Few Things
``` python
beatles = ["john","paul","george","ringo","stuart"]
beatles.remove("stuart")
print beatles
>> ["john","paul","george","ringo"]
```

##### It's Dangerous to Go Alone! Take This
``` python
my_dict = {
    "fish": ["c", "a", "r", "p"],
    "cash": -4483,
    "luck": "good"
}
print my_dict["fish"][0]
```

#### A Day at the Supermarket
##### This is KEY!
``` python
# A simple dictionary
d = {"foo" : "bar"}

for key in d: 
    print d[key]  # prints "bar" 
```

#### Student Becomes the Teacher

##### Lesson Number One

``` python
animal_sounds = {
    "cat": ["meow", "purr"],
    "dog": ["woof", "bark"],
    "fox": [],
}
print animal_sounds["cat"]
```

#### Lists and Functions

##### Appending to a list
``` python
n = [1, 3, 5]
# Append the number 4 here
n.append(4)
```

##### Removing elements from lists
This exercise will expand on ways to remove items from a list. You actually have a few options. For a list called `n`:

1. `n.pop(index)` will remove the item at `index` from the list and return it to you:
``` python
n = [1, 3, 5]
n.pop(1)
# Returns 3 (the item at index 1)
print n
# prints [1, 5]
```
2. `n.remove(item)` will remove the actual `item` if it finds it:
``` python
n.remove(1)
# Removes 1 from the list,
# NOT the item at index 1
print n
# prints [3, 5]
```
3. `del(n[1])` is like `.pop` in that it will remove the item at the given index, but it won't return it:
``` python
del(n[1])
# Doesn't return anything
print n
# prints [1, 5]
```

##### Passing a range into a function
``` python
range(6) # => [0,1,2,3,4,5]
range(1,6) # => [1,2,3,4,5]
range(1,6,3) # => [1,4]
```

 - range(stop)
 - range(start, stop)
 - range(start, stop, step)

##### Iterating over a list in a function
Now that we've learned about `range`, we have two ways of iterating through a list.
 - Method 1 : ` for item in list`
``` python
for item in list:
    print item
```

 - Method 2 : iterate through indexes
 ``` python
 for i in range(len(list)):
    print list[i]
```

**Method 1** is useful to loop through the list, but it's not possible to modify the list this way. **Method 2** uses indexes to loop through the list, making it possible to also modify the list if needed. Since we aren't modifying the list, feel free to use either one on this lesson!

##### Using two lists as two arguments in a function
``` python
a = [1, 2, 3]
b = [4, 5, 6]
print a + b
# prints [1, 2, 3, 4, 5, 6]
```

#### Battleship!

##### Make a List
``` python
print ["O"] * 5
# prints ['O', 'O', 'O', 'O', 'O']
```
##### Printing Pretty
``` python 
letters = ['a', 'b', 'c', 'd']
print " ".join(letters)
print "---".join(letters)
```

##### Hide...
``` python
from random import randint
coin = randint(0, 1) # 0, 1
dice = randint(1, 6) # 1, 2, 3, 4, 5, 6
```

#### Loops

##### While / else
``` python
while condition:
    pass
else:
    pass 
```

##### For your strings
``` python
word = "eggs!"
for c in word:
    print c
```

##### Looping over a dictionary
``` python
d = {'x': 9, 'y': 10, 'z': 20}
for key in d:
    if d[key] == 10
        print "This dictionary has the value 10!"
```

##### Counting as you go
``` python
choices = ['pizza', 'pasta', 'salad', 'nachos']

print 'Your choices are:'
for index, item in enumerate(choices):
    print index + 1, item
```
##### Multiple lists
It's also common to need to iterate over two lists at once. This is where the built-in `zip` function comes in handy.

`zip` will create pairs of elements when passed two lists, and will stop at the end of the shorter list.

`zip` can handle three or more lists as well!

##### For / else
``` python
names = ['Hyde', 'Jack', 'Dorothy', 'Jane']

for name in names:
    print name
else:
    print "No more name"
```

#### Advanced Topics in Python

##### keys() and values()
``` python
my_dict = {
    "Name" : "Junggu Lee",
    "Company" : "LGE",
    "Age" : 41
}

print my_dict.keys()
print my_dict.values()
print my_dict.items()
```

##### The 'in' Operator
``` python
for number in range(5):
    print number,

d = { "name": "Eric", "age": 26 }
for key in d:
    print key, d[key],

for letter in "Eric":
    print letter,  # note the comma!
```

##### List Comprehension Syntax
``` python
new_list = [x for x in range(1,6)]
# => [1, 2, 3, 4, 5]

doubles = [x*2 for x in range(1,6)]
# => [2, 4, 6, 8, 10]

doubles_by_3 = [x*2 for x in range(1,6) if (x*2)%3 == 0]
# => [6]

```

##### List Slicing Syntax
``` python
[start:end:stride]
```

##### Reversing a List
``` python
letters = ['A', 'B', 'C', 'D', 'E']
print letters[::-1]
```

##### Anonymous Functions
See the `lambda` bit? Typing

``` python
lambda x: x % 3 == 0
```
Is the same as

``` python
def by_three(x):
    return x % 3 == 0
```

##### Lambda Syntax
``` python
my_list = range(16)
print filter(lambda x: x % 3 == 0, my_list)
```

##### Try it!
``` python
cubes = [x**3 for x in range(1, 11)]
filter(lambda x: x % 3 == 0, cubes)
```

#### Binary Representaion
##### Lesson 10:The Base 2 Number System
``` python
print 0b1,    #1
print 0b10,   #2
```

##### The bin() Function
 - `bin()` function
 - `oct()` function
 - `hex()` function

``` python
print bin(1)
print bin(2)
```

##### int()'s Second Parameter
``` python
int("42")
# ==> 42

int("110", 2)
# ==> 6
```

#### Introduction to Classes
##### Class Syntax
``` python
class NewClass(object):
    # Class magic here
    pass
```

##### Let's Not Get Too Selfish
``` python
class Animal(object):
    def __init__(self, name):
        self.name = name
```

##### Inheritance Syntax
``` python
class DerivedClass(BaseClass):
    # code goes here
```

##### Override!
``` python
class Employee(object):
    def __init__(self, name):
        self.name = name
    def greet(self, other):
        print "Hello, %s" % other.name

class CEO(Employee):
    def greet(self, other):
        print "Get back to work, %s!" % other.name

ceo = CEO("Emily")
emp = Employee("Steve")
emp.greet(ceo)
# Hello, Emily
ceo.greet(emp)
# Get back to work, Steve!
```

``` This Looks Like a Job For ...
``` python
class Derived(Base):
   def m(self):
       return super(Derived, self).m()
```

#### File Input/Output
##### See It to Believe It

``` python
my_list = [i**2 for i in range(1,11)]
# Generates a list of squares of the numbers 1 - 10

f = open("output.txt", "w")

for item in my_list:
    f.write(str(item) + "\n")

f.close()
```

##### Reading
``` python
my_file = open("output.txt", "r")
print my_file.read()
my_file.close()
```

##### Reading Between the Lines
``` python
my_file = open("text.txt", "r")

print my_file.readline()
print my_file.readline()
print my_file.readline()

my_file.close()
```

##### The 'with' and 'as' Keywords
Programming is all about getting the computer to do the work. Is there a way to get Python to automatically close our files for us?

Of course there is. This is Python.

You may not know this, but file objects contain a special pair of built-in methods: `__enter__()` and `__exit__()`. The details aren't important, but what is important is that when a file object's `__exit__()` method is invoked, it automatically closes the file. How do we invoke this method? With with and as.

The syntax looks like this:

``` python
with open("file", "mode") as variable:
    # Read or write to the file
```

``` python
with open("text.txt", "w") as textfile:
	textfile.write("Success!")
```

##### Case Closed?
``` python
f = open("bg.txt")
f.closed
# False
f.close()
f.closed
# True
```







