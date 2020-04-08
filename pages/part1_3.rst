.. title: part1_3
.. slug: part1_3
.. date: 2020-04-08 14:59:39 UTC-06:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

Part 1c - Writing Function to Compute Wind Chill Index
This is intended to pick off right where part 1b left off- you had just commited your new script that reads the file, saving the variables of date, time, and tempout in a data dictionary.

In this section you will compute wind chill index by writing your first function and learning about basic math operators.

python Okay, now that you've read the data in a way thatis easy to modify later, it is time to actually do something with the data.

Compute the wind chill factor, which is the cooleing effect of the wind. As wind speed increases the rate at which a body loses heat increases. The formula for this is:

W
C
I
=
a
+
(
b
∗
t
)
−
(
c
∗
v
2
)
+
(
d
∗
t
∗
v
2
)

Where WCI refers to the Wind Chill in degrees F, t is temperature in degrees F, v is wind speed in mph, and the other variables are as follows: a = 35.74, b = 0.6215, c = 35.75, and d = 0.4275. Wind Chill Index is only defined for temperatures within the range -45 to +45 degrees F.

You've read the temperature data into the tempout variable, but to do this calculationyou also needto read the windspeed variable from column 7.

Modify the columns variable to read:

columns = {'date': 0, 'time': 1, 'tempout': 2, 'windspeed': 7}
and modify the types variable to be:

types = {'tempout': float, 'windspeed': float}
git Great! Save this in your git repo. Stage and commit (git commit -m "Reading windspeed as well").
python Now, let's write our first function to computethe wind chill factor. We'll add this function to the bottom of the file.

# Compute the wind chill temperature
def compute_windchill(temp, windspeed):
   a = 35.74
   b = 0.6215
   c = 35.75
   d = 0.4275

   v16 = windspeed ** 0.16
   wci = a + (b * temp) - (c * v16) + (d * temp * v16)
   return wci
To indicate a function in python you type def for define, the name of your function, and then in parenthesis the input arguments of that function, followed by a colon. On the next lines tab-indented is the code of your function, and your return value.

Here is your first introduction math operators in Python. Addition, subtraction, and multiplication look much like you'd expect. A double astericks, **, indicates an exponential. A backslash, /, is for division, and a double backslash, //, is for integer division.

And then let's compute a new list with windchill data atthe bottom of mysci.py:

# Let's actually compute the wind chill factor
windchill = []
for temp, windspeed in zip(data['tempout'], data['windspeed']):
    windchill.append(compute_windchill(temp, windspeed))
Now we'll call our function. Initialize a list for wind chill with empty square brackets, []. And in a for loop, loop through our temperature and wind speed data, applying the function to each tuple data pair. tuples are ordered like lists, but they are indicated by parenthesis, (), instead of square brackets and cannot be changed or appended. tuples are generally faster than lists.

We use the zip function in Python to automatically unravel the tuples. Take a look at zip([1,2], [3,4,5]). What is the result?

And finally, add a DEBUG section to see theresults:

# DEBUG
print(windchill)
git Clean up, stage, and commit (git commit -m "Compute wind chill factor")
python Now, the wind chill factor is actually in the data file, so we can read it from the file and compare that value to our computed values. To do this, we need to read the windchill from column 12 as a float:

Edit the columns and types dictionaries:

columns = {'date': 0, 'time': 1, 'tempout': 2, 'windspeed': 7,
           'windchill': 12}
NOTE: the line continuation indentation

and

types = {'tempout': float, 'windspeed': float, 'windchill': float}
Then, in a DEBUG section at the end of your script to compare the two different values (from data and computed by our function):

# DEBUG
for wc_data, wc_comp in zip(data['windchill'], windchill):
    print(f'{wc_data:.5f}   {wc_comp:.5f}   {wc_data - wc_comp:.5f}')
Using f-strings with float formatting you can determine the precision with which to print the values to. .5f means you want 5 places after the decimal point.

Test the results. What do you see? Our computation isn't very good is it?

git Clean up, stage, and commit (git commit -m "Compare wind chill factors")
python Now, format the output so that it's easy to understand and rename this script to something indicative of what it actually does.

To the end of the file, add:

# Output comparison of data
print('                ORIGINAL  COMPUTED')
print(' DATE    TIME  WINDCHILL WINDCHILL DIFFERENCE')
print('------- ------ --------- --------- ----------')
for date, time, wc_orig, wc_comp in zip(data['date'], data['time'], data['windchill'], windchill):
    print(f'{date} {time:>6} {wc_orig:9.6f} {wc_comp:9.6f} {wc_orig-wc_comp:10.6f}')
Here you used f-string formatting with more f-string formatting options. >6 indicates that you'd like the characters of the string to be right-justified and to take up 6 spaces.

9f specifies that you want the value to fill 9 spaces, so 9.6f indicates you'd like the value to fill 9 spaces with 6 of them being after the decimal point. Same concept for 10.6f

You now have your first complete Python script!

git DON'T CLEAN UP! Just stage and commit(git commit -m "Output formatting comparison data")
git Let's rename this script to something meaningful and indicative of the computation inside.

$ git mv mysci.py windchillcomp.py
$ git commit -m "Renaming first script"
git Let's push to GitHub!

First you have to create a remote repository.

Go to https://github.com/ and create or login to your account.
At the top right of any Github page, there is a '+' icon. Click that, then select 'New Repository'.
Name your repository, "NCAR_python_tutorial_2020".

It is best practice for your local project and GitHub repository to share a name.

And click "Create Repository"
Copy the link to your GitHub repository.

Typically this will have the form: Copy the link in the input right beneath the title, it should look something like this: "https://github.com/<user_name>/NCAR_python_tutorial_2020.git"

Then to set your remote repository, in your project terminal type:

$ git remote add origin <remote repository URL>
And verify your remote repository:

$ git remote -v
And finally push your project to GitHub:

$ git push origin master
Think of GitHub as online storage for versions of your project, much like hosting your code in a Google Drive, but with better features specific to coding. A lot of GitHub's features show their usefulness when you are working collaboratively, sharing your code with other scientists, or if you wanted to display and easily visualize changes in your code between commits.





That concludes the part 1 of this virtual tutorial where you learned to write your first Python script.

In this section you calculated wind chill index by writing and calling your first function. You also learned about Python math operators, the zip() command, tuple datastructure, f-string formatting, and how to push your repository to GitHub.

