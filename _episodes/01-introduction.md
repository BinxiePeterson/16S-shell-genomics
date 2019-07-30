---
title: "Introducing the Shell"
teaching: 20
exercises: 5
questions:
- "What is a command shell and why would I use one?"
- "How can I move around on my computer?"
- "How can I see what files and directories I have?"
- "How can I specify the location of a file or directory on my computer?"
objectives:
- "Describe key reasons for learning shell."
- "Navigate your file system using the command line."
- "Demonstrate the use of tab completion, and explain its advantages."
keypoints:
- "The shell gives you the ability to work more efficiently by using keyboard commands rather than a GUI."
- "`pwd`, `ls`, and `cd` are useful commands to navigate a file system."
- "Tab completion can reduce errors from mistyping and make work more efficient in the shell."
---

## What is a shell and why should I care?

A *shell* is a computer program that presents a command line interface
which allows you to control your computer using commands entered
with a keyboard instead of controlling graphical user interfaces
(GUIs) with a mouse/keyboard combination.

There are many reasons to learn about the shell:

* Many bioinformatics tools can only be used through a command line interface, or 
have extra capabilities in the command line version that are not available in the GUI.
This is true, for example, of BLAST, which offers many advanced functions only accessible
to users who know how to use a shell.  
* The shell makes your work less boring. In bioinformatics you often need to do
the same set of tasks with a large number of files. Learning the shell will allow you to
automate those repetitive tasks and leave you free to do more exciting things.  
* The shell makes your work less error-prone. When humans do the same thing a hundred different times
(or even ten times), they're likely to make a mistake. Your computer can do the same thing a thousand times
with no mistakes.  
* The shell makes your work more reproducible. When you carry out your work in the command-line 
(rather than a GUI), your computer keeps a record of every step that you've carried out, which you can use 
to re-do your work when you need to. It also gives you a way to communicate unambiguously what you've done, 
so that others can check your work or apply your process to new data.  
* Many bioinformatic tasks require large amounts of computing power and can't realistically be run on your
own machine. These tasks are best performed using remote computers or cloud computing, which can only be accessed
through a shell.

![Automation](../img/gvng.jpg)

In this lesson you will learn how to use the command line interface to move around in your file system. 

## How to access the shell

On a Mac or Linux machine, you can access a shell through a program called Terminal, which is already available
on your computer. If you're using Windows, you'll need to download a separate program to access the shell.


> ## Accessing the shell  
> **Mac**  
> On Mac the shell is available through Terminal  
> Applications -> Utilities -> Terminal  
> You can drag the Terminal application to your Dock for easy access.
> 
> **Windows**  
> For Windows, we're going to be using gitbash.  
> Download and install [gitbash](http://msysgit.github.io).
> Open up the program.
> 
> **Linux**    
> The shell is available by default when you connect to a remote server.  
{: .callout}


## Starting with the shell

We will spend most of our time learning about the basics of the shell
by manipulating some experimental data.

We're going to be working with data that has been preloaded onto our remote server. 

You can log-in to the remote server using the information in the Etherpad. First 
open your shell (through the Terminal application) and then enter the text starting
with `ssh` from the Etherpad. Each of you will have a different log-in. This will 
prevent us from accidentally changing each other's files as we work through the
exercises.  

## Navigating your file system

The part of the operating system responsible for managing files and directories
is called the **file system**.
It organizes our data into files,
which hold information,
and directories (also called "folders"),
which hold files or other directories.

Several commands are frequently used to create, inspect, rename, and delete files and directories.

> ## Preparation Magic
>
> If you type the command:
> `PS1='$ '`
> into your shell, followed by pressing the 'enter' key,
> your window should look like our example in this lesson.  
> This isn't necessary to follow along (in fact, your prompt may have
> other helpful information you want to know about).  This is up to you!  
{: .callout}

~~~
$
~~~
{: .bash}

The dollar sign is a **prompt**, which shows us that the shell is waiting for input;
your shell may use a different character as a prompt and may add information before
the prompt. When typing commands, either from these lessons or from other sources,
do not type the prompt, only the commands that follow it.

Let's find out where we are by running a command called `pwd`
(which stands for "print working directory").
At any moment, our **current working directory**
is our current default directory,
i.e.,
the directory that the computer assumes we want to run commands in
unless we explicitly specify something else.
Here,
the computer's response is `/home/username`,
which is the top level directory within our HPC system:

~~~
$ pwd
~~~
{: .bash}

~~~
/home/username
~~~
{: .output}

Let's look at how our file system is organized.  

At the top is our `username` directory, which holds all the 
subdirectories and files.

Inside that directory are file(s) and other directories:
`dc_sample_data`
and
`project`

We'll be working with many of the subdirectories within these two directories throughout this workshop.  


The command to change locations in our file system is `cd`, followed by a
directory name to change our working directory.
`cd` stands for "change directory".

Let's say we want to navigate to the `dc_sample_data` directory we saw above.  We can
use the following command to get there:

~~~
$ cd dc_sample_data
~~~
{: .bash}

We can see files and subdirectores in this directory by running `ls`,
which stands for "listing":

~~~
$ ls
~~~
{: .bash}

~~~
sra_metadata  untrimmed_fastq 
~~~
{: .output}

`ls` prints the names of the files and directories in the current directory in
alphabetical order,
arranged neatly into columns.
We can make its output more comprehensible by using the **flag** `-F`,
which tells `ls` to add a trailing `/` to the names of directories:

~~~
$ ls -F
~~~
{: .bash}

~~~
sra_metadata/  untrimmed_fastq/
~~~
{: .output}

Anything with a "/" after it is a directory.  
Things with a "*" after them are programs.  
If there are no decorations, it's a file.

`ls` has lots of other options. To find out what they are, we can type:

~~~
$ man ls
~~~
{: .bash}

Some manual files are very long. You can scroll through the file using
your keyboard's down arrow or use the space key to go forward one page
and the `b` key to go backwards one page. When you are done reading, hit `q`
to quit.

> ## Challenge
> Use the `-l` option for the `ls` command to display more information for each item 
> in the directory. What is one piece of additional information this long format
> gives you that you don't see with the bare `ls` command?
>
> > ## Solution
> > ~~~
> > $ ls -l
> > ~~~
> > {: .bash}
> > 
> > ~~~
> > drwxrwxr-x 4 user user     4096 Oct 6  07:25 sra_metadata
> > drwxrwxr-x 4 user user     4096 Oct 6  07:25 untrimmed_fastq
> > ~~~
> > {: .output}
> > 
> > The additional information given includes the name of the owner of the file,
> > when the file was last modified, and whether the current user has permission
> > to read and write to the file.
> > 
> {: .solution}
{: .challenge}

No one can possibly learn all of these arguments, that's why there is a manual page. You can (and should) refer to the manual page or other help files as needed.

Let's go into the `untrimmed_fastq` directory and see what is in there.

~~~
$ cd untrimmed_fastq
$ ls -F
~~~
{: .bash}

~~~
SRR097977.fastq  SRR098026.fastq
~~~
{: .output}

This directory contains two files with `.fastq` extensions. FASTQ is a format
for storing information about sequencing reads and their quality.
We will be learning more about FASTQ files in a later lesson.

### Shortcut: Tab Completion

Typing out file or directory names can waste a
lot of time and it's easy to make typing mistakes. Instead we can use tab complete 
as a shortcut. When you start typing out the name of a directory or file, then
hit the tab key, the shell will try to fill in the rest of the
directory or file name.

For example, type `cd` to go back to your home directory, then enter:

~~~
$ cd dc_sam<tab>
~~~
{: .bash}

The shell will fill in the rest of the directory name for
`dc_sample_data`.

Now change directories to `untrimmed_fastq` in `dc_sample_data`

~~~
$ cd dc_sample_data/untrimmed_fastq
~~~
{: .bash}

Notice that we can move two (or more) directory levels at a time by placing a `/` 
between directory names.

Using tab complete can be very helpful. However, it will only autocomplete
a file or directory name if you've typed enough characters to provide
a unique identifier for the file or directory you are trying to access.

If we navigate back to our `untrimmed_fastq` directory and try to access one
of our sample files:

~~~
$ cd dc_sample_data/untrimmed_fastq
$ ls SRR09<tab>
~~~
{: .bash}

Nothing happens because there are multiple files which start with
`SRR09`. The shell does not know which one to fill in. When you hit
tab again, the shell will list the possible choices.

~~~
$ ls SRR09<tab><tab>
~~~
{: .bash}

Tab completion can also fill in the names of programs, which can be useful if you
remember the begining of a program name. 

~~~
$ pw<tab><tab>
~~~
{: .bash}

~~~
pwck   pwconv    pwd   pwdx    pwunconv
~~~
{: .output}

Displays the name of every program that starts with `pw`. 


## More information on the shell

Shell cheat sheets:<br>
* [http://fosswire.com/post/2007/08/unixlinux-command-cheat-sheet/](http://fosswire.com/post/2007/08/unixlinux-command-cheat-sheet/)
* [https://github.com/swcarpentry/boot-camps/blob/master/shell/shell_cheatsheet.md](https://github.com/swcarpentry/boot-camps/blob/master/shell/shell_cheatsheet.md)

Explain shell - a web site where you can see what the different components of
a shell command are doing.  
* [http://explainshell.com](http://explainshell.com)
* [http://www.commandlinefu.com](http://www.commandlinefu.com)

