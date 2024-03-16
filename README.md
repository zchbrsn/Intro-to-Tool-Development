[Markdown Quick Ref](https://wordpress.com/support/markdown-quick-reference/)

# Intro-to-Tool-Development

## Integrated Development Environment

First, we need to choose a platform to write the code on.  It is as simple as writing in a text editor and using the interpreter to run the file, however specific language syntax and errors will not be visible.  Integrated Development Environments (IDE) are used to help detect errors and fix syntax to make it easier for the programmers.  There are a lot of IDEs out there, so decide on one that is comfortable for you.

For the purposes of this course, I'll be using [Visual Studio Code](https://code.visualstudio.com/).  It is free and can be customized to fit various needs and programming languages.

# 

## Command Line Arguments

There are a couple ways we can define command line arguments
1. Importing the sys library and accessing argv
2. Using a more full-bodied library such as argparse

By using sys, we will access an argument by its index:
``import sys

print(f'First argument: {sys.argv[1]}')
``
Notice that we are actually calling the second item in the array, the first `sys.argv[0]` will contain the name of the program.
