What Is a Program?
-------------
A program is a sequence of instructions that specifies how to perform a computation.
The computation might be something mathematical, such as solving a system of equat
ions or finding the roots of a polynomial, but it can also be a symbolic computation,
such as searching and replacing text in a document or (strangely enough) compiling a
program.
The details look different in different languages, but a few basic instructions appear in
just about every language:

input: 

 - Get data from the keyboard, a file, or some other device.

output:

 - Display data on the screen or send data to a file or other device.

math:

 - Perform basic mathematical operations like addition and
   multiplication.
   
conditional execution:

 - Check for certain conditions and execute the appropriate code.

repetition:

 - Perform some action repeatedly, usually with some variation.

Believe it or not, that’s pretty much all there is to it. Every program you’ve ever used, no
matter how complicated, is made up of instructions that look pretty much like these. So
you can think of programming as the process of breaking a large, complex task into
smaller and smaller subtasks until the subtasks are simple enough to be performed with
one of these basic instructions.
That may be a little vague, but we will come back to this topic when we talk about
algorithms.


> **Source:**   
> :fa-book:  **Think Python** by Allen B. Downey  - 2012


#Run Python Scripts
If you can't execute or run a Python script, then programming is pointless. When you run a Python script, the interpreter converts a Python program into something that that the computer can understand. Executing a Python program can be done in two ways: calling the Python interpreter with a shebang line, and using the interactive Python shell.

##Run a Python Script as a File
Generally programmers write stand alone scripts, that are independent to live environments. Then they save it with a ".py" extension, which indicates to the operating system and programmer that the file is actually a Python program. After the interpreter is invoked, it reads and interprets the file. The way Python scripts are run on Windows versus Unix based operating systems is very different. We'll show you the difference, and how to run a Python script on Windows and Unix platforms.

### Run a Python script under Windows with the Command Prompt

Windows users must pass the path of the program as an argument to the Python interpreter. Such as follows:
```shell	
C:\Python27\python.exe C:\Users\Username\Desktop\my_python_script.py
```
Note that you must use the full path of the Python interpreter. If you want to simply type python.exe C:\Users\Username\Desktop\my_python_script.py you must add python.exe to your PATH environmental variable.
Note that Windows comes with two Python executables - python.exe and pythonw.exe. If you want a terminal to pop-up when you run your script, use python.exe However if you don't want any terminal pop-up, use pythonw.exe. pythonw.exe is typically used for GUI programs, where you only want to display your program, not the terminal.

### Run a Python Script Under Mac, Linux, BSD, Unix, etc
On platforms like Mac, BSD or Linux (Unix) you can put a "shebang" line as first line of the program which indicates the location of the Python interpreter on the hard drive. It's in the following format:
```shell	
#!/path/to/interpreter
```
A common shebang line used for the Python interpreter is as follows:
```shell	
#!/usr/bin/env python
```
You must then make the script executable, using the following command:
```shell	
chmod +x my_python_script.py
```
Unlike Windows, the Python interpreter is typically already in the $PATH environmental variable, so adding it is un-necessary.

You can then run a program by invoking the Python interpreter manually as follows:
```shell	
python firstprogram.py
```


##Python Execution with the Shell (Live Interpreter)
Assuming that you already have Python installed and running well (if you're getting an error, see this post), open the terminal or console and type 'python' and hit the 'Enter' key. You will then be directed immediately to the Python live interpreter. Your screen will display a message something like:
```shell	
user@hostname:~ python
Python 3.3.0 (default, Nov 23 2012, 10:26:01) 
[GCC 4.2.1 Compatible Apple Clang 4.1 ((tags/Apple/clang-421.11.66))] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```
The Python programmer should keep in mind one thing: that while working with the live interpreter, everything is read and interpreted in real-time. For example loops iterate immediately, unless they are part of function. So it requires some mental planning. Using the Python shell is typically used to execute code interactively. If you want to run a Python script from the interpreter, you must either import it or call the Python executable.


> **Source:**   
> :fa-link:  http://pythoncentral.io/execute-python-script-file-shell/






## Debugging and Errors
### What Is Debugging?
Programming is error-prone. For whimsical reasons, programming errors are called
**bugs** and the process of tracking them down is called **debugging**.
Three kinds of errors can occur in a program: syntax errors, runtime errors, and se
mantic errors. It is useful to distinguish between them in order to track them down more
quickly.
### Error Types :

####Syntax Errors
Python can only execute a program if the syntax is correct; otherwise, the interpreter
displays an error message. Syntax refers to the structure of a program and the rules
about that structure.For example, parentheses have to come in matching pairs, so
(1 + 2) is legal, but 8) is a **syntax error**.
In English readers can tolerate most syntax errors, which is why we can read the poetry
of e. e. cummings without spewing error messages. Python is not so forgiving. If there
is a single syntax error anywhere in your program, Python will display an error message
and quit, and you will not be able to run your program. During the first few weeks of
your programming career, you will probably spend a lot of time tracking down syntax
errors. As you gain experience, you will make fewer errors and find them faster.

#### Runtime Errors
The second type of error is a runtime error, so called because the error does not appear
until after the program has started running. These errors are also called exceptions
because they usually indicate that something exceptional (and bad) has happened.
Runtime errors are rare in the simple programs you will see in the first few chapters, so
it might be a while before you encounter one.

#### Semantic Errors
The third type of error is the semantic error. If there is a semantic error in your program,
it will run successfully in the sense that the computer will not generate any error mess
ages, but it will not do the right thing. It will do something else. Specifically, it will do
what you told it to do.
The problem is that the program you wrote is not the program you wanted to write. The
meaning of the program (its semantics) is wrong. Identifying semantic errors can be
tricky because it requires you to work backward by looking at the output of the program
and trying to figure out what it is doing.


> **Source:**   
> :fa-book:  **Think Python** by Allen B. Downey  - 2012