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
![a1box.](../images/a1box.png)

And for all the variables you create a new box is created with the variable name to hold the value. If you change the value of the variable the box will be updated with the new value. That means doing

```c	
a = 2;
```
will result in

![a2box.](../images/a2box.png)


Assigning one variable to another makes a copy of the value and put that value in the new box.
```c	
int b = a;
```
![b2box.](../images/b2box.png) ![a2box.](../images/a2box.png)

But in Python variables work more like tags unlike the boxes you have seen before. When you do an assignment in Python, it tags the value with the variable name.
```python	
a = 1
```
![a1tag.](../images/a1tag.png)

and if you change the value of the varaible, it just changes the tag to the new value in memory. You dont need to do the housekeeping job of freeing the memory here. Python's Automatic Garbage Collection does it for you. When a value is without names/tags it is automatically removed from memory.

```python	
a = 2
```
![a2tag.](../images/a2tag.png)

Assigning one variable to another makes a new tag bound to the same value as show below.

```python	
b = a
```
![ab2tag.](../images/ab2tag.png)  
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





## Assignment statements in Python are more interesting than you might think



In this article, we will take a deep look at three kinds of assignment statements in Python and discuss what’s going on under the hood.


```python	
>>> my_string = "Hello World"                # right hand side is a simple expression
>>> another_string = my_string               # right hand side is another variable
>>> another_string = another_string + "!"    # right hand side is an operation
```


What we find may surprise you.

**What happens when the right hand side is a simple expression?**

```python	
>>> my_string = "Hello World"
```
In simple terms, this creates a string “Hello World” in memory and assigns the name my_string to it. If you are using CPython[1], then we can even check the memory address explicitly by using the built in function id .

```python	
>>> my_string = “Hello World” 
>>> id(my_string)
140400709562064
```
That big number 140400709562064 denotes where the data lives in the memory. It will be very useful for us in this entire discussion.
What happens if we create another string with the same value?
```python	
>>> another_string = “Hello World”
```

Does it reuse the previous “Hello World” stored in memory or does it create an independent copy? Let’s check this by querying the id function again.
```python	
>>> id(another_string)
140400709562208
```
This outputs a different id, so this must be an independent copy. We conclude that:

> **Note:**
Assignment statements where the right hand side is a simple expression creates independent copies every time.

While for everyday programming, this is the rule we should remember, there are actually some weird exceptions to this rule. Here’s an example.

```python	
>>> my_string = “hello”
>>> id(my_string)
140400709562016
>>> another_string = “hello”
>>> id(another_string)
140400709562016
```


In this case, two consecutive assignment statements did not create independent copies. Why?
It gets interesting now.
For optimizing memory, Python treats a special set of objects differently. The string “hello” belongs to this privileged set and has a different behavior. The exact set depends on the implementation like CPython, PyPy, Jython or IronPython. For CPython, the special rule applies to:

 - Strings without whitespaces and less than 20 characters and
 - Integers from -5 to +255.

These objects are always reused or interned. The rationale behind doing this is as follows:

 1. Since programmers use these objects frequently, interning existing
    objects saves memory.
 2. Since immutable objects like tuples and strings cannot be modified,
    there is no risk in interning the same object.
    
However, Python does not do this for all immutable objects because there is a runtime cost involved for this feature. For interning an object, it must first search for the object in memory, and searching takes time. This is why the special treatment only applies for small integers and strings, because finding them is not that costly.

**What happens when the right hand side is an existing Python variable?**
Let’s move on to the second type of assignment statement where the right hand side is an existing Python variable.

```python	
>>> another_string = my_string
```

In this case, nothing is created in memory. After the assignment, both variables refer to the already existing object. It’s basically like giving the object an additional nickname or alias. Let’s confirm this by using the id function.

```python	
>>> my_string = “Hello World”
>>> id(my_string)
140400709562160
>>> another_string = my_string
>>> id(another_string)
140400709562160
```

The natural question at this stage is : what if, instead of just giving the existing object an alias, we wanted to create an independent copy?
For mutable objects, this is possible. You can either use the copy module of Python (which works on all objects) or you may use copy methods specific to the class. For a list, you have several possibilities for creating copies, all of which have different runtime.

```python	
>>> my_list = [1, 2, 3]
>>> copy_of_my_list = my_list.copy()       # fastest, works only on latest Python versions
>>> copy_of_my_list = my_list[:]           # same runtime as List.copy()
>>> copy_of_my_list = list(my_list)        # slightly slower
>>> import copy
>>> copy_of_my_list = copy.copy(my_list)   # slowest
```

How can you copy an immutable object? Well…you can’t! At least not in a straightforward way. If you try to use the copy module or the slicing notation, you will get back the same object and not an independent copy. Here’s proof.

```python	
# Standard ways of copying lists do not apply for tuples

>>> my_tuple = (1, 2, 3)
>>> id(my_tuple)
140371873244816
>>> another_tuple = my_tuple[:]
>>> id(another_tuple)
140371873244816

# The copy module also doesn’t help

>>> import copy 
>>> another_tuple = copy.copy(my_tuple)
>>> id(another_tuple)
140371873244816
```
More importantly, there is no reason for explicitly copying an immutable object anyway. We will see why in a moment when we discuss the third kind of assignment statement.
**What happpens when the right hand side is an operation?**

In this case, what happens depends on the result of the operation. We will discuss two simple cases:

 1. adding an element to an immutable object (like a tuple) and
 2. adding an element to a mutable object (like a list).

Let’s start with the case of the tuple.

```python	
>>> another_tuple +=  (4,)
```
When you add a new element to a tuple using another_tuple += (4,), this creates a new object in memory. The immutability of tuples is key to understanding this. Since tuples are immutable, any operation that leads to a changed tuple would result in an independent copy.
This is the reason why you don’t need to explicitly copy immutable objects : it happens automatically under the hood. Here’s an example.

```python	
>>> my_tuple = (1, 2, 3)
>>> another_tuple = my_tuple     # both variables point to the same object
>>> another_tuple += (4,)        # this statement creates a new independent object
>>> print(another_tuple) 
(1, 2, 3, 4)
>>> print(my_tuple)              # the old one remains unharmed
(1, 2, 3)
```

The situation is much different for mutable objects and much more confusing. Let’s try the same example, but now for lists.
```python	
>>> my_list = [1, 2, 3]
>>> another_list = my_list     # both variables point to the same object
>>> another_list += [4,]       # this statement modifies the object in place
>>> print(another_list)
[1, 2, 3, 4]
>>> print(my_list)             # the original list is modified
[1, 2, 3, 4]
```

Mutable objects can be modified in place. Some operations modify the list in place and some operations don’t. In this case, the statement another_list += [4,] calls another_list.__iadd__([4,]) and __iadd__ modifies the existing object in place.
To make things doubly confusing, we would have completely different results if we used a slightly different notation.

```python	
>>> my_list = [1, 2, 3]
>>> another_list = my_list              # both variables point to the same object
>>> another_list = another_list + [4,]  # this creates an independent copy
>>> print(another_list)
[1, 2, 3, 4]
>>> print(my_list)                      # the original list is unharmed
[1, 2, 3]  
```

Woah! What’s going on? What changed?
It turns out that when we change the third line, Python now internally calls a different function another_list.__add__([4,]) instead of __iadd__. This function returns a new copy instead of modifying the list in place.
To prevent this confusion, it is always better to create a true copy of the list if you wish to prevent modification to the original.
Let’s remember the list copy methods from before. They were List.copy(), [:], list() and copy.copy(). This is what we should use.


```python	
>>> my_list = [1, 2, 3]
>>> another_list = my_list.copy()   # this creates an independent copy
>>> another_list += [4,]            # this statement modifies the independent copy
>>> print(another_list)
[1, 2, 3, 4]
>>> print(my_list)                  # the original list is unharmed
[1, 2, 3]   
```

There’s one last gotcha that can happen when copying lists.
Suppose we have a list that has a nested list inside it. We copy this list using List.copy() and then modify the nested list. Unfortunately, this will modify the original list again!

```python	
>>> my_list = [[1, 2, 3], 4, 5]
>>> another_list = my_list.copy()
>>> another_list[0] += [6,]
>>> print(another_list)
[[1, 2, 3, 6], 4, 5]
>>> print(my_list)
[[1, 2, 3, 6], 4, 5] 
```

Why did that happen? Didn’t we just copy the original list?
The truth is : we actually don’t have a completely independent copy in this case. The copy() function generates a shallow copy. To see what it does, let’s look at the ids of all the elements in my_list and the ids of all the elements in the copied list.

```python	
# for my_list

>>> my_list = [[1, 2, 3], 4, 5]
>>> id(my_list)
140371873277424
>>> print([id(x) for x in my_list])
[140371873599288, 13820176, 13820152]

# for another_list obtained by my_list.copy()

>>> id(another_list)
140371873317016
>>> print([id(x) for x in another_list])
[140371873599288, 13820176, 13820152]
```

We see the ids of my_list and another_list are indeed different, indicating another_list is a copy. But the ids of the elements contained in another_list have the same ids as the elements in my_list . So the elements have not been copied!
This is the property of shallow copy. It creates a new copy of the object but reuses the attributes and elements of the old copy. Thus, when you modify the elements of the new copy, you are modifying the elements of the old copy too.
To solve this problem, we need to copy an object along with all its attributes and elements. This can be achieved by copy.deepcopy.


```python	
>>> my_list = [[1, 2, 3], 4, 5]
>>> another_list = copy.deepcopy(my_list)
>>> another_list[0] += [6,]
>>> another_list
[[1, 2, 3, 6], 4, 5]
>>> my_list
[[1, 2, 3], 4, 5]
```

Deep copy is a quite time intensive operation and can take 1o times longer to complete compared to a shallow copy. But in some situations, it is unavoidable.

### Conclusion
This brings me to the end of this discussion. To summarize, we have talked about the different scenarios which can arise in an assignment statement in Python. We found that:

 - When the right hand side is a simple expression, a new copy is
   created every time. There are some exceptions to this rule, which
   depend on the implementation
 - When the right hand side is an existing Python variable, then an
   alias is created for the existing copy.
 - When the right hand side is an operation, then the outcome depends on
   the operation. In a simple case involving a tuple, we saw that an
   independent copy was created. In the same case with lists, we saw
   that the list was modified in place in one case (when we used
   __iadd__) and a new copy was generated in another case (when we used __add__).
 - List item
 - Mutable objects can be copied but immutable objects cannot be copied
   in a straightforward way. There is also no need to copy immutable
   objects.
 - To copy a mutable object along with all its attributes and elements,
   we need to use deep copy.


> **Source:**   
> :fa-link: https://medium.com/broken-window/many-names-one-memory-address-122f78734cb6

