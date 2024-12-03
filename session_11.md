## Project Configuration

To set up your SSH connection with GitHub, you'll need to configure your SSH settings as follows:

```
Host github.com
HostName github.com
User git
PreferredAuthentications publickey
IdentityFile ~/<replace-your-file-name>
```

### Basic Git Commands

- **Initialize a Git Repository**: 
  To create a new Git repository within a folder, use the command:
  ```
  git init
  ```
  This command sets up the necessary structure for a Git repository in the specified directory.

- **Check the Status of Your Files**: 
  To view the current state of your files and see which changes have been staged, modified, or are untracked, use:
  ```
  git status
  ```

- **Stage Changes for Commit**: 
  To prepare files for a commit, you can use:
  ```
  git add <file-name>
  ```
  For example, if you have 100 scripts related to user functionality such as signup, login, and password recovery, you would add completed files to the staging area temporarily. 

  For instance, after finalizing changes in the signup script, you would run:
  ```
  git add signup
  ```

### Configuring Your Identity

Before making your first commit, it's essential to set your user information so that your commits are attributed correctly. Run the following commands with your GitHub username and email:
```
git config --global user.name "your-user-name"
git config --global user.email "your-email-id"
```

### Committing Changes

Once your changes are staged, you can save them to your local repository with a descriptive message:
```
git commit -m "as part of bug fix"
```
This marks the completion of your changes locally before syncing with the remote repository.

### Setting Up GitHub

To connect your local repository with GitHub, follow these steps:

1. **Sign Up for GitHub**: If you don’t already have an account, create one.
2. **Create or Use an Existing SSH Key Pair**: Generate a public/private key pair for secure access.
3. **Add Your Public Key to GitHub**: Copy the public key and add it to your GitHub account settings.
4. **Retain Your Private Key**: Keep the private key safe and secure.
5. **Create an .ssh Directory**: Inside your home directory, create a folder named .ssh if it doesn’t already exist.
6. **Create a Config File**: Within the .ssh folder, create a configuration file without any extensions and add the earlier SSH settings.

### Organizing Your Development Workflow

Make sure to set your username and email before making any commits to ensure proper attribution.

To initiate a new repository on GitHub, start by creating the repository in your GitHub account.

When developing, you typically use an Integrated Development Environment (IDE) to streamline your coding efforts.

### Branching Strategy

In your workflow, the `master` branch typically represents the production environment (PROD). Here’s a recommended branching strategy:

1. Duplicate the code for a specific file, edit it, and review the changes carefully before proceeding.
2. Create a new branch for your features or fixes (e.g., `feature-123`), where you can make and test your changes independently.
3. After testing your changes, merge the branch back into the main or master branch to deploy to production.

Always manage the main branch diligently, as it reflects the production version of your project.
