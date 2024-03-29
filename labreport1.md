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
This command stands for 'list' and intuitively, we can guess that it should print out a list of a directories contents. Let's see what happens in our three cases.
## No arguments
In this case, no arguments are passed into the `ls` command and it is entered plainly into the terminal. In this experiment, we start from the `/home` directory.

```
[user@sahara ~]$ ls
lecture1
```

Interesting! It prints out `lecture1` and that is colored in blue while the rest are colored normally in black. What happens if we use `ls` on `/home/lecture1`?

```
[user@sahara ~/lecture1]$ ls
Hello.class  Hello.java  messages  README
```

Here, `messages` is in blue while everything else is black. How about in `/home/lecture1/messages`?

```
[user@sahara ~/lecture1/messages]$ ls
en-us.txt  es-mx.txt  id.txt  zh-cn.txt
```

Here, nothing is blue and everything is 'normal' in color. As we can see, using `ls` with no arguments simply results in the terminal outputting a list of all the 'children' (files, directories, etc.) that are inside the current working directory. When we are in `/home`, there is only `lecture1`, while the `lecture1` and `messages` directory contained their own individual files and directories. The `ls` command printed out the contents within these directories when we used `cd` to move our current working directory into them.

Another thing to note is that files are colored black, while directories are colored blue when using `ls`.

This is **not** an error and it is an intended functionality of the `ls` command to print the contents of the current working directory when no arguments are provided as the system interprets it as the user asking for a list of the current working directory.

## Argument: Path to a directory
In this case, a path to a directory is passed into `ls`. Starting from `/home`, we try to enter the path to `/lecture1/messages` into the ls command.

```
[user@sahara ~]$ ls lecture1/messages
en-us.txt  es-mx.txt  id.txt  zh-cn.txt
```

As we can see, this is equivalent to using `cd` to move into `/home/lecture1/messages` and then typing `ls` - these are the contents of the `messages` directory. We can then see that passing a path to a directory into `ls` results in the terminal printing the contents of that directory we passed into the command.

This is **not** an error - it is again intended functionality of the `ls` command.

## Argument: Path to a file
Now, we try passing a path to a file into the `ls` command. Starting from the `/home/lecture1` directory, we try to pass the `Hello.java` file into the command.

```
[user@sahara ~/lecture1]$ ls Hello.java
Hello.java
```

What if we try to pass `en-us.txt` that is inside `messages` into `ls` from `/home/lecture1`?

```
[user@sahara ~/lecture1]$ ls messages/en-us.txt 
messages/en-us.txt
```

What if we go from `/home` and try to access that `en-us.txt` file?

```
[user@sahara ~]$ ls lecture1/messages/en-us.txt 
lecture1/messages/en-us.txt
```

As we can see, when we try to pass a file's path into `ls`, it basically just repeats what we enter as an argument back at us. When we are accessing a file that is directly in the current working directory, it just prints the name of the file (as we just put the name of the file as well). What's interesting is that it *doesn't* seem to print the path, but just repeats what was entered. We can see this by looking at the last output - it doesn't print `/home/lecture1/messages/en-us.txt`, it just prints exactly what we give it.

This is **not** an error - it still prints an appropriate output, but it definitely does seem useless.

# Command: `cat`
The `cat` command stands for concatenate - which means to 'join' strings or text together. It is harder to guess what this does by it's name, so let's try to see what happens in our 3 cases.
## No arguments
Typing just `cat` into the terminal with no arguments has an interesting result. Here, we start from `/home`.

```
[user@sahara ~]$ cat

```

It seemingly removes the `[user@sahara ~]` portion and prompts us to type on the empty space. What happens if we do that?

```
[user@sahara ~]$ cat
hi
hi
Hello
Hello
This is a test of the cat command!
This is a test of the cat command!
```

Interestingly, typing the cat command without any arguments let's us type whatever we want into blank space and the terminal will then print back to us exactly what we wrote. This happens regardless of what directory we are in and what files are in that directory - the cat command simply makes us enter a 'repeat back' mode.

This is **not** an error and is likely a feature implemented for when for some reason, the user decides that they want to output a purely user-typed message into the terminal (though I'm not sure why they wouldn't just use `echo <message>` instead). I struggled a bit with figuring out how to exit this mode, but I've found that clicking CTRL + C or CTRL + D works to return to the normal mode.

## Argument: Path to a directory
What happens if we pass the path to a directory into the `cat` command? Let's see! Starting from the `/home` directory, we attempt to pass the `/home/lecture1` directory into the command.

```
[user@sahara ~]$ cat lecture1
cat: lecture1: Is a directory
```

The terminal simply tells us that `lecture1` is a directory - not a file. There is no way for the `cat` command to concatenate a directory as there is nothing to concatenate! This **is** an error message - the `cat` command cannot work with a directory at all.

## Argument: Path to a file
So now that we know the `cat` command cannot work with a directory, what happens if we pass a file? Starting from the `/home` directory, we attempt to pass `Hello.java` into the command using its path `/home/lecture1/Hello.java`

```
[user@sahara ~]$ cat lecture1/Hello.java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

public class Hello {
  public static void main(String[] args) throws IOException {
    String content = Files.readString(Path.of(args[0]), StandardCharsets.UTF_8);    
    System.out.println(content);
  }
}
```

These are the contents of the Hello.java file! Let's experiment a bit more. What happens if we try this on two files? Starting from the `/home` directory, we pass two arguments in: the path for `Hello.java` and the path for the `en-us.txt` file in `messages`

```
[user@sahara ~]$ cat lecture1/Hello.java lecture1/messages/en-us.txt 
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

public class Hello {
  public static void main(String[] args) throws IOException {
    String content = Files.readString(Path.of(args[0]), StandardCharsets.UTF_8);    
    System.out.println(content);
  }
}Hello World!
```

How about three files? We add the path for `es-mx.txt` in the `messages` directory onto it!

```
[user@sahara ~]$ cat lecture1/Hello.java lecture1/messages/en-us.txt lecture1/messages/es-mx.txt 
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

public class Hello {
  public static void main(String[] args) throws IOException {
    String content = Files.readString(Path.of(args[0]), StandardCharsets.UTF_8);    
    System.out.println(content);
  }
}Hello World!
¡Hola Mundo!
```

We can see here that the `cat` command prints out the contents of the file whose path is passed into it. Additionally, when multiple files are given, the `cat` command concatenates them - 'joining' the texts - together. We can string more than just two files together using the `cat` command as well! This is the standard functionality of the `cat` command - displaying and, as its name suggests, concatenating the contents of files together and outputting them into the terminal. When only one file is specified, it just outputs the contents of that one file with nothing to concatenate together. With more than one file, it concatenates the contents of all the files.

This is **not** an error - it is the intended functionality of the `cat` command.

Let's try a small experiment. What if we try using `cat` on a `.class` file? More specifically, the `Hello.class` file located in the `lecture1` directory.

```
[user@sahara ~]$ cat lecture1/Hello.class 
����A2

java/lang/Object<init>()java/lang/String




java/nio/file/Pathof;(Ljava/lang/String;[Ljava/lang/String;)Ljava/nio/file/Path;
!java/nio/charset/StandardCharsetsUTF_8Ljava/nio/charse
t/Charset;

java/nio/file/Files
readStringB(Ljava/nio/file/Path;Ljava/nio/charset/Charset;)Ljava/lang/String;
 java/lang/SystemoutLjava/io/PrintStream;
"#$
%&java/io/PrintStreamprintln(Ljava/lang/String;)V(HelloCodeLineNumberTablemain([Ljava/lang/String;)V
Exceptions/java/io/IOException
SourceFile
Hello.java!')*��*+,)9*2����L�
```

The `cat` command still outputs the contents of the file, but it is relatively illegible. This is because `Hello.class` is a binary file that is created after the Java Compiler compiles the `Hello.java` file. It has content, sure, and the `cat` command can still output that. However, it is meant for the computer to read and interpret. Interestingly, we can still see some remnants of the code in the `Hello.java` file here. 

This is still **not** an error - just a weird application of the command.
