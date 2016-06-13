---
title       : Loops Demo
description : There are several techniques to repeatedly execute Python code. While loops are like repeated if statements; the for loop is there to iterate over all kinds of data structures. Learn all about them in this chapter.
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/intermediate_python/intermediate_python_ch4_slides.pdf
  
--- type:MultipleChoiceExercise lang:python xp:50 skills:2 key:3859b984d9
## while: warming up

The while loop is like a repeated if statement. The code is executed over and over again, as long as the condition is `True`. Have another look at its recipe.

```
while condition :
    expression
```

Can you tell how many printouts the following `while` loop will do?

```
x = 1
while x < 4 :
    print(x)
    x = x + 1
```

*** =instructions
- 0
- 1
- 2
- 3
- 4

*** =hint
If you're not sure about the result, simply copy the code and paste it in the IPython Shell. How many lines are printed to the IPython Shell?

*** =sct
```{python}
icmsg = "Incorrect, try again. Try to simulate the while loop in your thoughts."
sucmsg = "Correct! After 3 runs, `x` will be equal to 4, causing `x < 4` to evaluate to `False`. This means that the `while` loop is executed 3 times, giving three printouts."
test_mc(4, msgs = [icmsg, icmsg, icmsg, sucmsg, icmsg]) # if 2 is the correct option.
```


--- type:NormalExercise lang:python xp:100 skills:2 key:c1152771dd
## Basic while loop

Below you can find the example from the video where the `error` variable, initially equal to `50.0`, is divided by 4 and printed out on every run:

```
error = 50.0
while error > 1 :
    error = error / 4
    print(error)
```

This example will come in handy, because it's time to build a `while` loop yourself! We're going to code a `while` loop that implements a very basic control system for a [reverted pendulum](https://en.wikipedia.org/wiki/Inverted_pendulum). If there's an offset from standing perfectly straight, the `while` loop will incrementally fix this offset.

*** =instructions
- Create the variable `offset` with an initial value of `8`.
- Code a `while` loop that keeps running as long as `offset` is not equal to `0`. Inside the `while` loop:
  + Print out the sentence "correcting...".
  + Next, decrease the value of `offset` by 1. You can do this with `offset = offset - 1`.
  + Finally, print out `offset` so you can see how it changes.

*** =hint
- Write `offset = 8` outside of the `while` loop to initialize the `offset` variable.
- The `while` loop condition is `offset != 0`. Inside the while loop you need three lines of code.

*** =sample_code
```{python}
# Initialize offset


# Code the while loop

```

*** =solution
```{python}
# Initialize offset
offset = 8

# Code the while loop
while offset != 0 :
    print("correcting...")
    offset = offset - 1
    print(offset)
```

*** =sct
```{python}
msg = "Keep looping while `offset != 0`"
for i in range(-1,2):
  test_while_loop(1, test=lambda i=i, msg=msg: test_expression_result({"offset": i}, incorrect_msg = msg))

msg = "Make sure you subtract `1` from `offset`"
for i in range(3,5):
  test_while_loop(1, body=lambda i=i, msg=msg: test_object_after_expression("offset", {"offset": i}, undefined_msg = msg, incorrect_msg = msg))
  
msg = "Make sure you first print out `\"correcting...\"` exactly and then print out `offset`, after you subtract `1` from it"
for i in range(3,5):
  test_while_loop(1, body=lambda i=i, msg=msg: test_expression_output({"offset": i}, incorrect_msg = msg))

test_object("offset")
  
success_msg("Well done!")
```

--- type:NormalExercise lang:python xp:100 skills:2 key:da45185854
## Add conditionals

The `while` loop that corrects the `offset` is a good start, but what if `offset` is negative? You can try to run the sample code on the right where `offset` is initialized to `-6`, but your sessions will be disconnected. The `while` loop will never stop running, because `offset` will be further decreased on every run. `offset != 0` will never become `False` and the `while` loop continues forever.

Fix things by putting an `if`-`else` statement inside the `while` loop.

*** =instructions
- Inside the `while` loop, replace `offset = offset - 1` by an `if`-`else` statement:
  + If `offset > 0`, you should decrease `offset` by 1.
  + Else, you should increase `offset` by 1.
- If you've coded things correctly, hitting _Submit Answer_ should work this time.

*** =hint
Inside the `while` loop, replace the second line with
```
if offset > 0 :
    offset = offset - 1
else :
    ...
```
Can you fill in the dots?

*** =sample_code
```{python}
# Initialize offset
offset = -6

# Code the while loop
while offset != 0 :
    print("correcting...")
    offset = offset - 1
    print(offset)
```

*** =solution
```{python}
# Initialize offset
offset = -6

# Code the while loop
while offset != 0 :
    print("correcting...")
    if offset > 0 :
        offset = offset - 1
    else :
        offset = offset + 1
    print(offset)
```

*** =sct
```{python}
msg = "Keep looping while `offset != 0`"
for i in range(-1,2):
  test_while_loop(1, test=lambda i=i, msg=msg: test_expression_result({"offset": i}, incorrect_msg = msg))

msg = "Make sure you subtract `1` from `offset` if it's `> 0` and else add `1`"
for i in range(-3,3):
  test_while_loop(1, body=lambda i=i, msg=msg: test_object_after_expression("offset", {"offset": i}, undefined_msg = msg, incorrect_msg = msg))
  
msg = "Make sure you first print out `\"correcting...\"` exactly and then print out `offset`, after you changed it"
for i in range(-3,3):
  test_while_loop(1, body=lambda i=i, msg=msg: test_expression_output({"offset": i}, incorrect_msg = msg))

test_object("offset")

success_msg("Good work! The `while` loop is not that often used in Data Science, so let's head over to the `for` loop.")
```

--- type:VideoExercise lang:python xp:50 skills:2 key:90b30275d6
## for loop

*** =video_link
//player.vimeo.com/video/148376018

*** =video_hls
//videos.datacamp.com/transcoded/799_intermediate_python/v1/hls-ch4_2.master.m3u8

--- type:NormalExercise lang:python xp:100 skills:2 key:3f7ec57dda
## Loop over a list

Have another look at the `for` loop that Filip showed in the video:

```
fam = [1.73, 1.68, 1.71, 1.89]
for height in fam : 
    print(height)
```

As usual, you simply have to indent the code with 4 spaces to tell Python which code should be executed in the `for` loop.

The `areas` variable, containing the area of different rooms in your house, is already defined.

*** =instructions
Write a `for` loop that iterates over all elements of the `areas` list and prints out every element separately.

*** =hint
Copy and paste the example code and change some variables. This time you're working with `areas` instead of `fam`.

*** =sample_code
```{python}
# areas list
areas = [11.25, 18.0, 20.0, 10.75, 9.50]

# Code the for loop

```

*** =solution
```{python}
# areas list
areas = [11.25, 18.0, 20.0, 10.75, 9.50]

# Code the for loop
for area in areas :
    print(area)
```

*** =sct
```{python}
msg = "Make sure to loop over `areas`"
test_for_loop(1, for_iter=lambda msg=msg: test_expression_result(incorrect_msg = msg))

msg = "Print out `area`"
test_for_loop(1, body=lambda msg=msg: test_expression_output(incorrect_msg = msg, context_vals = ["test"]))
success_msg("Great! That wasn't too hard, was it?")
```

--- type:NormalExercise lang:python xp:100 skills:2 key:5cd8886454
## Indexes and values (1)

Using a `for` loop to iterate over a list only gives you access to every list element in each run, one after the other. If you also want to access the index information, so where the list element you're iterating over is located, you can use [`enumerate()`](https://docs.python.org/3/library/functions.html#enumerate).

As an example, have a look at how the `for` loop from the video was converted:

```
fam = [1.73, 1.68, 1.71, 1.89]
for index, height in enumerate(fam) :
    print("index " + str(index) + ": " + str(height))
```

*** =instructions
Adapt the `for` loop in the sample code to use [`enumerate()`](https://docs.python.org/3/library/functions.html#enumerate). On each run, a line of the form `"room x: y"` should be printed, where x is the index of the list element and y is the actual list element, i.e. the area. Make sure to print out this exact string, with the correct spacing.

*** =hint
Copy and paste the example code and change some variables. You'll also have to adapt the [`print()`](https://docs.python.org/3/library/functions.html#print) statement. Pay attention to the correct spacing and capitalization!

*** =sample_code
```{python}
# areas list
areas = [11.25, 18.0, 20.0, 10.75, 9.50]

# Change for loop to use enumerate()
for a in areas :
    print(a)
```

*** =solution
```{python}
# areas list
areas = [11.25, 18.0, 20.0, 10.75, 9.50]

# Code the for loop
for index, area in enumerate(areas) :
    print("room " + str(index) + ": " + str(area))
```

*** =sct
```{python}
msg = "Make sure to loop over `index, area` in `enumerate(areas)`"
test_for_loop(1, for_iter=lambda msg=msg: test_function("enumerate", not_called_msg = msg, incorrect_msg = msg))

msg = "Have another look at the example. Print out the correct string, with the correct spacing"
test_for_loop(1, body=lambda msg=msg: test_expression_output(incorrect_msg = msg, context_vals = [2, "test"]))

success_msg("Well done!")
```

--- type:NormalExercise lang:python xp:100 skills:2 key:a31c388208
## Indexes and values (2)

For non-programmer folks, `room 0: 11.25` is strange. Wouldn't it be better if the count started at 1?

*** =instructions
Adapt the [`print()`](https://docs.python.org/3/library/functions.html#print) function in the `for` loop on the right so that the first printout becomes `"room 1: 11.25"`, the second one `"room 2: 18.0"` and so on.

*** =hint
Only a small change is needed: add `+1` at the appropriate location.

*** =sample_code
```{python}
# areas list
areas = [11.25, 18.0, 20.0, 10.75, 9.50]

# Code the for loop
for index, area in enumerate(areas) :
    print("room " + str(index) + ": " + str(area))
```

*** =solution
```{python}
# areas list
areas = [11.25, 18.0, 20.0, 10.75, 9.50]

# Adapt the printout
for index, area in enumerate(areas) :
    print("room " + str(index + 1) + ": " + str(area))
```

*** =sct
```{python}
msg = "Do not change or remove `areas`, it was coded for you."
test_object("areas", undefined_msg = msg, incorrect_msg = msg)

msg = "Make sure to loop over `index, area` in `enumerate(areas)`"
test_for_loop(1, for_iter=lambda msg=msg: test_function("enumerate", not_called_msg = msg, incorrect_msg = msg))

msg = "Loop `index, areas` over `enumerate(areas)` and print out `index + 1`"
test_for_loop(1, body=lambda msg=msg: test_expression_output(incorrect_msg = msg, context_vals = [2, "test"]))

success_msg("Much better!")
```

--- type:NormalExercise lang:python xp:100 skills:2 key:c3a959fe62
## Loop over list of lists

Remember the `house` variable from the Intro to Python course? Have a look at its definition on the right. It's basically a list of lists, where each sublist contains the name and area of a room in your house.

It's up to you to build a `for` loop from scratch this time!

*** =instructions
Write a `for` loop that goes through each sublist of `houses` and prints out `the x is y sqm`, where x is the name of the room and y is the area of the room.

*** =hint
If your `for` loop is defined as:
```
for x in house :
    ...
```
You can use `x[0]` to access the name of the room and `x[1]` to access the corresponding area. The [`print()`](https://docs.python.org/3/library/functions.html#print) calls should then be:
```
print("the " + str(x[0]) + " is " + str(x[1]) + " sqm")
```

*** =sample_code
```{python}
# house list of lists
house = [["hallway", 11.25], 
         ["kitchen", 18.0], 
         ["living room", 20.0], 
         ["bedroom", 10.75], 
         ["bathroom", 9.50]]
         
# Build a for loop from scratch
```

*** =solution
```{python}
# house list of lists
house = [["hallway", 11.25], 
         ["kitchen", 18.0], 
         ["living room", 20.0], 
         ["bedroom", 10.75], 
         ["bathroom", 9.50]]
         
# Build a for loop from scratch
for x in house :
    print("the " + str(x[0]) + " is " + str(x[1]) + " sqm")
```

*** =sct
```{python}
msg = "Do not change or remove `house`, it was coded for you."
test_object("house", undefined_msg = msg, incorrect_msg = msg)

msg = "Make sure to loop over `x` in `house` (you don't need [`enumerate()`](https://docs.python.org/3/library/functions.html#enumerate) here)"
test_for_loop(1, for_iter=lambda msg=msg: test_expression_result(incorrect_msg = msg))

msg = "Have another look at the instructions. Did you print out the exact strings that were asked for? You can use `x[0]` and `str(x[1])` to print out the name of the room and the area as a string"
test_for_loop(1, body=lambda msg=msg: test_expression_output(incorrect_msg = msg, context_vals = ["test", 30]))

success_msg("Off to next video!")
```

--- type:VideoExercise lang:python xp:50 skills:2 key:be56896aad
## Looping Data Structures, Part 1

*** =video_link
//player.vimeo.com/video/148376019

*** =video_hls
//videos.datacamp.com/transcoded/799_intermediate_python/v1/hls-ch4_3.master.m3u8

--- type:NormalExercise lang:python xp:100 skills:2 key:f5cc571625
## Loop over dictionary

In Python 3, you need the [`items()`](https://docs.python.org/3/library/stdtypes.html#dict.items) method to loop over a dictionary:

```
world = { "afghanistan":30.55, 
          "albania":2.77,
          "algeria":39.21 }
          
for key, value in world.items() :
    print(key + " -- " + str(value))
```

Remember the `europe` dictionary that contained the names of some European countries as key and their capitals as corresponding value? Go ahead and write a loop to iterate over it!

*** =instructions
Write a `for` loop that goes through each key:value pair of `europe`. On each iteration, `"the capital of x is y"` should be printed out, where x is the key and y is the value of the pair.

*** =hint
- Start from the example code and change some variable names: it's `europe` instead of `world` now.
- If the key is set to `key` and the value to `value` in each iteration, you'll need the following [`print()`](https://docs.python.org/3/library/functions.html#print) call:
```
print("the capital of " + str(key) + " is " + str(value))
```

*** =sample_code
```{python}
# Definition of dictionary
europe = {'spain':'madrid', 'france':'paris', 'germany':'bonn', 
          'norway':'oslo', 'italy':'rome', 'poland':'warsaw', 'australia':'vienna' }
          
# Iterate over europe

```

*** =solution
```{python}
# Definition of dictionary
europe = {'spain':'madrid', 'france':'paris', 'germany':'bonn', 
          'norway':'oslo', 'italy':'rome', 'poland':'warsaw', 'australia':'vienna' }
          
# Iterate over europe
for key, value in europe.items() :
     print("the capital of " + str(key) + " is " + str(value))
```

*** =sct
```{python}
msg = "Do not change or remove `europe`, it was coded for you."
test_object("europe", undefined_msg = msg, incorrect_msg = msg)

msg = "Make sure to loop over `key, value` in `europe`"
test_for_loop(1, for_iter=lambda msg=msg: test_expression_result(incorrect_msg = msg))

msg = "Have another look at the instructions. Print out the exact strings that were asked for"
test_for_loop(1, body=lambda msg=msg: test_expression_output(incorrect_msg = msg, context_vals = ["test", "nothing"]))

success_msg("Great! Notice that the order of the printouts doesn't correspond with the order used when defining `europe`. Remember: dictionaries are inherently unordered!")
```

--- type:NormalExercise lang:python xp:100 skills:2 key:f1abea987c
## Loop over Numpy array

If you're dealing with a 1D Numpy array, looping over all elements can be as simple as:

```
for x in my_array :
    ...
```

If you're dealing with a 2D Numpy array, it's more complicated. A 2D array is built up of multiple 1D arrays. To explicitly iterate over all separate elements of a multi-dimensional array, you'll need this syntax:

```
for x in np.nditer(my_array) :
    ...
```

Two Numpy arrays that you might recognize from the intro course are available in your Python session: `np_height`, a Numpy array containing the heights of Major League Baseball players, and `np_baseball`, a 2D Numpy array that contains both the heights (first column) and weights (second column) of those players.

*** =instructions
- Import the `numpy` package under the local alias `np`.
- Write a `for` loop that iterates over all elements in `np_height` and prints out `"x inches"` for each element, where x is the value in the array.
- Write a `for` loop that visits every element of the `np_baseball` array and prints it out.

*** =hint
- Inside the first `for` loop use `print(str(el) + " inches")` if `el` is an element of the Numpy array.
- In the second `for` loop, use `np.nditer(np_baseball)`.

*** =pre_exercise_code
```{python}
import pandas as pd
import numpy as np
mlb = pd.read_csv("http://s3.amazonaws.com/assets.datacamp.com/course/intro_to_python/baseball.csv")
np_height = np.array(mlb['Height'])
np_baseball = np.array(mlb[['Height', 'Weight']])
```

*** =sample_code
```{python}
# Import numpy as np


# For loop over np_height


# For loop over np_baseball
```

*** =solution
```{python}
# Import numpy as np
import numpy as np

# For loop over np_height
for x in np_height :
    print(str(x) + " inches")

# For loop over np_baseball
for x in np.nditer(np_baseball) :
    print(x)
```

*** =sct
```{python}
test_import("numpy",
  not_imported_msg = "You can import numpy by using `import numpy`.",
  incorrect_as_msg = "You should set the correct alias for `numpy`, import it `as np`.")


msg = "`np_height` is a 1D array. You can loop over it using `x in np_height`, no need to use `np.nditer()`"
test_for_loop(1, for_iter=lambda msg=msg: test_expression_result(incorrect_msg = msg))

msg = "Have another look at the instructions. Print out the exact strings that were asked for"
test_for_loop(1, body=lambda msg=msg: test_expression_output(incorrect_msg = msg, context_vals = [3]))

msg = "Make sure to loop over `x` in `np.nditer(np_baseball)`"
test_for_loop(2, for_iter=lambda msg=msg: test_function("numpy.nditer", not_called_msg = msg, incorrect_msg = msg))

msg = "Have another look at the instructions. Print out the exact strings that were asked for"
test_for_loop(2, body=lambda msg=msg: test_expression_output(incorrect_msg = msg, context_vals = [3]))

success_msg("Wow, that's a lot of output! Try to add an additional argument `end = " "` to the [`print()`](https://docs.python.org/3/library/functions.html#print) call - the output will be mesmerizing!")

```

--- type:VideoExercise lang:python xp:50 skills:2 key:9be6d4ed29
## Looping Data Structures, Part 2

*** =video_link
//player.vimeo.com/video/152824186

*** =video_hls
//videos.datacamp.com/transcoded/799_intermediate_python/v1/hls-ch4_4.master.m3u8


--- type:NormalExercise lang:python xp:100 skills:2 key:8d7faf58dc
## Loop over DataFrame (1)

Iterating over a Pandas DataFrame is typically done with the [`iterrows()`](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.iterrows.html) method. Used in a `for` loop, every observation is iterated over and on every iteration the row label and actual row contents are available:

```
for lab, row in brics.iterrows() :
    ...
```

In this and the following exercises you will be working on the `cars` DataFrame. It contains information on the cars per capita and whether people drive right or left for seven countries in the world.

*** =instructions
Write a `for` loop that iterates over the rows of `cars` and on each iteration perform two [`print()`](https://docs.python.org/3/library/functions.html#print) calls: one to print out the row label and one to print out all of the rows contents.

*** =hint
Start from the the code example. change the `brics` variable to `cars` and replace `...` with two [`print()`](https://docs.python.org/3/library/functions.html#print) calls.

*** =pre_exercise_code
```{python}
f = open('cars.csv', "w")
f.write(""",cars_per_cap,country,drives_right
US,809,United States,True
AUS,731,Australia,False
JAP,588,Japan,False
IN,18,India,False
RU,200,Russia,True
MOR,70,Morocco,True
EG,45,Egypt,True""")
f.close()
```

*** =sample_code
```{python}
# Import cars data
import pandas as pd
cars = pd.read_csv('cars.csv', index_col = 0)

# Iterate over rows of cars

```

*** =solution
```{python}
# Import cars data
import pandas as pd
cars = pd.read_csv('cars.csv', index_col = 0)

# Iterate over rows of cars
for lab, row in cars.iterrows() :
    print(lab)
    print(row)
```

*** =sct
```{python}
msg = "Don't change or remove the predefined import."
test_import("pandas", not_imported_msg = msg, incorrect_as_msg = msg)

msg = "Don't change or remove the predefined DataFrame, `cars`."
test_object("cars", undefined_msg = msg, incorrect_msg = msg)

msg = "Make sure to loop over `lab, row` in `cars.iterrows()`"
test_for_loop(1, for_iter=lambda msg=msg: test_function("cars.iterrows", not_called_msg = msg, incorrect_msg = msg))

msg = "Have another look at the instructions. Print out the exact strings that were asked for. You will two [`print()`](https://docs.python.org/3/library/functions.html#print) calls"
test_for_loop(1, body=lambda msg=msg: test_expression_output(incorrect_msg = msg, context_vals = ["a lab", "a row"]))

success_msg("Well done!")
```

--- type:NormalExercise lang:python xp:100 skills:2 key:b0fd26d4e3
## Loop over DataFrame (2)

The row data that's generated by [`iterrows()`](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.iterrows.html) on every run is a Pandas Series. This format is not very convenient to print out. Luckily, you can easily select variables from the Pandas Series using square brackets:

```
for lab, row in brics.iterrows() :
    print(row['country'])
```

*** =instructions
Adapt the code in the for loop such that the first iteration prints out `"US: 809"`, the second iteration `"AUS: 731"`, and so on. Make sure to print out this exact string, with the correct spacing.

*** =hint
- You don't have to change anything about `for lab, row in cars.iterrows()`.
- Remove the two printouts and put another one instead. Inside the [`print()`](https://docs.python.org/3/library/functions.html#print) call you'll need `str(row['cars_per_cap'])`.

*** =pre_exercise_code
```{python}
f = open('cars.csv', "w")
f.write(""",cars_per_cap,country,drives_right
US,809,United States,True
AUS,731,Australia,False
JAP,588,Japan,False
IN,18,India,False
RU,200,Russia,True
MOR,70,Morocco,True
EG,45,Egypt,True""")
f.close()
```

*** =sample_code
```{python}
# Import cars data
import pandas as pd
cars = pd.read_csv('cars.csv', index_col = 0)

# Adapt for loop
for lab, row in cars.iterrows() :
    print(lab)
    print(row)
```

*** =solution
```{python}
# Import cars data
import pandas as pd
cars = pd.read_csv('cars.csv', index_col = 0)

# Adapt for loop
for lab, row in cars.iterrows() :
    print(lab + ": " + str(row['cars_per_cap']))
```

*** =sct
```{python}
msg = "Don't change or remove the predefined import."
test_import("pandas", not_imported_msg = msg, incorrect_as_msg = msg)

msg = "Don't change or remove the predefined DataFrame, `cars`."
test_object("cars", undefined_msg = msg, incorrect_msg = msg)

msg = "Make sure to loop over `lab, row` in `cars.iterrows()`"
test_for_loop(1, for_iter=lambda msg=msg: test_function("cars.iterrows", not_called_msg = msg, incorrect_msg = msg))

msg = "Have another look at the instructions. Print out the exact strings that were asked for, with the correct spacing. You should use this statement: `str(row['cars_per_cap'])` somewhere in the [`print()`](https://docs.python.org/3/library/functions.html#print) statement"
test_for_loop(1, body=lambda msg=msg: test_expression_output(incorrect_msg = msg, context_vals = ["a lab", {"cars_per_cap": 3}]))

success_msg("Nice!")
```

--- type:NormalExercise lang:python xp:100 skills:2 key:84efa4277e
## Add column (1)

In the video, Filip showed you how to add the length of the country names of the `brics` DataFrame in a new column:

```
for lab, row in brics.iterrows() :
    brics.loc[lab, "name_length"] = len(row["country"])
```

You can do similar things on the `cars` DataFrame.

*** =instructions
- Use a `for` loop to add a new column, named `COUNTRY`, that contains a uppercase version of the country names in the `"country"` column. You can use the string method [`upper()`](https://docs.python.org/2/library/stdtypes.html#str.upper) for this.
- To see if your code worked, print out `cars`. Don't indent this code, so that it's not part of the `for` loop.

*** =hint
- Start from the code example and replace `brics` with `cars`. This time you want to create a column named `"COUNTRY"`. You'll also need `row["country"].upper()`.
- To print out a variable `x`, write `print(x)` on a new line in the script. Don't indent this line!

*** =pre_exercise_code
```{python}
f = open('cars.csv', "w")
f.write(""",cars_per_cap,country,drives_right
US,809,United States,True
AUS,731,Australia,False
JAP,588,Japan,False
IN,18,India,False
RU,200,Russia,True
MOR,70,Morocco,True
EG,45,Egypt,True""")
f.close()
```

*** =sample_code
```{python}
# Import cars data
import pandas as pd
cars = pd.read_csv('cars.csv', index_col = 0)

# Code for loop that adds COUNTRY column



# Print cars
print(cars)
```

*** =solution
```{python}
# Import cars data
import pandas as pd
cars = pd.read_csv('cars.csv', index_col = 0)

# Code for loop that adds COUNTRY column
for lab, row in cars.iterrows() :
    cars.loc[lab, "COUNTRY"] = row["country"].upper()
    
# Print cars
print(cars)
```

*** =sct
```{python}
msg = "Don't change or remove the predefined import."
test_import("pandas", not_imported_msg = msg, incorrect_as_msg = msg)

msg = "Make sure to loop over `lab, row` in `cars.iterrows()`"
test_for_loop(1, for_iter=lambda msg=msg: test_function("cars.iterrows", not_called_msg = msg, incorrect_msg = msg))

msg = "Have another look at the instructions. Use `cars.loc[lab, 'COUNTRY'] = row[...].upper()`"
test_for_loop(1, body=lambda msg=msg: test_object_after_expression("cars", incorrect_msg = msg, context_vals = ["AUS", {"country": "australia", "cars_per_cap": 3}]))

msg = "Make sure to print out the result using `print(cars)`."
test_function("print", not_called_msg = msg, incorrect_msg = msg)

success_msg("Great, but you might remember that there is also an easier way to do this.")
```

--- type:NormalExercise lang:python xp:100 skills:2 key:ba24be46f5
## Add column (2)

Using [`iterrows()`](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.iterrows.html) to iterate over every observation of a Pandas DataFrame is easy to understand, but not very efficient. On every iteration, you're creating a new Pandas Series.

If you want to add a column to a DataFrame by calling a function on another column, the [`iterrows()`](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.iterrows.html) method in combination with a `for` loop is not the preferred way to go. Instead, you'll want to use [`apply()`](http://http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.apply.html).

Compare the [`iterrows()`](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.iterrows.html) version with the [`apply()`](http://http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.apply.html) version to get the same result in the `brics` DataFrame:

```
for lab, row in brics.iterrows() :
    brics.loc[lab, "name_length"] = len(row["country"])
    
brics["name_length"] = presidents["country"].apply(len)
```

We can do a similar thing to call the [`upper()`](https://docs.python.org/2/library/stdtypes.html#str.upper) method on every name in the `country` column. However, [`upper()`](https://docs.python.org/2/library/stdtypes.html#str.upper) is a **method**, so we'll need a slightly different approach:


*** =instructions
- Replace the `for` loop with a one-liner that uses `.apply(str.upper)`. The call should give the same result: a column `COUNTRY` should be added to `cars`, containing an uppercase version of the country names.
- As usual, print out `cars` to see the fruits of your hard labor

*** =hint
- You'll need `cars["..."] = cars["..."].apply(str.upper)`

*** =pre_exercise_code
```{python}
f = open('cars.csv', "w")
f.write(""",cars_per_cap,country,drives_right
US,809,United States,True
AUS,731,Australia,False
JAP,588,Japan,False
IN,18,India,False
RU,200,Russia,True
MOR,70,Morocco,True
EG,45,Egypt,True""")
f.close()
```

*** =sample_code
```{python}
# Import cars data
import pandas as pd
cars = pd.read_csv('cars.csv', index_col = 0)

# Use .apply(str.upper)
for lab, row in cars.iterrows() :
    cars.loc[lab, "COUNTRY"] = row["country"].upper()
```

*** =solution
```{python}
# Import cars data
import pandas as pd
cars = pd.read_csv('cars.csv', index_col = 0)

# Use .apply(str.upper)
cars["COUNTRY"] = cars["country"].apply(str.upper)
```

*** =sct
```{python}
msg = "Don't change or remove the predefined import."
test_import("pandas", not_imported_msg = msg, incorrect_as_msg = msg)

msg = "You have to change the `\"COUNTRY\"` column of the `cars` DataFrame using `cars[\"country\"].apply(str.upper)`."
test_object("cars", undefined_msg = msg, incorrect_msg = msg)
test_student_typed("\]\s*\.\s*apply\s*\(", not_typed_msg = msg)
success_msg("Great job! It's time to blend everything you've learned together in a case-study. Head over to the next chapter!")
```
