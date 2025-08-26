# Branches: Exploring Alternate Timelines

## Why Bother with Branches?

Imagine you have a great idea for a new feature for the robot. You start coding, but then you realize that your changes are breaking everything. What do you do? You could try to undo all of your changes, but that's a pain. Or, you could use **branches**.

A branch is like an alternate timeline for your code. You can create a new branch and make all of your changes there, without affecting the main codebase. If your idea works out, you can merge your branch back into the main timeline. If it doesn't, you can just delete the branch and pretend it never happened.

## What Exactly *Are* Branches?

Think of your project's history as a tree. The main trunk is the **main branch** (often called `main` or `master`). This is the official, working version of your code.

When you create a new branch, you're creating a new branch off of the main trunk. You can then add new commits to this branch, and it will grow independently of the main trunk.

This is great for:

* **Trying out new ideas:** You can create a branch to experiment with a new feature, without worrying about breaking the main codebase.
* **Fixing bugs:** You can create a branch to fix a bug, and then merge it back into the main branch when you're done.
* **Working with a team:** Everyone can work on their own branch, and then merge their changes together when they're ready.

### Hopping Between Branches

Switching between branches is super easy. You just use the `git checkout` command. For example, to switch to a branch called `my-new-feature`, you would run:

```
git checkout my-new-feature
```

And to create a new branch and switch to it at the same time, you can use the `-b` flag:

```
git checkout -b my-new-feature
```

## The Grand Unification: Merging

So you've finished your new feature on its own branch. How do you get it back into the main codebase? You **merge** it.

A merge takes all of the commits from your branch and adds them to another branch. It's like taking your alternate timeline and making it the official timeline.

Sometimes, a merge is easy. If the two branches haven't changed the same files, Git can just combine them automatically. But if they *have* changed the same files, you'll have a **merge conflict**. We talked about this in the last lesson. It's just a matter of telling Git how to combine the changes.

## How We Use Branches

On our team, we have a simple branching strategy:

* **`main`:** This branch is always stable and working. It's the code that we would put on the robot at a competition.
* **`dev`:** This is our development branch. It's where we merge all of our new features. It might not always be perfectly stable, but it's where the latest and greatest code lives.
* **Feature branches:** When you want to work on a new feature, you create a new branch off of `dev`. When you're done, you merge your feature branch back into `dev`.

This workflow keeps our `main` branch clean and stable, while still allowing us to work on new features in parallel.

And that's the magic of branches! They're a powerful tool that will make your life as a programmer much, much easier.