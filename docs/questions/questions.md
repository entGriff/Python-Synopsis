## Difference between \__str__  and   \__repr__ in Python

Ever wondered what happens when you call Python’s built-in str(X), with X being any object you want? The return value of this function depends on the two magic methods \__str__ being the first choice and \__repr__ as a fallback. But what’s the difference between them? When having a look at the docs

```python	
>>> help(str)
'Create a new string object from the given object.'
>>> help(repr)
'Return the canonical string representation of the object.'
```
they seem to be fairly similar. Let’s see them in action:
```python	
>>> str(123)
'123'
>>> repr(123)
'123'
```
Alright no difference for now.
```python	
>>> str('Python')
'Python'
>>> repr('Python')
"'Python'"
```
A second pair of quotes around our string. Why?
With the return value of repr() it should be possible to recreate our object using eval(). This function takes a string and evaluates it’s content as Python code. In our case passing “‘Python’“ to it works, whereas ‘Python’ leads to an error cause it’s interpreted as the variable Python which is of course undefined. Let’s move on…
```python	
>>> import datetime
>>> now = datetime.datetime.now() 
>>> str(now)
'2015-04-04 20:51:31.766862'
>>> repr(now)
'datetime.datetime(2015, 4, 4, 20, 51, 31, 766862)'
```

This is some significant difference. While str(now) computes a string containing the value of now, repr(now) again returns the Python code needed to rebuild our now object.

The following clues might help you to decide when to use which:


 str()  | repr() | 
------|------|
**make object readable** | **need code that reproduces object**|
**generate output for end user **| **generate output for developer**| 

These points should also be considered when writing __str__ or __repr__ for your classes.


> **Source:**   
> :fa-link: http://brennerm.github.io/posts/python-str-vs-repr.html

### answers from stackoverflow :
https://stackoverflow.com/questions/1436703/difference-between-str-and-repr-in-python
https://stackoverflow.com/questions/18393701/the-difference-between-str-and-repr


## What  is a Slot?
A slot is nothing more than a memory management nicety: when you define __slots__ on a class, you’re telling the Python interpreter that the list of attributes described within are the only attributes this class will ever need, and a dynamic dictionary is not needed to manage the references to other objects within the class. This can save enormous amounts of space if you have thousands or millions of objects in memory.
For example, if you define:
```python	
class Foo:
    __slots__ = ['x']
    def __init__(self, n):
        self.x = n

y = Foo(1)
print y.x  # prints "1"
y.x = 2
print y.x  # prints "2"
y.z = 4    # Throws exception.
print y.z
```
Without the __slots__ definition, that last assignment would have worked.  Without any other magic (say, overrides of getattr or setattr), you can always assign attributes to an object.  But with a __slots__ definition, you can’t: python hasn’t allocated a dictionary for the object, so you’re stuck with what you’ve got and nothing more.
Slots should only be used as a memory optimization tool; using it to constrain attribute management is silly, and breaks important features like static serialization.

> **Source:**   
> :fa-link: http://www.elfsternberg.com/2009/07/06/python-what-the-hell-is-a-slot/

### Avoiding Dynamically Created Attributes
The attributes of objects are stored in a dictionary "__dict__". Like any other dictionary, a dictionary used for attribute storage doesn't have a fixed number of elements. In other words, you can add elements to dictionaries after they have been defined, as we have seen in our chapter on dictionaries. This is the reason, why you can dynamically add attributes to objects of classes that we have created so far: 
```python	
>>> class A(object):
...     pass
... 
>>> a = A()
>>> a.x = 66
>>> a.y = "dynamically created attribute"
```
The dictionary containing the attributes of "a" can be accessed like this:
```python	
>>> a.__dict__
{'y': 'dynamically created attribute', 'x': 66}
```
You might have wondered that you can dynamically add attributes to the classes, we have defined so far, but that you can't do this with built-in classes like 'int', or 'list':
```python	
>>> x = 42
>>> x.a = "not possible to do it"
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'int' object has no attribute 'a'
>>> 
>>> lst = [34, 999, 1001]
>>> lst.a = "forget it"
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'list' object has no attribute 'a'
```

Using a dictionary for attribute storage is very convenient, but it can mean a waste of space for objects, which have only a small amount of instance variables. The space consumption can become critical when creating large numbers of instances. Slots are a nice way to work around this space consumption problem. Instead of having a dynamic dict that allows adding attributes to objects dynamically, slots provide a static structure which prohibits additions after the creation of an instance. 

When we design a class, we can use slots to prevent the dynamic creation of attributes. To define slots, you have to define a list with the name __slots__. The list has to contain all the attributes, you want to use. We demonstrate this in the following class, in which the slots list contains only the name for an attribute "val". 

```python	
class S(object):

    __slots__ = ['val']

    def __init__(self, v):
        self.val = v


x = S(42)
print(x.val)

x.new = "not possible"
```

If we start this program, we can see, that it is not possible to create dynamically a new attribute. We fail to create an attribute "new":
```python	
42
Traceback (most recent call last):
  File "slots_ex.py", line 12, in <module>
    x.new = "not possible"
AttributeError: 'S' object has no attribute 'new'
```

We mentioned in the beginning that slots are preventing a waste of space with objects. Since Python 3.3 this advantage is not as impressive any more. With Python 3.3 Key-Sharing Dictionaries are used for the storage of objects. The attributes of the instances are capable of sharing part of their internal storage between each other, i.e. the part which stores the keys and their corresponding hashes. This helps to reduce the memory consumption of programs, which create many instances of non-builtin types.

> **Source:**   
> :fa-link: http://www.python-course.eu/python3_slots.php

### answers from stackoverflow :
https://stackoverflow.com/questions/472000/usage-of-slots

## what means name mangling in python
http://radek.io/2011/07/21/private-protected-and-public-in-python/
### answers from stackoverflow :
https://stackoverflow.com/questions/7456807/python-name-mangling


## Python - dir() - how can I differentiate between functions/method and simple attributes?

To show a list of the defined names in a module, for example the math module, and their types you could do:
```python	
[(name,type(getattr(math,name))) for name in dir(math)]
```
getattr(math,name) returns the object (function, or otherwise) from the math module, named by the value of the string in the variable "name". For example type(getattr(math,'pi')) is 'float'

> **Source:**   
> :fa-link: https://stackoverflow.com/questions/26818007/python-dir-how-can-i-differentiate-between-functions-method-and-simple-att