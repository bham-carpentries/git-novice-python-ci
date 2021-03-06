---
title: Conflicts
teaching: 15
exercises: 0
questions:
- "What do I do when my changes conflict with someone else's?"
objectives:
- "Explain what conflicts are and when they can occur."
- "Resolve conflicts resulting from a merge."
keypoints:
- "Conflicts occur when two or more people change the same file(s) at the same time."
- "The version control system does not allow people to overwrite each other's changes blindly, but highlights conflicts so that they can be resolved."
---

Now you've put your repository on Gitlab, you could invite others to download (or 'clone') and
make their own changes and improvements. They would have their own local copy of the
repository and commit to it just like you've been doing. If they then wanted to make their
work available to you, they could 'push' the changes to the repository (or create a merge/pull
request which you would need to approve).

At this point though, you're quite likely to hit conflicts. As soon as people can work
in parallel, they'll likely step on each other's
toes.  This will even happen with a single person: if we are working on
a piece of software on both our laptop and a server in the lab, we could make
different changes to each copy.  Version control helps us manage these
[conflicts]({{ page.root }}/reference/#conflicts) by giving us tools to
[resolve]({{ page.root }}/reference/#resolve) overlapping changes.

To see how we can resolve conflicts, we must first create one.  The file
`functions.py` currently looks like this both locally and on GitLab:
repository:

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

Click on the `functions.py` file in the GitLab interface to view it and then click on the blue 'Edit' button. In the
editor that's brought up, change the docstring again:

~~~
def sum_function(list):
    """
    A method which takes a list as an argument and
    returns the sum as a floating point number.

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

Now let's make a different change to the same line in the code on the **local** copy
**without** updating from GitHub:

~~~
$ nano functions.py
$ cat functions.py
~~~
{: .bash}

~~~
def sum_function(list):
    """
    A function which takes a list of integers and floating point 
    numbers as an argument and returns the sum of them as a float.

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

We can commit the change locally:

~~~
$ git add functions.py
$ git commit -m "Add a line in my copy"
~~~
{: .bash}

~~~
[master 07ebc69] Add a line in my copy
 1 file changed, 1 insertion(+)
~~~
{: .output}

but Git won't let us push it to GitLab:

~~~
$ git push origin master
~~~
{: .bash}

~~~
To https://gitlab.bham.ac.uk/elvidgsm-dasp/planets-pepperr.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://gitlab.bham.ac.uk/elvidgsm-dasp/planets-pepperr.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Merge the remote changes (e.g. 'git pull')
hint: before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
~~~
{: .output}

![The Conflicting Changes](../fig/conflict.svg)

Git rejects the push because it detects that the remote repository has new updates that have not been
incorporated into the local branch.
What we have to do is pull the changes from GitLab,
[merge]({{ page.root }}/reference/#merge) them into the copy we're currently working in,
and then push that.
Let's start by pulling:

~~~
$ git pull origin master
~~~
{: .bash}

~~~
remote: Counting objects: 5, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 3 (delta 1)
Unpacking objects: 100% (3/3), done.
From https://github.com/vlad/planets
 * branch            master     -> FETCH_HEAD
Auto-merging functions.py
CONFLICT (content): Merge conflict in functions.py
Automatic merge failed; fix conflicts and then commit the result.
~~~
{: .output}

The `git pull` command updates the local repository to include those
changes already included in the remote repository.
After the changes from remote branch have been fetched, Git detects that changes made to the local copy 
overlap with those made to the remote repository, and therefore refuses to merge the two versions to
stop us from trampling on our previous work. The conflict is marked in
in the affected file:

~~~
$ cat functions.py
~~~
{: .bash}

~~~
def sum_function(list):
    """
<<<<<<< HEAD
    A method which takes a list as an argument and
    returns the sum as a floating point number.
=======
    A function which takes a list of integers and floating point 
    numbers as an argument and returns the sum of them as a float.
>>>>>>> dabb4c8c450e8475aee9b14b4383acc99f42af1d

    Parameters
    ----------
    list: list
        Must be floats or ints
~~~
{: .output}

Our change is preceded by `<<<<<<< HEAD`.
Git has then inserted `=======` as a separator between the conflicting changes
and marked the end of the content downloaded from GitHub with `>>>>>>>`.
(The string of letters and digits after that marker
identifies the commit we've just downloaded.)

It is now up to us to edit this file to remove these markers
and reconcile the changes.
We can do anything we want: keep the change made in the local repository, keep
the change made in the remote repository, write something new to replace both,
or get rid of the change entirely.
Let's change it to use the first one:

~~~
$ cat functions.py
~~~
{: .bash}

~~~
def sum_function(list):
    """
    A method which takes a list as an argument and
    returns the sum as a floating point number.

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

To finish merging,
we add `functions.py` to the changes being made by the merge
and then commit:

~~~
$ git add functions.py
$ git status
~~~
{: .bash}

~~~
On branch master
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:

	modified:   functions.py

~~~
{: .output}

~~~
$ git commit -m "Merge changes from GitLab"
~~~
{: .bash}

~~~
[master 2abf2b1] Merge changes from GitLab
~~~
{: .output}

Now we can push our changes to GitLab:

~~~
$ git push origin master
~~~
{: .bash}

~~~
Counting objects: 10, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 697 bytes, done.
Total 6 (delta 2), reused 0 (delta 0)
To https://gitlab.bham.ac.uk/elvidgsm-dasp/planets-pepperr.git
   dabb4c8..2abf2b1  master -> master
~~~
{: .output}

Git keeps track of what we've merged with what,
so we don't have to fix things by hand again
if we or a collaborator pulls again the repository:

~~~
$ git pull origin master
~~~
{: .bash}

~~~
remote: Counting objects: 10, done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 6 (delta 2), reused 6 (delta 2)
Unpacking objects: 100% (6/6), done.
From https://github.com/vlad/planets
 * branch            master     -> FETCH_HEAD
Updating dabb4c8..2abf2b1
Fast-forward
 functions.py | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
~~~
{: .output}

We get the merged file:

~~~
$ cat functions.py
~~~
{: .bash}

~~~
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
We removed the conflict on this line
~~~
{: .output}

We don't need to merge again because Git knows someone has already done that.

Git's ability to resolve conflicts is very useful, but conflict resolution
costs time and effort, and can introduce errors if conflicts are not resolved
correctly. If you find yourself resolving a lot of conflicts in a project,
consider these technical approaches to reducing them:

- Pull from upstream more frequently, especially before starting new work
- Use topic branches to segregate work, merging to master when complete
- Make smaller more atomic commits
- Where logically appropriate, break large files into smaller ones so that it is
  less likely that two authors will alter the same file simultaneously

Conflicts can also be minimized with project management strategies:

- Clarify who is responsible for what areas with your collaborators
- Discuss what order tasks should be carried out in with your collaborators so
  that tasks expected to change the same lines won't be worked on simultaneously
- If the conflicts are stylistic churn (e.g. tabs vs. spaces), establish a
  project convention that is governing and use code style tools (e.g.
  `htmltidy`, `perltidy`, `rubocop`, etc.) to enforce, if necessary

