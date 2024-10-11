How to Find and Replace Text in a File on Linux
LinuxOperating SystemOpen Source
Introduction

In Linux-based operating systems, there are many ways to search (find) and replace text in a file. Depending on the size of a file and the complexity of the find and replace operation, different tools and commands may be more appropriate. In this article, we'll learn a few different methods of finding and replacing text in Linux environments.
Using the sed command to find and replace text

The sed (stream editor) command line tool is another powerful tool that can be used to find and replace text in files on Linux. This tool is often used to perform more complex text transformations (manipulations) and could be performed in both interactive and non-interactive modes. To search and replace text in a file using sed, we need to supply two arguments: the search string and the replace string respectively. Here is a good example of how to use sed to replace all occurrences of "make" with "cmake" in a file called "cmd.txt" −

$ sed 's/make/cmake/g' cmd.txt > ncmd.txt

The ‘s/’ keyword in the given command is used to specify performing a replace operation. The first "make" argument is the search string and the second "cmake" argument is the replacement string. The ‘g/’ at the end of the command is used to specify that all occurrences of search string are to be replaced, not just the first one in this. The output of the command is redirected to a new file called "ncmd.txt".
Using the awk command to find and replace text

The awk command is a versatile programming language that is often used to transform text data. It can also be used to search and replace text in a file in Linux. To find and replace text in a file using awk command, you need to supply two arguments: the search string and the replace string.

Here is a good example of how to use awk tool to replace all occurrences of "apple" with "banana" in a file called "fruits.txt" −

$ awk '{gsub(/apple/, "banana"); print}' fruits.txt > latest_fruits.txt

The gsub() function in the awk command is used to do a global replacement of the search string with the replace string. Output of the command is saved in a new file called "latest_fruits.txt".
Using the vi editor to find and replace text

Another way to find and replace text in a file on Linux is to use the vi text editor. vi is a versatile text editor that can be used to perform a variety of text editing tasks, including finding and replacing text.

To find and replace text in vi, you must first open the file in vi by running the following command −

$ vi file.txt

Once the file is open in vi, press the Esc key to enter normal mode. Then type the following command to start a find and replace operation −

:%s/oldword/newword/g

This command will look for all occurrences of the word "oldword" in the file and replace each instance with the word "newword".
Using the grep and sed command to find and replace text

One of the simplest and most powerful tools for finding and replacing text in Linux is grep and sed. grep is a command-line tool for finding specific patterns in text-based data, while sed is a stream editor that can perform various text transformations on a file.

Here's an example of how to use grep and sed to find a specific word in a file and replace it with a new word −

$ grep -l 'oldword' file.txt | xargs sed -i 's/oldword/newword/g'

This command will look for all occurrences of the word "old word" in the file "file.txt" and replace each instance with the word "new word".
Using the perl command to find and replace text

Finally, another tool that can be used to find and replace text in a file on Linux is the perl command. perl is a high-level programming language that can be used for a variety of purposes, including text processing.

Here's an example of how to use Perl to find and replace text in a file −

$ perl -pi -e 's/oldword/newword/g' file.txt

This command will look for all occurrences of the word "oldword" in the file "file.txt" and replace each instance with the word "newword". The original file will be modified, so be careful when using this command.
Conclusion

In conclusion, there are several ways to find and replace text in a file on Linux, including using the sed, awk, and perl commands, as well as the graphical user interface of a text editor like gEdit or Vim. Which method you choose depends on your specific requirements and the complexity of the text transformation you need to perform. Whether you are a novice or an experienced Linux user, one of these methods will surely meet your needs.
Pradeep Jhuriya
Pradeep Jhuriya

https://www.tutorialspoint.com/how-to-find-and-replace-text-in-a-file-on-linux