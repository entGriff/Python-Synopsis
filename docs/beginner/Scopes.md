### Scopes - Python Scope Basics

Now that you’re ready to start writing your own functions, we need to get more formal
about what names mean in Python. When you use a name in a program, Python creates,
changes, or looks up the name in what is known as a namespace—a place where names
live. When we talk about the search for a name’s value in relation to code, the term
scope refers to a namespace: that is, the location of a name’s assignment in your code
determines the scope of the name’s visibility to your code.  
Just about everything related to names, including scope classification, happens at assignment
time in Python. As we’ve seen, names in Python spring into existence when
they are first assigned values, and they must be assigned before they are used. Because
names are not declared ahead of time, Python uses the location of the assignment of a
name to associate it with (i.e., bind it to) a particular namespace. In other words, the
place where you assign a name in your source code determines the namespace it will
live in, and hence its scope of visibility.  
Besides packaging code, functions add an extra namespace layer to your programs—
by default, all names assigned inside a function are associated with that function’s
namespace, and no other. This means that:  


- Names defined inside a def can only be seen by the code within that def. You cannot
even refer to such names from outside the function.  
- Names defined inside a def do not clash with variables outside the def, even if the
same names are used elsewhere. A name X assigned outside a given def (i.e., in a
different def or at the top level of a module file) is a completely different variable
from a name X assigned inside that def.  


In all cases, the scope of a variable (where it can be used) is always determined by where
it is assigned in your source code and has nothing to do with which functions call which.
In fact, as we’ll learn in this chapter, variables may be assigned in three different places,
corresponding to three different scopes:  
- If a variable is assigned inside a def, it is local to that function.  
- If a variable is assigned in an enclosing def, it is nonlocal to nested functions.  
- If a variable is assigned outside all defs, it is global to the entire file.  
We call this lexical scoping because variable scopes are determined entirely by the locations
of the variables in the source code of your program files, not by function calls.  
For example, in the following module file, the X = 99 assignment creates a global variable
named X (visible everywhere in this file), but the X = 88 assignment creates a
local variable X (visible only within the def statement):  

```python
X = 99
def func():
    X = 88
```

Even though both variables are named X, their scopes make them different. The net
effect is that function scopes help to avoid name clashes in your programs and help to
make functions more self-contained program units.  

#### Scope Rules
 Before we started writing functions, all the code we wrote was at the top level of a
module (i.e., not nested in a def), so the names we used either lived in the module itself
or were built-ins predefined by Python (e.g., open). Functions provide nested namespaces
(scopes) that localize the names they use, such that names inside a function
won’t clash with those outside it (in a module or another function). Again, functions
define a local scope, and modules define a global scope. The two scopes are related as
follows:  
- `The enclosing module is a global scope.` Each module is a global scope—that
is, a namespace in which variables created (assigned) at the top level of the module
file live. Global variables become attributes of a module object to the outside world
but can be used as simple variables within a module file.
- `The global scope spans a single file only.` Don’t be fooled by the word “global”
here—names at the top level of a file are only global to code within that single file.
There is really no notion of a single, all-encompassing global file-based scope in Python. Instead, names are partitioned into modules, and you must always import
a module explicitly if you want to be able to use the names its file defines. When
you hear “global” in Python, think “module.”  
- `Each call to a function creates a new local scope.` Every time you call a function,
you create a new local scope—that is, a namespace in which the names created
inside that function will usually live. You can think of each def statement (and
lambda expression) as defining a new local scope, but because Python allows functions
to call themselves to loop (an advanced technique known as recursion), the
local scope in fact technically corresponds to a function call—in other words, each
call creates a new local namespace. Recursion is useful when processing structures
whose shapes can’t be predicted ahead of time.  
- `Assigned names are local unless declared global or nonlocal.` By default, all
the names assigned inside a function definition are put in the local scope (the
namespace associated with the function call). If you need to assign a name that
lives at the top level of the module enclosing the function, you can do so by declaring
it in a global statement inside the function. If you need to assign a name
that lives in an enclosing def, as of Python 3.0 you can do so by declaring it in a
nonlocal statement.  
- `All other names are enclosing function locals, globals, or built-ins.` Names
not assigned a value in the function definition are assumed to be enclosing scope
locals (in an enclosing def), globals (in the enclosing module’s namespace), or builtins
(in the predefined __builtin__ module Python provides).


There are a few subtleties to note here. First, keep in mind that code typed at the
interactive command prompt follows these same rules. You may not know it yet, but
code run interactively is really entered into a built-in module called __main__; this
module works just like a module file, but results are echoed as you go. Because of this,
interactively created names live in a module, too, and thus follow the normal scope
rules: they are global to the interactive session. You’ll learn more about modules in the
next part of this book.

Also note that any type of assignment within a function classifies a name as local. This
includes = statements, module names in import, function names in def, function argument
names, and so on. If you assign a name in any way within a def, it will become a
local to that function.

Conversely, in-place changes to objects do not classify names as locals; only actual name
assignments do. For instance, if the name L is assigned to a list at the top level of a
module, a statement L = X within a function will classify L as a local, but L.append(X)
will not. In the latter case, we are changing the list object that L references, not L itself—
L is found in the global scope as usual, and Python happily modifies it without requiring
a global (or nonlocal) declaration. As usual, it helps to keep the distinction between
names and objects clear: changing an object is not an assignment to a name.





> **Source:**   
> :fa-book:  **Learning Python, Fourth Edition** by Mark Lutz  - 2009

good resource : http://sebastianraschka.com/Articles/2014_python_scope_and_namespaces.html