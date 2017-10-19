## Conditional Execution
In order to write useful programs, we almost always need the ability to check conditions
and change the behavior of the program accordingly. Conditional statements give us this
ability. The simplest form is the if statement:

```python
if x > 0:
    print 'x is positive'
```

The boolean expression after if is called the condition. If it is true, then the indented
statement gets executed. If not, nothing happens.
if statements have the same structure as function definitions: a header followed by an
indented body. Statements like this are called compound statements.
There is no limit on the number of statements that can appear in the body, but there has
to be at least one. Occasionally, it is useful to have a body with no statements (usually
as a place keeper for code you haven’t written yet). In that case, you can use the pass
statement, which does nothing.

```python
if x < 0:
    pass # need to handle negative values!
```
### Alternative Execution
A second form of the if statement is alternative execution, in which there are two
possibilities and the condition determines which one gets executed. The syntax looks
like this:

```python
if x%2 == 0:
    print 'x is even'
else:
    print 'x is odd'
```

If the remainder when x is divided by 2 is 0, then we know that x is even, and the program
displays a message to that effect. If the condition is false, the second set of statements is
executed. Since the condition must be true or false, exactly one of the alternatives will
be executed. The alternatives are called branches, because they are branches in the flow
of execution.

### Chained Conditionals
Sometimes there are more than two possibilities and we need more than two branches.
One way to express a computation like that is a chained conditional:  

```python
if x < y:
    print 'x is less than y'
elif x > y:
    print 'x is greater than y'
else:
    print 'x and y are equal'
```
elif is an abbreviation of “else if.” Again, exactly one branch will be executed. There is
no limit on the number of elif statements. If there is an else clause, it has to be at the
end, but there doesn’t have to be one.  

```python
if choice == 'a':
    draw_a()
elif choice == 'b':
    draw_b()
elif choice == 'c':
    draw_c()
```  
Each condition is checked in order. If the first is false, the next is checked, and so on. If
one of them is true, the corresponding branch executes, and the statement ends. Even
if more than one condition is true, only the first true branch executes.

### Nested Conditionals
One conditional can also be nested within another. We could have written the tri
chotomy example like this:

```python
if x == y:
    print 'x and y are equal'
else:
    if x < y:
        print 'x is less than y'
    else:
        print 'x is greater than y'
```  

The outer conditional contains two branches. The first branch contains a simple state
ment. The second branch contains another if statement, which has two branches of its
own. Those two branches are both simple statements, although they could have been
conditional statements as well.  
Although the indentation of the statements makes the structure apparent, nested
conditionals become difficult to read very quickly. In general, it is a good idea to avoid
them when you can.  
Logical operators often provide a way to simplify nested conditional statements. For
example, we can rewrite the following code using a single conditional:  

```python
if 0 < x:
    if x < 10:
        print 'x is a positive single-digit number.'
```  
The print statement is executed only if we make it past both conditionals, so we can
get the same effect with the and operator:  

```python
if 0 < x and x < 10:
    print 'x is a positive single-digit number.'
```  

> **Source:**   
> :fa-book:  **Think Python** by Allen B. Downey  - 2012


## If-Else statements in Python By Udemy
The if-else statement is a staple of most programming languages. It is used to test different conditions and execute code accordingly. You can think of it as a ‘map’ used to make decisions in the program.

The basic syntax is as follows:

```python
if condition1 = True:
      execute code1
else:               
      execute code2
```  
In plain English, this can be described as follows:
`If condition1 is true, then execute the code included in code1. If it is not true, then run code2`

A few things to note about the syntax:
- Each if/else statement must close with a colon (:)
- Code to be executed as part of any if/else statement must be indented by four spaces, equivalent to one press of the Tab key.
- Although not explicitly required, every if statement must also include an else statement – it just makes for a better program.

You use if-else statements a lot in your every day. Virtually every decision you make involves some form of if-else statements. “If the bacon is cheap, I’ll buy a pound. If not, I’ll grab some mac and cheese”, “if I wake up before 6, I’ll head out for a jog. Otherwise, I’ll head straight to work”, and “if the traffic is light, we’ll make the movie theater in time. Else, we’ll just have to grab dinner and go back home” – these are some simple if-else decisions we’ve all made in our everyday life. Thus, by using if-else statements in Python, you give the program the ability to make decisions depending on the user input.

But enough talk; let’s try to understand if-else statements with an example:

```python
x = 5
if x > 5:
          print "X is larger than five!"
else:
          print "X is smaller than or equal to five!"
```  
this program basically instructs Python to:
- Check the value of x.
- If the value of x is more than 5, print that “X is larger than five”.
- If the value of x is less than or equal to 5, print “X is smaller than or equal to five”.

As we’ll learn below, the decision making capabilities of if-else conditions will come very handy when you want to create complicated programs.

### Testing Multiple Conditions with Elif
The above if-else syntax is great if you want to test just one condition, but what happens when you want to check multiple conditions?

This is where the Elif statement comes in handy.  
Elif is a shortened form of Else-If. The syntax can be seen as follows:

```python
if condition1 = True:
         execute code1
elif condition2 = True:
         execute code2
else:  
         execute code3
```  
In plain English, you can read this as follows:
`If condition1 is true, execute code1. Else, if condition2 is true, execute code2. If neither condition1 or condition2 are true, execute code3.`

There is no limit to the number of elif statements you can include in a Python program. You can test dozens of conditions using multiple elif statements as long as you close with an else statement.  
Let’s try to understand this with an example:  

```python
x = 5
if x == 5:
          print "Wow, X is EXACTLY five!"
elif x > 5:
          print "X is now MORE than five!"
else:
          print "X is now LESS than five!"
```  

So what exactly is happening here? Let’s break it down into individual steps:  

- Python first checks if the value of x is exactly equal to 5, as given in the first if statement.
- If x is equal to five, Python executes the code included within the first if statement and exits the program.
- If, however, x is not equal to 5, Python goes to the second elif statement. It now checks if x is greater than 5.
- In case x is more than 5, Python executes the second block of code under the elif statement and exits the program.
- However, if both conditions are not met, that is, x is neither equal to, nor greater than five, Python displays the output under the third else statement.

As mentioned above, an if-else conditional block can include as many elif statements as you want.

### Nested If-Else Statements
So far, we’ve used just a single level of if-else statements. But what if you want to make decisions within decisions? That’s like saying: “if the oranges are fresh, buy a dozen if they are more than $5/lb, and two dozen if they are less than $5/lb”

In programmer-speak (i.e. algorithmically) this can be written as follows: 

```python
orange_quality = “fresh”
orange_price = 4.0
if orange_quality == “fresh”:
          if orange_price < 5:
                    buy 24.0
          else: 
                    buy 12.0
else:
          don’t_buy_oranges
```   
This is an example of a nested if-else statement – an if-else statement inside another if-else statement. These can help you make more complex decisions and give you even finer control over the program flow. In terms of syntax, they can be written as follows:  

```python
if condition1 =  True:
          if condition2 = True:
                  execute code1
          elif condition3 = True:
                  execute code2
          else:
                  execute code3
else:
          execute code4
``` 
Thus, the syntax rules are the same as a standard if-statement – i.e. nested statements must be tabbed in. Theoretically, you can nest as many if-else statements as you want, but it is poor practice to go more than two levels deep. 

> **Source:**   
> :fa-link: https://blog.udemy.com/python-if-else/


## How To Write Conditional Statements in Python 3
Conditional statements are part of every programming language. With conditional statements, we can have code that sometimes runs and at other times does not run, depending on the conditions of the program at that time.

When we fully execute each statement of a program, moving from the top to the bottom with each line executed in order, we are not asking the program to evaluate specific conditions. By using conditional statements, programs can determine whether certain conditions are being met and then be told what to do next.  
  
Let’s look at some examples where we would use conditional statements:  

- If the student receives over 65% on her test, report that her grade passes; if not, report that her grade fails
- If he has money in his account, calculate interest; if he doesn’t, charge a penalty fee
- If they buy 10 oranges or more, calculate a discount of 5%; if they buy fewer, then don’t

Through evaluating conditions and assigning code to run based on whether or not those conditions are met, we are writing conditional code.  


This tutorial will take you through writing conditional statements in the Python programming language.  

### If statement
We will start with the if statement, which will evaluate whether a statement is true or false, and run code only in the case that the statement is true.

In a plain text editor, open a file and write the following code:  

```python
grade = 70

if grade >= 65:
    print("Passing grade")
``` 

With this code, we have the variable grade and are giving it the integer value of 70. We are then using the if statement to evaluate whether or not the variable grade is greater than or equal ( >= ) to 65. If it does meet this condition, we are telling the program to print out the string Passing grade.

In this case, the grade of 70 does meet the condition of being greater than or equal to 65, so you will receive the following output once you run the program:  

```python
Output
Passing grade
```   
Let’s now change the result of this program by changing the value of the grade variable to 60:

```python
grade = 60

if grade >= 65:
    print("Passing grade")
```  

When we save and run this code, we will receive no output because the condition was not met and we did not tell the program to execute another statement.

To give one more example, let us calculate whether a bank account balance is below 0. Let’s create a file called `account.py` and write the following program:

```python
balance = -5

if balance < 0:
    print("Balance is below 0, add funds now or you will be charged a penalty.")
```  

When we run the program with python account.py, we’ll receive the following output:

```python
Output
Balance is below 0, add funds now or you will be charged a penalty.
```  
In the program we initialized the variable `balance` with the value of -5, which is less than 0. Since the balance met the condition of the if statement (balance < 0), once we save and run the code, we will receive the string output. Again, if we change the balance to 0 or a positive number, we will receive no output.

### Else Statement
It is likely that we will want the program to do something even when an `if` statement evaluates to false. In our grade example, we will want output whether the grade is passing or failing.

To do this, we will add an else statement to the grade condition above that is constructed like this:

```python
grade = 60

if grade >= 65:
    print("Passing grade")

else:
    print("Failing grade")
```  

Since the grade variable above has the value of 60, the if statement evaluates as false, so the program will not print out Passing grade. The else statement that follows tells the program to do something anyway.

When we save and run the program, we’ll receive the following output:

```python
Output
Failing grade
```  
If we then rewrite the program to give the grade a value of `65` or higher, we will instead receive the output `Passing grade`.

To add an else statement to the bank account example, we rewrite the code like this:

```python
balance = 522

if balance < 0:
    print("Balance is below 0, add funds now or you will be charged a penalty.")

else:
    print("Your balance is 0 or above.")
``` 

Here, we changed the balance variable value to a positive number so that the else statement will print. To get the first if statement to print, we can rewrite the value to a negative number.

By combining an if statement with an else statement, you are constructing a two-part conditional statement that will tell the computer to execute certain code whether or not the if condition is met.  

### Else if statement
So far, we have presented a Boolean option for conditional statements, with each if statement evaluating to either true or false. In many cases, we will want a program that evaluates more than two possible outcomes. For this, we will use an else if statement, which is written in Python as elif. The elif or else if statement looks like the if statement and will evaluate another condition.

In the bank account program, we may want to have three discrete outputs for three different situations:

- The balance is below 0
- The balance is equal to 0
- The balance is above 0

The `elif` statement will be placed between the if statement and the else statement as follows:

```python
. . .
if balance < 0:
    print("Balance is below 0, add funds now or you will be charged a penalty.")

elif balance == 0:
    print("Balance is equal to 0, add funds soon.")

else:
    print("Your balance is 0 or above.")
``` 

Now, there are three possible outputs that can occur once we run the program:
- If the variable balance is equal to 0 we will receive the output from the elif statement (Balance is equal to 0, add funds soon.)
- If the variable balance is set to a positive number, we will receive the output from the else statement (Your balance is 0 or above.).
- If the variable balance is set to a negative number, the output will be the string from the if statement (Balance is below 0, add funds now or you will be charged a penalty).

What if we want to have more than three possibilities, though? We can do this by writing more than one elif statement into our code.

In the `grade.py` program, let’s rewrite the code so that there are a few letter grades corresponding to ranges of numerical grades:

- 90 or above is equivalent to an A grade
- 80-89 is equivalent to a B grade
- 70-79 is equivalent to a C grade
- 65-69 is equivalent to a D grade
- 64 or below is equivalent to an F grade

To run this code, we will need one `if` statement, three `elif` statements, and an `else` statement that will handle all failing cases.

Let’s rewrite the code from the example above to have strings that print out each of the letter grades. We can keep our else statement the same.

```python
. . .
if grade >= 90:
    print("A grade")

elif grade >=80:
    print("B grade")

elif grade >=70:
    print("C grade")

elif grade >= 65:
    print("D grade")

else:
    print("Failing grade")
``` 

Since elif statements will evaluate in order, we can keep our statements pretty basic. This program is completing the following steps:

- If the grade is greater than 90, the program will print A grade, if the grade is less than 90, the program will continue to the next statement...
- If the grade is greater than or equal to 80, the program will print B grade, if the grade is 79 or less, the program will continue to the next statement...
- If the grade is greater than or equal to 70, the program will print C grade, if the grade is 69 or less, the program will continue to the next statement...
- If the grade is greater than or equal to 65, the program will print D grade, if the grade is 64 or less, the program will continue to the next statement...
- The program will print Failing grade because all of the above conditions were not met.

### Nested If Statements

Once you are feeling comfortable with the if, elif, and else statements, you can move on to nested conditional statements. We can use nested if statements for situations where we want to check for a secondary condition if the first condition executes as true. For this, we can have an if-else statement inside of another if-else statement. Let’s look at the syntax of a nested if statement:

```python
if statement1:              #outer if statement
    print("true")

    if nested_statement:    #nested if statement
        print("yes")

    else:                   #nested else statement
        print("no")

else:                       #outer else statement
    print("false")
``` 

A few possible outputs can result from this code:  
- If `statement1` evaluates to true, the program will then evaluate whether the nested_statement also evaluates to true. If both cases are true, the output will be:

```python
Output
true
yes
``` 
- If, however, statement1 evaluates to true, but nested_statement evaluates to false, then the output will be:

```python
Output
true
no
``` 
- And if statement1 evaluates to false, the nested if-else statement will not run, so the else statement will run alone, and the output will be:

```python
Output
false
``` 

We can also have multiple if statements nested throughout our code:

```python
if statement1:                  #outer if 
    print("hello world")

    if nested_statement1:       #first nested if 
        print("yes")

    elif nested_statement2:     #first nested elif
        print("maybe")

    else:                       #first nested else
        print("no")

elif statement2:                #outer elif
    print("hello galaxy")

    if nested_statement3:       #second nested if
        print("yes")

    elif nested_statement4:     #second nested elif
        print("maybe")

    else:                       #second nested else
        print("no")

else:                           #outer else
    statement("hello universe")
``` 

In the above code, there is a nested if statement inside each if statement in addition to the elif statement. This will allow for more options within each condition.

Let’s look at an example of nested if statements with our grade.py program. We can check for whether a grade is passing first (greater than or equal to 65%), then evaluate which letter grade the numerical grade should be equivalent to. If the grade is not passing, though, we do not need to run through the letter grades, and instead can have the program report that the grade is failing. Our modified code with the nested if statement will look like this:

```python
. . .
if grade >= 65:
    print("Passing grade of:")

    if grade >= 90:
        print("A")

    elif grade >=80:
        print("B")

    elif grade >=70:
        print("C")

    elif grade >= 65:
        print("D")

else:
    print("Failing grade")
``` 

If we run the code with the variable grade set to the integer value 92, the first condition is met, and the program will print out Passing grade of:. Next, it will check to see if the grade is greater than or equal to 90, and since this condition is also met, it will print out A.

If we run the code with the grade variable set to 60, then the first condition is not met, so the program will skip the nested if statements and move down to the else statement, with the program printing out `Failing grade`.

We can of course add even more options to this, and use a second layer of nested if statements. Perhaps we will want to evaluate for grades of A+, A and A- separately. We can do so by first checking if the grade is passing, then checkingto see if the grade is 90 or above, then checkingto see if the grade is over 96 for an A+ for instance:

```python
. . .
if grade >= 65:
    print("Passing grade of:")

    if grade >= 90:
        if grade > 96:
            print("A+")

        elif grade > 93 and grade <= 96:
            print("A")

        elif grade >= 90:
            print("A-")
. . .
``` 

In the code above, for a grade variable set to 96, the program will run the following:

- Check if the grade is greater than or equal to 65 (true)
- Print out Passing grade of:
- Check if the grade is greater than or equal to 90 (true)
- Check if the grade is greater than 96 (false)
- Check if the grade is greater than 93 and also less than or equal to 96 (true)
- Print A
- Leave these nested conditional statements and continue with remaining code

The output of the program for a grade of 96 therefore looks like this:
```python
Output
Passing grade of:
A
``` 
Nested if statements can provide the opportunity to add several specific levels of conditions to your code.

### Conclusion
By using conditional statements like the if statement, you will have greater control over what your program executes. Conditional statements tell the program to evaluate whether a certain condition is being met. If the condition is met it will execute specific code, but if it is not met the program will continue to move down to other code.

> **Source:**   
> :fa-link: https://www.digitalocean.com/community/tutorials/how-to-write-conditional-statements-in-python-3-2