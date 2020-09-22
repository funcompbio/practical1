---
layout: page
title: Practical 1
permalink: /practical1/
---

# Setup and background

In this practical we will use some basic commands to navigate and manipulate the Unix file system. You
need to have access to the command-line of your operating system. Please check the
[setup](https://funcompbio.github.io/setup) webpage to make sure that you have access to some flavor of
an Unix operating system and its command line.

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
typing the commands `whoami` (first) and `pwd` (second) on the shell prompt. After you type each command
you should press the `Enter` key to ask the shell to execute the command. Your interaction with the shell
in the terminal window should look similar to the following image.

![](./terminaldefault.png)

The shell prompt may display different information to the left of the cursor and usually ends with the
dollar sign. The solely purpose of the shell prompt is to indicate where we can start typing commands,
while the purpose of the cursor is to indicate that the shell is waiting for us to type commands.
In the image above the shell prompt it is displaying the name of the host computer (`messi`) and the
the current PWD, which corresponds to our _home_ directory and for this reason is abbreviated
with the tilde `~`.

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

and you should see a trailing slash character '/' right after the name of each file that is a
directory, i.e., you should find for instance 'practical1/'. Next, let's change our default PWD to the
new directory we have created.

```
$ cd practical1
```

To check whether we have successfully changed the PWD to the new directory, use again the command `pwd`.

# Copying and moving files

Locate the path where you have downloaded the two COVID19 data files and copy them to your current brand
new directory using the command `cp`. **For instance**, if one of the files **were** located at

```
/Users/robert/Downloads/catalunya_setmanal.zip
```

then the command to copy that file to the current PWD **would be**

```
cp /Users/robert/Downloads/catalunya_setmanal.zip .
```

**Tip:** when writing long paths it is useful to exploit the so-called _tab-completion mechanism_, which consists of pressing the `TAB` key (typically located above the `Caps Lock` key) once you've written a few letter of a file name in the path. If those few letters constitute a unique prefix of the filename, the rest of the filename will be written for you by the shell. If the prefix is not unique, by pressing the `TAB` key twice, the shell will show your the two or more filenames that match that prefix.

Note that because `/Users/robert` corresponds in this example to the _home_ directory of the user, we
could use the abbreviation `~`, corresponding to the _home_ directory, to write the previous command line as

```
cp ~/Downloads/catalunya_setmanal.zip .
```

Note that the previous command will work regardless of what is your username, as long as the sought file
is stored in the `Downloads` directory. **Tip:** In keyboards with a Spanish layout, the tilde `~` character can be written by pressing the keys
`AltGr+4`.

Once you have copied the two files, please verify using the command `ls` that the two files are indeed
in your current PWD. If you have been successfull, you have probably typed twice the `cp` command. However,
because the two filenames start with the prefix `catalunya`, you could have done the job with one single
command by using the _wildcard_ character `*` as follows

```
$ cp /Users/robert/Downloads/catalunya* .
```
