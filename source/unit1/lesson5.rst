Lesson 5: Customizing SenseHAT Output
=====================================================

:Authors: Paul Xu, Marcus Penny
:Date: Jan 31, 2018
:Time: 1 hour

Lesson Information
--------------------------------------

In the previous lesson the students learned how to light up the SenseHAT. In this lesson they will learn how to customize SenseHAT output by passing parameters to functions.  They will first encounter complex data structures - lists.  They will also learn what some of the common mistakes are and how to debug them.

.. sidebar:: CT Concepts

    .. rubric:: Computational Thinking Skills:

    - **Abstraction**: Functions and Parameterization
    - **Abstraction**: Data Structures
    - **Analysis**: Errors and Debugging

    .. rubric:: Standard Alignments:

    N/A

    .. rubric:: Cross-discipline Applications:

    The analogy between functions in computer science and mathematical functions

The purpose of the lesson is to:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Learn the syntax of passing parameters to functions
2. Learn the idea of lists
3. Understand and use the Input - Computation - Output Structure
4. Understand the basics of debugging

Driving Questions:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- How to customize output message on the SenseHAT LED Matrix?
- What are lists and how to use them?
- How are most computer programs structured?
- What do we do if things go wrong?

Computer Science Concepts:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    | Functions, Parameters, Input, Computation, Output, Debugging

Materials Needed:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    | Raspberry Pi 3 with SenseHAT

Target Skills:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
|

.. admonition:: Students will be able to

    1. SWBAT change SenseHAT output by passing parameters to functions
    2. SWBAT use lists to represent colors
    3. SWBAT write programs using the Input - Computation - Output structure.

--------------------------------------------

Instructional Plan and Structure
--------------------------------------------

Overview of the lesson (5 minutes)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This part builds on what students wrote in the last session, in which they wrote their first program to use the ``sense.show_message()`` function to output a scrolling message of their choice to SenseHAT.  In this lesson we will first answer this burning question: how do we change the output?

Changing the scroll speed of the SenseHAT output (10 minutes)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
In the last lesson we learned that by passing different ``strings`` to the ``sense.show_message()`` function, we can change the output message that we show on the SenseHAT.  We also learned that functions are small, pre-written programs that accept different **parameters** to do different things.  It turns out that we can also adjust many other things by adding more **parameters**. When there are two or more parameters, we have a slightly different way of passing them to a function.  Here is how:

.. math::

    function(parameter1, parameter2, parameter3, ...)

Parameters are separated by commas.  Each parameter has a name.  For example, in order to change the speed at which the text scrolls, we can add this parameter (write it down on the whiteboard) ``scroll_speed=0.05``.  ``scroll_speed`` is the name of the parameter, and like how we assign values to variables, we also use the equal sign ``=`` to assign values to parameters.  Now you can change the value ``0.05`` to see how the scroll speed of the text changes.

.. tip::

    We usually omit the name of the first parameter.

Changing the colors of the SenseHAT output (20 minutes)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Let's go on to passing the function more parameters so we can also customize the colors of the SenseHAT output.  But before that, think of this question: **How does the computer know different colors?**

Computers are not like us.  It cannot automatically translate our language to what it understands.  However, it can understand numbers.  Therefore, computer programmers developed a system called ``RGB`` for computers to understand and show us different colors.  In the ``RGB`` system, ``R`` stands for **red**, ``G`` stands for **green**, and ``B`` for **blue**.  For each color, we have ``0`` to ``255``, a total of **256** levels of intensity.  By mixing different color intensities, we get different colors.  It is like using a color palette.

Feel free to use this `Online Color Palette <https://www.rapidtables.com/web/color/RGB_Color.html>`_ to get your own colors.  Make sure you write down the colors and the RGB values that you find desirable.

Now, in order for Python to understand the colors you have picked, we need to pass these three values to Python.  However, it also needs to understand that these three values need to be understood as a whole.  We use ``lists`` to do this job.  Lists the easiest way in Python to put things together as a whole.  To use lists, you put comma-separated values (or variables) into a pair of square brackets.  For example, this list means **red**: ``[255, 0, 0]``.

We can now pass these lists to two new parameters ``text_colour=`` and ``back_colour=`` to change the text color and background color respectively.  Note the spelling of ``colour``.  Raspberry Pi and SenseHAT are developed by the British so you will see British spelling of words a lot.::

    sense.show_message("Hello Python", scroll_speed = 0.05, 
                       text_colour = [255, 0, 0], back_colour = [0, 0, 255])

Notice that sometimes code can be too long to be shown on one line.  You can break the code into different lines by inserting line breaks (``ENTER`` key) into the brackets of functions right after the commas.

Why isn't my code working? (20 minutes)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Often the code simply does not work, which can be really frustrating.  Here we are going to break our code and see how Python behaves.  Sometimes Python will show us exactly where things go wrong, and why things go wrong.

.. rubric:: Misspelling ``sense_hat`` package name:

.. code-block:: python
    :linenos:
    :emphasize-lines: 1

    from sensehat import SenseHat
    sense = SenseHat()

    sense.show_message("Hello Python!")

    Traceback (most recent call last):
    File "/home/pi/Desktop/sense.py", line 1, in <module>
        from sensehat import SenseHat
    ImportError: No module named 'sensehat'

.. rubric:: Misspelling ``SenseHat`` class name:

.. code-block:: python
    :linenos:
    :emphasize-lines: 1

    from sense_hat import Sensehat
    sense = SenseHat()

    sense.show_message("Hello Python!")

    Traceback (most recent call last):
    File "/home/pi/Desktop/sense.py", line 1, in <module>
        from sense_hat import Sensehat
    ImportError: cannot import name 'Sensehat'

.. rubric:: Missing ``()``

.. code-block:: python
    :linenos:
    :emphasize-lines: 2

    from sense_hat import SenseHat
    sense = SenseHat

    sense.show_message("Hello Python!")

    Traceback (most recent call last):
    File "/home/pi/Desktop/sense.py", line 4, in <module>
        sense.show_message("Hello Python")
    TypeError: show_message() missing 1 required positional argument: 'text_string'

.. rubric:: Misspelling ``SenseHat()`` object

.. code-block:: python
    :linenos:
    :emphasize-lines: 2

    from sense_hat import SenseHat
    sense = Sensehat()

    sense.show_message("Hello Python!")

    Traceback (most recent call last):
    File "/home/pi/Desktop/sense.py", line 2, in <module>
        sense = Sensehat()
    NameError: name 'Sensehat' is not defined
    
.. rubric:: Misspelling ``sense.show_message()`` function name

.. code-block:: python
    :linenos:
    :emphasize-lines: 4

    from sense_hat import SenseHat
    sense = Sensehat()

    sense.show_Message("Hello Python!")

    Traceback (most recent call last):
    File "/home/pi/Desktop/sense.py", line 4, in <module>
        sense.show_Message("Hello Python")
    AttributeError: 'SenseHat' object has no attribute 'show_Message'

.. rubric:: Missing quotation marks around the string

.. code-block:: python
    :linenos:
    :emphasize-lines: 4

    from sense_hat import SenseHat
    sense = Sensehat()

    sense.show_message(Hello Python)

    File "/home/pi/Desktop/sense.py", line 4
        sense.show_message(Hello Python)
                                  ^
    SyntaxError: invalid syntax

Review and Assessment (5 minutes)
--------------------------------------------
1. Why do we use lists?
2. What is the RGB color system?
3. How do we pass a function multiple parameters?