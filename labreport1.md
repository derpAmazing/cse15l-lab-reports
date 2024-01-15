# CSE 15L Lab Report 1 - Remote Access and FileSystem
Week 1's lab report is a blog post detailing the use of 3 filesystem commands that we learned in class:
- `cd`
- `ls`
- `cat`

In particular, this lab report will detail and show examples of what happens when certain types of arguments are passed into these commands, namely:
1. When no arguments are passed into the command
2. When a path to a directory is passed into the command
3. When a path to a file is passed into the command

The directory used in this lab report is [here](https://github.com/ucsd-cse15l-f23/lecture1)

# Command: `cd`
The command cd stands for **change directory**. By this, we can quickly assume that normally a path to a directory is one that should be passed into the command.
## No arguments
No arguments means that we enter just `cd` into the terminal with nothing else at all.
Starting from the directory `/home/lecture1/messages`, we can see that before entering the command, our line looks like this:

```[user@sahara ~/lecture1/messages]$ cd```

After entering the command, our line changes to this:

```[user@sahara ~]$ ```

The same thing happens when we enter `cd` from `/home/lecture1`, where we go from: 

```[user@sahara ~/lecture1]$ cd```

to:

```[user@sahara ~]$ ```

This shows us that typing `cd` without any arguments returns us to the home directory. We can confirm this by using `pwd` - print working directory, which would tell us that after the `cd` command is executed our current working directory always becomes `/home`. Nothing about the filesystem itself matters.

```
[user@sahara ~/lecture1/messages]$ cd
[user@sahara ~]$ pwd
/home
```

This happens because `cd` means change directory, and when no argument is passed at all the system simply returns us to the home directory. This is **not** an error and is likely a useful feature that is used often.

## Argument: Path to a directory

In this instance, a path to a directory is passed into the command. Here we start at the home directory, `/home`, before entering:

```cd lecture1```

Then we can check what happens by using `pwd` to check our current working directory. This is what the output looks like:

```
[user@sahara ~]$ cd lecture1
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```

We can continue from `/home/lecture1` and into `/home/lecture1/messages` by entering `cd messages`.

```
[user@sahara ~/lecture1]$ cd messages
[user@sahara ~/lecture1/messages]$ pwd
/home/lecture1/messages
```

If we start from `/home`, we can enter `cd lecture1/messages` to do both of those in one line.

```
[user@sahara ~]$ cd lecture1/messages
[user@sahara ~/lecture1/messages]$ pwd
/home/lecture1/messages
```

This is the 'standard' functionality of the `cd` command - changing directories. As the file directory we are working with consists of a directory called `lecture1`, which then contains some files and the `messages` directory, we are able to traverse this directory by entering a path to a directory into the `cd` command. The system takes the argument - a path to a directory - and 'moves' our working directory there. This is **not** an error - it is the intended functionality of `cd`.

## Argument: Path to a file

What happens if instead of a path to a directory, we pass a path to a file into `cd`?

We start from the `/home` directory, and try to access the `Hello.java` file available in the `/home/lecture1` directory. We can do that by appending `Hello.java` in front of the directory path of `lecture1`.

```
[user@sahara ~]$ cd lecture1/Hello.java
bash: cd: lecture1/Hello.java: Not a directory
[user@sahara ~]$ 
```

As we can see, our current working directory does not change in this case and instead, the terminal prints a message telling us that `Hello.java` is *not* a directory. This **is** an error and it happens because `cd` is used for the user to 'travel' through directories. However, a file like `Hello.java` is not a directory and we cannot 'travel' into a file to see other files and directories that it holds. This happens regardless of what file is provided into `cd` - it can only accept a path to a directory as an argument. After all, `cd` stands for 'change directory', so how and why would it be able to change our working directory into a file?

# Command: `ls`
## No arguments
## Argument: Path to a directory
## Argument: Path to a file
# Command: `cat`
## No arguments
## Argument: Path to a directory
## Argument: Path to a file
