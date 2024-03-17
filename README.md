[Markdown Quick Ref](https://wordpress.com/support/markdown-quick-reference/)

# Intro-to-Tool-Development

## Integrated Development Environment

First, we need to choose a platform to write the code on.  It is as simple as writing in a text editor and using the interpreter to run the file, however specific language syntax and errors will not be visible.  Integrated Development Environments (IDE) are used to help detect errors and fix syntax to make it easier for the programmers.  There are a lot of IDEs out there, so decide on one that is comfortable for you.

For the purposes of this course, I'll be using [Visual Studio Code](https://code.visualstudio.com/).  It is free and can be customized to fit various needs and programming languages.

# Port Scanner

A port scanner is one of the simplest ways to start learning networking and sockets in programming.  It simply connects to the specified IP and port and prints if the port is open or if it is closed.  We need to import the socket library and use some methods from that library to create a socket.

```
import socket

ip = "127.0.0.1"
port = 9999
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

try:
    conn = sock.connect((ip, port))
    print(f'[+] {port} is open')
    sock.close()

except socket.error:
    print(f'[-] {port} is closed')
    sock.close()
```

In this program, we specify the IP address as a string and the port as an integer.  Then use the socket function to create a IPv4 (AF_INET) and TCP (SOCK_STREAM) socket.

The try/except is used for error handling, so in this program, we will create a socket and attempt to connect to the specified IP and port combination.  If it is successful, the program will print that the port is open, otherwise it will go to the except block and print that the port is closed.

## Command Line Arguments

It can become very time consuming to constantly edit the script with a new IP and port.  We can use dynamic programming to specify the IP and port as command line arguments that get passed onto the program so that we do not have to edit the program, we just run the program multiple times.

There are a couple ways we can define command line arguments
1. Importing the sys library and accessing argv
2. Using a more full-bodied library such as argparse

By using sys, we will access an argument by its index:
```
import sys

print(f'First argument: {sys.argv[1]}')
```
Notice that we are actually calling the second item in the array, the first `sys.argv[0]` will contain the name of the program.

In this way, we can run the program like so and access variable arguments that fit our needs.
```
> python3 my_program.py Hello
First argument: Hello
```
