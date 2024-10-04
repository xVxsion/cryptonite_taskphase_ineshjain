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
