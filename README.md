[Markdown Quick Ref](https://wordpress.com/support/markdown-quick-reference/)

# Introductions

1. Name
2. Optional: Work Role
3. Programming or language experience
4. What would you like to learn from this course or a project goal for the future

# Intro-to-Tool-Development

## Integrated Development Environment

First, we need to choose a platform to write the code on.  It is as simple as writing in a text editor and using the interpreter to run the file, however specific language syntax and errors will not be visible.  Integrated Development Environments (IDE) are used to help detect errors and fix syntax to make it easier for the programmers.  There are a lot of IDEs out there, so decide on one that is comfortable for you.

For the purposes of this course, I'll be using [Visual Studio Code](https://code.visualstudio.com/).  It is free and can be customized to fit various needs and programming languages.

## Port Scanner

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

## Looping

Running the program for every single port on a target will take a very long time.  It is much faster to loop through a series of specified port ranges and let the program continue to run without user intervention.

We will modify the previous port scanner and specify a port range.

```
import socket

ip = "127.0.0.1"
ports = [1, 2, 3, 4, 5]
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

for port in ports:
    try:
        conn = sock.connect((ip, port))
        print(f'[+] {port} is open')
        sock.close()

    except socket.error:
        print(f'[-] {port} is closed')
        sock.close()
```

In this way, we specify a series of ports that we would like to scan, but this list could get very long and overwhelming.  Alternatively, we could pick a range bettwen two numbers and Python will loop through each number in between.

```
import socket

ip = "127.0.0.1"
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

for port in range(65536):
    try:
        conn = sock.connect((ip, port))
        print(f'[+] {port} is open')
        sock.close()

    except socket.error:
        print(f'[-] {port} is closed')
        sock.close()
```

The range starts at 0 and will continue to loop until (and excluding) 65536.

## Command Line Arguments

It can become very time consuming to constantly edit the script with a new IP and port.  We can use dynamic programming to specify the IP and port as command line arguments that get passed onto the program so that we do not have to edit the program, we just run the program multiple times.

There are a couple ways we can define command line arguments
1. Importing the sys library and accessing argv
2. Using a more full-bodied library such as argparse

### sys.argv

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

We can edit the port scanner to allow us to specify an IP and port from the command line.

```
import socket
import sys

if (len(sys.argv) != 3):
    print(f'Usage: python3 {sys.argv[0]} target port')
    sys.exit()

ip = sys.argv[1]
port = int(sys.argv[2])
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

try:
    conn = sock.connect((ip, port))
    print(f'[+] {port} is open')
    sock.close()

except socket.error:
    print(f'[-] {port} is closed')
    sock.close()
```

We want to include a usage statement and error handling for if the user does not specify the correct amount of arguments.  More error handling could be included to ensure the user enters specifically an IP address and a valid port, but this is outside the scope of this introductory course and since we will be using these tools personally.

### argparse

Argparse provides a LOT more functionality to the command line ability, but can be a bit daunting at first.  Argparse requires an "ArgumentParser" object and methods are specified for each argument by using the add_argument function.  Once all arguments have been added, call "parse_args", then the arguments can be accessed by the variable name and the argument name.

```
import socket
import argparse

parser = argparse.ArgumentParser(prog='Port Scanner',
                                 description='A simple TCP port Scanner',)

parser.add_argument('ip', default='127.0.0.1', help='The target IP address')
parser.add_argument('-p', '--port', help='A single port')
parser.add_argument('-b', '--begin', help='The beginning of the port range')
parser.add_argument('-e', '--end', help='The end of the port range')

args = parser.parse_args()

sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
ip = args.ip

if (args.begin and args.end):
    ports = range(int(args.begin), int(args.end))
    for port in ports:
        try:
            conn = sock.connect((ip, port))
            print(f'[+] {port} is open')
            sock.close()

        except socket.error:
            print(f'[-] {port} is closed')
            sock.close()
else:
    port = int(args.port)
    try:
        conn = sock.connect((ip, port))
        print(f'[+] {port} is open')
        sock.close()

    except socket.error:
        print(f'[-] {port} is closed')
        sock.close()
```

Additionally, arguments can be optional or positional.  Positional arguments are required to be called in the order that they are specified in the program, whereas optional require certain flags to be set in order to access them.  In this program, the IP argument is positional and required.  The port, begin, and end are all optional, but the program will error out if they are not specified.

## Threading, multiprocessing, and asyncio

This is a much more advanced topic, but the scanner can become even faster if tap into these synchronous programming elements and run each port scan concurrent to the others.

# Brainstorming and Collaboration

At this point, let's consider some ways we can achieve solutions personally or in our work environment using python and tools we have at our disposal.

* Web scraping
* Password cracking
* Keylogger
* Server/Client
* Recreating OS binaries
* Reading/writing files

# Resources

[Replit (Web IDE)](https://replit.com/) \
[Leetcode (Practice)](https://leetcode.com/) \
[Codewars (Practice)](https://www.codewars.com/) \
[Python3 Official Documentation](https://docs.python.org/3/)
