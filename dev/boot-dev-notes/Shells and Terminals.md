---
title: Learn Shells and Terminals
tags:
  - boot-dev
  - basic-programming
  - shell-utilities
date: 2/1/25
---
### CLI:
- You'll often hear the terms "terminal", "shell", "command line", "CLI", and "command prompt" used interchangeably, but often they all refer to the same thing: a program that allows you to interact with your computer in a text-based way.
### What's a GUI?

If you don't have a technical background, you're probably used to interacting with your phone or computer using a [graphical user interface](https://en.wikipedia.org/wiki/Graphical_user_interface) (GUI). When you use a mouse to click on fancy icons, buttons, and menus, you're using a GUI.

To be fair, it's usually easier to teach someone how to use a GUI than a CLI. You can simply point to things and say "click here" or "drag this there". But GUIs do have some drawbacks:

- **They're weak.** You are given much more control over your computer through a CLI. With a GUI you're limited to the options that the developer of the GUI has given you.
- **They're slow.** Once you know the commands to type, it's much faster to type them than to click through endless menus with a mouse.
- **They're not as reproducible.** If you want to share a set of instructions, you can just copy and paste commands without worrying about screen sizes and user preferences.
- **They're not automatable.** It's easy to write code that manipulates text (as you've seen in Python), but it's much harder to write code that manipulates GUIs.
- **They're not as cool.** You will be invited to 90% fewer romantic outings if you are a GUI user.

### What is a terminal?

- As we talked about, the terms "shell", "CLI", and "terminal" are often used to refer to the same thing: the program that lets you issue text-based commands.
- However, to get pedantic, the "terminal" is just one _specific part_ of that program. Historically, the word "terminal" meant a physical device that you could type commands into, essentially a keyboard and a screen.
- A terminal emulator is a program that emulates a physical terminal. It's a program that lets you type commands into a window on your computer.
- _Which_ commands you're able to use isn't determined by the terminal emulator that you happen to be using. It's determined by the "shell", which we'll talk about later.
### What is a shell?

- So if your terminal is just a program that lets you issue text-based commands and renders the output of those commands...
	...What is the program that _runs_ those commands???
- That's a shell.
- Shells do a lot of things, but their main job is to interpret the commands you type and execute them.
- Shells are often referred to as "REPL"s. REPL stands for
	- Read
	- Eval (evaluate)
	- Print
	- Loop
- This is a fancy way of saying that shells are programs that:
	1. Read the commands you type
	2. Evaluate those commands, usually by running other programs on your computer
	3. Print the output of those commands
	4. Give you a new prompt to type another command and repeat

```bash
# to eval a result 
expr 123456 + 7890
```
### Variables:
- Both Bash and Zsh are shells, and they also happen to be powerful programming languages. They have variables, functions, loops, and more. That said, only [crazy people](https://bashsta.cc/) write large programs in shell languages... shells are optimized for running other programs and writing small scripts, not for writing programs.
```bash 
name="hello"
```

```bash
bankname="WorldBanc"
founded="1969"
ceo="Jeff Gates"
echo "$bankname was founded in $founded by $ceo"
```
### History:
- hen you're working in a REPL, it's _really_ helpful to be able to see the commands you've typed in the past. That way you can easily re-run them, or copy and paste them into a script.
```bash 
history
```
- You'll often want to re-run a command that you've run before. You could just type it out again, but assuming you don't have the [WPM](https://en.wikipedia.org/wiki/Words_per_minute) of ThePrimeagen, that's going to be a pain.
- Instead, you can use the up and down arrows to cycle through your command history. Focus your terminal window and use the "up" arrow key to start cycling through your command history. If you recently restarted your terminal type a few commands first, like:
```bash
echo hello
echo world
```
- If your terminal is feeling cluttered with text, you can clear it with the `clear` command, or by pressing `ctrl + l`. 
### FileSystems:
- All the data stored on your computer is organized into files and directories. Files and directories are organized into a tree-like structure called a filesystem.
- Directories (same as "folders" on Windows) are just containers that hold files and other directories.
- Files are just a dump of raw binary data: 1's and 0's. The bytes in a file can represent anything: text, images, videos, etc.
- The filesystem tree starts with a single directory called the [root directory](https://en.wikipedia.org/wiki/Root_directory). The root directory contains files and directories, which can contain more files and directories, and so on.
- When you open your terminal, your _working directory_ (the one you're "in") is going to be... somewhere. Most commonly it is your ["home" directory](https://en.wikipedia.org/wiki/Home_directory).
```bash 
# get the working dir 
pwd
```
- The output of your `pwd` command is a _filepath_. A filepath is a string that describes the location of a file or directory on your computer. Yours should look something like this:
```
/Users/wagslane
```
- The text might be different, but the structure should be the same. Let's break it down:
	- The first slash (`/`) represents the _root directory_. It's the tippy-top of the filesystem tree.
	- The next part (`Users`) is the name of a directory inside the root directory.
	- Finally, the last part (`wagslane`) is the name of a directory inside the `Users` directory.
- So this path represents a directory 2 levels down from the root directory:

```
root
  └── Users
        └── wagslane
```
- 