.. title: part1_1
.. slug: part1_1
.. date: 2020-04-08 14:38:38 UTC-06:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
.. hidetitle: True

=========================
1.1 - First Python Script
=========================

This section of the Zero to Thirty tutorial will focus on teaching you Python through the creation of your first script. 

You will learn about syntax and the reasoning behind why things are done the way they done along the way. 

We will also incorporate lessons on the use of git because we highly you recommend version controling your work.

We are assuming you are familiar with bash and terminal commands. If not `here is a cheat sheet <https://cheatography.com/davechild/cheat-sheets/linux-command-line/>`_

Part 1.1 - Reading a .txt File
------------------------------

In building your first Python script we will set up our workspace, read a .txt file, and learn git fundamentals.

Open a terminal to begin:

1. Create a directory:

    $ mkdir ncar_python_tutorial

    The first thing we have to do is create a directory to store our work. Let's call it "ncar_python_tutorial."

2. Go into the directory:

    $ cd ncar_python_tutorial

3. Create a virtual environment for this project:

    $ conda create --name ncar_python_tutorial python
    A conda environment is a directory that contains a collection of packages or libraries that you would like installed and accessible for this workflow. Type conda create --name , the name of your project, here that is "ncar_python_tutorial," and then specify that you are using python to create a virtual environment for this project.

    It is a good idea to create new environments for different projects because since Python is open source, new versions of the tools you use may become available. This is a way of guaranteeing that your script will use the same versions of packages and libraries and should run the same as you expect it to.

4. Make the directory a git repository:

    $ git init .

    A Git repository tracks changes made to files within your project. It looks like a .git/ folder inside that project.

    This command adds version control to this new ncar_python_tutorial directory and all of its contents.

5. Create a data directory:

    $ mkdir data
    And we'll make a directory for our data.

6. Go into the data directory:

    $ cd data

7. Download sample data from the CU Boulder weather station:

    $ curl -O https://sundowner.colorado.edu/weather/atoc8/wxobs20170821.txt

    This weather station is a Davis Instruments wireless Vantage Pro2 located on the CU-Boulder east campus at the SEEC building (40.01 N, 05.24 W, 5250 ft elevation). The station is monitored by the Atmospheric and Oceanic Sciences (ATOC) department and is part of the larger University of Colorado ATOC Weather Network.

8. Check the status of your repository

    $ git status

    You will see the newly downloaded file listed as an "untracked file." Git status will tell you what to do to untracked files. Those instructions mirror the next 2 steps:

9. Add the file to the git staging area:

    $ git add wxobs20170821.txt

    By adding this datafile to your directory, you have made a change that is not yet reflected in our git repository. Type "git add" and then the name of the altered file to stage your change.

10. Check your git status once again

    $ git status

    Now this file is listed as a "change to be commited," i.e. staged. Staged changes can now be commited to your repository history.

11 Commit the file to the git repository:

    $ git commit -m "Adding sample data file"

    With "git commit", you've updated your repository with all the changes you staged, in this case just one file.

12. Look at the git logs:

    $ git log

    If you type "git log" you will show a log of all the commits, or changes made to your repository.

13. Go back to the top-level directory:

    $ cd ..

14. And now that you've set up our workspace, create a blank Python script, called "mysci.py":

    $ touch mysci.py

15. Edit the mysci.py file using nano, vim, or your favorite text editor:

. . code-block:: python

    print("Hello, world!")

::


        Your classic first command will be to print "Hello World".

16. Try testing the script by typing "python" and then the name of your script:

    $ python mysci.py

Yay! You've just created your first Python script.

17. You probably won't need to run your Hello World script again, so delete the print("Hello, world!") line and start over with something more useful - we'll read the first 4 lines from our datafile.

    Change the mysci.py script to read:
.. code_block:: python

    # Read the data file
    filename = "data/wxobs20170821.txt"
    datafile = open(filename, 'r')

    print(datafile.readline())
    print(datafile.readline())
    print(datafile.readline())
    print(datafile.readline())

    datafile.close()

::
    
    First create a variable for your datafile name, which is a string - this can be in single or double quotes.

    Then create a variable associated with the opened file, here it is called datafile.

    The 'r' argument in the open command indicates that we are opening the file for reading capabilities. Other input arguments for open include 'w', for example, if you wanted to write to the file.

    The readline command moves through the open file, always reading the next line.

    And remember to close your datafile.

    Comments in Python are indicated with a hash, as you can see in the first line # Read the data file. Comments are ignored by the interpreter.

18. And test your script again by typing:

    $ python mysci.py

    Testing of your script with python mysci.py should be done every time you wish to execute the script. This will no longer be specified as a unique step in between every change to our script.

19. Change the mysci.py script to read your whole data file:

.. code-block:: python

    # Read the data file
    filename = "data/wxobs20170821.txt"
    datafile = open(filename, 'r')
    data = datafile.read()
    datafile.close()

    # DEBUG
    print(data)
    print('data')

::

    Our code is similar to the before, but now we've read the entire file. To test that this worked. We'll print(data). Print statements in python require parenthesis around the object you wish to print, here it is data.

    Try print('data') as well, now Python will print the string 'data', as it did for the hello world function, instead of the information stored in the variable data.

    Don't forget to execute with python mysci.py

20. Change the mysci.py script to read your whole data file using a context manager with:

.. code-block:: python

    # Read the data file
    filename = "data/wxobs20170821.txt"
    with open(filename, 'r') as datafile:
    data = datafile.read()

    # DEBUG
    print(data)

::

    Again this is a similar method of opening the datafile, but we now use with open. The with statement is a context manager that provides clean-up and assures that the file is automatically closed after you've read it.

    The indendation of the line data = datafile.read() is very important. Python is sensitive to white space and will not work if you mix spaces and tabs (Python does not know your tab width). It is best practice to use spaces as opposed to tabs (tab width is not consistent between editors).

    Combined these two lines mean: with the datafile opened, I'd like to read it.

    And execute with python mysci.py.

21. What did we just see? What is the data object? What type is data? How do we find out?

    Add the following to the DEBUG section of our script:

.. code-block:: python

    print(type(data))

::

    And execute with `python mysci.py`

    Object types refer to 'float' 'integer' 'string' or other types that you can create.

    Python is a dynamically typed language, which means you don't have to explicitly specify the datatype when you name a variable, Python will automatically figure it out by the nature of the data.

22. Now, clean up the script by removing the DEBUG section, before we commit this to git.

23. Let's check the status of our git repository

    $ git status

    Note what files have been changed in the repository.

24. Stage these changes:

    $ git add mysci.py

25. Let's check the status of our git repository,again. What's different from the last time we checked the status?

    $ git status

26. Commit these changes:

    $ git commit -m "Adding script file"

    Here a good commit message -m for our changes would be "Adding script file"

27. Let's check the status of our git repository, now. It should tell you that there are no changes made to your repository (i.e., your repository is up-to-date with the state of the code in your directory).'

    $ git status

28. Look at the git logs, again:

    $ git log

    You can also print simplified logs with the --oneline option.




That concludes the first lesson of this virtual tutorial.

In this section you set up a workspace by creating your directory, conda environment, and git repository. You downloaded a .txt file and read it using the Python commands of open(), readline(), read(), close(), and print(), as well as the context manager with. You should be familiar with the str datatype. You also used fundamental git commands such as git init, git status, git add, git commit, and git logs.

Please continue to `Part 1.2 <link://slug/part1_2>`_. 
