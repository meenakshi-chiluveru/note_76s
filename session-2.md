# linux commands
1. ls - list subdirectories
2. / - root directories
3. cd - change directory
4. ls -l -lengthy format in alphabetical order
5. d - directory
6. - - file
7. cd .. = one step back
8. ls -lr = reverse alphabetical order
9. ls lt - latest will come on top
10. ls -ltr - old files on top
11. ls -la == list all files and folders including hidden


# CRUD(CREATE,READ,UPDATE,DELETE)
- `touch`: This command creates an empty file.  
- `mkdir`: This command creates a folder.   

# update file with content
Use the command 'cat > "filename"' to open a file. 
Enter the content and then press Ctrl+D to save it. 
The (>) symbol replaces the entire content, while (>>) appends to it.
# to read file
cat filename

# remove file and folder
1.1. Use `rm filename` to remove a file.  
2. Press `tab` to auto-select files.  
3. Use `rmdir` to remove an empty directory.  
4. Use `rm -r foldername` to recursively delete all files and folders within a directory.


copy
------------------------
To copy files, you can use the command:  
`cp source destination`  

Just a heads-up: the `cp` command is specifically for files.  

If you want to copy directories and their contents, use:  
`cp -r source destination`  

And if you need to remove a folder and everything inside it, you can do so with:  
`rm -r folder_name`  

Happy coding!

=======================================

cut
-----------------------------
The 'mv' command is a fundamental utility in Unix and Linux systems that stands for "move." It is primarily used to move files or directories from one location to another. The basic syntax for the command is:

```bash
mv source destination
```

In this context, "source" refers to the file or directory you want to move, while "destination" represents the location where you want it to be moved. 

Interestingly, when you use the 'mv' command within the same directory, it can also serve as a renaming tool. For example, if you want to rename a file, you can use the command as follows:

```bash
mv oldfilename newfilename
```

In this case, "oldfilename" is the current name of the file, and "newfilename" is what you want the file to be called after the operation. This dual functionality makes the 'mv' command a versatile tool for managing files and directories effectively.

grep is used to filter text in files. The syntax for using grep is: grep [word] [filename]. For example, to find the word "bin" in the file "passwd," you would use the command: grep bin /etc/passwd. The command `cat /etc/passwd` displays user information in Linux.
# linux is bydefault case sensitive
The command `grep -i` enables case-insensitive searches. For example, to search for the term "devops" in the file "passwd," you would use the command:
grep -i devops passwd


Piping: in Linux allows the output of one command to be used as the input for another command.
------------------------------------------------------------
Piping in Linux is a powerful feature that enables you to take the output from one command and use it as the input for another. This capability allows you to create more complex and efficient command combinations, enhancing your workflow.
$ cat passwd | grep -i devops
devops
DEVOPSYou can effectively locate entries related to "devops" in the passwd file by using the following command:

```
cat passwd | grep -i devops
```

This will provide you with the results:

```
devops
DEVOPS
```

By using this command, you ensure that you identify all variations of "devops," which can greatly enhance your data analysis process. This approach is a great step toward thorough and comprehensive results!


Wget vs. Curl  
------------------------------  
Wget is a powerful tool for downloading files and can be used with the command: `wget https://github.com/git-for-windows/git/releases/download/v2.47.0.windows.2/Git-2.47.0.2-64-bit.exe`. It is particularly useful for downloading entire websites or files recursively.

On the other hand, Curl is designed to transfer data and is commonly used for fetching content directly to the terminal. This makes it a great choice for quickly viewing or manipulating text data from a URL. 

Both tools have their unique strengths, so choosing between them depends on your specific needs!

### Understanding `cut` and `awk`

`cut` and `awk` are powerful command-line utilities used for text processing in Unix-like systems. They allow users to extract specific sections or "fragments" of data from lines of text, often based on a delimiter.

#### Using `cut`
The `cut` command extracts portions of each line based on a specified delimiter. The syntax for `cut` is as follows:

```
cut -d [delimiter] -f [field_number]
```

**Example:**
Consider the following command:
```
echo hello:meenakshi:how:re:you | cut -d : -f1
```
This command uses the colon (`:`) as the delimiter and extracts the first field. The output will be:
```
hello
```

This functionality is particularly useful when working with structured data, such as CSV files or system logs, where specific fields are separated by a character.










