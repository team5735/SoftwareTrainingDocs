# INTRO TO GIT

## What is git?

git is the most popular version control system for programmers, and for good
reason. It is used to track changes throughout a codebase, and to collaborate
with others on a project.

git contains many tools to this end, including:

- commits
- history viewing
- branches
- remotes
- many GUIs
- merging
- pull requests

### I heard about this "GitHub" thing, what's that about?

Yes, that's the industry standard "git host." A "git host" is a website where
people put git repositories. The point is similar to something like Google
Drive: essentially, there's one central website which holds essentially the
"master copy" of your project. More on remotes, repositories, and other git
shenanigans later.

The important thing is that git is NOT GitHub. GitHub is a company that hosts a
whole bunch of git repositories, with some extra features that programmers
might want, such as "forking" and "pull requests." It also has some
project-management features, such as "projects" and "issues." We use it because
everybody else does, although there are many alternatives that offer mostly the
same features, such as GitLab, Codeberg, Sourcehut, just to name a few.

## Ok, so what is a git re-po-si-tory? Sounds confusing.

git repositories are essentially just a directory (a folder) with a lot of
files, with information about who made what, where the files came from, and
where changes should go. We can think of it as a "project". It's very
complicated until you start to work with other people at the same time.

Speaking of working with other people, let's talk about that. Everybody who
contribuites to a repository has their own copy of the repository on their
computer. They get this copy by "cloning" the "master copy" (which GitHub
hosts! It's all starting to make sense). From then on, any changes they make to
their own repository can be "pushed" to the master copy, updating the master
with their changes. You can also "pull" changes from the master copy to your
copy, bringing in changes other people have made.

With these operations, which have appropriately named git commands (`git
clone`, `git push` and `git pull`), it's easy to see how people can collaborate
on a project. However, everything goes awry when we consider what happens after
the following sequence of events:

1. Person A clones the repository
2. Person B clones the repository
3. Person A makes changes
4. Person A pushes changes
5. Person B makes changes

The issue is that the master copy is now ahead of person B's copy. If person B
were to push their changes, which happened relative to the repository they saw
in step 1, they would overwrite person A's changes, which is a very bad idea.
To prevent this from happening, git will detect that you're pushing something
that would overwrite changes, and it doesn't let you. The solution is for
person B to pull the repository, which lets them see the changes that person A
has made. But then we have the same issue: we have two, potentially conflicting
changes that need to be reconciled. The solution for this? A merge.

## But first, commits!

Commits are the smallest unit of a change in git. Ideally, if people commit
properly, then every change they make (e.g., fixing a bug, adding a feature,
...) is a commit. git sees commits as, essentially, a bunch of lines that were
changed. So in that sense, one commit represents the differences between the
repository as it was before the commit and the repository as it is after the
commit.

We can visualize the entire history of a project as a series of commits, like
this:

```
A <── B <── C <── D <── E <── F
```

where each letter is a commit. In reality, commits have names like 27c8ce6,
which is actually an abbreviation for 27c8ce6b53a652020f94e19b2d8da6bdc016540e.
Normally you never have to deal with the scary internal name, but it's good to
know it exists, so when you see it, you understand that it's the name of a
commit.

The arrows in the diagram go from each commit to its parent (each commit can
only have one parent, except for merge commits, which are complicated).

In these commit diagrams, all commits will be named based off of when they were created.

### Making a commit

To make a commit, you need to do the following:

1. Write code
2. Stage the files you changed
3. Commit

In order to stage the files, that is, tell git that you're ready to commit the
changes they contain, you can run `git add .` in a terminal, assuming you're in
the bottommost folder in the repository. Then you run `git commit -m
"message"`, replacing "message" with your commit message (in quotation marks.)

## The merge

Merges are a way of bringing together two so-called "divergent histories" by
looking at all the changes they've made since they diverged. This can be easier
understood with a simple diagram:

```
    ┌─ B <── C
A <─┤
    └─ D <── E
```

Here, both B and C have A as a parent. This is the case when two people have
cloned the same repository and then made their own commits without pulling or
pushing. It's important to realize that this i a perfectly fine and normal
situation, and will happen often if there's more than one person contribuiting
to a project. Reconciling these two histories is the purpose of `git merge`.

After a merge, the history looks like this:

```
    ┌─ B <── C <─┐
A <─┤            ├─ F
    └─ D <── E <─┘
```

Commit F is a merge commit. There's a chance that there are actually no changes
recorded in F, which is the case when D and E didn't change any files that B
and C did. Keep in mind that this is a simplified case, but this is the most
common case that comes up when dealing with multiple people contribuiting to a
project. The real picture is more complicated simply because of branches. More
on that later, but that's definitely not an "intro" topic.

## That's cool and all, but what do I need to do when git yells at me?

Here's what is very likely to be the first error message you see, after trying
to `git push` a change to a repository that somebody else has `git push`ed to:

```
To github.com:<repository>
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'github.com:<repository>'
hint: Updates were rejected because the remote contains work that you do not
hint: have locally. This is usually caused by another repository pushing to
hint: the same ref. If you want to integrate the remote changes, use
hint: 'git pull' before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

It's telling you what to do next, `git pull`. So let's do that! This'll fix everything, right?

```
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 346 bytes | 173.00 KiB/s, done.
From github.com:<repository>
   f267526..511f8da  master     -> origin/master
hint: You have divergent branches and need to specify how to reconcile them.
hint: You can do so by running one of the following commands sometime before
hint: your next pull:
hint:
hint:   git config pull.rebase false  # merge
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint:
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
fatal: Need to specify how to reconcile divergent branches.
```

Oh...

So, here's the issue. This is in a tiny testing repository, so I actually have
example commit names. Why not use them!

(The initial commit is a commit that acts as the very first commit in a
repository. It has no parent.)

```
f267526 (initial commit) <── 511f8da (commit from repository A) origin/master
   ^
   └── 1299080 (commit from repository B) master
```

More words have appeared! Inside parenthesis is the name of the commit.
Repositories A and B are in place of person A and B from the earlier example.
After the parenthesis, it says what branch is currently pointing to that
commit. Branches come later, remember, so I'll just say this for now: the
person who just tried to pull is person B, who has repository B, which is why
their commit says "master," whereas the commit that says "origin/master" is the
latest commit in the origin repository.

The reason 1299080 is "based on" (has a parent of) f267526, instead of 511f8da,
is because at the time person B made that commit, their local repository had
never heard of 511f8da, because even though the "master repository" may have
heard of it, due to it having been pushed, they hadn't pulled it yet. Which is
fine. But now person B has to deal with this (not person A), and they do that
by merging it in.

The command to do that is `git merge origin/master`, but be careful. Sometimes,
certain git hosts (*cough cough* GitHub, but only sometimes *cough cough*) will
create the default branch as "main" instead, and in that case there's no such
thing as "origin/master". So how do you tell? Look back at the command output
the `git pull` that failed, specifically this line:

   `f267526..511f8da  master     -> origin/master`

It says origin/master here because of the way I made the testing repository.
But it may say origin/main, or maybe something else, but that's for branches
which is LATER, goddammit.

## So what can I do with this?

Well, you can write code and commit it (on every change, so that everything is
easier). You can push and handle a push conflict. And you understand enough to
be able to read more about git.

Beyond that, branches are really the only complicated thing that you need to
learn. Once you learn that, you can do everything you can do with git, save for
a few very situational commands.
