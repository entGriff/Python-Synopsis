# Quick Tip: What Is a Metaclass in Python


This quick tip gives a brief overview of what we mean by a metaclass in Python and shows some examples of the concept.

Before delving into this article, I should point out an important point [about classes in Python](http://code.tutsplus.com/tutorials/a-smooth-refresher-on-pythons-classes-and-objects--cms-25598) which makes it easier for us to grasp the concept of metaclasses.

## Is a Class an Object in Python?!


If you've used a programming language other than Python, the concept you understood about classes is most likely that it is a way used to create new objects. This is also true in Python, but Python even takes it one more step further—classes are also considered objects!

So, if you created the following class in Python:

```python	
class myClass(object):
    pass
```
This simply means that an object with the name myClass has been created in memory. Since this object is able to create new objects, it is considered a class. This means we can apply object operations on classes in Python, as classes are objects themselves.

We can thus do operations on classes like assigning the class to a variable, as follows:
```python	
class_object = myClass()
print class_object
```
Which returns:
```python	
<__main__.myClass object at 0x102623610>
```

You can even pass the class `myClass` as a parameter to a method, as follows:
```python	
def class_object(object):
    print object
     
class_object(myClass)
```

Which returns the following output:
```python	
<class '__main__.myClass'>
```
In addition to other operations you can normally apply on objects.

## Metaclasses

Maybe you have come across the `type` keyword in Python? You most likely used it to check the type of some object, as shown in the following examples:
```python	
print type('abder')
print type(100)
print type(100.0)
print type(int)
```
In which case you would get the following output:
```python	
<type 'str'>
<type 'int'>
<type 'float'>
<type 'type'>
```
Looking at the output, everything seems pretty clear until you come to the type type. To see what this might mean, let's go back to our class we defined at the beginning of this article:
```python	
class myClass(object):
    pass
```
Now, do the following:
```python	
print type(myClass)
```
What would be the output of this statement? It will surprisingly be:
```python	
<type 'type'>
```
So, we can conclude that the type of classes in Python is `type`!

What is the relation between a `type` and a `metaclass`? Well, a `type` is a `metaclass`, provided that the default `metaclass` is `type`. I know this might be confusing, especially that type can be used to return the class of some object as shown above, but this is due to the backward compatibility in Python. So, if you write:
```python	
print type(type)
```
You will get:

```python	
<type 'type'>
```


Meaning that a `type` is a `type`!

The term `metaclass` simply means something used to create classes. In other words, it is the class of a class, meaning that the instance of a class in this case is a class. Thus, `type` is considered a `metaclass` since the instance of a `type` is a class.

For instance, when we mentioned the following statement above:
```python	
class_object = myClass()
```

This simply builds an object/instance of the class `myClass`. In other words, we used a class to create an object. 

In the same way, when we did the following:
```python	
class myClass(object):
    pass
```
The `metaclass` was used to create the class `myClass` (which is considered a `type`). So, like the object being an instance of a class, a class is an instance of a `metaclass`.


### Using Metaclass to Create a Class

In this section, we are going to see how we can use a `metaclass` to create a class, rather than using the `class` statement as we saw in the classes and objects tutorial. As we saw above, the default `metaclass` is `type`. Thus, we can use the following statement to create a new class:
```python	
new_class = type('myClass',(),{})
```
If you want to make things simpler, you can assign the same class name myClass to the variable name.

The dictionary `{ }` here is used to define the attributes of the class. So, having the following statement:
```python	
myClass = type('myClass',(),{'a':True})
```
Is similar to:
```python	
class myClass(object):
    a = True
```
### The __metaclass__ Attribute

Say that we created the class `myClass` as follows:
```python	
class myClass(object):
    __metaclass__ = myMetaClass
    pass
```
In this case, class creation will occur using myMetaClass instead of type, as follows:
```python	
myClass = myMetaClass(className, bases, dictionary)
```

### Creation and Initialization of a Metaclass

If you want to have control on how you create and initialize a class after its creation, you can simply use the metaclass __new__ method and __init__ constructor, respectively. So, when myMetaClass above is called, this is what will be happening behind the scenes:

```python	
myClass = myMetaClass.__new__(myMetaClass, name, bases, dictionary)
myMetaClass.__init__(myClass, name, bases, dictionary)
```


> **Source:**   
> :fa-link: https://code.tutsplus.com/tutorials/quick-tip-what-is-a-metaclass-in-python--cms-26016



