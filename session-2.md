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

The `awk` utility is a powerful tool used for processing and analyzing text data by dividing it into columns.

------------------

To specify the delimiter for splitting the data, you can use the `-F` option. For example, if you want to print the first column of data when using a forward slash (/) as the delimiter, the command would be:

```bash
awk -F / '{print $1}'
```

If you need to retrieve the last column of data from a file, you can also accomplish this with the same delimiter by using the following command:

```bash
awk -F / '{print $NF}'
```

In this case, `$NF` represents the last field in the current record.

Another example is when extracting data from the `/etc/passwd` file, where the fields are separated by colons (:). To print the first column (which typically contains usernames), you can use:

```bash
cat passwd | awk -F : '{print $1}'
```

Here, the `-F :` option tells `awk` to split the input based on colons. This command will output a list of usernames from the `passwd` file.

name
ls
cat
cp
mv
grep
cut
awk

head and tail
-------------------------------------
To view the first 10 lines of a file, use the command:  
**head filename**  

To display the last 10 lines, you can use:  
**tail filename**  

If you need to see the first 2 lines specifically, the command would be:  
**head -n 2 filename**  

These commands are useful for quickly accessing portions of a file's content!

Editors
---------------------------------------
**Comprehensive Guide to Vim Commands**

Vim, short for Vi IMproved, is a highly configurable and widely-used text editor that operates primarily in command-line environments, making it a favorite among developers and system administrators. Below is a detailed overview of essential commands and modes that will help you navigate and utilize Vim more effectively.

### 1. Opening Files

To edit a file with Vim, you can use the following command in the terminal:

```bash
vim filename
```

Replace `filename` with the actual name of the file you want to open. If the file does not exist, Vim will create a new file with that name.

### 2. Modes in Vim

Vim operates in several modes, each serving different purposes:

- **Normal Mode**: Default mode for navigation and executing commands. You enter this mode when you open a file.
- **Insert Mode**: Used for entering text. You can switch to this mode by pressing `i` or `o`.
- **Command Mode**: In this mode, you can execute various commands. Enter this mode by pressing the `:` key.

### 3. Basic Commands

Here are some fundamental commands that you will frequently use:

- **Quitting the File**:
  - `:q` - This command will quit Vim without saving any changes you might have made.
  - `:wq` - This command writes (saves) the changes and then exits the editor.
  - `:q!` - Use this command to exit Vim without saving changes, regardless of unsaved modifications.

- **Creating a New File**: To create and edit a new file, run:
  
  ```bash
  vim filename
  ```
  
  This will open a new buffer for the specified filename.

### 4. Line Numbering

To enhance your navigation within the file, you can display or hide line numbers:

- `:set nu` - Enables line numbering, displaying the corresponding line number next to each line.
- `:set nonu` - Disables line numbering if you prefer a cleaner view without numbers.

### 5. Searching Text

Vim provides powerful search capabilities:

- To search for a word from the top of the document, enter:
  
  ```bash
  /word
  ```
  
  Replace `word` with the term you're looking for. Press `Enter` to execute the search.
  
- To search for a word from the bottom of the document, use:
  
  ```bash
  ?word
  ```
  
  Again, replace `word` with your search term.

### 6. Navigating the Document

Efficient navigation within a document is crucial. Here are some useful shortcuts:

- Press `Shift + G` to instantly jump to the bottom of the document.
- Press `gg` to navigate back to the top of the document.
- After performing a search, pressing `n` will take you to the next occurrence of the searched word.
- To clear the highlight from the last search, use the command:
  
  ```bash
  :noh
  ```

### 7. Undoing Changes

To undo the last change you made, simply type:

```bash
u
```

This command can be repeated to continue undoing previous changes, allowing you to revert to earlier versions of your document.

### Conclusion

By mastering these commands and modes, users can significantly improve their productivity and efficiency while using Vim. The editor’s extensive functionality might seem daunting at first, but with practice, it becomes an invaluable tool for text editing. Happy editing!

replace the content/word
-------------------------
To search for and replace text within a line in your document, you can use the following commands:

1. To replace the first occurrence of a specific word in the current line where your cursor is located, you can use the command:
   ```
   :s/word_to_find/word_to_replace
   ```
   For example, if you want to replace the first occurrence of the word "root" with "ROOT," you would type:
   ```
   :s/root/ROOT
   ```

2. If you want to replace all occurrences of the specified word within the current line, you can append the `g` (global) flag to the previous command:
   ```
   :s/word_to_find/word_to_replace/g
   ```
   For instance, to replace all instances of "root" with "ROOT" in the current line, use:
   ```
   :s/root/ROOT/g
   ```

3. To replace occurrences on a particular line, you can specify the line number before the `s` command. For example, if you want to replace all occurrences of "hello" with "hi" on line 2, the command would be:
   ```
   :2s/hello/hi/g
   ```

4. If you wish to replace a word throughout the entire file, you can use the following syntax:
   ```
   :%s/word_to_find/word_to_replace/g
   ```
   For example, to replace all occurrences of "sbin" with "SBIN" across the entire file, you would type:
   ```
   :%s/sbin/SBIN/g
   ```

5. Similarly, if you want to replace a different word throughout the file, simply adjust the command like this:
   ```
   :%s/word/newword/g
   ```

6. To copy a line of text, you can use the `yy` command, which will copy the current line where the cursor is located.

7. To paste the copied line, simply use the `p` command. If you want to paste the copied line multiple times, you can specify the number before the `p` command. For example, to paste the copied line 10 times, you would type:
   ```
   10p
   ```

This comprehensive guide should help you effectively search and replace text using these commands in your document.











