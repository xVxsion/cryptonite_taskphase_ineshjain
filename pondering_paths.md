# Pondering Paths

## The Root

The root of the filesystem is a directory, and every directory can contain other directories and files.
You refer to files and directories by their path.
A path from the root of the filesystem starts with / (that is, the root of the filesystem), and describes the set of directories that must be descended into to find the file.
Every piece of the path is demarcated with another /.

<br>

Alright, so the filesystem starts at /.
Under that, there are a whole mess of other directories, configuration files, programs, and, most importantly, flags.

```
hacker@paths~the-root:~$ /pwn
BOOM!!!
Here is your flag:
pwn.college{AT6Es9belcTlD6kPeZypSko6TU0.dhzN5QDLyETO0czW}
```

In this challenge, we just have to invoke `/pwn` function which returns the flag value stored at that path directory.

## Program and absolute paths

As we proceed the paths inside the root directories get more complex.
In the challenge we access a complex path `/challenge/run`, and it returns the flag.
```
hacker@paths~program-and-absolute-paths:~$ /challenge/run
Correct!!!
/challenge/run is an absolute path! Here is your flag:
pwn.college{oToSsSdEp0GoXXeBszzBuzeOadt.dVDN1QDLyETO0czW}
```

## Position thy self

The Linux filesystem has tons of directories with tons of files.
You can navigate around directories by using the `cd` (change directory) command and passing a path to it as an argument.
This affects the "current working directory" of your process (in this case, the bash shell).
Each process has a directory in which it's currently hanging out.

<br>

In this challenge, we need to change directories to the one they specify in the running prompts.
Navigate to it, in this case `/usr/bin` and run the `/challenge/run` function.


