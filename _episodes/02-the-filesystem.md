---
title: "The Filesystem"
teaching: 15
exercises: 5
questions:
- "How can I give my computer directions to files I want to access?"
objectives:
- "Navigate the Unix file system."
- "Understand and use file paths and relative paths."
- "Keyboard shortcuts to make work more efficiently at the command line."
keypoints:
- "The shell gives you the ability to work more efficiently by using keyboard commands rather than a GUI."
- "pwd, ls, and cd are useful commands to navigate a file system."
- "Tab completion can reduce errors from mistyping and make work more efficient in the shell."
---


## The Unix directory file structure (a.k.a. where am I?)

As you've already just seen, you can move around in different directories
or folders at the command line. Why would you want to do this, rather
than just navigating around by clicking on folders as you might usually do.

When you're working with bioinformatics programs, you're working with
your data and it's key to be able to have that data in the right place
and make sure the program has access to the data. Many of the problems
people run in to with command line bioinformatics programs is not having the
data in the place the program expects it to be.


## Moving around the file system

We've learned how to use `pwd` to find our current location within our file system. 
We've also learned how to use `cd` to change locations and `ls` to list the contents
of a directory. Now we're going to learn some additional commands for moving around 
within our file system.

What if we want to move back up and out of this directory and to our top level 
directory? Can we type `cd dc_sample_data`? Try it and see what happens.

~~~
$ cd dc_sample_data
~~~
{: .bash}

~~~
-bash: cd: dc_sample_data: No such file or directory
~~~
{: .output}

Your computer looked for a directory or file called `dc_sample_data` within the 
directory you were already in. It didn't know you wanted to look at a directory level
above the one you were located in. 

We have a special command to tell the computer to move us back or up one directory level. 

~~~
$ cd ..
~~~
{: .bash}


Now we can use `pwd` to make sure that we are in the directory we intended to navigate
to, and `ls` to check that the contents of the directory are correct.

~~~
$ pwd
~~~
{: .bash}

~~~
/home/username/dc_sample_data
~~~
{: .output}

~~~
$ ls
~~~
{: .bash}

~~~
sra_metadata  untrimmed_fastq
~~~
{: .output}

From this output, we can see that `..` did indeed take us back one level in our file system. 

You can chain these together like so:

~~~
$ ls ../
~~~
{: .bash}

prints the contents of `/home/username` which is your home directory. 

> ## Finding hidden directories
>
> There is a hidden directory in our file system. Explore the options for `ls` to 
> find out how to see hidden directories. List the contents of the directory and 
> identify the name of the text file in that directory.
> 
> Hint: hidden files and folders in Unix start with `.`, for example .my_hidden_directory
>
> > ## Solution
> > 
> > First use the `man` command to look at the options for `ls`. 
> > ~~~
> > $ man ls
> > ~~~
> > {: .bash}
> > 
> > The `-a` option is short for `all` and says that it causes `ls` to "not ignore
> > entries starting with ." This is the option we want. 
> > 
> > ~~~
> > $ ls -a
> > ~~~
> > {: .bash}
> > 
> > ~~~
> > .  ..  .hidden	sra_metadata    untrimmed_fastq
> > ~~~
> > {: .output}
> > 
> > The name of the hidden directory is `.hidden`. We can navigate to that directory
> > using `cd`. 
> > 
> > ~~~
> > $ cd .hidden
> > ~~~
> > {: .bash}
> > 
> > And then list the contents of the directory using `ls`. 
> > 
> > ~~~
> > $ ls
> > ~~~
> > {: .bash}
> > 
> > ~~~
> > youfoundit.txt
> > ~~~
> > {: .output}
> > 
> > The name of the text file is `youfoundit.txt`.
> {: .solution}
{: .challenge}

## Examining the contents of other directories

By default, the `ls` commands lists the contents of the working
directory (i.e. the directory you are in). You can always find the
directory you are in using the `pwd` command. However, you can also
give `ls` the names of other directories to view. Navigate to the
home directory if you are not already there.

~~~
$ cd
~~~
{: .bash}

Then enter the command:

~~~
$ ls dc_sample_data
~~~
{: .bash}

~~~
sra_metadata  untrimmed_fastq
~~~
{: .output}

This will list the contents of the `dc_sample_data` directory without
you needing to navigate there.

The `cd` command works in a similar way.

Try entering:

~~~
$ cd
$ cd dc_sample_data/untrimmed_fastq
~~~
{: .bash}

This will take you to the `untrimmed_fastq` directory without having to go through
the intermediate directory.

> ## Navigating practice
> 
> Navigate to your home directory. From there, list the contents of the `untrimmed_fastq` 
> directory. 
> 
> > ## Solution
> >
> > ~~~
> > $ cd
> > $ ls dc_sample_data/untrimmed_fastq/
> > ~~~
> > {: .bash}
> > 
> > ~~~
> > SRR097977.fastq  SRR098026.fastq 
> > ~~~
> > {: .output}
> > 
> {: .solution}
{: .challenge}

## Full vs. Relative Paths

The `cd` command takes an argument which is a directory
name. Directories can be specified using either a *relative* path or a
full *absolute* path. The directories on the computer are arranged into a
hierarchy. The full path tells you where a directory is in that
hierarchy. Navigate to the home directory, then enter the `pwd`
command.

~~~
$ cd  
$ pwd  
~~~
{: .bash}

You will see: 

~~~
/home/username
~~~
{: .output}

This is the full name of your home directory. This tells you that you
are in a directory called `username`, which sits inside a directory called
`home` which sits inside the very top directory in the hierarchy. The
very top of the hierarchy is a directory called `/` which is usually
referred to as the *root directory*. So, to summarize: `username` is a
directory in `home` which is a directory in `/`.

Now enter the following command:

~~~
$ cd /home/username/dc_sample_data/.hidden
~~~
{: .bash}

This jumps forward multiple levels to the `.hidden` directory. 
Now go back to the home directory. 

~~~
$ cd
~~~
{: .bash}

You can also navigate to the `.hidden` directory using:

~~~
$ cd dc_sample_data/.hidden
~~~
{: .bash}


These two commands have the same effect, they both take us to the `.hidden` directory.
The first uses the absolute path, giving the full address from the home directory. The
second uses a relative path, giving only the address from the working directory. A full
path always starts with a `/`. A relative path does not.

A relative path is like getting directions from someone on the street. They tell you to
"go right at the stop sign, and then turn left on Main Street". That works great if
you're standing there together, but not so well if you're trying to tell someone how to
get there from another country. A full path is like GPS coordinates. It tells you exactly
where something is no matter where you are right now.

You can usually use either a full path or a relative path
depending on what is most convenient. If we are in the home directory,
it is more convenient to enter the relative path since it
involves less typing.

Over time, it will become easier for you to keep a mental note of the
structure of the directories that you are using and how to quickly
navigate amongst them.

> ## Relative path resolution
> 
> Using the filesystem diagram below, if `pwd` displays `/Users/thing`,
> what will `ls ../backup` display?
> 
> 1.  `../backup: No such file or directory`
> 2.  `2012-12-01 2013-01-08 2013-01-27`
> 3.  `2012-12-01/ 2013-01-08/ 2013-01-27/`
> 4.  `original pnas_final pnas_sub`
> 
> ![File System for Challenge Questions](../fig/filesystem-challenge.svg)
> 
> > ## Solution
> >  1. No: there *is* a directory `backup` in `/Users`.
> >  2. No: this is the content of `Users/thing/backup`,
> >   but with `..` we asked for one level further up.
> >  3. No: see previous explanation.
> >    Also, we did not specify `-F` to display `/` at the end of the directory names.
> >  4. Yes: `../backup` refers to `/Users/backup`.
> {: .solution}
{: .challenge} 

### Navigational Shortcuts

There are some shortcuts which you should know about. Dealing with the
home directory is very common. So, in the shell the tilde character,
`~`, is a shortcut for your home directory. Navigate to the `dc_sample_data`
directory:

~~~
$ cd
$ cd dc_sample_data
~~~
{: .bash}

Then enter the command:

~~~
$ ls ~
~~~
{: .bash}

This prints the contents of your home directory, without you needing to 
type the full path. 

To summarize, while you are in the `shell` directory, the commands
`ls ~`, `ls ~/.`, and `ls /home/username` all do exactly the
same thing. These shortcuts are not necessary, they are provided for
your convenience.

