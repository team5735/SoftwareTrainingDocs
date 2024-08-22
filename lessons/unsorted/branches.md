# BRANCHES

## Why are branches?

Branches essentially let you split up the project's history so that different
people or groups can work on different, diverging versions of the project, that
are then merged together. The merge will reconcile all the changes from the
varying branches and it will end up as if everybody had worked on the same
project using just normal commits, pushes and pulls, but it's a lot easier to
split up like this than it is to just work together messily.

## What are branches?

Here's a good way to think of a branch: imagine a tree. The main trunk is the
"master" branch (again, sometimes called "main" for... reasons), which is also
sometimes called "trunk" due to this very analogy. Each branch is an offshoot
of another branch, usually the trunk branch. The idea is to model different
develoment directions. Consider the following:

1. You encounter an issue with the code
2. You consider how to fix the issue and come up with multiple solutions
3. You can now make multiple branches to try out different solutions
4. Whichever branch fixes the issue the best gets merged and the others are
   deleted.

Let's visualize this, shall we? This graph is of the same format as the ones in
the intro.

```
                               ┌─ D <── E <── F (resolution 1 branch)
A <── B <── C: issue spotted <─┤
                               └─ G <── H <── I <── J <── K (resolution 2 branch)
```

(Note that the commits can be in any order, they don't have to all be on one
branch and then the other).

Here, the team split into two branches (resolutions 1 & 2), and each branch
attempts to solve the issue separately. Note that no code from branch 1 can be
seen in branch 2. This avoids conflicts entirely, so people can work on the
branch for resolution 1 without worrying about bothering the people working on
branch 2. It also helps mentally separate the two solutions, but you can still
cross-pollinate by simply making the same changes to each branch.

Anybody can switch to any of the *three* branches at any time (the third is the
branch that the other two were branched off of) and write code there. In other
words, anybody working anwhere on the entire repository can do any of these
things:

- Make progress towards resolution 1
- Make progress towards resolution 2
- Add code to the main branch, between the two, essentially meaning writing
  code concerning neither fix to the issue (perhaps somewhere else in the
  codebase)

### Waitwaitwait how do you switch between branches?

This one's easy: just use `git checkout <branch>` to switch to <branch>. That's
all there is to it.

Also, use `git checkout -b <branch>` to checkout to a branch that doesn't exist
(= create it and checkout it).

There's also `git branch` for listing branches and `git branch -d <branch>` for
removing one (but you can only delete a branch after it's fully merged. That
way you can't lose the changes in the branch). If you want to delete a branch
that *has* been merged (careful! dangerous!), you can use `git branch -D
<branch>`. If you didn't mean to, you can restore a deleted branch, given the
magic numbers that `git branch -d` outputs (which is actually a commit name!
crazy, right?), with `git checkout -b <name of the restored branch> <commit
name, aka magic numbers>` (so, for example, `git checkout -b fix-stupid-mistake
1299080`, assuming `git branch -d` printed `1299080` as its output and you want
the restored branch to be called `fix-stupid-mistake`).

## So one of the fixes was resolved as the best one. What now?

You may realize that this image is actually quite similar to this image from
the intro, where you had a divergent history, but in that case the divergences
were between your local branch and the one on the server (the local one was
called master, the one on the server was called origin/master).

```
f267526 (initial commit) <── 511f8da (commit from repository A) origin/master
   ^
   └── 1299080 (commit from repository B) master
```

The only difference is that we have three branches (assuming that somebody
worked on the neither-fix branch) (note that a "feature" branch is the common
term for a branch where a feature is being developed, as opposed to one where
e.g. a bug is being fixed):

```
                               ┌─ D <── E <── F (resolution 1 branch)
                               │
A <── B <── C: issue spotted <─┼─ L <── M <── N (feature branch)
                               │
                               └─ G <── H <── I <── J <── K (resolution 2 branch)
```

git can handle this! All you need to do is tell it which branch you want to
merge into the main (neither-fix) branch.

Let's say, for the sake of argument, that all that work (2 extra commits!) on
the resolution 2 branch turned out to be for naught because of some fatal flaw.
No problem, it seems like we're merging the fixes from resolution 1 into the
feature branch. So let's do that!

`git checkout feature`
`git merge resolution-1`

Easy, right? But wait- what if the feature branch changed something since the
branches split that the resolution branch changed as well? In that case, you
have a merge conflict. This is easy to resolve in VS Code, or really in any
text editor, but I'll explain how it's done in VS Code.

Here's an image I stole off the internet that shows how VS Code displays merge conflicts:

![merge conflicts](https://i.sstatic.net/9Yz5D.jpg)

And here's what that looks like when you open that same file with a normal text
editor, so I can explain it better:

```
<<<<<<< HEAD
code code code
=======
other code other code other code
>>>>>>> resolution-1
```

What this is showing you is two different versions of the same part of the
code. The part under HEAD is the version that exists on the branch you're
merging into, which in our case is the version that exists on the "feature"
branch. The part between the ======= and resolution-1 is how that same place in
the code looks on the resolution-1 branch. In the VS Code UI, you can click on
"Accept Incoming Change" or "Accept Current Change" to replace this conflicting
area with the version that you're merging in ("other code other code other
code" in our example) or with the version on the branch that you're merging
into ("code code code" in our example). Finally, the other buttons let you
replace this whole mess with a mixture of the two.

### Ok, so I just handled a bunch of merge conflicts. What now?

Well, that's an easy answer: add them like you would any changes and commit
them. Make sure you mention that you merged two branches in your commit
message.

## Merging the other way

So we just considered what could be the most complicated case of merging one of
two topic branches into the branch they both came from, with that center branch
having progressed since the topics' creation. But what if we want it to not be
stupidly difficult to merge the fix branches in when the time comes? Well, we
can do that quite easily, by just merging the feature branch into the fix
branches.

This is the same concept: essentially, we take all the changes in the feature
branch that that specific fix branch hasn't seen yet, and add them to the fix
branch. If this is done intermittently, then the fix branches won't diverge too
much from the feature branches, making it easier to merge them in when the time
comes. This operation is as easy as `git merge feature` when you have the fix branch currently checked out.

### git merge is confusing :( I can never remember which way it merges.

The argument you give it (the branch name you put after `git merge`) is merged
into the current branch. You can also merge two branches into each other
without having checked one of them out, but that's even more confusing and
prone to error, so just ignore it.

## How we use branches at Control Freaks

Here's how our software team is organized:

- We have a "main" or "master" branch that is stable, i.e. it's tested and it
  **works**.
- We have a "dev" branch that is being actively developed and may or may not
  work.
- We have topic branches, made off of the dev branch, that each implement one
  feature.

At any one point, we could have any number of topic branches. Here's an example snapshot of how the branches could be in the middle of the build season:

```
main <─┐
       │
       └─ dev <── (commits)
           │
           ├─ topic-1
           ├─ topic-2
           └─ topic-3
```

After each topic is completed, it's merged into dev, with perhaps intermittent
merges from dev into each of the topics to ensure they don't fall *too* far
behind. Topics are deleted once merged. Finally, we only merge dev into main when it's
been thoroughly tested. dev shouldn't ever get deleted.
