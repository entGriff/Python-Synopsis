# Datatype & Variables

Variables are named locations which are used to store references to the object stored in memory. The names we choose for variables and functions are commonly known as Identifiers. In python Identifiers must obey the following rules.

 1. All identifiers must start with letter or underscore ( _ ) , you
    can’t use digits. For e.g my_var  is valid identifier while 1digit 
    is not.
 2. Identifiers can contain letters, digits and underscores ( _  ). 
 3. They  can be of any length.
 4. Identifier can’t be a keyword (keywords are reserved words that
    Python uses for special purpose).Following are Keywords in python 3.
    
    []()  | []() | []() 
------|------|------
**and** | **exec**| **not**
**as**| **finally**| **or**
**assert**| **for**	| **pass**
**break**| **from**| **print**
**class**| **global**| **raise**
**continue**| **if**| **return**
**def**| **import**| **try**
**del**| **in**| **while**
**elif**| **is**| **with**
**else**| **lambda**| **yield**
**except**|


## Assigning Values to Variables

Values are basic things that programs works with. For e.g 1 , 11 , 3.14 , "hello"  are all values. In programming terminology they are also commonly known as literals. Literals can be of different type for e.g 1 , 11  are of type int , 3.14  is float and "hello"  is string . Remember in python everything is object even basic data types like int, float, string, we will elaborate more on this in later chapters.

In python you don’t need to declare types of variable ahead of time. Interpreter automatically detects the type of the variable by the data it contains. To assign value to a variable equal sign ( = ) is used. =  is also known as assignment operator.

Following are some examples of variable declaration:

```python	
x = 100                       # x is integer
pi = 3.14                     # pi is float
empname = "python is great"   # empname is string
 
a = b = c = 100 # this statement assign 100 to c, b and a.
```
> **Note:**
In the above code x  stores reference to the 100  ( which is an int object ) , x  don’t store 100 itself.

In Python comments are preceded by a pound sign ( # ). Comments are not programming statements that python interpreter executes while running the program. Comments are used by programmers to remind themselves how the program works. They are also used to write program documentation.


```python	
#display hello world
print("hello world")
```

###  Simultaneous Assignments
Python allow simultaneous assignment syntax like this:
  
```python	
var1, var2, ..., varn = exp1, exp2, ..., expn
```
this statements tells the python to evaluate all the expression on the right and assign them to the corresponding variables on the left. Simultaneous Assignments is helpful to swap values of two variables. For e.g
```python	
>>> x = 1
>>> y = 2
 
>>> y, x = x, y # assign y value to x and x value to y
```

## Python Data Types
Python has 5 standard data types namely.
a) [Numbers](http://thepythonguru.com/python-numbers/)
b) [String](http://thepythonguru.com/python-strings/)
c)  [List](http://thepythonguru.com/python-lists/)
d) [Tuple](http://thepythonguru.com/python-tuples/)
e) [Dictionary](http://thepythonguru.com/python-dictionaries/)
f)  Boolean – In Python True and False  are boolean literals.  But the following values are also considered as false.

**[] – empty list , () – empty tuple , {} – empty dictionary** 


## Receiving input from Console
input()  function is used to receive input from the console.

Syntax:  input([prompt]) -> string

input()  function accepts an optional string argument called prompt  and returns a string.
```python	
>>> name = input("Enter your name: ")
>>> Enter your name: tim
>>> name
'tim'
```
Note that input()  returns string even if you enter a number, to convert it to an integer you can use int() or eval() .

```python	
>> age = int(input("Enter your age: "))
Enter your age: 22
>>> age
22
>>> type(age)
<class 'int'>
```






> **Source:**   
> :fa-link: http://thepythonguru.com



## Understanding Python variables and Memory Management

Have you ever noticed any difference between variables in Python and C? For example, when you do an assignment like the following in C, it actually creates a block of memory space so that it can hold the value for that variable

```c	
int a = 1;
```

You can think of it as putting the value assigned in a box with the variable name as shown below.
![a1box.](../images/a1box.PNG)

And for all the variables you create a new box is created with the variable name to hold the value. If you change the value of the variable the box will be updated with the new value. That means doing

```c	
a = 2;
```
will result in

![a2box.](../images/a2box.PNG)


Assigning one variable to another makes a copy of the value and put that value in the new box.
```c	
int b = a;
```
![b2box.](../images/b2box.PNG) ![a2box.](../images/a2box.PNG)

But in Python variables work more like tags unlike the boxes you have seen before. When you do an assignment in Python, it tags the value with the variable name.
```python	
a = 1
```
![a1tag.](../images/a1tag.PNG)

and if you change the value of the varaible, it just changes the tag to the new value in memory. You dont need to do the housekeeping job of freeing the memory here. Python's Automatic Garbage Collection does it for you. When a value is without names/tags it is automatically removed from memory.

```python	
a = 2
```
![a2tag.](../images/a2tag.PNG)

Assigning one variable to another makes a new tag bound to the same value as show below.

```python	
b = a
```
![ab2tag.](../images/ab2tag.PNG)
Other languages have 'variables'. Python has 'names'.

## A bit about Python's memory management

As you have seen before, a value will have only one copy in memory and all the variables having this value will refer to this memory location. For example when you have variables a, b, c having a value 10, it doesn't mean that there will be 3 copy of 10s in memory. There will be only one 10 and all the variables a, b, c will point to this value. Once a variable is updated, say you are doing a += 1 a new value 11 will be allocated in memory and a will be pointing to this.

Let's check this behaviour with Python Interpreter. Start the Python Shell and try the following for yourselves.

```python	
>>> a = 10
>>> b = 10
>>> c = 10
>>> id(a), id(b), id(c)
(140621897573616, 140621897573616, 140621897573616)
>>> a += 1
>>> id(a)
140621897573592
```

id() will return an objects memory address (object's identity). As you have noticed, when you assign the same integer value to the variables, we see the same ids. But this assumption does not hold true all the time. See the following for example

```python	
>>> x = 500
>>> y = 500
>>> id(x)
4338740848
>>> id(y)
4338741040
```
What happened here? Even after assigning the same integer values to different variable names, we are getting two different ids here. These are actually the effects of CPython optimization we are observing here. CPython implementation keeps an array of integer objects for all integers between -5 and 256. So when we create an integer in that range, they simply back reference to the existing object. You may refer the following [links](http://stackoverflow.com/questions/306313/is-operator-behaves-unexpectedly-with-integers) for more information.

Let's take a look at strings now.


```python	
>>> s1 = 'hello'
>>> s2 = 'hello'
>>> id(s1), id(s2)
(4454725888, 4454725888)
>>> s1 == s2
True
>>> s1 is s2
True
>>> s3 = 'hello, world!'
>>> s4 = 'hello, world!'
>>> id(s3), id(s4)
(4454721608, 4454721664)
>>> s3 == s4
True
>>> s3 is s4
False
```



Looks interesting, isn't it? When the string was a simple and shorter one the variable names where referring to the same object in memory. But when they became bigger, this was not the case. This is called interning, and Python does interning (to some extent) of shorter string literals (as in s1 and s2) which are created at compile time. But in general, Python string literals creates a new string object each time (as in s3 and s4). Interning is runtime dependant and is always a trade-off between memory use and the cost of checking if you are creating the same string. There's a built-in intern() function to forcefully apply interning. Read more about interning from the following links.

[Stack Overflow: Does Python intern Strings?](http://stackoverflow.com/questions/17679861/does-python-intern-strings)
[Stack Overflow: Python String Interning](http://stackoverflow.com/questions/15541404/python-string-interning)
[Internals of Python String Interning](http://guilload.com/python-string-interning/)






> **Source:**   
> :fa-link: http://foobarnbaz.com/2012/07/08/understanding-python-variables/