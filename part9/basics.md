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

**Problem 2: Write a program that takes an argument and prints current username if the argument is 'whoami'.**

I know this is a stupid example, but this will teach something. There are various ways to get current user and depending on OS and how the program is being run, the results can be inaccurate. Also there are a few ways to handle command line  argument, but that will be another post.

Create whoami.py and save the following contents in it.

```py
import sys
import getpass

if sys.argv[1] == 'whoami':
  print("Current user is " + getpass.getuser())
else:
  print("Invalid argument")
```



