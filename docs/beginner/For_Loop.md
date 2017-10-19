## How To Construct For Loops in Python 3

Using loops in computer programming allows us to automate and repeat similar tasks multiple times. In this tutorial, we’ll be covering Python’s for loop.

A for loop implements the repeated execution of code based on a loop counter or loop variable. This means that for loops are used most often when the number of iterations is known before entering the loop, unlike while loops which are conditionally based.

## For Loops
In Python, for loops are constructed like so:  

```python
for [iterating variable] in [sequence]:
    [do something]
```

The something that is being done will be executed until the sequence is over.  

Let’s look at a for loop that iterates through a range of values:  

```python
for i in range(0,5):
   print(i)
```
When we run this program, the output looks like this:
```python
Output
0
1
2
3
4
```
This for loop sets up i as its iterating variable, and the sequence exists in the range of 0 to 5.  

Then within the loop we print out one integer per loop iteration. Keep in mind that in programming we tend to begin at index 0, so that is why although 5 numbers are printed out, they range from 0-4.  

You’ll commonly see and use for loops when a program needs to repeat a block of code a number of times.  

### For Loops using range()
One of Python’s built-in immutable sequence types is range(). In loops, range() is used to control how many times the loop will be repeated.  
When working with range(), you can pass between 1 and 3 integer arguments to it:  

- start states the integer value at which the sequence begins, if this is not included then start begins at 0
- stop is always required and is the integer that is counted up to but not included
- step sets how much to increase (or decrease in the case of negative numbers) the next iteration, if this is omitted then step defaults to 1

We’ll look at some examples of passing different arguments to `range()`.

First, let’s only pass the stop argument, so that our sequence set up is `range(stop)`:

```python
for i in range(6):
   print(i)
```
In the program above, the stop argument is 6, so the code will iterate from 0-6 (exclusive of 6):

```python
Output
0
1
2
3
4
5
```
Next, we’ll look at range(start, stop), with values passed for when the iteration should start and for when it should stop:  
```python
for i in range(20,25):
   print(i)
```  

Here, the range goes from 20 (inclusive) to 25 (exclusive), so the output looks like this:  

```python
Output
20
21
22
23
24
```  
The step argument of range() is similar to specifying stride while slicing strings in that it can be used to skip values within the sequence.

With all three arguments, step comes in the final position: range(start, stop, step). First, let’s use a step with a positive value:  

```python
for i in range(0,15,3):
   print(i)
```  
In this case, the for loop is set up so that the numbers from 0 to 15 print out, but at a step of 3, so that only every third number is printed, like so:


```python
Output
0
3
6
9
12
```  
We can also use a negative value for our step argument to iterate backwards, but we’ll have to adjust our start and stop arguments accordingly:  

```python
for i in range(100,0,-10):
   print(i)
```  

Here, 100 is the start value, 0 is the stop value, and -10 is the range, so the loop begins at 100 and ends at 0, decreasing by 10 with each iteration. We can see this occur in the output:

```python
Output
100
90
80
70
60
50
40
30
20
10
```  
When programming in Python, `for` loops often make use of the range() sequence type as its parameters for iteration.

### For Loops using Sequential Data Types
Lists and other data sequence types can also be leveraged as iteration parameters in for loops. Rather than iterating through a range(), you can define a list and iterate through that list.

We’ll assign a list to a variable, and then iterate through the list: 

```python
sharks = ['hammerhead', 'great white', 'dogfish', 'frilled', 'bullhead', 'requiem']

for shark in sharks:
   print(shark)
```  

In this case, we are printing out each item in the list. Though we used the variable shark, we could have called the variable any other valid variable name and we would get the same output:

```python
Output
hammerhead
great white
dogfish
frilled
bullhead
requiem
```  
The output above shows that the for loop iterated through the list, and printed each item from the list per line.

Lists and other sequence-based data types like strings and tuples are common to use with loops because they are iterable. You can combine these data types with range() to add items to a list, for example:


```python
sharks = ['hammerhead', 'great white', 'dogfish', 'frilled', 'bullhead', 'requiem']

for item in range(len(sharks)):
   sharks.append('shark')

print(sharks)
```  

```python
Output
['hammerhead', 'great white', 'dogfish', 'frilled', 'bullhead', 'requiem', 'shark', 'shark', 'shark', 'shark', 'shark', 'shark']
```  

Here, we have added a placeholder string of 'shark' for each item of the length of the sharks list.

You can also use a for loop to construct a list from scratch:

```python
integers = []

for i in range(10):
   integers.append(i)

print(integers)
```  

In this example, the list integers is initialized empty, but the for loop populates the list like so:

```python
Output
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```  

Similarly, we can iterate through strings:

```python
sammy = 'Sammy'

for letter in sammy:
   print(letter)
```  

```python
Output
S
a
m
m
y
```  

Iterating through tuples is done in the same format as iterating through lists or strings above.

When iterating through a dictionary, it’s important to keep the key : value structure in mind to ensure that you are calling the correct element of the dictionary. Here is an example that calls both the key and the value:

```python
sammy_shark = {'name': 'Sammy', 'animal': 'shark', 'color': 'blue', 'location': 'ocean'}

for key in sammy_shark:
   print(key + ': ' + sammy_shark[key])
```  


```python
Output
name: Sammy
animal: shark
location: ocean
color: blue
```  


When using dictionaries with for loops, the iterating variable corresponds to the keys of the dictionary, and dictionary_variable[iterating_variable] corresponds to the values. In the case above, the iterating variable key was used to stand for key, and sammy_shark[key] was used to stand for the values.

Loops are often used to iterate and manipulate sequential data types.  

### Nested For Loops
Loops can be nested in Python, as they can with other programming languages.

A nested loop is a loop that occurs within another loop, structurally similar to nested if statements. These are constructed like so: 


```python
for [first iterating variable] in [outer loop]: # Outer loop
    [do something]  # Optional
    for [second iterating variable] in [nested loop]:   # Nested loop
        [do something]  
```  


The program first encounters the outer loop, executing its first iteration. This first iteration triggers the inner, nested loop, which then runs to completion. Then the program returns back to the top of the outer loop, completing the second iteration and again triggering the nested loop. Again, the nested loop runs to completion, and the program returns back to the top of the outer loop until the sequence is complete or a break or other statement disrupts the process.

Let’s implement a nested for loop so we can take a closer look. In this example, the outer loop will iterate through a list of integers called num_list, and the inner loop will iterate through a list of strings called alpha_list.

```python
num_list = [1, 2, 3]
alpha_list = ['a', 'b', 'c']

for number in num_list:
    print(number)
    for letter in alpha_list:
        print(letter)
```  

When we run this program, we’ll receive the following output: 

```python
Output
1
a
b
c
2
a
b
c
3
a
b
c
```  
The output illustrates that the program completes the first iteration of the outer loop by printing 1, which then triggers completion of the inner loop, printing a, b, c consecutively. Once the inner loop has completed, the program returns to the top of the outer loop, prints 2, then again prints the inner loop in its entirety (a, b, c), etc.

Nested for loops can be useful for iterating through items within lists composed of lists. In a list composed of lists, if we employ just one for loop, the program will output each internal list as an item:

```python
list_of_lists = [['hammerhead', 'great white', 'dogfish'],[0, 1, 2],[9.9, 8.8, 7.7]]

for list in list_of_lists:
    print(list)
```  

```python
Output
['hammerhead', 'great white', 'dogfish']
[0, 1, 2]
[9.9, 8.8, 7.7]
```  
In order to access each individual item of the internal lists, we’ll implement a nested for loop:

```python
list_of_lists = [['hammerhead', 'great white', 'dogfish'],[0, 1, 2],[9.9, 8.8, 7.7]]

for list in list_of_lists:
    for item in list:
        print(item)
```  

```python
Output
hammerhead
great white
dogfish
0
1
2
9.9
8.8
7.7
```  


When we utilize a nested for loop we are able to iterate over the individual items contained in the lists.



### Conclusion

This tutorial went over how for loops work in Python and how to construct them. For loops continue to loop through a block of code provided a certain number of times.

From here, you can continue to learn about looping by reading tutorials on [while](https://www.digitalocean.com/community/tutorials/how-to-construct-while-loops-in-python-3) loops and [break, continue, and pass statements.](https://www.digitalocean.com/community/tutorials/how-to-use-break-continue-and-pass-statements-when-working-with-loops-in-python-3)
