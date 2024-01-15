# CSE 15L Lab Report 1 - Remote Access and FileSystem
Week 1's lab report is a blog post detailing the use of 3 filesystem commands that we learned in class:
- `cd`
- `ls`
- `cat`

In particular, this lab report will detail and show examples of what happens when certain types of arguments are passed into these commands, namely:
1. When no arguments are passed into the command
2. When a path to a directory is passed into the command
3. When a path to a file is passed into the command

The directory used in this lab report is [here]https://github.com/ucsd-cse15l-f23/lecture1

# Command: `cd`
The command cd stands for **change directory**. By this, we can quickly assume that normally a path to a directory is one that should be passed into the command.
## No arguments
No arguments means that we enter just `cd` into the terminal with nothing else at all.
Starting from the directory /home/lecture1/messages, we can see that before entering the command, our line looks like this:
```[user@sahara ~/lecture1/messages]$ cd```

After entering the command, our line changes to this:
```[user@sahara ~]$ ```

The same thing happens when we enter `cd` from /home/lecture1, where we go from: 
```[user@sahara ~/lecture1]$ cd```

to:
```[user@sahara ~]$ ```

This shows us that typing `cd` without any arguments returns us to the home directory. We can confirm this by using `pwd` - print working directory, which would tell us that after the `cd` command is executed, we are always returned to the /home directory:
```
[user@sahara ~/lecture1/messages]$ cd
[user@sahara ~]$ pwd
/home
```

## Argument: Path to a directory
## Argument: Path to a file
# Command: `ls`
## No arguments
## Argument: Path to a directory
## Argument: Path to a file
# Command: `cat`
## No arguments
## Argument: Path to a directory
## Argument: Path to a file
