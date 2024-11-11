# Git Basics: Essential Commands and Workflows

## Table of Contents
1. Introduction
2. Creating a New Git Repository
3. Checking Git Status
4. Creating and Switching Branches
5. Merging a Branch into `main`
6. Resources

## Introduction

Git is a distributed version control system used by developers to track changes to files and collaborate on projects. In this guide you will learn how to create a new repository from a local folder, how to create a new branch off of main, and how to merge that branch back into main.

---

## Creating a New Git Repository

To start using Git in an existing folder, you need to initialize it as a Git repository.

1. **Navigate to the folder where your project is located**. If you haven't created the folder yet, you can create it and navigate into it:

    ```bash
    mkdir my-project
    cd my-project
    ```

2. **Initialize the Git repository** by running the following command:

    ```bash
    git init
    ```

   This command creates a new `.git` directory in the folder, which is used by Git to track the project.

3. **Add files to the repository**. Git doesn't automatically track files in your project. To add all the files in the directory, run:

    ```bash
    git add .
    ```

4. **Commit the changes**. Once you’ve added files to Git, you need to commit them:

    ```bash
    git commit -m "Initial commit"
    ```

5. **Tag the commit**. Optionally you can add a tag to the commit for easy retrieval:

    ```bash
    git tag <tag_name>
    ```

---

## Checking Git Status

To check the current status of your repository (such as which files have been modified, added, or are staged for commit), use the `status` command:

```bash
git status
```

This will show the current branch you are working on and all files and their current status. Files in your gitignore will not show up here.

## Creating and Switching Branches

Branches are a fundamental feature of Git, allowing you to work on different features or fixes independently without compromising the work on main. To create and switch branches, follow these steps:

### Create a new branch

You can create a new branch from your current position by running:

```bash
git checkout -b new-feature
```

This creates a new branch called `new-feature` and switches you to that branch.

### Switch to an existing branch

To switch to an already existing branch use git checkout. For example, to switch back to the main branch:

```bash
git checkout main
```

### List all branches

To see all branches in your repository, use:

```bash
git branch
```

This will show a list of all branches. The current branch will be highlighted with an asterisk.

In order to see remote branches as well use:

```bash
git branch -a
```

### Delete a branch (optional)

If you no longer need a branch, you can delete it with:

```bash
git branch -d branch-name
```

### Merging a Branch into `main`

Once you've completed the work on a branch, it's time to merge it into the `main` branch. Here's how to do that:

Switch to the `main` branch:

```bash
git checkout main
```
Make sure your main branch is up to date by using:

```bash
git status
```

If it needs to be updated from the remote branch you can pull from origin:

```bash
git pull origin main
```

Merge the feature branch into `main`. Assuming you want to merge the `new-feature` branch into `main`, use:

```bash
git merge new-feature
```

This will bring all the changes from the `new-feature` branch into `main`.

### Resolve any merge conflicts

If there are conflicts (i.e., changes in both branches that cannot be automatically merged), Git will notify you. You’ll need to manually resolve the conflicts in the affected files, stage the changes, and then commit the merge:

```bash
git add .
git commit -m "Resolved merge conflicts and merged new-feature into main"
```

### Push changes to a remote repository (if applicable)

If you’re working with a remote repository (e.g., GitHub, GitLab), you’ll want to push your changes to the remote:

```bash
git push origin main
```

---

## Resources

- [Pro Git Book](https://git-scm.com/book/en/v2)
- [Git Documentation](https://git-scm.com/docs)
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)


