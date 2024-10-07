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
```
You cannot use the 'cd' command in this level, and must retrieve the flag by
absolute path. Plus, I hid the flag in a different directory! You can find it
in the file /usr/include/asm-generic/flag. Go cat it out **without** cding into
that directory!
hacker@commands~more-catting-practice:~$ cat  /usr/include/asm-generic/flag
pwn.college{QezrZjY53d_Ph0GlwXeuHx-ZMxL.dBjM5QDLyETO0czW}
```
Things we learnt : You can specify all sorts of paths as arguments to commands.

## Grepping for a needle in a haystack

Sometimes, the files that you might cat out are too big.
The grep command to search for the contents we need.
<br>
Syntax : `hacker@dojo:~$ grep SEARCH_STRING /path/to/file`
<br>
Invoked like this, grep will search the file for lines of text containing SEARCH_STRING and print them to the console.

```
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{0YU-DU8Bkb9gwlTmxGDEYQQna-2.ddTM4QDLyETO0czW}
```

In this challenge, we use the `grep` command to search for the flag in the hundreds of lines of text.
Hint : The flag always contains the string `pwn.college`.

## Listing files

`ls` will list files in all the directories provided to it as arguments, and in the current directory if no arguments are provided.
In this challenge we need to access the path of the directory by running the path containing the flag after finding it in the listed files under the `/challenge` directory.

