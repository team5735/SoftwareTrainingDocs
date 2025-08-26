# Git and GitHub: Your Time Machine for Code

This is meant to go along with the git slides you can find in the team Google Drive folder, assuming I've done my job.

## What is this "Git" Thing, Anyway?

Imagine you're writing an essay. You write a draft, then another, and another. What if you want to go back to a previous version? That's where a **version control system** comes in. And for programmers, the version control system of choice is **Git**.

Git is like a time machine for your code. It lets you:

* Track changes to your files.
* Go back to previous versions of your code.
* Collaborate with other people on the same project without stepping on each other's toes.

### And What About GitHub?

If Git is the time machine, then **GitHub** is the time machine factory. It's a website where you can store your Git projects (which we call **repositories**). It's like Google Drive for your code, but with a bunch of extra features for programmers.

> **Key takeaway:** Git is the tool, GitHub is the website where we use the tool.

## Your First Repository

A **repository** (or "repo" for short) is just a fancy word for a project that's being tracked by Git. It's a folder with all of your code, plus a special hidden folder where Git keeps track of all the changes.

When we work on a project as a team, everyone has their own copy of the repo on their computer. You can make changes to your copy, and then "push" those changes to the main repo on GitHub so that everyone else can see them. You can also "pull" changes from the main repo to get the latest updates from your teammates.

This is how we all stay in sync and work together on the same codebase.

## Commits: The Building Blocks of History

A **commit** is a snapshot of your code at a specific point in time. Every time you make a change to your code, you can "commit" that change. This creates a new snapshot in your project's history.

Think of it like saving your progress in a video game. Each commit is a save point that you can go back to if you mess something up.

### Making a Commit

To make a commit, you need to do two things:

1.  **Stage your changes:** This is where you tell Git which files you want to include in the commit.
2.  **Commit your changes:** This is where you actually create the snapshot and add a message describing what you changed.

## Merging: When Worlds Collide

So what happens when you and a teammate both make changes to the same file at the same time? This is called a **merge conflict**, and it's a normal part of working with Git.

When you have a merge conflict, Git will tell you that it can't automatically merge the changes. It's up to you to look at the two sets of changes and decide which one to keep (or how to combine them).

Don't worry, it's not as scary as it sounds! VS Code has a great tool for resolving merge conflicts that makes it easy to see what's going on.

## When Git Gets Mad

Sometimes, Git will give you an error message that looks like a bunch of gibberish. Don't panic! The error messages usually tell you what's wrong and how to fix it.

The most common error you'll see is when you try to push your changes to a repo that has new changes that you don't have yet. Git will tell you to `git pull` first to get the latest changes. This is Git's way of making sure you don't accidentally overwrite someone else's work.

## What Now?

You now know enough about Git to be dangerous! You can write code, commit it, and push it to a repository. You also know how to handle the most common Git issues.

In the next lesson, we'll talk about **branches**, which are a powerful tool for working on new features without breaking the main codebase.
