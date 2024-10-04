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


```
hacker@paths~position-thy-self:~$ /challenge/run
Incorrect...
You are not currently in the /etc/apt/sources.list.d directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-thy-self:~$ cd /etc/apt/sources.list.d
hacker@paths~position-thy-self:/etc/apt/sources.list.d$ /usr/bin$
ssh-entrypoint: /usr/bin$: No such file or directory
hacker@paths~position-thy-self:/etc/apt/sources.list.d$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{cE_0rxQApNh1sjVxs6ZlEVeKbGH.dZDN1QDLyETO0czW}
hacker@paths~position-thy-self:/etc/apt/sources.list.d$
```

Things we learnt :
1. The symbol `~` shows the current your shell is located in.
2. A function doesn't run and returns an incorrect value if its in the wrong directory.


## Position elsewhere

This challenge is supposed to serve as a practice for `Position thy self` again.
We switch directories and run the absolute path to get the flag.
```
hacker@paths~position-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /home directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-elsewhere:~$ cd /home
hacker@paths~position-elsewhere:/home$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{sTCxg9rDF6qtRaRKrAp7M6OBkgv.ddDN1QDLyETO0czW}
```



## Position yet elsewhere

This challenge is supposed to serve as a practice for `Position thy self` again.
We switch directories and run the absolute path to get the flag.
```
hacker@paths~position-yet-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /sys/kernel directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-yet-elsewhere:~$ cd /sys/kernel
hacker@paths~position-yet-elsewhere:/sys/kernel$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{snXK0bNwlHzOKEykPNwyKm3PWsO.dhDN1QDLyETO0czW}
```


## Implicit relative paths, from /

Things we learnt :
1. If you put in absolute paths everywhere, then it really doesn't matter what directory you are in.
2. The current working directory does matter for relative paths.
3. A relative path is any path that does not start at root (i.e., it does not start with `/`).
4. A relative path is interpreted relative to your current working directory (`cwd`).
5. Your `cwd` is the directory that your prompt is currently located at.
(This means how you specify a particular file, depends on where the terminal prompt is located)
6. Imagine we want to access some file located at `/tmp/a/b/my_file`.
      - If my cwd is `/`, then a relative path to the file is `tmp/a/b/my_file`.
      - If my cwd is `/tmp`, then a relative path to the file is `a/b/my_file`.
      - If my cwd is `/tmp/a/b/c`, then a relative path to the file is `../my_file`. The `..` refers to the parent directory.

```
hacker@paths~implicit-relative-paths-from-:~$ /challenge/run
Incorrect...
You are not currently in the / directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~implicit-relative-paths-from-:~$ cd /
hacker@paths~implicit-relative-paths-from-:/$ challenge/run
Correct!!!
challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{kjlPoMWxkpjLg6MvdMQE6SPJ4ZH.dlDN1QDLyETO0czW}
```

In this challenge you run the run command in the mentioned directory. 
The catch is to use the relative path of the directory.

## Explicit relative paths, from /

In most operating systems, including Linux, every directory has two implicit entries that you can reference in paths: `.` and `..`.
The first, `.`, refers right to the same directory, so the following absolute paths are all identical to each other:
- /challenge
- /challenge/.
- /challenge/./././././././././
- /./././challenge/././

The following relative paths are also all identical to each other:
- challenge
- ./challenge
- ./././challenge
- challenge/.

Things we learnt : If your current working directory is `/`, the above relative paths are equivalent to the above absolute paths.

```
hacker@paths~explicit-relative-paths-from-:~$ /challenge/run
Incorrect...
You are not currently in the / directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~explicit-relative-paths-from-:~$ cd /
hacker@paths~explicit-relative-paths-from-:/$ ./challenge/run
Correct!!!
./challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{4XDCHIXhsoeg18pf7dOmZXVvD7Q.dBTN1QDLyETO0czW}
```

In this challenge you run the run command in the mentioned directory. 
The catch is to use the relative path of the directory. (invoked explicitly)


## Implicit relative path

Important note :
```
hacker@dojo:~$ cd /challenge
hacker@dojo:/challenge$ run
```
This will not invoke /challenge/run.
This is actually a safety measure. I
f Linux searched the current directory for programs every time you entered a naked path, 
you could accidentally execute programs in your current directory that happened to have the same names as core system utilities!
As a result, the above commands will yield an error.

```
hacker@paths~implicit-relative-path:~$ cd /challenge
hacker@paths~implicit-relative-path:/challenge$ ./run
Correct!!!
./run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{o4CADANv9oMr7j9xkHqjfAy9Eb3.dFTN1QDLyETO0czW}
```

## Home Sweet Home

Every user has a home directory, typically under /home in the filesystem.
In the dojo, you are the hacker user, and your home directory is /home/hacker.
<br>
Note that the expansion of ~ is an absolute path, and only the leading ~ is expanded.
This means, for example, that ~/~ will be expanded to /home/hacker/~ rather than /home/hacker/home/hacker.
<br>

In this challenge, /challenge/run will write a copy of the flag to any file you specify as an argument on the commandline, with these constraints:
- Your argument must be an absolute path.
- The path must be inside your home directory.
- Before expansion, your argument must be three characters or less.

```
hacker@paths~home-sweet-home:~$  /challenge/run ~/~
Writing the file to /home/hacker/~!
... and reading it back to you:
pwn.college{4visOrjAto1Fti-Hd4hWhTbBTg8.dNzM4QDLyETO0czW}
```

