---
title: Exploring History
teaching: 25
exercises: 0
questions:
- "How can I identify old versions of files?"
- "How do I review my changes?"
- "How can I recover old versions of files?"
objectives:
- "Explain what the HEAD of a repository is and how to use it."
- "Identify and use Git commit numbers."
- "Compare various versions of tracked files."
- "Restore old versions of files."
keypoints:
- "`git diff` displays differences between commits."
- "`git restore` recovers old versions of files."
---

As we saw in the previous lesson, we can refer to commits by their
identifiers.  You can refer to the _most recent commit_ of the working
directory by using the identifier `HEAD`.

We've been adding one things to the functions.py file and then checking the changes using `git status` and `git diff`.  Before we start,
let's make a change to `functions.py` by adding a return type to the method:

~~~
$ nano functions.py
$ cat functions.py
~~~
{: .bash}

~~~
def sum_function(list) -> float:
    """
    A function which takes a list as an argument and
    returns the floating point sum.

    Parameters
    ----------
    list: list
        Must be floats or ints

    Returns
    -------
    float:
        The sum of the elements in list
    """
    sum = 0.0
    for item in list:
        sum += item
    return sum
~~~
{: .output}

Now, let's see what we get.

~~~
$ git diff HEAD functions.py
~~~
{: .bash}

~~~
diff --git a/functions.py b/functions.py
index c6835ed..536cfac 100644
--- a/functions.py
+++ b/functions.py
@@ -1,4 +1,4 @@
-def sum_function(list):
+def sum_function(list) -> float:
     """
     A function which takes a list as an argument and
     returns the floating point sum.
~~~
{: .output}

which is the same as what you would get if you leave out `HEAD` (try it).  The
real goodness in all this is when you can refer to previous commits.  We do
that by adding `~1` 
(where "~" is "tilde", pronounced [**til**-d*uh*]) 
to refer to the commit one before `HEAD`.

~~~
$ git diff HEAD~1 functions.py
~~~
{: .bash}

If we want to see the differences between older commits we can use `git diff`
again, but with the notation `HEAD~1`, `HEAD~2`, and so on, to refer to them:

~~~
$ git diff HEAD~2 functions.py
~~~
{: .bash}

~~~
diff --git a/functions.py b/functions.py
index e4b4bb8..536cfac 100644
--- a/functions.py
+++ b/functions.py
@@ -1,4 +1,18 @@
-def sum_function(list):
+def sum_function(list) -> float:
+    """
+    A function which takes a list as an argument and
+    returns the floating point sum.
+
+    Parameters
+    ----------
+    list: list
+        Must be floats or ints
+
+    Returns
+    -------
+    float:
+        The sum of the elements in list
+    """
     sum = 0.0
     for item in list:
         sum += item
~~~
{: .output}

We could also use `git show` which shows us what changes we made at an older commit as well as the commit message, rather than the _differences_ between a commit and our working directory that we see by using `git diff`.

~~~
$ git show HEAD~2 functions.py
~~~
{: .bash}

~~~
commit 095f874fbaf2a15a349230f66b0bbdd69c97a931
Author: Ryan Pepper <r.pepper@bham.ac.uk>
Date:   Mon Dec 6 19:12:12 2021 +0000

    Created a summing function in functions.py

diff --git a/functions.py b/functions.py
new file mode 100644
index 0000000..e4b4bb8
--- /dev/null
+++ b/functions.py
@@ -0,0 +1,5 @@
+def sum_function(list):
+    sum = 0.0
+    for item in list:
+        sum += item
+    return sum
~~~
{: .output}

In this way,
we can build up a chain of commits.
The most recent end of the chain is referred to as `HEAD`;
we can refer to previous commits using the `~` notation,
so `HEAD~1`
means "the previous commit",
while `HEAD~123` goes back 123 commits from where we are now.

We can also refer to commits using
those long strings of digits and letters
that `git log` displays.
These are unique IDs for the changes,
and "unique" really does mean unique:
every change to any set of files on any computer
has a unique 40-character identifier.
My first commit was given the ID
`095f874fbaf2a15a349230f66b0bbdd69c97a931`,
so let's try this (note that on your machine it will be different):

~~~
$ git diff 095f874fbaf2a15a349230f66b0bbdd69c97a931 functions.py
~~~
{: .bash}

~~~
diff --git a/functions.py b/functions.py
index e4b4bb8..cbd1b2f 100644
--- a/functions.py
+++ b/functions.py
@@ -1,5 +1,41 @@
 def sum_function(list) -> float:
+    """
+    A function which takes a list as an argument and
+    returns the floating point sum.
+
+    Parameters
+    ----------
+    list: list
+        Must be floats or ints
+
+    Returns
+    -------
+    float:
+        The sum of the elements in list
+    """
     sum = 0.0
     for item in list:
         sum += item
     return sum
~~~
{: .output}

That's the right answer,
but typing out random 40-character strings is annoying,
so Git lets us use just the first few characters to get the same result:

~~~
$ git diff f22b25e functions.py
~~~
{: .bash}

All right! So
we can save changes to files and see what we've changed—now how
can we restore older versions of things?
Let's suppose we want to get rid of that change that we added - we don't want to add the return type. `git status` tells us that the file has been changed, but those changes haven't been staged:

~~~
$ git status
~~~
{: .bash}

~~~
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)

	modified:   functions.py

no changes added to commit (use "git add" and/or "git commit -a")
~~~
{: .output}

We can put things back the way they were
by using `git restore`:

~~~
$ git restore --source HEAD functions.py
$ cat functions.py
~~~
{: .bash}

~~~
def sum_function(list):
    """
    A function which takes a list as an argument and
    returns the floating point sum.

    Parameters
    ----------
    list: list
        Must be floats or ints

    Returns
    -------
    float:
        The sum of the elements in list
    """
    sum = 0.0
    for item in list:
        sum += item
    return sum
~~~
{: .output}

As you might guess from its name,
`git restore` restores an old version of a file.
In this case,
we're telling Git that we want to recover the version of the file recorded in `HEAD`,
which is the last saved commit.
If we want to go back even further,
we could use a commit identifier instead:

~~~
$ git restore --source 424982e functions.py
~~~
{: .bash}

~~~
$ cat functions.py
~~~
{: .bash}

~~~
def sum_function(list):
    """
    A function which takes a list as an argument and
    returns the sum

    Parameters
    ----------
    list: list
        Must be floats or ints

    Returns
    -------
    float:
        The sum of the elements in list
    """
    sum = 0.0
    for item in list:
        sum += item
    return sum
~~~
{: .output}

~~~
$ git status
~~~
{: .bash}

~~~
# On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git restore <file>..." to discard changes in working directory)
#
#	modified:   functions.py
#
no changes added to commit (use "git add" and/or "git commit -a")
~~~
{: .output}

If we had gone one step further and staged something to be committed,
this can be restored by adding the `--staged` flag (by default, it will restore to HEAD):
~~~
$ git restore --staged functions.py
~~~
{: .bash}

> ## Checkout or Restore?
>
> In older versions of git, the command `checkout` was used instead of `restore`. Apart from being more
> confusing, this could lead to being in something called a 'detached HEAD' state if you mistyped the command.
> Luckily, this should not happen any more unless you want it to!
{: .callout}

It's important to remember that we must use the commit number that identifies the state of the repository *before* the change we're trying to undo. A common mistake is to use the number of
the commit in which we made the change we're trying to get rid of.
In the example below, we want to retrieve the state from before the most
recent commit (`HEAD~1`), which is commit `f22b25e`:

![Git Checkout](../fig/git-checkout.svg)

So, to put it all together,
here's how Git works in cartoon form:

![https://figshare.com/articles/How_Git_works_a_cartoon/1328266](../fig/git_staging.svg)

> ## Simplifying the Common Case
>
> If you read the output of `git status` carefully,
> you'll see that it includes this hint:
>
> ~~~
> (use "git restore <file>..." to discard changes in working directory)
> ~~~
> {: .bash}
>
> As it says,
> `git restore` without a version identifier using the `--source` option restores files
> to their state at the last commit, i.e. HEAD. This is generally what you will want to do!
{: .callout}

The fact that files can be reverted one by one
tends to change the way people organize their work.
If everything is in one large document,
it's hard (but not impossible) to undo changes to the introduction
without also undoing changes made later to the conclusion.
If the introduction and conclusion are stored in separate files,
on the other hand,
moving backward and forward in time becomes much easier.

> ## Recovering Older Versions of a File
>
> Jennifer has made changes to the Python script that she has been working on for weeks, and the
> modifications she made this morning "broke" the script and it no longer runs. She has spent
> ~ 1hr trying to fix it, with no luck...
>
> Luckily, she has been keeping track of her project's versions using Git! Which commands below will
> let her recover the last committed version of her Python script called
> `data_cruncher.py`?
>
> 1. `$ git restore`
>
> 2. `$ git restore data_cruncher.py`
>
> 3. `$ git restore --source HEAD~1 data_cruncher.py`
>
> 4. `$ git restore --source <unique ID of last commit> data_cruncher.py`
>
> 5. Both 2 and 4
{: .challenge}
