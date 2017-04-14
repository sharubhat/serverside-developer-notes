# Python basics

I need to decide whether to learn python2 or 3 by the time I finish this paragraph. The most confusing part is to decide whether to learn python2 or python3. From what I have read so far, they are not compatible with each other. Most of existing modules are in python2 as it's more popular but it's probably a good idea to move forward. **My goal is to get up and running quickly.**

Well, I am going to learn **python3**. So this notes will be all about Python-3. BUT, if I run into serious issues and need to fall back to version2 midway, I may choose to do that. We developers spend most of our time solving problems. So I will keep these notes mostly problem statement, solution model.

**Tools:**

1. Obviously python3 installation. You could use homebrew on mac or install manually. A lot of help is available, so skipping the details.
2. IDE or editors: Will begin with IDLE that's supplied with python. Coming from java world, I am a fan of jetbrains products. So will most likey switch to pycharm community edition soon.

**Problem 1 : Write a program that prints current time.**

Create a file time.py and save the following contents.

```py
from datetime import datetime

print(datetime.today())
```

If you are in IDLE, you could save and hit F5 to run this. Or run `$python3 time.py` from command line.

Note that you can also run these two lines in REPL \(read-eval-print-loop\) and get the same results.

**Study notes:**

Python always starts at beginning of the file and executes the code line by line.

Python interpreter is also known as Python. The only difference compared to languages like Java is that python interpreter runs the code line by line and there is no notion of compiling entire source code into a class file.

Lets now try something more then a 'hello world' style introductory program.

**Problem 2: Write a program that takes an argument and prints current username if the argument is 'whoami' or 'currentuser'.**

I know this is a stupid example, but this will teach something. There are various ways to get current user and depending on OS and how the program is being run, the results can be inaccurate. Also there are a few ways to handle command line  argument, but that will be another post.

Create whoami.py and save the following contents in it.

```py
import sys
import getpass

if sys.argv[1] == 'whoami':
  print("Current user is " + getpass.getuser())
elif sys.argv[1] == 'currentuser':
  print("Current user is " + getpass.getuser())
else:
  print("Invalid argument")
```

What if you want to print the current user when the argument matches 'whoami' or 'currentuser'?

```py
keywords = ['whoami', 'currentuser']
if len(sys.argv) > 1 and sys.argv[1] in keywords:
```

Few things to note here are,

* logical and is 'and' instead of '&&' like in java
* 'in' keyword allows you to check if a list contains given element
* 'elif' is short for else if
* len\(\) function returns length of a collection
* there is no concept of declaring the type of a variable. They are inferred at runtime and can change when a value of different type is assigned to them.
* ':' introduces a suite of code \(you heard it, block of code is called suite in python\). suits are preceded by a colon \(:\), this is requirement of the language.
* parenthesis are not used in python to represent suits, indentation takes care of it
* we fixed a bug in the first solution which would throw `IndexError: list index out of range` if no argument is passed to the program

**Problem 2.1: Print the current user's name twice with 3 seconds delay between the two print statements. **

Again this silly requirement is to show the usage of 'for' keyword and sleep\(\) function from 'time' library. The only reason for introducing sleep here is it's something that comes up often while debugging and so is good to know. So the updated program would look like this.

```py
import getpass
import sys
import time

keywords = ['whoami', 'currentuser']

for i in [1, 2]:
    if len(sys.argv) > 1 and sys.argv[1] in keywords:
        print("Current user is " + getpass.getuser())
    else:
        print("Invalid argument")
    time.sleep(3)
```

**Be careful about indentation**. Can't stress it enough.

Since we are talking about for loop here, an example of string which is self explanatory.

```py
for ch in "Hello World":
    print(ch)
```

Note: range\(5\) returns a list \[0, 1, 2, 3, 4\]





