# Digesting Documentations

## Learning from Documentation

Things we learnt : The correct usage of programs depends, in a large part, in the proper specification of arguments to them.
<br>
Recall the `-a` of `ls`; `-a` in the hidden files challenge of the Basic Commands module: that `-a` was an argument that told `ls` to list out hidden files as well as non-hidden files.
Because we wanted to list out hidden files, invoking `ls` with the `-a` argument was the correct way to use it in our scenario.

```
hacker@man~learning-from-documentation:~$ /challenge/challenge --giveflag
Correct argument! Here is your flag:
pwn.college{gBos6kOky3tZywodCGXuUe-TbxR.dRjM5QDLyETO0czW}
```

In this challenge, we need to `/challenge/challenge` with the argument `--giveflag` to retrieve the flag.

## Learning Complex Usage

Remember : `find` has a `-name` argument, 
and the `-name` argument itself takes an argument specifying the name to search for.
<br>
Many other commands are analogous.

```
hacker@man~learning-complex-usage:~$ /challenge/challenge --printfile not-the-flag
Correct argument! Here is the not-the-flag file:
pwn.college{w15YAvuXb-kz-Z1v3AdC5X8TMpd.dVjM5QDLyETO0czW}
```

In this challenge, we need to pass the filename `not-the-flag` as an argument to the `--printfile`, 
which in turn is the argument to the directory path `/challenge/challenge`.

## Reading Manuals

The man command : `man` is short for manual, 
and will display (if available) the manual of the command you pass as an argument.
For example, let's say we wanted to learn about the `yes` command (yes, this is a real command):
<br>
`hacker@dojo:~$ man yes`
<br>
You can scroll around the manpage with your arrow keys and PgUp/PgDn.
When you're done reading the manpage, you can hit `q` to quit.
```
hacker@man~reading-manuals:~$ man challenge

CHALLENGE(1)                                                       Challenge Commands                                                       CHALLENGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --wlxkqv NUM
              print the flag if NUM is 483

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The repository for this dojo: <https://github.com/pwncollege/linux-luminarium/>

SEE ALSO
       man(1) bash-builtins(7)

pwn.college                                                             May 2024                                                            CHALLENGE(1
hacker@man~reading-manuals:~$  /challenge/challenge --wlxkqv 483
Correct usage! Your flag: pwn.college{wlxkqVv4H_jGbnW83SCj8XcsQlg.dRTM4QDLyETO0czW}
```
In this challenge, we needed to call the manual for the challenge command.
Read through the manual and find the command clue.
Run the command with the correct argument, and retrieve the flag.

## Searching Manuals

You can scroll man pages with the arrow keys (and PgUp/PgDn) and search with `/`.
After searching, you can hit `n` to go to the next result and `N` to go to the previous result.
Instead of `/`, you can use `?` to search backwards!

```
hacker@man~searching-manuals:~$ man challenge
hacker@man~searching-manuals:~$ /challenge/challenge  --isalcun
Initializing...
Correct usage! Your flag: pwn.college{I7LWf3ahpSxnkcEleDCyjzad5F-.dVTM4QDLyETO0czW}
```

In this challenge, we had to search through the `challenge` command manual.
To search for the flag type in `/flag` and go through the results, 
using the `n` until you find the valid argument. 
(in this case `--txak`) 
Run the command with the argument and retrieve the flag.

## Searching for Manuals

HINT 1: `man man` teaches you advanced usage of the man command itself, and you must use this knowledge to figure out how to search for the hidden manpage that will tell you how to use `/challenge/challenge`
<br>
HINT 2: Though the man page is randomly named, you still actually use /challenge/challenge to get the flag!
<br>
In this challenge, we call the `man man` function which returns the manual for `man`.
In this manual we search for a command which can lead us to the `challenge` manual.
We find the use of `-k` which states : 
```
hacker@man~searching-for-manuals:~$ man -k challenge
wwqlxxroom (1)       - print the flag!
hacker@man~searching-for-manuals:~$ man wwqlxxroom

CHALLENGE(1)                                      Challenge Commands                                     CHALLENGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --wwqlxx NUM
              print the flag if NUM is 811

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The repository for this dojo: <https://github.com/pwncollege/linux-luminarium/>

SEE ALSO
       man(1) bash-builtins(7)

pwn.college                                            May 2024                                          CHALLENGE(1)
hacker@man~searching-for-manuals:~$ /challenge/challenge --wwqlxx 811
Correct usage! Your flag: pwn.college{wwXN8E11qCl_5x5xr4V0_oV1Iom.dZTM4QDLyETO0czW}
```
The manual gives the correct argument to run `/challenge/challenge`.

## Helpful Programs

Some programs don't have a manual page, but might tell you how to run them if invoked with a special argument.
Usually, this argument is `--help`, but it can often be `-h` or, in rare cases, `-?`, `help`,
or other esoteric values like `/?` (though that latter is more frequently encountered on Windows).

```
hacker@man~helpful-programs:~$ /challenge/challenge --help
usage: a challenge to make you ask for help [-h] [--fortune] [-v] [-g GIVE_THE_FLAG] [-p]

optional arguments:
  -h, --help            show this help message and exit
  --fortune             read your fortune
  -v, --version         get the version number
  -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                        get the flag, if given the correct value
  -p, --print-value     print the value that will cause the -g option to give you the flag
hacker@man~helpful-programs:~$ /challenge/challenge -p
The secret value is: 854
hacker@man~helpful-programs:~$ /challenge/challenge -g 854
Correct usage! Your flag: pwn.college{YtKbtZ_BdZUvI__y85kqeRBIbya.ddjM4QDLyETO0czW}
```

In this challenge, we need to call the `--help` argument on the challenge function.
Follow the leads to retrieve the flag.

## Help for Builtins

Some commands, rather than being programs with man pages and help options, are built into the shell itself.
These are called builtins.
Builtins are invoked just like commands, but the shell handles them internally instead of launching other programs.
You can get a list of shell builtins by running the builtin `help`.
```
hacker@man~help-for-builtins:~$ help challenge
challenge: challenge [--fortune] [--version] [--secret SECRET]
    This builtin command will read you the flag, given the right arguments!

    Options:
      --fortune         display a fortune
      --version         display the version
      --secret VALUE    prints the flag, if VALUE is correct

    You must be sure to provide the right value to --secret. That value
    is "gHHjyS7b".
hacker@man~help-for-builtins:~$ challenge --secret gHHjyS7b
Correct! Here is your flag!
pwn.college{gHHjyS7b_eGv6dLU0vmEYD-sH0a.dRTM5QDLyETO0czW}
```
In this challenge, we call the `help` function for the built-in `challenge` function.
This gives us the arguments to pass to the function to retrieve the flags.
