## How Exactly Do Context Managers Work?

Context managers (PEP 343) are pretty important in Python. You probably use one every time you open a file:
```python
with open('cake.txt') as c:
    gobble_gobble(c)
```
But how well do you understand what’s going on behind the scenes?

### CONTEXT MANAGER CLASSES
It’s actually quite simple. A context manager is a class that implements an `__enter__` and an `__exit__` method.

Let’s imagine you want to you print a line of text to the console surrounded with asterisks. Here’s a context manager to do it:

```python
class asterisks():
    def __enter__(self):
        print('*' * 32)
        
    def __exit__(self, exc_type, exc_val, exc_tb):
        print('*' * 32)
```
The `__exit__` method takes three arguments apart from `self`. Those arguments contain information about any errors that occurred inside the `with` block.

You can use `asterisks` in the same way as any of the built-in context managers:
```python
>>> with asterisks():
>>>     print("Context Managers Rock!")
********************************
Context Managers Rock!
********************************
```

### ACCESSING THE CONTEXT INSIDE THE WITH BLOCK
If you need to get something back and use it inside the with block – such as a file descriptor – you simply return it from `__enter__`:
```python
class myopen():
    def __init__(self, filename, filemode):
        self.filename = filename
        self.filemode = filemode

    def __enter__(self):
        self.file = open(self.filename, self.filemode)
        return self.file

    def __exit__(self, exc_type, exc_val, exc_tb):
        self.file.close()
```
`myopen` works identically to the built-in `open`:
```python
with myopen("beer.txt") as b:
    guzzle_guzzle(b)
```

### THE CONTEXTMANAGER DECORATOR

Thankfully, you don’t have to implement a class every time. The `contextlib` package has a `contextmanager` decorator that you can apply to generators to automatically transform them into context managers:
```python
from contextlib import contextmanager

@contextmanager
def spoiler():
    print('<spoiler>')
    yield
    print('</spoiler>')
```
The code before `yield` corresponds to `__enter__` and the code after `yield` corresponds to `__exit__`. A context manager generator should have exactly one `yield` in it.

It works the same as the class version:
```python
>>> with spoiler():
>>>     print("Jon Snow is Luke's father.")
<spoiler>
Jon Snow is Luke's father.
</spoiler>
```

### ROLL YOUR OWN CONTEXTMANAGER DECORATOR
The implementation in `contextlib` is complicated, but it’s not hard to write something that works similarly with the exception of a few edge cases:
```python
def contextmanager(gen):
    class CMWrapper(object):
        def __init__(self, wrapped):
            self.generator = wrapped

        def __enter__(self):
            return next(self.generator)

        def __exit__(self, ex_type, value, traceback):
            try:
                next(self.generator)
            except StopIteration:
                pass

    def inner(*args, **kwargs):
        return CMWrapper(gen(*args, **kwargs))

    return inner
```
It’s not as robust as the real implementation, but it should be understandable. Here are the key points:
- The inner function instantiates a copy of the nested CMWrapper class with a handle on the generator passed into the decorator.  
- `__enter__` calls next() on the generator and returns the yielded value so it can be used in the with block.  
- `__exit__` calls next() again and catches the StopIteration exception that the generator throws when it finishes.  

That’s it for now. If you want to learn more about context managers, I recommend you take a look at the code for `contextlib`.

> **Source:**   
> :fa-link: https://www.smallsurething.com/how-exactly-do-context-managers-work/


## Python Context Managers and the "with" Statement (__enter__ & __exit__)    **VIDEO**
[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/iba-I4CrmyA/0.jpg)](https://youtu.be/iba-I4CrmyA)


