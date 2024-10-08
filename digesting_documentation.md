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

