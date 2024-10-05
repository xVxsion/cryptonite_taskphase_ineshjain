# Comprehending Commands

## cat : not the pet, but the command

One of the most critical Linux commands is `cat`.
`cat` is most often used for reading out files.
`cat` will concatenate (hence the name) multiple files if provided multiple arguments.
<br>
In this challenge, the flag is stored in the `flag` path in the home directory.
Calling that path, will return the flag.
```
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{UmoVbbL8Hyqsp5xADzgDiuoq1YJ.dFzN1QDLyETO0czW}
```

Note: If you give no arguments at all, cat will read from the terminal input and output it.

## catting absolute paths

Unlike the last challenge, in this one the flag is stored in the absolute path `/flag`.
Calling that path, will return the flag.
```
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{gfkpFMpIgRB0oAjVozjCZ_Lk56k.dlTM5QDLyETO0czW}
```

Fun fact : `/flag` is where the flag always lives in pwn.college, but unlike in this challenge, you typically can't access that file directly.

## More catting practice

In this challenge, we must retrieve the flag by using the absolute path of the directory as an argument to `cat`.
