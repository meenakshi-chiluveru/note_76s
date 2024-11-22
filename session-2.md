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








