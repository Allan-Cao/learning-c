# Introduction to glibc

## glibc

GNU C Library or glibc provides an interface to make system calls to the linux kernal.

## RTFMan page

man pages provide information on commands in linux.

Open the man page for glibc commands with
```console
man 2 open
```

## errno

errno is a variable that holds the value of an error that is set during a function call. One can check the value (referencing the man page) to determine what specifically occured. One can also use

```c
perror("open");
```

to get the specifics on errors.
