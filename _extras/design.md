---
layout: page
title: Lesson Design
permalink: /design/
---
## Assumptions
*   Audience
    *   Graduate students in numerate disciplines from cosmology to economics
    *   Who understand very basic statistics (mean, standard deviation, correlation coefficient)
    *   And have manipulated data in spreadsheets and with interactive tools like SAS
    *   But have *not* programmed beyond CPD (copy-paste-despair)
*   Constraints
    *   One full day 09:00-16:00
        *   05:30 teaching time
        *   1:00 for lunch
        *   0:30 total for two coffee breaks
    *   Learners use native installs on their own machines
    *   No dependence on other Carpentry modules
        *   In particular, must not require knowledge of shell or version control
    *   Use the Jupyter Notebook
        *   Authentic tool used by many instructors
        *   There isn't really an alternative
        *   And means that even people who have seen a bit of Python before
            will probably learn something
*   Data
    * GenBank files from NCBI
*   Focus on programming, not data viz/analysis. We cover that in the R part
*   Exercises will mostly *not* be "write this code from scratch"
    *   Want lots of short exercises that can reliably be finished in allotted time
    *   So use MCQs, fill-in-the-blanks, Parsons Problems, "tweak this code", etc.
*   Lesson materials
    *   Notes for instructors and self-study will be written in Markdown
    *   Learners will be provided with one Notebook per episode containing exercises

## Desired Results

### Goals

1.  Get learners to the stage decribed in the "Software" section of
    "[Good Enough Practices in Scientific Computing][good-enough]".
    *   Goals
        1.  Make it easy for people (including your future self) to understand and (re)use your code
        2.  Modular, comprehensible, reusable, and testable all come together
    *   Rules
        1.  Every analysis step is represented textually (complete with parameter values)
        2.  Every program or script has a brief explanatory comment at the start
        3.  Programs of all kinds (including "scripts") are broken into functions
        4.  No duplication
        5.  Functions and variables have meaningful names
        6.  Dependencies and requirements are explicit (e.g., a requirements.txt file)
            *   This rule is *not* covered in this lesson
        7.  Commenting/uncommenting are not routinely used to control program behavior
        8.  Use a simple example or test data set to run to tell if it's working at all
            and whether it gives a known correct output for a simple known input
        9.  Submit code to a reputable DOI-issuing repository upon submission of paper,
            just like data
            *   This rule is *not* covered in this lesson
2.  Enable them to make sense of other onlines tutorials and resources

### Summative Assessment

* Midpoint:
* Final: Given a 2-3 page program to extract data from GenBank files:
    1. Find and fix a bug in the feature scan code
    2. Add an option to export found features to a CSV file for use in spreadsheet programs

### Essential Questions

How do I...

*   ...read, analyze, and manipulate GenBank files / genome data?
*   ...process multiple data sets?
*   ...tell if my program is working correctly?
*   ...fix it when it's not?
*   ...find and use software other people have written instead of writing my own?

### Learners Will Be Able To...

*   Run code interactively
*   Run code saved in a file
*   Write single-condition `if` statements
*   Convert between basic data types (integer, float, string)
*   Call built-in functions
*   Use `help` and online documentation
*   Import a library using an alias
*   Call something from an imported library
*   Read tabular data into an array or data frame
*   Do collective operations on arrays and data frames
*   Interpret common error messages
*   Track down bugs by running small tests of program modules
*   Write non-recursive functions taking a fixed number of named parameters
*   Create literate programs in the Jupyter Notebook

### Learners Will Know...

*   That a program is a piece of lab equipment that implements an analysis
    *   Needs to be validated/calibrated before/during use
    *   Makes analysis reproducible, reviewable, shareable
*   That programs are written for people, not for computers
    *   Meaningful variable names
    *   Modularity for readability as well as re-use
    *   No duplication
    *   Document purpose and use
*   That there is no magic: the programs they use are no different
    in principle from those they build
*   How to assign values to variables
*   What integers, floats, strings, and data frames are
*   How to trace the execution of a `for` loop
*   How to create and index lists
*   How to trace the execution of `if`/`else` statements
*   The difference between defining and calling a function
*   What a call stack is
*   Where to find documentation on standard libraries
*   How to find out what else scientific Python offers

## Learning Plan

Step-by step learning plan to help design the episodes.

*   Running and Quitting Interactively (09:00)
    *   Teaching: 15 min (because setup issues)
    *   Exercises: 0 min (accounted for in teaching time - no separate exercise)
        *   Run the Notebook
        *   Create a few Markdown cells
        *   Create and execute a Python cell that prints 1+2
*   Variables and Assignment (09:15)
    *   Teaching: 5 min
    *   Exercises: 5 min
        *   Trace behavior of swapping (`a, b = b, a` the old fashioned way)
            with an intermediate variable
        *   Calculate elapsed time in seconds using named values for seconds per minute, etc.
*   Data Types and Type Conversion (09:25)
    *   Teaching: 5 min
    *   Exercises: 5 min
        *   Predict result types (or errors) of various operations
        *   Add conversion functions to broken code to make it work
*   Built-in Functions (and Methods) and Help (09:35)
    *   Teaching: 10 min
    *   Exercises: 10 min
        *   Chain calculations with max and min
        *   Find a useful method using help(str)
        *   Parsons Problem to achieve specific results with string methods
*   Error Messages (09:55)
    *   Teaching: 5 min (review of error messages seen to date)
    *   Exercises: 10 min
        *   Diagnose and fix small errors (some syntax, some runtime)
*   Libraries (Including Aliases) (10:10)
    *   Teaching: 5 min
    *   Exercises: 5 min
        *   Operations with math library
        *   Look things up in the python.org docs
*   Coffee: 15 min (10:20)
*   Lists (10:35)
    *   Teaching: 10 min
    *   Exercises: 10 min
        *   Indexing exercises
        *   Conversion from list to string and back
        *   Sum values in a list
*   For Loops (10:55)
    *   Teaching: 10 min
    *   Exercises: 10 min
        *   Reverse a string by repeated append
        *   Trace execution of loop
*   Conditionals (11:15)
    *   Teaching: 5 min (inside loop)
    *   Exercises: 10 min
        *   Count vowels
        *   Report badly-sized files inside loop
*   Intro to Biopython (11:30)
    *   Teaching: 15 min
    *   Exercises: 15 min
        *   Loading the Biopython library
        *   Use glob.glob to find files
        *   Parsing sequence files
        *   Extract features from SeqRecords
        *   Compare sets of EC numbers
*   Lunch: 60 min (12:00)
*   Writing Functions (13:00)
    *   Teaching: 10 min
    *   Exercises: 15 min
        *   Check size of a single data file
        *   Check sizes of all data files in a directory
            *   Write new function using previous function
*   Programming Style (13:25)
    *   Teaching: 10 min (mostly to introduce checklist)
    *   Exercises: 15 min
        *   Clean up badly-written 20-line program
*   Debugging (13:50)
    *   Teaching: 10 min (divide and conquer)
    *   Exercises: 15 min
        *   Debug three-function program
*   Defensive Programming (14:15)
    *   Teaching: 5 min
    *   Exercises: 10 min
        *   Add assertions to functions based on docstrings
*   Coffee: 15 min (14:30)
*   Reading Tabular Data (14:45)
    *   Teaching: 5 min
    *   Exercises: 10 min
        *   Read one continent's subset of gapminder CSV data
    *   Callout:
        *   How to read data from Excel spreadsheets via export to CSV
        *   How to read data from Excel spreadsheets directly (needs another library)
*   Pandas Data Frames (15:00)
    *   Teaching: 10 min
    *   Exercises: 10 min
        *   Import Pandas
        *   Create and display a data frame
*   Next Steps (15:20)
    *   Teaching: 15 min
    *   Excercises: 0 min
*   Wrap-Up (15:40)
    *   Teaching: 15 min
        *   Overview of key SciPy modules
        *   How to find and install libraries
        *   Running Python from the command line
        *   Other editing tools
    *   Exercises: 0 min
*   Finish (15:55)
