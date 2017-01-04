# How Linux Works:

## What Every Superuser Should Know

### by Brian Ward

Ward, Brian. *How Linux Works: What Every Superuser Should Know.* San Francisco: No Starch Press, 2015. Print.

***

## Chapter 2 - "Basic Commands and Directory Hierarchy"

#### p.11

The majority of commands listed in this chapter are *Unix* commands rather than Linux-specific commands.

###### Beginning Unix books:

* *The Linux Command Line* \(No Starch Press, 2012\)
* *Unix for the Impatient* \(Addison-Wesley Professional, 1995\)
* *Learning the Unix Operating System, 5th Edition* \(O'Reilly, 2001\)

#### 2.1 The Bourne Shell: /bin/sh, p.12

A *shell* is a program that runs commands, like the ones that users enter, and also serves as a small programming environment.

*Shell scripts* actually comprise many important parts of the system and are text files that contain a sequence of shell commands.

There are many different Unix shells, but they all derive from the *Bourne shell* \(/bin/sh\) - a standard shell developed at Bell Labs for early versions of Unix.

Linux uses, as a default in most distros, a shell called *bash*, which stands for "Bourne-again shell".

`chsh` is a command used to change the shell used.

#### 2.2 Using the Shell, p.12

##### 2.2.1 The Shell Window, p.12

A shell window is also known as the *terminal*.

'$' denotes a shell command run as a user, '#' denotes a shell command run as the superuser.

##### 2.2.2 *cat*, p.13

`cat` outputs the contents of one or more files.

```bash
$ cat <file1> <file2> ...
```

`cat` prints the contents of `<file1>` `<file2>` and any other files specified - it is known as *cat* because it concatenates the contents of the files if more than one is specified.

##### 2.2.3 Standard Input and Standard Output, p.13

Unix processes use I/O *streams* to read and write data.

The source of an input stream can be a file, a device, a terminal, or an output stream from another process.

`CTRL-D` stops the current standard input entry from the terminal \(and often terminates a program\).

`CTRL-C` terminates a program regardless of its input or output.

*Standard input* is an input stream provided by the Linux kernel rather than a stream connected to a file.

*Standard output*, similarly, is an output stream provided by the kernel.

*stdin* and *stdout* are common abbreviations for standard in and out.

There is a third standard I/O stream called *standard error*

#### 2.3 Basic Commands, p.14

`ls` lists the contents of a directory, the current directory being the default.

`cp` copies files

`mv` renames or moves a file

`touch` creates a file - if the file already exists it is not changed, except for its timestamp.

`rm` deletes a file - generally those deleted files can not be recovered.

`echo` prints its arguments to the standard output.

#### 2.4 Navigating Directories, p.16

The Unix director hierarchy starts at /, also known as the *root directory*.

A *full* or *absolute* path is one that starts at the root, /.

A path component identified by two dots \(..\) specifies the parent of a directory.

A path component identified by one dot \(.\) refers to the current directory.

A path that does not begin with the root directory, /, is called a *relative path*.

`cd` changes the shell's *current working directory*. With no specified directory, `cd` returns to the *home directory*, or the directory the user is in upon login.

`mkdir` creates a new directory.

`rmdir` removes a directory. It will not work on a directory that contains anything, unless the flags -rf are specified, which will force the deletion of the directory and all its contents.

##### 2.4.4 Shell Globbing \(Wildcards\), p.17

The glob character '\*' tells the shell to match any number of arbitrary characters.

* `at*` expands to all filenames that start with `at`
* `*at` expands to all filenames that end with `at`
* `*at*` expands to all filename that contain `at`

The '?' instructs the shell to match exactly *one* arbitrary character. \(`b?at` matches `boat` and `brat`\)

One of these symbols enclosed in single quotes is not expanded.

#### 2.5 Intermediate Commands, p.18

##### 2.5.1 *grep*, p.18

`grep` prints the lines from a file or input stream that match an expression

`grep` is useful for operating on multiple files at once because it prints the filename in addition to the matching line.

`grep` understands *regular expressions* or *regex* which provide more powerful and flexible searching ability than globs.

Two important `grep` options are `-i` for case-insensitive matches and `-v` for search inversion.

Regex `.*` is equal to the shell `*` character, and `.` is equal to the shell `?` character.

Learning more about the `grep` command:

* The grep\(1\) manual page.
* *Mastering Regular Expressions, 3rd Edition* \(O'Reilly, 2006\)
* *Programming Perl, 4th Edition* \(O'Reilly, 2012\) - Regular Expressions Chapter
* *Introduction to Automata Theory, Languages, and Computation, 3rd Edition* \(Prentice Hall, 2006\)

##### 2.5.2 *less*, p.19

`less` displays the contents of its input one screen at a time - piped into `|`

The `less` command is an enhanced version of an older program named `more`, `less` may not exist on older or embedded Unix systems.

text is also searchable within `less` - `/word` searches forward and `?word` searches backward, `n` continues the search.

##### 2.5.3 *pwd*, p.19

`pwd` outputs the name of the current working directory \(*print working directory*\).

##### 2.5.4 *diff*, p.20

`diff` shows the differences between two files

```bash
$ diff <file1> <file2>
```

`diff -u` outputs in a way that may be useful for automated tools.

##### 2.5.5 *file*, p.20

The `file` command outputs what the system thinks a file's type is.

##### 2.5.6 *find* and *locate*, p.20

`find` searches a directory for a particular file

```bash
$ find <dir> -name <file> -print
```

`find` accepts special pattern-matching characters such as '*', but they need to be enclosed in single quotes so the shell's pattern-matching doesn't interfere.

`locate` also searches for files, but searches an index instead of the system. Faster, but useless if the file being searched for is newer.

##### 2.5.7 *head* and *tail*, p.21

`head` shows a portion of the beginning of a file.

`tail` shows a portion of the end of a file.

10 lines by default, can be changed with the `-n` or `+n` option for `head` and `tail` respectively, `n` = number of lines

##### 2.5.8 *sort*, p.21

`sort` puts the lines of a text file in alphanumeric order. If a files lines start with numbers and you want to sort in numerical order, use the `-n` option. The `-r` option reverses the order of the sort.

#### 2.6 Changing Your Password and Shell

The `passwd` command changes passwords

`chsh` will change the shell for the duration of that terminal's life

#### 2.7 Dot Files, p.21

`ls -a` will show *dot files* in addition to whatever else is in the directory.

Dot files are not shown by default by many programs and will not be globbed unless searched by `.*`

There is nothing inherently different about dot files or directories, other than their tendency to hide.

#### 2.8 Environment and Shell Variables, p.21

*Shell variables* are temporary values stored by an instance of the shell and can be assigned by the equal operator. `VAR=blah`

The value can then be accessed with `$VAR`

*Environment variables* are similar to shell variables, but have a greater scope in the system - environment variables can be passed into programs that the shell runs, while shell variables can not.

`export VAR` will push the shell variable to the environment.

Many programs read environment variables for configuration and options.

#### 2.9 The Command Path, p.22

`PATH` is a special environment variable that contains the *command path*, which is a list of system directories that the shell searches when trying to locate a command.

Directories can be added to the PATH easily

```bash
$ PATH=<dir>:$PATH
$ PATH=$PATH:<dir>
```

These codes will append a directory to the beginning or the end of a PATH, respectively.

A config file must be modified to change the PATH permanently. 

#### 2.10 Special Characters, p.23

[Jargon File](http://www.catb.org/jargon/html/)

*The New Hacker's Dictionary* \(MIT Press, 1996\)

**Table 2-1:** Special Characters, p.23

**Character** | **Name\(s\)** | **Uses**
--- | --- | ---
\* | asterisk, star | Regular expression, glob character
\. | dot | Current directory, file/hostname delimiter
\! | bang | Negation, command history
\| | pipe | Command pipes 
/ | \(forward\) slash | Directory delimiter, search command
\\ | backslash | Literals, macros \(*never* directories\)
$ | dollar | Variable denotation, end of line
' | tick, \(single\) quote | Literal strings
\` | backtick, backquote | Command substitution
" | double quote | Semi-literal strings
^ | caret | Negation, beginning of line
~ | tilde, squiggle | Negation, directory shortcut
\# | hash, sharp, pound | Comments, preprocessor, substitutions
\[ \] | \(square\) brackets | Ranges
\{ \} | braces, \(curly\) brackets | Statement blocks, ranges
\_ | underscore, under | Cheap substitute for a space

Control characters are often marked with a caret - ex. \^C for `CTRL-C`

#### 2.11 Command-Line Editing, p.24

Forget about the arrow keys\!

**Table 2-2:** Command-Line Keystrokes

**Keystroke** | **Action**
--- | ---
`CTRL-B` | Move the cursor left
`CTRL-F` | Move the cursor right
`CTRL-P` | View the previous command \(or move the cursor up\)
`CTRL-N` | View the next command \(or move the cursor down\)
`CTRL-A` | Move the cursor to the beginning of the line
`CTRL-E` | Move the cursor to the end of the line
`CTRL-W` | Erase the preceding word
`CTRL-U` | Erase from cursor to beginning of line
`CTRL-K` | Erase from cursor to end of line
`CTRL-Y` | Paste erased text \(for example from `CTRL-U`\)

#### 2.12 Text Editors, p.24

Vi and Emacs are the two de facto standard Unix editors.

Emacs can do almost anything and has extensive online help, but involves some extra typing.

Vi is fast as fast gets and 'plays' somewhat like a video game.

*Learing the vi and Vim Editors: Unix Text Processing, 7th Edition* \(O'Reilly, 2008\)

*GNU Emacs Manual* \(Free Software Foundation, 2011\)

Vi runs in a terminal window, Emacs runs in a GUI by default, but can also be run in the terminal.

#### 2.13 Getting Online Help, p.25

*manual pages* or *man pages* offer documentation and help for basic commands.

`man <command>` brings up the man page for `<command>`, if it exists.

`man -k <keyword>` searches the man pages by keyword, if the command is not known.

Manual pages are referenced by numbered sections.

**Table 2-3:** Online Manual Sections, p.26

**Section** | **Description**
--- | ---
1 | User commands
2 | System calls
3 | Higher-level Unix programming library documentation
4 | Device interface and driver information
5 | File descriptions \(system configuration files\)
6 | Games
7 | File formats, conventions, and encodings \(ASCII, suffixes, and so on\)
8 | System commands and servers

Manual pages can be selected by section.

`<command>` plus `--help` or `-h` often brings up information

The GNU Project switched from man pages to *info* or *textinfo*, which often contains more information than the man pages do.

`info <command>` will bring up an info page.

#### 2.14 Shell Input and Output, p.27

`<command> > <file>` sends the output of `<command>` to `<file>` instead of the terminal.

The shell will create `<file>` if it doesn't already exist and will erase \(*clobber*\) the file if it does.

`-C`  will prevent clobbering in bash.

`<command> >> <file>` will append output instead of overwriting.

`|` sends the standard output of one command to the standard input of another command.

`2>` will redirect the standard error, the number 2 identifying the *streamID* that the `>` is directed to affect.

The `<` character will channel a file to a program's standard input. This syntax is uncommon because most Unix commands accept filenames as arguments.

#### 2.15 Understanding Error Messages, p.28

Unix errors usually tell you exactly what went wrong.

The general anatomy of a Unix error message is `<program name> - <file name> - <error message>`

Always address the first error first, often the first is the root cause of the following errors.

Warnings \!= errors - warnings will not prevent a program from running, necessarily.

##### 2.15.2 Common Errors, p.29

`No such file or directory` - Caused when trying to access a file or directory that does not exist.

`File exists` - Caused by trying to create a file or directory that already exists.

`Not a directory` or `Is a directory` - Caused by trying to use a file or directory incorrectly.

`No space left on device` - No more disk space.

`Permission denied` - Caused by trying to read or write to a file without sufficient permissions.

`Operation not permitted` - Usually caused by trying to kill a process that you do not own.

`Segmentation fault` or `Bus error` - Caused by a program incorrectly accessing system memory. Can be caused by programming mistakes or by passing incorrect arguments to a program.

#### 2.16 Listing and Manipulating Processes, p.30

Each process on a system has a numeric *process ID* \(PID\).

`ps` will show a list of running processes

The fields shown by `ps` are as follows:  

Field | Explanation
--- | ---
**PID** | The process ID
**TTY** | The terminal device where the process is running.
**STAT** | The process status, i.e. what the process is doing and where its memory resides.
**TIME** | The amount of CPU time in minutes and seconds that the process has used so far.
**COMMAND** | The name of the process, can be changed from its original value by a process.

Some `ps` options in the BSD style:

* `ps x` shows all running processes you own
* `ps ax` shows all running processes on the system
* `ps u` shows more detailed information on the processes
* `ps w` shows full command names, not just what fits on a line

##### 2.16.2 Killing Processes, p.31

To terminate a process, send it a signal with the kill command.

`kill <pid>` is the command to kill a process, which sends a request to the kernel for it to signal another process.

The default kill signal is `TERM` or terminate. A process can also be frozen with `kill -STOP <pid>`

`kill -KILL <pid>` will end a process indiscriminately, without allowing the process to clean itself up, save, etc.

shells also support *job control*, which allows the user to pause and restart processes, but its use is not recommended by the author.

Adding a `&` to a shel command instructs the shell to run the process in the background, allowing other commands to be entered, as in `gunzip <file.gz> &`

Using the `&` modifier to create background processes in this way may cause problems with *stdin* and/or *stdout*, however.

#### 2.17 File Modes and Permissions, p.33

Every Unix file has a set of *permissions* that determine whether you can read, write, or run the file.

![Linux File Permissions](http://linuxcommand.org/images/permissions_diagram.gif)

The first bit of a file's permissions indicate what kind of file it is: `d` for directory, `-` for a *regular* file.

The next three sets of three indicate the file's *user*, *group*, and *other* permissions, respectively.

##### 2.17.1 Modifying Permissions, p.34

`chmod` can be used to change permissions on a file.

`$ chmod g+r <file>` - `$ chmod o+r <file>` add read permissions to *group* and *other* or *world*, respectively.

`$ chmod go+r <file>` combines the above into one command.

Permissions can also be changed absolutely with numerals represented in octal form.

`$ chmod 644 <file>` sets *user* to read/write and *group* and *other* to read, for example.

![File Permissions Numerically](http://2.bp.blogspot.com/-V2eWUJugBJ0/Ui4Y1TJ45aI/AAAAAAAAAzQ/gwxcb-GlTGA/s1600/chmod4.png)

**Table 2-4:** Absolute Permission Modes  

**Mode** | **Meaning** | **Used For**
--- | --- | ---
644 | user: read/write; group, other: read | files
600 | user: read/write; group, other: none | files
755 | user: read/write/execute; group, other: read/execute | directories, programs
700 | user: read/write/execute; group, other: none | directories, programs
711 | user: read/write/execute; group, other: execute | directories
 
Directories also have permissions.

`umask` is a shell command that can apply default permission levels.

##### 2.17.2 Symbolic Links, p.35

A *symbolic link* is a file that points to another file or a directory, effectively creating an alias - similar to a shortcut in Windows.

`lrwxrwxrwx 1 ruser users 11 Feb 27 13:52 somedir -> /home/origdir` is an example of how a symbolic link might look in a directory listing.

There can also be symbolic links that linked to other symbolic links, known as *chained symbolic links*

`$ ln -s <target> <linkname>` will create a symbolic link `<linkname>` pointing to `<target>` the `-s` flag denotes a symbolic link.

Without the `-s` flag `ln` will create a *hard link*, which gives another real filename to a single file which has the same status as the old filename.

#### 2.18 Archiving and Compressing FIles, p.37

`gzip` is a program that will compress to `.gz` files.

`gunzip` is a program that will uncompress `.gz` files.

`gzip` will not crate an archive \(place multiple files together into one compressed file\), `tar` is the standard Unix program for archiving.

`$ tar cvf <archive>.tar <file1> <file2>` puts files/directories 1 & 2 into an archive.tar.

Tar's `c` flag activates *create mode*, the `v` flag activates verbose diagnostic output, the `f` flag activates the file option which tells tar the file it's creating.

`$ tar xvf <archive>.tar` unpacks an archive.tar file. the `x` flag denotes extract mode.

`$ tar tvf <archive>.tar` verifies an archive.tar's integrity and prints the names of all files inside, the `t` flag denotes *table-of-contents* mode.

Tar's `p` flag is used to preserve the permissions of the files archived, rather than imposing default permissions used by the system.

Tar's `z` flag invokes `zcat`, which will uncompress a .tar.gz file before unpacking it.

`.tgz` is another form of `.tar.gz`

Other compression utilities common to Unix/Linux include `bzip2`/`bunzip2`/`.bz2` or `xz`/`unxz`/`.xz`

#### Linux Directory Hierarchy Essentials, p.40

![Linux Directory Hierarchy](http://linuxforums.org.uk/MGalleryItem.php?id=1541)

[Filesystem Hierarchy Standard](http://www.pathname.com/fhs/)

`/bin` contains ready-to-run programs, including most of the basic Unix commands.

`/dev` contains device files.

`/etc` core system configuration directory, contains user password, boot, device, networking, and other setup files.

`/home` holds personal directories for regular users.

`/lib` abbreviation for library. holds library files containing code tha executables can use.

`/proc` provides system statistics through a browsable directory-and-file interface.

`/sys` similar to `/proc` in that it provides a device and system interface.

`/sbin` the place for system executables. Programs in `/sbin` directories relate to system management.

`/tmp` a storage area for smaller, temporary files. `/tmp` is usually cleared regularly as part of regular system activity.

`/usr` does not contain user files! Contains a similar directory hierarchy to the root hierarchy and has similar files and directory divisions. A historic anomoly.

`/var` the variable subdirectory where programs record runtime information. System logging, user tracking, caches, and other files that system programs create and manage are here.

##### 2.19.1 Other Root Subdirectories, p.41

`/boot` contains kernel boot loader files. The files here pertain only to the very first stage of the Linux startup procedure.

`/media` is a base attachment point for removable media such as flash drives, found in many distros.

`/opt` may contain additional third-party software, many systems do not use `/opt`.

##### 2.19.2 The */usr* Directory, p.41

`/usr` is where most of the user-space programs and data reside.

In addition to `/usr/bin`, `/user/sbin`, and `/usr/lib`, `/usr` contains the following:  

* `/include` - holds header files used by the C compiler.
* `/info` - contains GNU info manuals.
* `/local` - where administrators can install their own software - structure similar to `/` and `/usr`.
* `/man` - contains manual pages.
* `/share` - contains files that should work on other kinds of Unix machines with no loss of functionality. Because there are no longer space issues on modern systems, `/share` directories are becoming rare.

##### 2.19.3 Kernel Location, p.42

On Linux systems, the kernel is normally in `/vmlinuz` or `/boot/vmlinuz`

Once the boot loader runs and sets the kernel in motion, the main kernel file is no longer used by the running system.

*Loadable kernel modules*, located in `/lib/modules`, are modules that the kernel can load and unload on demand during the course of normal system operation.

#### 2.20 Running Commands as the Superuser, p.42

Disadvantages of `su`:

* No record of system-altering commands.
* No record of the users who performed system-altering commands.
* No access to your normal shell environment.
* Root password required.

##### 2.20.1 *sudo*, p.42

Most larger distros use a package called `sudo` to allow administrators run commands as root when they are logged in as themselves.

The users allowed to use the `sudo` command are described in the `/ec/sudoers` file.

`sudo` has many options, which makes the syntax in the `/etc/sudoers` file complicated.

When editing the `/etc/sudoers` file use the `visudo` command, as it checks for file syntax errors after the file is saved.