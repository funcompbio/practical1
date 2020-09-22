---
layout: page
title: Practical 1
permalink: /practical1/
---

# Setup and background

In this practical we will use some basic commands to navigate and manipulate the Unix file system. You
need to have access to the [command-line interface](https://en.wikipedia.org/wiki/Command-line_interface)
of your operating system. Please check the [setup](/setup/) webpage to make
sure that you have access to some flavor of an Unix operating system and its command line.

To practise working with files from the Unix command-line we will download some COVID19 data. Please
follow the next two steps:

1. Go to the Catalan Health Departament COVID data portal at [https://dadescovid.cat](https://dadescovid.cat)
   and switch the language to "ENGLISH" using the pull-down menu on the top-right corner of the page.
2. Follow the downloads link and on the next page click and download the two files corresponding to the
   "7 DAY AGGREGATION" and the "DAILY DATA" for "CATALUNYA". Make sure you know exactly where in your
   filesystem these two files have been downloaded. **Tip:** some browsers automatically download files into
   a folder called "Downloads" or under a name corresponding to the translation of "Downloads" to the default
   language of your operating system.

# Creating your first directory

Open a terminal window and figure out which is your username and your default path working directory (PWD) by
typing the commands `whoami` (first) and `pwd` (second) on the
[command prompt](https://en.wikipedia.org/wiki/Command-line_interface#Command_prompt).
After you type each command you should press the `Enter` key to ask the shell to execute the command. Your
interaction with the shell in the terminal window should look similar to the following image.

![](./terminaldefault.png)

The command prompt may display different information to the left of the cursor and usually ends with the
dollar sign. The solely purpose of the command prompt is to indicate where we can start typing commands,
while the purpose of the cursor is to indicate that the shell is waiting for us to type commands.
In the image above the command prompt it is displaying the name of the host computer (`messi`) and the
the current PWD, which corresponds to our
[_home_ directory](https://en.wikipedia.org/wiki/Home_directory)
and for this reason is abbreviated with the tilde `~`. In the image above the home directory is
`/Users/robert`, but tipically in a Unix system the home directory would hang from a directory called
`/home`.

Now, give the command to create a directory called `practical1`:

```
$ mkdir practical1
```

To check whether we have successfully created a directory called `practical1` we can use the command
`ls` and verify whether among the listed files we can find the name `practical1`. The output of `ls`
consists of the names of every file in your current PWD. It may useful to distinguish between regular
files and directories, you can do that in different ways, one of them using the option `-F`:

```
$ ls -F
```

You should see a trailing slash character '/' right after the name of each file that is a
directory, i.e., you should find for instance 'practical1/'.

# Using the online manual

The Unix system an online manual pages for each of its commands that can be accessed through the
command `man` giving as first argument the name of the command for which you want to read its manual
page. For instance, try to access the manual page of the command `ls` by doing:

```
man ls
```

All manual pages have the same structure of sections `NAME`, `SYNOPSIS`, `DESCRIPTION`, etc. and
you can browse through it by using the `Enter` key to scroll one line at a time, the `Space` key
to scroll by page, the `b` key to scroll one page backwards and the `q` key to quit the manual. Checkout
the meaning of the option `F` in the manual of `ls` and the manual page for `mkdir`. Make sure you
understand what is said in the section `NAME`.

# Changing the default path working directory 

We can change our default PWD to the new directory we have created before by doing:

```
$ cd practical1
```

To check whether we have successfully changed the PWD to the new directory, use again the command `pwd`.

# Copying and moving files

Locate the path where you have downloaded the two COVID19 data files and use the `ls` command to verify
that they are indeed stored on that directory. If you have downloaded the two files in a directory called
**for instance** `Downloads` located right below a home directory called **for instance** `/Users/robert`,
you can use the `ls` command as follows to check out the presence of those files in that directory

```
$ ls /Users/robert/Downloads
```

It may happen that you have lots of other files on that directory and becomes difficult to distinguish
whether your files of interest are really there. In this case, because the two files names that you have
downloaded start with the prefix `catalunya` you can use the so-called
[_wildcard_ character](https://en.wikipedia.org/wiki/Wildcard_character) `*` to restrict the file listing
operation to those two files by typing on the command-line:

```
$ ls /Users/robert/Downloads/catalunya*
```

So that if they are really there you will see only both of them, and eventually any other file that
starts with the prefix `catalunya`.  Now, copy both files to your current brand
new directory using the command `cp`. **For instance**, if one of the files **were** located at

```
/Users/robert/Downloads/catalunya_setmanal.zip
```

then the command to copy that file to the current PWD **would be**

```
cp /Users/robert/Downloads/catalunya_setmanal.zip .
```

**Tip:** when writing long paths it is useful to exploit the so-called _tab-completion mechanism_, which consists of pressing the `Tab` key (typically located above the `Caps Lock` key) once you've written a few letters of a file name in the path. If those few letters constitute a unique prefix of the filename, the rest of the filename will be written for you by the shell. If the prefix is not unique, by pressing the `Tab` key twice, the shell will show your the two or more filenames that match that prefix. Actually, the tab-completion mechanism also works for commands: if you type `cp` and press `Tab`, the shell will show you all the available commands that start with `cp`.

Note that because `/Users/robert` corresponds in this example to the _home_ directory of the user, we
could use the abbreviation `~`, corresponding to the _home_ directory, to write the previous command line as

```
cp ~/Downloads/catalunya_setmanal.zip .
```

Note that the previous command will work regardless of what is your username, as long as the sought file
is stored in the `Downloads` directory. **Tip:** In keyboards with a Spanish layout, the tilde `~` character can be written by pressing the keys
`AltGr+4`.

Once you have copied the two files, please verify using the command `ls` that the two files are indeed
in your current PWD. If you have been successful, you have probably typed twice the `cp` command. However,
because the two filenames start with the prefix `catalunya`, you could have done the job with one single
command by using again the wildcard character `*` as follows

```
$ cp /Users/robert/Downloads/catalunya* .
```

Because you have copied the two files, they will stay in their original directory from where you have copied them, e.g., in `/Users/robert/Downloads` in the example above. A slightly different operation is to **move** the files, which means that they are removed from their original location once they are copied into their destination. The command to move the files, instead of copy them, is `mv` with an analogous syntax to `cp`. Try to move the files and check out that they dissapear from their original location.

# Unpacking and uncompressing files

The two files we have copied to our directory called `practical1` should have the following names:

 * `catalunya_setmanal.zip`
 * `catalunya_diari.zip`

The [filename extension](https://en.wikipedia.org/wiki/Filename_extension) `.zip` indicates that these two files contained packaged (possibly more than one file) and compressed (reduced in size) files. To unpackage and uncompress these two files we can use the command `unzip`. A good practise is to make a first call to `unzip` using the option `-l` to list the contents of each file without unpackaging and uncompressing them:

```
unzip -l catalunya_setmanal.zip
unzip -l catalunya_diari.zip
```

**Tip:** when you need to repeat a previous command-line or your next command-line resembles pretty much
a previous one, you can use the up and down arrows to go through the history of all the command-lines that
you have typed before to either repeat it by pressing enter or to modify it. In the previous case, you could
have recover the previous command-line and replace the string `setmanal` by `diari`.

The previous operation allows us to anticipate what files are going to be created by unpackaging and
uncompressing these two `.zip` files. Let's do that now:

```
unzip catalunya_setmanal.zip
unzip catalunya_diari.zip
```

Use the `ls` command to see that you have indeed obtain some new files as a result of the previous command.

# Removing files

There are two commands to remove files. One is `rmdir` and the other is `rm`. Check their respective manual pages and figure out what is the difference between these two commands reading only the `NAME` section. Going back to our COVID19 data files, you should have now four files, the two `.zip` files and two new `.csv` files, corresponding to the unpackaged and uncompressed COVID19 data files. Because we have now the `.csv` files, we do not need anymore the `.zip` files, remove these two `.zip` files by doing:

```
rm *.zip
```

Here we have used the wildcar character `*` to specify that we want to remove all files whose filename
ends with `.zip`. Check out with the command `ls` that they indeed have been removed. **WARNING**: the
Unix system has no bin were removed files could go before being finally removed by emptying the bin. In
the command-line interface of a Unix system, if you accidentally remove a file, **you cannot recover it**.
Because of that, you should pay attention when you use the wildcar character `*`, because an unintended
space character before or after the `*` could imply **removing all files of your PWD**.

At this point, you have typed quite a few Unix commands and have the terminal window full of characters.
Now and then you may want to clear the terminal window. You can do that by either typing the command
`clear` or pressing the keys `Ctrl+l`.

# Exploring file contents

The two COVID19 data files that we have at this point successfully downloaded, copied into a folder and
uncompressed have extension `.csv`. This gives us two important pieces of information about those two
files:

  1. The two files are [_text files_](https://en.wikipedia.org/wiki/Text_file).
  2. The contents of those two files is in [_CSV_](https://en.wikipedia.org/wiki/Comma-separated_values)
     format.

The first point implies that we can inspect the contents of each of the files from the command-line
using any of the following Unix commands

  * `head <filename>`: shows the contents of the beginning of the file.
  * `tail <filename>`: shows the contents of the end of the file.
  * `cat <filename>`: shows the entire contents of the file.
  * `more <filename>`: like `cat` but paginating the output. Use the `Enter` key to scroll line-by-line,
    the `Space` key to scroll by pages and the `q` key to quit.

The second point implies that the contents are organized as a table, where each line contains a
record of the data and each record consists of a given number of values separated by some delimiter
character, typically the comma character `,` but also the semicolon `;`, sometimes the colon `:`, etc.
In a CSV file, the first line may contain column names describing the kind of values stored in the rest
of the lines at the corresponding place.

Finally, a very useful command to summarize the contents of a text file is `wc`, which provides
the number of lines, words and characters in a text file. When multiple files are given, either by
specifying their names one after each other or by using the wildcard character (e.g., `*.csv`),
those statistics are given for each file and also their grand totals. Use the `wc` command on the
CSV COVID19 data files.
