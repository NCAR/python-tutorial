.. title: yourfirst
.. slug: yourfirst
.. date: 2020-04-08 14:29:40 UTC-06:00
.. tags:
.. category:
.. link:
.. description:
.. type: text
.. hidetitle: True
.. has_math: True

.. role:: bash(code)
   :language: bash

.. role:: python(code)
   :language: python

=========================================
Your First Python Tutorial for Scientists
=========================================
Welcome to Your First Python tutorial for scientists! In this self-paced
course you will learn how to write Python code using Python best practices.
Through these instructions you will develop Python scripts and use Git and
GitHub to save and organize your work.  At the end of this tutorial you will
have a grasp of how to begin building your own library of Python tools for
your scientific analysis workflows.

-----------
Why Python?
-----------

You're already here because you want to learn to use Python for your data
analysis and visualizations. Python can be compared to other high-level,
interpreted, object-oriented languages, but is especially great because it is
free and open source!

High level languages:
    Other high level languages include MatLab, IDL, and NCL. The advantage of
    high level languages is that they provide functions, data structures, and
    other utilities that are commonly used, which means it takes less code to
    get real work done. The disadvantage of high level languages is that they
    tend to obscure the low level aspects of the machine such as: memory use,
    how many floating point operations are happening, and other information
    related to performance. C and C++ are all examples of lower level
    languages. The "higher" the level of language, the more computing
    fundamentals are abstracted.

Interpreted languages:
    Most of your work is probably already in interpreted languages if you've
    ever used IDL, NCL, or MatLab (interpreted languages are typically also
    high level). So you are already familiar with the advantages of this: you
    don't have to worry about compiling or machine compatability (it is
    portable). And you are probably familiar with their deficiencies: sometimes
    they can be slower than compiled languages and potentially more memory
    intensive.

Object Oriented languages:
    Objects are custom datatypes. For every custom datatype, you usually have
    a set of operations you might want to conduct. For example, if you have an
    object that is a list of numbers you might want to apply a mathematical
    operation, such as sum, onto this list object in bulk. Not every  function
    can be applied to every datatype; it wouldn't make sense to apply a
    logarithm to a string of letters or to capitalize a list of numbers. Data
    and the operations applied to them are grouped together into one object.

Open source:
    Python as a language is open source which means that there is a community
    of developers behind its codebase. Anyone can join the developer community
    and contribute to deciding the future of the language. When someone
    identifies gaps to Python's abilities, they can write up the code to fill
    these gaps. The open source nature of Python means that Python as a
    language is very adaptable to shifting needs of the user community.

Python is a language designed for rapid prototyping and efficient programming.
It is easy to write new code quickly with less typing.

----------------------------
Why another Python tutorial?
----------------------------

What makes this Python tutorial unique is that it has been designed specifically
to meet the needs of, and feedback from, atmospheric and oceanic scientists
making the transition with the NCAR-wide
`pivot-to-Python <https://www.ncl.ucar.edu/Document/Pivot_to_Python/>`_.
In particular, this tutorial should be useful to any scientist who already knows how to program
in some other language but is taking up Python for the first time. By spending the
first course on pure Python without importing any additional packages, our "Your First"
tutorial addresses the concerns that most tutorials either pick up speed too quickly
by going into the intricacies of third-party packages before explaining how Python is
different from other languages, or get too bogged down in basic programming concepts
that anyone with programming experience already knows. This tutorial attempts to hit
the sweet spot between too high-level and too low-level. By using coding examples
with real atmospheric datasets and questions, the skills and techniques taught are
easily applied to actual atmospheric or oceanic workflows.
We hope that this tailored approach to teaching and sharing computational tools
effectively addresses the concerns and needs of the geoscience community.

.. seealso::

   - `Official Python 3 Documentation <https://docs.python.org/3/>`_
   - `Official GitHub Documentation <https://help.github.com/en>`_
   - `Official Git Documentation <https://git-scm.com/doc>`_

..

---------------------------
Requirements & Installation
---------------------------

If you don't have conda installed at all,
`please install it. <https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html>`_

1. Check that you have conda or miniconda installed on your OS by checking your
   conda version:

   .. code-block:: bash

      $ conda --version

   ..

   At the time of writing this, the latest version of conda is 4.8. If you have
   an old version of conda installed, update it.

2. If necessary, update:

   .. code-block:: bash

      $ conda update -n base conda

   ..

   .. note::
      If you have a *really* old version of conda it might be easier to delete it and then reinstall it. But before doing this you have to check your env-list with :bash:`conda env list` to see if there are any environments you created and want to save.

   ..

3. Check your conda version again.

   .. code-block:: bash

      $ conda --version


4. `Install Git. <https://git-scm.com/book/en/v2/Getting-Started-Installing-Git>`_

   Git is a program that tracks changes made to files. This makes it easy to
   maintain access to multiple versions of your code as you improve it, and
   revert your code back to a previous version if you've made any mistakes.


-------------------------
First Python Script
-------------------------

This section of the tutorial will focus on teaching you Python through the
creation of your first script.  You will learn about syntax and the reasoning
behind why things are done the way they are done along the way.  We will also
incorporate lessons on the use of Git because we highly recommend you version
controling your work.

We are assuming you are familiar with bash and terminal commands. If not
`here is a cheat sheet <https://cheatography.com/davechild/cheat-sheets/linux-command-line/>`_.

~~~~~~~~~~~~~~~~~~~
Reading a .txt File
~~~~~~~~~~~~~~~~~~~

In building your first Python script we will set up our workspace, read a
:code:`.txt` file, and learn Git fundamentals.

Open a terminal to begin.

.. note::

   On Windows, open **Anaconda Prompt**. On a Mac or Linux machine, simply open **Terminal**.

..

1. Create a directory:

   .. code-block:: bash

      $ mkdir python_tutorial

   ..

   The first thing we have to do is create a directory to store our work.
   Let's call it :code:`python_tutorial`.

2. Go into the directory:

   .. code-block:: bash

      $ cd python_tutorial

3. Create a virtual environment for this project:

   .. code-block:: bash

     $ conda create --name python_tutorial python

   ..

   A conda environment is a directory that contains a collection of packages
   or libraries that you would like installed and accessible for this workflow.
   Type :bash:`conda create --name` and the name of your project, here that is
   :code:`python_tutorial`, and then specify that you are using python to create a
   virtual environment for this project.

   It is a good idea to create new environments for different projects because
   since Python is open source, new versions of the tools you use may become
   available. This is a way of guaranteeing that your script will use the same
   versions of packages and libraries and should run the same as you expect it
   to.

   .. seealso::

      `More information on Conda environments <https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html>`_

   ..

4. And activate your Conda environment:

   .. code-block:: bash

     $ conda activate python_tutorial

   ..

5. Make the directory a Git repository:

   .. code-block:: bash

      $ git init .

   ..

   A Git repository tracks changes made to files within your project. It looks
   like a :code:`.git/` folder inside that project.

   This command adds version control to this new python_tutorial directory
   and all of its contents.

   .. seealso::

      `More information on Git repositories <https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository>`_

   ..

6. Create a data directory:

   .. code-block:: bash

      $ mkdir data

   ..

   And we'll make a directory for our data.

7. Go into the data directory:

   .. code-block:: bash

      $ cd data

8. Download sample data from the CU Boulder weather station:

   .. code-block:: bash

      $ curl -kO https://sundowner.colorado.edu/weather/atoc8/wxobs20170821.txt

   ..

   This weather station is a Davis Instruments wireless Vantage Pro2 located on
   the CU-Boulder east campus at the SEEC building (40.01 N, 05.24 W, 5250 ft
   elevation). The station is monitored by the Atmospheric and Oceanic Sciences
   (ATOC) department and is part of the larger University of Colorado ATOC
   Weather Network.

9. Check the status of your repository:

   .. code-block:: bash

      $ git status

   ..

   You will see the newly created :bash:`data` directory (which is listed as
   :bash:`./`, since you are currently *in* that directory) is listed as
   "untracked," which means all of the files you added to that directory are
   *also* untracked by Git.  The :bash:`git status` command will tell you what
   to do with untracked files. Those instructions mirror the next 2 steps:

10. Add the file to the Git staging area:

    .. code-block:: bash

       $ git add wxobs20170821.txt

    ..

    By adding this datafile to your directory, you have made a change that is
    not yet reflected in our Git repository. Every file in your working directory is classified
    by git as "untracked", "unmodified", "modified", or "staged."
    Type :bash:`git add` and then the name of the altered file to stage your change,
    i.e. moving a file that is either untracked or modified to the staged category so they can be committed.

    .. seealso::

       `More information on git add <https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository>`_

    ..

11. Check your git status once again:

    .. code-block:: bash

       $ git status

    ..

    Now this file is listed as a "change to be commited," i.e. staged. Staged
    changes can now be commited to your repository history.

12. Commit the file to the Git repository:

    .. code-block:: bash

       $ git commit -m "Adding sample data file"

    ..

    With :bash:`git commit`, you've updated your repository with all the changes
    you staged, in this case just one file.

    .. note::

       On a Windows machine you may see the following: :bash:`warning: LF will be replaced by CRLF in mysci.py. The file will have its original line endings in your working directory`.
       Do not worry too much about this warning. CR refers to "Carriage Return Line Feed" and LF refers to "Line Feed." Both are used to indicate line termination.
       In Windows both a Carriage Return and Line Feed are required to note the end of a line, but in Linux/UNIX only a Line Feed is required. Most text editors can account for line ending differences between opperating systems, but sometimes a conversion is necessary.
       To silence this warning you can type :bash:`git config --global core.autocrlf false` in the terminal.

    ..

13. Look at the Git logs:

    .. code-block:: bash

       $ git log

    ..

    If you type :bash:`git log` you will show a log of all the commits, or changes
    made to your repository.

14. Go back to the top-level directory:

    .. code-block:: bash

       $ cd ..

    ..

15. And now that you've set up our workspace, create a blank Python script,
    called :code:`mysci.py`:

    .. code-block:: bash

       $ touch mysci.py

    ..

    .. note::

       If you are working on a Windows machine it is possible that :bash:`touch` will not be
       recognized as an internal or external command. If this is the case, run
       :bash:`conda install m2-base` to enable unix commands such as :bash:`touch`.

    ..

16. Edit the :code:`mysci.py` file using nano, vim, or your favorite text editor:

    .. code-block:: python
       :linenos:

       print("Hello, world!")

    ..

    Your classic first command will be to print :python:`Hello, world!`.

    .. note::

       On a Windows machine, it is possible `nano` or `vim` are not recognized as text editors within your terminal. In this case simply try to run `mysci.py` to open a notepad editor.

    ..

17. Try testing the script by typing :bash:`python` and then the name of your script:

    .. code-block:: bash

       $ python mysci.py

    ..

    **Yay!** You've just created your first Python script.


18. You probably won't need to run your Hello World script again, so delete the
    :python:`print("Hello, world!")` line and start over with something more useful -
    we'll read the first 4 lines from our datafile.

    Change the :code:`mysci.py` script to read:

    .. code-block:: python
       :linenos:

       # Read the data file
       filename = "data/wxobs20170821.txt"
       datafile = open(filename, 'r')

       print(datafile.readline())
       print(datafile.readline())
       print(datafile.readline())
       print(datafile.readline())

       datafile.close()

    ..

    First create a variable for your datafile name, which is a string - this
    can be in single or double quotes.

    Then create a variable associated with the opened file, here it is called
    :python:`datafile`.

    The :python:`'r'` argument in the open command indicates that we are opening
    the file for reading capabilities. Other input arguments for open include
    :python:`'w'`, for example, if you wanted to write to the file.

    The readline command moves through the open file, always reading the next
    line.

    And remember to close your datafile.

    Comments in Python are indicated with a hash, as you can see in the first
    line :python:`# Read the data file`. Comments are ignored by the interpreter.

    .. seealso::

       `More information on the open() function <https://docs.python.org/3/library/functions.html#open>`_

    ..

19. And test your script again by typing:

    .. code-block:: bash

       $ python mysci.py

    ..

    Testing of your script with :bash:`python mysci.py` should be done every time
    you wish to execute the script. This will no longer be specified as a
    unique step in between every change to our script.

20. Change the :code:`mysci.py` script to read your whole data file:

    .. code-block:: python
       :linenos:

       # Read the data file
       filename = "data/wxobs20170821.txt"
       datafile = open(filename, 'r')

       data = datafile.read()

       datafile.close()

       # DEBUG
       print(data)
       print('data')

    ..

    Our code is similar as before, but now we've read the entire file. To
    test that this worked. We'll :python:`print(data)`. Print statements in python
    require parenthesis around the object you wish to print, in this scenario the data object.

    Try :python:`print('data')` as well. Now Python will print the string
    :code:`data`, as it did for the hello world function, instead of the
    information stored in the variable data.

    Don't forget to execute with :bash:`python mysci.py`.

21. Change the :code:`mysci.py` script to read your whole data file using a context
    manager with:

    .. code-block:: python
       :linenos:

       # Read the data file
       filename = "data/wxobs20170821.txt"
       with open(filename, 'r') as datafile:
          data = datafile.read()

       # DEBUG
       print(data)

    ..

    Again this is a similar method of opening the datafile, but we now use :python:`with open`.
    The :python:`with` statement is a context manager that provides clean-up and
    assures that the file is automatically closed after you've read it.

    The indendation of the line :python:`data = datafile.read()` is very important.
    Python is sensitive to white space and will not work if you mix spaces and
    tabs (Python does not know your tab width). It is best practice to use
    spaces as opposed to tabs (tab width is not consistent between editors).

    Combined these two lines mean: with the datafile opened, I'd like to read
    it.

    And execute with :bash:`python mysci.py`.

    .. seealso::

       `More information on context managers <https://book.pythontips.com/en/latest/context_managers.html>`_

    ..

22. What did we just see? What is the data object? What type is data? How do we
    find out?

    Change the DEBUG section of our script to:

    .. code-block:: python
       :lineno-start: 6

       # DEBUG
       print(type(data))

    ..

    And execute with :bash:`python mysci.py`

    Object types refer to :python:`float`, :python:`integer`, :python:`string`
    or other types that you can create.

    Python is a dynamically typed language, which means you don't have to
    explicitly specify the datatype when you name a variable, Python will
    automatically figure it out by the nature of the data.

23. Now, clean up the script by removing the DEBUG section, before we commit
    this to Git.

24. Let's check the status of our Git repository

    .. code-block:: bash

       $ git status

    ..

    .. note::

       Take a look at which files have been changed in the repository!

    ..

25. Stage these changes:

    .. code-block:: bash

       $ git add mysci.py

    ..

26. Let's check the status of our Git repository,again. What's different from
    the last time we checked the status?

    .. code-block:: bash

       $ git status

    ..

27. Commit these changes:

    .. code-block:: bash

       $ git commit -m "Adding script file"

    ..

    Here a good commit message :code:`-m` for our changes would be
    :code:`"Adding script file"`

28. Let's check the status of our Git repository, now. It should tell you that
    there are no changes made to your repository (i.e., your repository is
    up-to-date with the state of the code in your directory).

    .. code-block:: bash

       $ git status

    ..

29. Look at the Git logs, again:

    .. code-block:: bash

       $ git log

    ..

    You can also print simplified logs with the :code:`--oneline` option.

-----

That concludes the first lesson of this virtual tutorial.

In this section you set up a workspace by creating your directory, conda
environment, and git repository. You downloaded a .txt file and read it using
the Python commands of :python:`open()`, :python:`readline()`, :python:`read()`,
:python:`close()`, and :python:`print()`, as well as the context manager
:python:`with`. You should be familiar with the :python:`str` datatype. You
also used fundamental git commands such as :bash:`git init`, :bash:`git status`,
:bash:`git add`, :bash:`git commit`, and :bash:`git log`.


.. seealso::

   - `Conda environments <https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html>`_
   - `Git repositories <https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository>`_
   - `The open() function <https://docs.python.org/3/library/functions.html#open>`_
   - `Context managers <https://book.pythontips.com/en/latest/context_managers.html>`_

..


~~~~~~~~~~~~~~~~~~~~~~~~~~
Creating a Data Dictionary
~~~~~~~~~~~~~~~~~~~~~~~~~~

This is intended to pick off right where "Reading in a .txt File" left off - you
had just commited your new script file that reads in the data from a file as a string.
You will now manipulate your data into a more usable format - a dictionary.
In doing so you will learn how to write iterative for loops and about Python
data structures.

Let's begin.

1. One big string isn't very useful, so use :python:`str.split()` to parse the data
   file into a data structure you can use.

   Change the :code:`mysci.py` script to read:

   .. code-block:: python
      :linenos:

      # Initialize my data variable
      data = []

      # Read and parse the data file
      filename = "data/wxobs20170821.txt"
      with open(filename, 'r') as datafile:

       # Read the first three lines (header)
       for _ in range(3):
          datafile.readline()

       # Read and parse the rest of the file
       for line in datafile:
          datum = line.split()
          data.append(datum)

      # DEBUG
      for datum in data:
         print(datum)

   ..

   The first thing that is different in this script is an initialized data
   variable; :python:`data = []` creates the variable data as an empty list which we
   will populate as we read the file. Python lists are a collection data type
   that are ordered and changeable - meaning you can call information out of
   the list by its index and you can add or delete elements to your list. Lists
   are denoted by square brackets, :python:`[]`.

   Then with the datafile open for reading capabilities, we are going to write
   two separate :python:`for` loops. A :python:`for` loop is used for iterating
   over a sequence (such as a list). It is important to note the syntax of Python
   :python:`for` loops: the :python:`:` at the end of the :python:`for` line, the
   tab-indentation of all lines within the :python:`for` loop, and perhaps the
   absence of an :code:`end for` that is found in languages such as Matlab.

   In your first :python:`for` loop, loop through the dummy variable :python:`_`
   in :python:`range(3)`. The :python:`range` function returns a sequence of
   numbers, starting at 0 and incrementing by 1 (by default), ending at the
   specified length. Here if you were to :python:`print(_)` on each line of the
   for loop you would see:

   .. code-block:: python

      0
      1
      2

   ..

   Try it out if you are unsure of how this works. Here the :python:`_` variable
   is a placeholder, meaning the variable is never called within the loop.

   So again, in the first :python:`for` loop, you execute the :python:`readline`
   command (which you will remember moves down to the next line each time it is
   consecutively called) 3 times to read through the file header (which is 3
   lines long). **Yay!** You have just written your first :python:`for` loop!

   Then in a second :python:`for` loop, you loop through lines in the remainder of
   your datafile. On each line, split it along white space. The
   :python:`string.split()` method splits a string into a list on a specified
   separator, the default being white space. You could use any character you
   like, but other useful options are :python:`/t` for splitting along tabs or
   :python:`,` along commas.

   Then you :python:`append` this split line list to the end of your data :python:`list`.
   The :python:`list.append()` method adds a single item to the end of your :python:`list`.
   After every line in your :python:`for` loop iteration, the data :python:`list` that was
   empty is one element longer. Now we have a :python:`list` of :python:`list`\s for our
   data variable - a :python:`list` of the data in each line for multiple lines.

   When you print each datum in data, you'll see that each datum is a :python:`list`
   of :python:`string` values.

   We just covered a lot of Python nuances in a very little bit a code!

   .. seealso::

      `More information on for-loops <https://book.pythontips.com/en/latest/for_-_else.html>`_
      `More information on Python lists <https://docs.python.org/3/tutorial/datastructures.html#more-on-lists>`_

   ..

2. Now, to practice list indexing, get the first, 10th, and last row in data.

   Change the DEBUG section of our :code:`mysci.py` script to:

   .. code-block:: python
      :lineno-start: 17

      # DEBUG
      print(data[0])
      print(data[9])
      print(data[-1])

   ..

   Index your list by adding the number of your index in square brackets,
   :python:`[]`, after the name of the :python:`list`. Python is 0-indexed so
   :python:`data[0]` refers to the first index and :python:`[-1]` refers to
   the last index.

3. Now, to practice slice indexing, get the first 10 rows in data.

   Change the DEBUG section of our :code:`mysci.py` script to:

   .. code-block:: python
      :lineno-start: 17

      # DEBUG
      for datum in data[0:10]:
         print(datum)

   ..

   Using a colon, :python:`:`, between two index integers :python:`a` and
   :python:`b`, you get all indexes between :python:`a` and :python:`b`. See
   what happens when you print :python:`data[:10]`, :python:`data[0:10:2]`, and
   :python:`data[slice(0,10,2)]`.  What's the difference?

4. Now, to practice nested indexing, get the 5th, the first 5, and every other
   column of row 8 in the data object.

   Change the DEBUG section of the :code:`mysci.py` script to:

   .. code-block:: python
      :lineno-start: 17

      # DEBUG
      print(data[8][4])
      print(data[8][:5])
      print(data[8][::2])

   ..

   In nested :python:`list` indexing, the first index determines the row, and the
   second determines the element from that row. Also try printing
   :python:`data[5:8][4]`, why doesn't this work?

5. Clean up the file (remove DEBUG section), stage the changes, and commit.

   .. code-block:: bash

      $ git add mysci.py
      $ git commit -m "Parsing file"

   ..


6. Can you remember which column is which? Is time the first column or the
   second? Which column is the temperature?

   Each column is a time-series of data. We would ideally like each time-series
   easily accessible, which is not the case when data is row-column ordered
   (like it currently is). (Remember what happens when you try to do something
   like :python:`data[:][4]`!)

   Let's get our data into a more convenient named-column format.

   Change :code:`mysci.py` to the following:

   .. code-block:: python
      :linenos:

      # Initialize my data variable
      data = {'date': [],
        'time': [],
        'tempout': []}

      # Read and parse the data file
      filename = "data/wxobs20170821.txt"
      with open(filename, 'r') as datafile:

         # Read the first three lines (header)
         for _ in range(3):
            datafile.readline()

         # Read and parse the rest of the file
         for line in datafile:
            split_line = line.split()
            data['date'].append(split_line[0])
            data['time'].append(split_line[1])
            data['tempout'].append(split_line[2])

      # DEBUG
      print(data['time'])

   ..

   First we'll initialize a dictionary, :python:`dict`, indicated by the curly
   brackets, :python:`{}`. Dictionaries, like :python:`list`\s, are changeable, but they
   are unordered. They have keys, rather than positions, to point to their
   elements. Here you have created 3 elements of your dictionary, all currently
   empty :python:`list`\s, and specified by the keys :python:`date`, :python:`time`, and
   :python:`tempout`. Keys act similarly to indexes: to pull out the :python:`tempout`
   element from data you would type :python:`data['tempout']`.

   Grab date (the first column of each line), time (the second column of each
   line), and temperature data (the third column), from each line and
   :python:`append` it to the :python:`list` associated with each of these data variables.

   .. seealso::

      `More on Python dictionaries <https://docs.python.org/3/tutorial/datastructures.html#dictionaries>`_

   ..

7. Clean up (remove DEBUG section), stage, and commit

   .. code-block:: bash

      $ git add mysci.py
      $ git commit -m "Parsing select time-series"

   ..

8. Now it's easy to get the time-series information for each column that we are
   interested in grabbing, and we can get each column by name. However,
   everything read from the text file is a :python:`str`. What if we want to do math on
   this data, then we need it to be a different data type!

   So, let's convert the tempout time-series to be a :python:`float` by changing the
   line:

   .. code-block:: python
      :lineno-start: 19

      data['tempout'].append(split_line[2])

   ..

   to:

   .. code-block:: python
      :lineno-start: 19

      data['tempout'].append(float(split_line[2]))

   ..

   The :python:`float` datatype refers to floating point real values - the datatype
   of any numbers with values after a decimal point. You could also change the
   datatype to :python:`int`, which will round the values down to the closest full
   integer.

   .. seealso::

      `More on Python numeric types (int, float, complex) <https://docs.python.org/3/library/stdtypes.html#numeric-types-int-float-complex>`_

   ..

9. Add a DEBUG section at the end and see what :python:`data['tempout']` now looks
   like.

   Do you see a difference? It should now be a list of floats.

10. Clean up (remove DEBUG section), stage, and commit

    .. code-block:: bash

       $ git add mysci.py
       $ git commit -m "Converting tempout to floats"

    ..

11. This seems great, so far! But what if you want to read more columns to our
    data later? You would have to change the initialization of the data
    variable (at the top of :code:`mysci.py`) and have to add the appropriate line
    in the "read and parse" section. Essentially, that means you need to
    maintain 2 parts of the code and make sure that both remain consistent with
    each other.

    This is generally not good practice. Ideally, you want to be able to change
    only one part of the code and know that the rest of the code will remain
    consistent. So, let's fix this.

    Change :code:`mysci.py` to:

    .. code-block:: python
       :linenos:

       # Column names and column indices to read
       columns = {'date': 0, 'time': 1, 'tempout': 2}

       # Data types for each column (only if non-string)
       types = {'tempout': float}

       # Initialize my data variable
       data = {}
       for column in columns:
          data[column] = []

       # Read and parse the data file
       filename = "data/wxobs20170821.txt"
       with open(filename, 'r') as datafile:

          # Read the first three lines (header)
          for _ in range(3):
             datafile.readline()

          # Read and parse the rest of the file
          for line in datafile:
             split_line = line.split()
             for column in columns:
                i = columns[column]
                t = types.get(column, str)
                value = t(split_line[i])
                data[column].append(value)

       # DEBUG
       print(data['tempout'])

    ..

    You have now created a columns :python:`dict` that points each data variable to
    its column-index. And a types :python:`dict`, that indicates what type to convert
    the data when necessary. When you want new variables pulled out of the
    datafile, change these two variables.

    Initializing the data :python:`dict` now includes a :python:`for` loop, where for each
    variable specified in columns, that key is initialized pointing to an empty
    :python:`list`. This is the first time you have looped over a :python:`dict` and added
    key-value pairs to a :python:`dict` via assignment.

    When reading and parsing the file, you created your first nested :python:`for`
    loop. For every line of the datafile, split that line - and then for every
    desired variable in the columns :python:`dict` (date, time, tempout): grab the
    datum from the current split line with the specified index (0, 1, 2), use
    the :python:`dict.get()` method to find the desired datatype if specified
    (avoiding :python:`key-not-found` errors and defaulting to :python:`str` if
    unspecified), convert the datum to the desired datatype, and :python:`append`
    the datum to the :python:`list` associated with each column key within the data
    :python:`dict`.

12. Clean up (remove DEBUG section), stage, and commit

    .. code-block:: bash

       $ git add mysci.py
       $ git commit -m "Refactoring data parsing code"

    ..

-----

That concludes the second lesson of this virtual tutorial.

In this section you saved the variables of date, time, and tempout in a data
dictionary.

You should now be familiar with the data structures :python:`list`\s (as well as list
indexing, nested lists, and the command :python:`list.append()`), :python:`dict`\s (their
keys and the command :python:`dict.get()`), and :python:`range`\s. You also learned to write
:python:`for` loops, about the :python:`float` datatype, and using the Python commands
:python:`str.split()`.

.. seealso::

   - `For-loops <https://book.pythontips.com/en/latest/for_-_else.html>`_
   - `Lists <https://docs.python.org/3/tutorial/datastructures.html#more-on-lists>`_
   - `Dictionaries <https://docs.python.org/3/tutorial/datastructures.html#dictionaries>`_

..


~~~~~~~~~~~~~~~~~
Writing Functions
~~~~~~~~~~~~~~~~~

This is intended to pick off right where "Creating a Data Dictionary" left off - you
had just commited your new script that reads the file, saving the variables of date,
time, and tempout in a data dictionary.
In this section you will compute wind chill index by writing your first
function and learning about basic math operators.

Let's begin.

1. Okay, now that you've read the data in a way that is easy to modify later,
   it is time to actually do something with the data.

   Compute the wind chill factor, which is the cooling effect of the wind. As
   wind speed increases the rate at which a body loses heat increases. The
   formula for this is:

   .. math::

      WCI = a + (b * t) - (c * v^{2}) + (d * t * v^{2})

   ..

   Where *WCI* refers to the Wind Chill in degrees F, *t* is temperature in
   degrees F, *v* is wind speed in mph, and the other variables are as
   follows: *a* = 35.74, *b* = 0.6215, *c* = 35.75, and *d* = 0.4275.
   Wind Chill Index is only defined for temperatures within the range -45 to
   +45 degrees F.

   You've read the temperature data into the tempout variable, but to do this
   calculation, you also need to read the windspeed variable from column 7.

   Modify the columns variable to read:

   .. code-block:: python
      :linenos:

      # Column names and column indices to read
      columns = {'date': 0, 'time': 1, 'tempout': 2, 'windspeed': 7}

   ..

   and modify the types variable to be:

   .. code-block:: python
      :lineno-start: 4

      # Data types for each column (only if non-string)
      types = {'tempout': float, 'windspeed': float}

   ..


2. Great! Save this in your Git repo. Stage and commit

   .. code-block:: bash

      $ git add mysci.py
      $ git commit -m "Reading windspeed as well"

   ..

3. Now, let's write our first function to computethe wind chill factor. We'll
   add this function to the bottom of the file.

   .. code-block:: python
      :lineno-start: 29

      # Compute the wind chill temperature
      def compute_windchill(t, v):
         a = 35.74
         b = 0.6215
         c = 35.75
         d = 0.4275

         v16 = v ** 0.16
         wci = a + (b * t) - (c * v16) + (d * t * v16)
         return wci

   ..

   To indicate a function in python you type :python:`def` for define, the name of your
   function, and then in parenthesis the input arguments of that function,
   followed by a colon. The preceding lines,the code of your function, are all tab-indented.
   If necessary specify your return value.

   .. seealso::

      `More on user defined functions <https://docs.python.org/3/reference/compound_stmts.html#function-definitions>`_

   ..

   Here is your first introduction to math operators in Python. Addition,
   subtraction, and multiplication look much like you'd expect. A double
   astericks, :python:`**`, indicates an exponential. A backslash, :python:`/`,
   is for division, and a double backslash, :python:`//`, is for integer division.

   And then let's compute a new list with windchill data at the bottom of
   :code:`mysci.py`:

   .. code-block:: python
      :lineno-start: 40

      # Let's actually compute the wind chill factor
      windchill = []
      for temp, windspeed in zip(data['tempout'], data['windspeed']):
         windchill.append(compute_windchill(temp, windspeed))

   ..

   Now we'll call our function. Initialize a :python:`list` for wind chill with empty
   square brackets, :python:`[]`. And in a :python:`for` loop, loop through our temperature
   and wind speed data, applying the function to each :python:`tuple` data pair.
   :python:`tuple`\s are ordered like :python:`list`\s, but they are indicated by
   parenthesis, :python:`()`, instead of square brackets and cannot be changed or
   appended. :python:`tuple`\s are generally faster than :python:`list`\s.

   We use the :python:`zip` function in Python to automatically unravel the
   :python:`tuple`\s. Take a look at :python:`zip([1,2], [3,4,5])`. What is the result?

   And finally, add a DEBUG section to see the results:

   .. code-block:: python
      :lineno-start: 45

      # DEBUG
      print(windchill)

   ..

4. Clean up, stage, and commit


   .. code-block:: bash

      $ git add mysci.py
      $ git commit -m "Compute wind chill factor"

   ..

5. Now, the wind chill factor is actually in the datafile, so we can read it
   from the file and compare that value to our computed values. To do this, we
   need to read the windchill from column 12 as a :python:`float`:

   Edit the columns and types :python:`dict`:

   .. code-block:: python
      :linenos:

      # Column names and column indices to read
      columns = {'date': 0, 'time': 1, 'tempout': 2, 'windspeed': 7,
                 'windchill': 12}

   ..

   ..

   .. note::

      Python requires that you indent any continued lines.  Take note that we indented the continued line above to align it with the starting :python:`{`-symbol.

   and

   .. code-block:: python
      :lineno-start: 5

      # Data types for each column (only if non-string)
      types = {'tempout': float, 'windspeed': float, 'windchill': float}

   ..

   Then, in a DEBUG section at the end of your script, compare the two
   different values (one from data and one computed by our function):

   .. code-block:: python
      :lineno-start: 46

      # DEBUG
      for wc_data, wc_comp in zip(data['windchill'], windchill):
         print(f'{wc_data:.5f}   {wc_comp:.5f}   {wc_data - wc_comp:.5f}')

   ..

   Using :python:`f-string`s with float formatting you can determine the precision
   with which to print the values to. The :python:`.5f` means you want 5 places after the
   decimal point.

   .. seealso::

      `More on string formatting <https://docs.python.org/3/library/string.html#format-string-syntax>`_

   ..

   Test the results. What do you see? Our computation isn't very good is it?

6. Clean up, stage, and commit

   .. code-block:: bash

      $ git add mysci.py
      $ git commit -m "Compare wind chill factors"

   ..

7. Now, format the output so that it's easy to understand and rename this
   script to something indicative of what it actually does.

   To the end of the file, add:

   .. code-block:: python
      :lineno-start: 46

      # Output comparison of data
      print('                ORIGINAL  COMPUTED')
      print(' DATE    TIME  WINDCHILL WINDCHILL DIFFERENCE')
      print('------- ------ --------- --------- ----------')
      zip_data = zip(data['date'], data['time'], data['windchill'], windchill)
      for date, time, wc_orig, wc_comp in zip_data:
         wc_diff = wc_orig - wc_comp
         print(f'{date} {time:>6} {wc_orig:9.6f} {wc_comp:9.6f} {wc_diff:10.6f}')

   ..

   Here you used *f-*:python:`string` formatting with more *f-*:python:`string` formatting
   options. The :python:`>6` indicates that you'd like the characters of the string to be
   right-justified and to take up 6 spaces.

   The :python:`9f` specifies that you want the value to fill 9 spaces, so :python:`9.6f`
   indicates you'd like the value to fill 9 spaces with 6 of them being after
   the decimal point. Same concept for :python:`10.6f`.

   You now have your first complete Python script!

8. DON'T CLEAN UP! Just stage and commit

   .. code-block:: bash

      $ git add mysci.py
      $ git commit -m "Output formatting comparison data"

   ..

9. Let's rename this script to something meaningful and indicative of the
   computation inside.

   .. code-block:: bash

      $ git mv mysci.py windchillcomp.py
      $ git commit -m "Renaming first script"

   ..

10. Let's push to GitHub!

    1. First you have to create a remote repository. Go to `GitHub <https://github.com/>`_
       and create or login to your account.

    2. At the top right of any Github page, there is a '+' icon. Click that,
       then select 'New Repository'.

    3. Name your repository :code:`python_tutorial`.
       It is best practice for your local project and GitHub repository to
       share a name.

    4. And click "Create Repository"

    5. Copy the link to your GitHub repository.

       Copy the link in the input right beneath the title, it should look
       something like this:

       :code:`https://github.com/<user_name>/<repo>.git`

    6. Then to set your remote repository, in your project terminal type:

       .. code-block:: bash

          $ git remote add origin <remote repository URL>

       ..

       .. note::

          Your remote repository URL is the link you copied in step 5!

       ..

    7. And verify your remote repository:

       .. code-block:: bash

          $ git remote -v

       ..

    8. And finally push your project to GitHub:

       .. code-block:: bash

          $ git push origin master

       ..

    Think of GitHub as online storage for versions of your project, much like
    hosting your code in a Google Drive, but with better features specific to
    coding. A lot of GitHub's features show their usefulness when you are
    working collaboratively, sharing your code with other scientists, or if
    you wanted to display and easily visualize changes in your code between
    commits.

-----

That concludes the "First Python Script" virtual tutorial where you learned to
write your first Python script.

In this section you calculated wind chill index by writing and calling your
first function. You also learned about Python math operators, the :python:`zip()`
command, :python:`tuple` datastructure, *f-*:python:`string` formatting, and how to push your
repository to GitHub.

.. seealso::

   - `User defined functions <https://docs.python.org/3/reference/compound_stmts.html#function-definitions>`_
   - `String formatting <https://docs.python.org/3/library/string.html#format-string-syntax>`_

..
