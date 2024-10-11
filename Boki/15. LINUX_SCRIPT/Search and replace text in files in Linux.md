
## 1. Overview[](https://www.baeldung.com/linux/recursive-search-and-replace#overview)

Searching for a pattern in a file and replacing it with a new text is a typical operation when we work in the Linux command line.

Sometimes, we want to search and replace all text files under a given directory, including the text files under its subdirectories.

In this tutorial, we’ll discuss how to search and replace in text files recursively through examples.

## 2. The Example[](https://www.baeldung.com/linux/recursive-search-and-replace#the-example)

Before we go into the detail of the solutions, let’s make an example directory called _myDir_ and create some subdirectories and files under it:

```bash
$ tree myDir
myDir
├── dir1
│   ├── dir1.1
│   │   ├── dir1.1.1
│   │   │   └── text1.1.1.txt
│   │   └── text1.1.txt
│   └── text1.txt
└── parent.txt
```

Let’s take a look at the content of each text file:

```bash
$ head $(find myDir -name "*.txt")
==> myDir/dir1/dir1.1/dir1.1.1/text1.1.1.txt <==
text1.1.1: I like Linux.

==> myDir/dir1/dir1.1/text1.1.txt <==
text1.1: I like Linux.

==> myDir/dir1/text1.txt <==
text1: I like Linux.

==> myDir/parent.txt <==
Parent: I like Linux.
```

Next, **we’re going to replace “_Linux”_ with “_Linux operating system_” in all text files under the _myDir_ directory.**

## 3. Divide and Conquer[](https://www.baeldung.com/linux/recursive-search-and-replace#divide-and-conquer)

We are not really facing an algorithm problem. However, we can borrow the “[Divide and Conquer](https://en.wikipedia.org/wiki/Divide-and-conquer_algorithm)” idea to solve it.

We can divide the problem into two sub-problems:

1.  Replace “_Linux_” with “_Linux operating system_” in a single file
2.  Find all text files under the given directory _myDir_

We’ll solve the two sub-problems separately, and then we’ll combine them to solve our original problem.

Next, let’s have a look at how to divide and conquer.

## 4. Search and Replace in a Single Text File[](https://www.baeldung.com/linux/recursive-search-and-replace#search-and-replace-in-a-single-text-file)

Firstly, let’s solve the problem: Replace “_Linux_” with “_Linux operating system_” in a single file.

In the Linux command line, we can do text substitution and save the result back to a file in many ways.

To solve this problem, we’ll pick the [_sed_](https://www.baeldung.com/linux/sed-editor) command to do the search and replace job.

Let’s see how a straightforward _sed_ command replaces “_Linux”_ with “_Linux operating system_” in the _parent.txt_:

```bash
$ sed -i 's/Linux/& operating system/g' parent.txt 
$ cat parent.txt
Parent: I like Linux operating system.
```

Next, we need to find all text files under the _myDir_ directory and solve the problem by passing the found files to the _sed_ command above.

## 5. Search and Replace Recursively[](https://www.baeldung.com/linux/recursive-search-and-replace#search-and-replace-recursively)

There are many ways to find all text files under the given directory and invoke the _sed_ command on found files.

In this section, we’ll address four different methods.

### 5.1. Using the _find_ Command and the _-exec <command> {} +_ Option[](https://www.baeldung.com/linux/recursive-search-and-replace#1-using-the-find-command-and-the-exec-ltcommandgt---option)

The [_find_](https://www.baeldung.com/linux/find-command) command can find files recursively under a given directory. Moreover, it provides an option “_-exec <command> {} +”_  to execute a command on all found files.

Let’s assemble our _sed_ command and a _find_ command to solve our problem:

```bash
$ find myDir -name '*.txt' -exec sed -i 's/Linux/& operating system/g' {} +
```

In the command above, **the “_{}_” is a placeholder that will be filled by all found files.** Therefore, the _sed_ command will look like:

```bash
$ sed -i '..code..' foundFile1 foundFile2 foundFile3...foundFileN
```

**In this way, we invoke the _sed_ command only once instead of _n_ times.**

Now, let’s check if all text files under the directory _myDir_ have been changed:

```bash
$ head $(find myDir -name "*.txt")
==> myDir/parent.txt <==
Parent: I like Linux operating system.

==> myDir/dir1/text1.txt <==
text1: I like Linux operating system.

==> myDir/dir1/dir1.1/text1.1.txt <==
text1.1: I like Linux operating system.

==> myDir/dir1/dir1.1/dir1.1.1/text1.1.1.txt <==
text1.1.1: I like Linux operating system.
```

### 5.2. Using the _find_ Command and the _xargs_ Command[](https://www.baeldung.com/linux/recursive-search-and-replace#2-using-the-find-command-and-the-xargs-command)

In the real world, we often see the _find_ command and the [_xargs_](https://www.baeldung.com/linux/xargs) command work together.

The _xargs_ command can read the output of the _find_ command, which is a list of files found, and then, build them into arguments of another command.

Let’s see how to combine these two commands to solve our problem:

```bash
$ find myDir -name '*.txt' | xargs sed -i 's/Linux/& operating system/g'
```

After we execute the command above, all text files under the _myDir_ directory will have been changed recursively.

### 5.3. Using the _grep_ Command and the _xargs_ Command[](https://www.baeldung.com/linux/recursive-search-and-replace#3-using-the-grep-command-and-the-xargs-command)

As the name says, the _find_ command can find files. With the –_Rl_ option, [the _grep_ command can do it as well.](https://www.baeldung.com/linux/common-text-search#3-recursively-search-a-directory)

Here, the _-R_ option tells _grep_ to search a directory recursively, while the _-l_ option is to skip the matching information and tell _grep_ to print only the file names of matched files.

Let’s see how to find all files containing pattern “_Linux_” using the _grep_ command:

```bash
$ grep -Rl 'Linux' myDir
myDir/parent.txt
myDir/dir1/text1.txt
myDir/dir1/dir1.1/text1.1.txt
myDir/dir1/dir1.1/dir1.1.1/text1.1.1.txt
```

Now, to solve our problem, we just pipe this result to the _xargs_ command:

```bash
$ grep -Rl 'Linux' myDir | xargs sed -i 's/Linux/& operating system/g'
```

Once again, all occurrences of “_Linux_” are replaced with “_Linux operating system_” in all text files under the _myDir_ directory.

### 5.4. Using the Zsh Glob (**)[](https://www.baeldung.com/linux/recursive-search-and-replace#4-using-the-zsh-glob-)

[Zsh](http://zsh.sourceforge.net/) is a powerful and popular shell. **Zsh glob supports the double-asterisk (**) glob to match files under the current directory and all its subdirectories.**

Let’s see how to list all text files recursively under the _myDir_ directory with Zsh:

```bash
(zsh)$ ls -1 myDir/**/*.txt
myDir/dir1/dir1.1/dir1.1.1/text1.1.1.txt
myDir/dir1/dir1.1/text1.1.txt
myDir/dir1/text1.txt
myDir/parent.txt
```

Therefore, we can solve our problem much simpler with Zsh:

```bash
(zsh)$ sed -i 's/Linux/& operating system/g' myDir/**/*.txt
```

We see that the _sed_ command alone can solve the problem.

Similarly, we can use the same glob to check if all occurrences of “_Linux_” in all text files are replaced:

```bash
(zsh)$ head myDir/**/*.txt
==> myDir/parent.txt <==
Parent: I like Linux operating system.

==> myDir/dir1/text1.txt <==
text1: I like Linux operating system.

==> myDir/dir1/dir1.1/text1.1.txt <==
text1.1: I like Linux operating system.

==> myDir/dir1/dir1.1/dir1.1.1/text1.1.1.txt <==
text1.1.1: I like Linux operating system.
```

## 6. Conclusion[](https://www.baeldung.com/linux/recursive-search-and-replace#conclusion)

In this article, we addressed four different approaches to search and replace recursively under a given directory.

The basic idea is first finding all text files and then passing the file list to a text substitution command like _sed_.

The _find, grep,_ and _xargs_ commands are pretty convenient ways to solve the problem.

However, if we are using Zsh, we shouldn’t forget the handy double-asterisk (**) glob. It can solve the problem in a more straightforward way.