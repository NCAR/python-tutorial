.. title: part1_2
.. slug: part1_2
.. date: 2020-04-08 14:58:42 UTC-06:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
.. hidetitle: True

=====================================
Part 1.2 - Creating a Data Dictionary
=====================================

This is intended to pick off right where part 1.1 left off - you had just commited your new script file that reads in the data from file as a string.

You will now manipulate your data into a more usable format - a dictionary.

In doing so you will learn how to write iterative for loops and about Python data structures.

1. One big string isn't very useful, so use ``str.split()`` to parse the data file into a data structure you can use.

   Change the mysci.py script to read:

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

   The first thing that is different in this script is an initialized data variable; ``data = []`` creates the variable data as an empty list which we will populate as we read the file. Python lists are a collection data type that are ordered and changeable - meaning you can call information out of the list by its index and you can add or delete elements to your list. Lists are denoted by square brackets, ``[]``.

   Then with the datafile open for reading capabilities, we are going to write two separate ``for`` loops. A ``for`` loop is used for iterating over a sequence (such as a list). It is important to note the syntax of Python ``for`` loops: the ``:`` at the end of for ``for`` line, the tab-indentation of all lines within the ``for`` loop, and perhaps the absence of an ``end for`` that is found in languages such as Matlab.

   In your first ``for`` loop, loop through the dummy variable ``_`` in ``range(3)``. ``range`` returns a sequence of numbers, starting at 0 and incrementing by 1 (by default), ending at the specified length. Here if you were to ``print(_)`` on each line of the for loop you would see:

   .. code-block:: python
    
      0
      1
      2

   ..

   Try it out if you are unsure of how this works. Here the ``_`` variable is a placeholder, meaning the variable is never called within the loop.

   So again, in the first ``for`` loop, you execute the ``readline`` command (which you will remember moves down to the next line each time it is consecutively called) 3 times to read through the file header (which is 3 lines long). **Yay!** You have just written your first ``for`` loop!

   Then in a second ``for`` loop, you loop through lines in the remainder of your datafile. On each line, split it along white space. The ``string.split()`` method splits a string into a list on a specified separator, the default being white space. You could use any character you like, but other useful options are ``/t`` for splitting along tabs or ``,`` along commmas.

   Then you ``append`` this split line list to the end of your data ``list``. The ``list.append()`` method adds a single item to the end of your ``list``. After every line in your ``for`` loop iteration, the data ``list`` that was empty is one element longer. Now we have a ``list`` of ``list``s for our data variable - a ``list`` of the data in each line for multiple lines.

   When you print each datum in data, you'll see that each datum is a ``list`` of ``string`` values.

   We just covered a lot of Python nuances in a very little bit a code!

   `More information on for-loops <https://book.pythontips.com/en/latest/for_-_else.html>`_
   `More information on Python lists <https://docs.python.org/3/tutorial/datastructures.html#more-on-lists>`_

2. Now, to practice list indexing, get the first, 10th, and last row in data.

   Change the DEBUG section of our mysci.py script to:

   .. code:: python
      :number-lines: 17

      # DEBUG
      print(data[0])
      print(data[9])
      print(data[-1])

   ..

   Index your list by adding the number of your index in square brackets, ``[]``, after the name of the ``list``. Python is 0-indexed so ``data[0]`` refers to the first index and ``[-1]`` refers to the last index.

3. Now, to practice slice indexing, get the first 10 rows in data.

   Change the DEBUG section of our mysci.py script to:

   .. code:: python
      :number-lines: 17

      # DEBUG
      for datum in data[0:10]:
         print(datum)
    
   ..

   Using a colon, ``:``, between two index integers ``a`` and ``b``, you get all indexes between a and b. See what happens when you print ``data[:10]``, ``data[0:10:2]``, and ``data[slice(0,10,2)]``. What's the difference?

4. Now, to practice nested indexing,get the 5th, first 5, and every other column of rows 8 in data.

   Change the DEBUG section of the mysci.py script to:

   .. code:: python
      :number-lines: 17

      # DEBUG
      print(data[8][4])
      print(data[8][:5])
      print(data[8][::2])

   ..    
    
   In nested ``list`` indexing, the first index determines the row, and the second determines the element from that row. Also try printing ``data[5:8][4]``, why doesn't this work?

5. Clean up the file (remove DEBUG section), stage the changes, and commit.

   .. code-block: bash

      $ git add mysci.py
      $ git commit -m "Parsing file"

   ..
   

6. Can you remember which column is which? Is time the first column or the second? Which column is the temperature?

   Each column is a time-series of data. We would ideally like each time-series easily accessible, which is not the case when data is row-column ordered (like it currently is). (Remember what happens when you try to do something like ``data[:][4]``!)

   Let's get our data into a more convenient named-column format.

   Change mysci.py to the following:

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
    
   First we'll initialize a dictionary, ``dict``, indicated by the curly brackets, ``{}``. Dictionaries, like ``list``s, are changeable, but they are unordered. They have keys, rather than positions, to point to their elements. Here you have created 3 elements of your dictionary, all currently empty ``list``s, and specified by the keys ``date``, ``time``, and ``tempout``. Keys act similarly to indexes: to pull out the ``tempout`` element from data you would type ``data['tempout']``.

   Grab date (the first column of each line), time (the second column of each line), and temperature data (the third column), from each line and ``append`` it to the ``list`` associated with each of these data variables.

   `More on Python dictionaries <https://docs.python.org/3/tutorial/datastructures.html#dictionaries>`_

7. Clean up (remove DEBUG section), stage, and commit
    
   .. code-block: bash

      $ git add mysci.py
      $ git commit -m "Parsing select time-series"

   ..

8. Now it's easy to get the time-series informationfor each column that we are interested in grabbing, and we can get each column by name. However, everything read fromthe text file is a str. What if we want to do math on this data, then we need it to be a different data type!

   So, let's convert the tempout time-series to be a ``float`` by changing the line:

   .. code:: python
      :number-lines: 19

      data['tempout'].append(split_line[2])   
    
   ..

   to:

   .. code:: python
      :number-lines: 19
   
      data['tempout'].append(float(split_line[2]))
    
   ..

   The ``float`` datatype refers to floating point real values - the datatype of any numbers with values after a decimal point. You could also change the datatype to ``int``, which will round the values down to the closest full integer.

   `More on Python numeric types (int, float, complex) <https://docs.python.org/3/library/stdtypes.html#numeric-types-int-float-complex>`_

9. Add a DEBUG section at the end and see what ``data['tempout']`` now looks like.

   Do you see a difference? It should now be a list of floats.

10.  Clean up (remove DEBUG section), stage, and commit 

   .. code-block: bash

      $ git add mysci.py
      $ git commit -m "Converting tempout to floats"

   ..

11. This seems great, so far! But what if you want to read more columns to our data later? You would have to change the initialization of the data variable (at the top of ``mysci.py``) and have to add the appropriate line in the "read and parse" section. Essentially, that means you need to maintain 2 parts of the code and make sure that both remain consistent with each other.

    This is generally not good practice. Ideally, you want to be able to change only one part of the code and know that the rest of the code will remain consistent. So, let's fix this.

    Change mysci.py to:

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

    You have now created a columns ``dict`` that points each data variable to its column-index. And a types ``dict``, that indicates what type to convert the data when necessary. When you want new variables pulled out of the datafile, change these two variables.

    Initializing the data ``dict`` now includes a ``for`` loop, where for each variable specified in columns that key is initialized pointing to an empty ``list``. This is the first time you have looped over a ``dict`` and added key-value pairs to a ``dict`` via assignment.

    When reading and parsing the file, you created your first nested ``for`` loop. For every line of the datafile, split that line - and then for every desired variable in the columns ``dict`` (date, time, tempout): grab the datum from the current split line with the specified index (0, 1, 2), use the ``dict.get()`` method to find the desired datatype if specired (avoiding ``key-not-found`` errors and defaulting to ``str`` if unspecified), convert the datum to the desired datatype, and ``append`` the datum to the ``list`` associated with each column key within the data ``dict``.

12. Clean up (remove DEBUG section), stage, and commit 

   .. code-block: bash

      $ git add mysci.py
      $ git commit -m "Refactoring data parsing code"

   ..

-----

That concludes the second lesson of this virtual tutorial.

In this section you saved the variables of date, time, and tempout in a data dictionary.

You should now be familiar with the data structures ``list``s (as well as list indexing, nested lists, and the command ``list.append()``), ``dict``s (their keys and the command ``dict.get()``), and ``range``s. You also learned to write ``for`` loops, about the ``float`` datatype, and using the Python commands ``str.split()``.

Please continue to `Part 1.3 <link://slug/part1_3>`_.

----------
Suggested resources:

`For-loops <https://book.pythontips.com/en/latest/for_-_else.html>`_
`Lists <https://docs.python.org/3/tutorial/datastructures.html#more-on-lists>`_

--------
`Return to Outline <link://slug/index>`_
