---
layout: post
title: "[Design] How is Pipe implemented in Unix/Linux "
comments: true
category: Design

---

# Overview

In Unix-like OS, __[a pipeline is a set of processes](https://goo.gl/0NAqd9) chained by their standard streams__, so that the output of each process (stdout) feeds directly as input (stdin) to the next one. 

[Pipes are unidirectional byte streams which connect the standard output](http://stackoverflow.com/a/17503877) from one process into the standard input of another process. __Neither process is aware of this redirection__ and behaves just as it would normally. It is the shell which sets up these temporary pipes between the processes.

# Process

1. Linux has a VFS called __pipefs__ that is mounted in the kernel (not in user space)

    > __[PipeFS](http://www.linux.org/threads/pipefs-sockfs-debugfs-and-securityfs.5383/)__ is a unique virtual filesystem. __This filesystem is mounted inside the kernel__ rather than in the userspace. While most filesystems are mounted under "/", PipeFS is mounted on "pipe:", __making PipeFS its own root__ (yes, a second root filesystem). 
    >
    > This filesystem is one superblock and cannot exceed that amount system-wide. The entry point of this filesystem/second-root is the system-call "pipe()". Unlike the other virtual/pseudo filesystems, this one cannot be viewed.
    >
    > Many of you may be wondering what purpose this PipeFS filesystem serves. Unix pipes use this filesystem. When a pipe is used (eg. ls | less), __the pipe() system-call makes a new pipe object on this filesystem__. Without this filesystem, pipes cannot be made. 
    >
    > Also, threads and forks communicate together via pipes. Without PipeFS, processes could not fork and threads could not communicate. 
    >
    > Network pipes also rely on this virtual/pseudo filesystem.

1. pipefs has a single super block and is mounted at it's own root (pipe:), alongside /

1. pipefs cannot be viewed directly unlike most file systems

1. The entry to pipefs is via the pipe(2) syscall

1. The pipe(2) syscall used by shells for piping with the | operator (or manually from any other process) creates a new file in pipefs which behaves pretty much like a normal file

1. The file on the left hand side of the pipe operator has its stdout redirected to the temporary file created in pipefs

1. The file on the right hand side of the pipe operator has its stdin set to the file on pipefs

1. pipefs is stored in memory and through some kernel magic

Ref: http://unix.stackexchange.com/q/148401
