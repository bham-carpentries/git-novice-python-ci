---
title: Creating a Repository
teaching: 10
exercises: 0
questions:
- "Where does Git store information?"
objectives:
- "Create a local Git repository."
keypoints:
- "`git init` initializes a repository."
- "Git stores all of its repository data in the `.git` directory."
---

Once Git is configured, we can start using it.

We will create a Python project called 'planets'.

First, let's create a directory in `Desktop` folder for our work and then move into that directory:

~~~
$ cd ~/Desktop
$ mkdir planets
$ cd planets
~~~
{: .bash}

When we are here, we're using 'planets' as our current working directory. We can check our current working directory at any time with:

~~~
$ pwd
/home/pepperr/Desktop/planets
~~~

We need to tell Git to make `planets` a [Git repository]({{ page.root }}/reference/#repository)—a place where
Git can store versions of our files:

~~~
$ git init
~~~
{: .bash}

If we use `ls` to show the directory's contents,
it appears that nothing has changed:

~~~
$ ls
~~~
{: .bash}

But if we add the `-a` flag which shows everything including hidden files,
we can see that Git has created a hidden directory within `planets` called `.git`:

~~~
$ ls -a
~~~
{: .bash}

~~~
.	..	.git
~~~
{: .output}

Git uses this special sub-directory to store all the information about the project, 
including all files and sub-directories located within the project's directory.
If we ever delete the `.git` sub-directory,
we will lose the project's history.

We can check that everything is set up correctly
by asking Git to tell us the status of our project:

~~~
$ git status
~~~
{: .bash}
~~~
# On branch master
#
# Initial commit
#
nothing to commit (create/copy files and use "git add" to track)
~~~
{: .output}

If you are using a different version of `git`, the exact
wording of the output might be slightly different.

> ## Places to Create Git Repositories
>
> Along with tracking information about planets (the project we have already created), 
> you might also like to track information about moons.
> You *could* create a `moons` project inside your `planets` 
> project with the following sequence of commands:
>
> ~~~
> $ cd ~/Desktop   # return to Desktop directory
> $ cd planets     # go into planets directory, which is already a Git repository
> $ ls -a          # ensure the .git sub-directory is still present in the planets directory
> $ mkdir moons    # make a sub-directory planets/moons
> $ cd moons       # go into moons sub-directory
> $ git init       # make the moons sub-directory a Git repository
> $ ls -a          # ensure the .git sub-directory is present indicating we have created a new Git repository
> ~~~
> {: .bash}
>
> Is the `git init` command, run inside the `moons` sub-directory, required for 
> tracking files stored in the `moons` sub-directory?
> 
> > ## Solution
> >
> > No, you do not need to make the `moons` sub-directory a Git repository 
> > because the `planets` repository will track all files, sub-directories, and 
> > sub-directory files under the `planets` directory.  Thus, in order to track 
> > all information about moons, you only needed to add the `moons` sub-directory
> > to the `planets` directory.
> > 
> > Additionally, Git repositories can interfere with each other if they are "nested":
> > the outer repository will try to version-control
> > the inner repository. Therefore, it's best to create each new Git
> > repository in a separate directory. To be sure that there is no conflicting
> > repository in the directory, check the output of `git status`. If it looks
> > like the following, you are good to go to create a new repository as shown
> > above:
> >
> > ~~~
> > $ git status
> > ~~~
> > {: .bash}
> > ~~~
> > fatal: Not a git repository (or any of the parent directories): .git
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}
> ## Correcting `git init` Mistakes
> If you have a redundant nested repository, it is redundant and may cause confusion
> down the road. You would like to remove the nested repository. How can you undo 
> his last `git init` in the `moons` sub-directory?
>
> > ## Solution -- USE WITH CAUTION!
> >
> > To recover from this little mistake, you can just remove the `.git`
> > folder in the moons subdirectory by running the following command from inside the `planets` directory:
> >
> > ~~~
> > $ rm -rf moons/.git
> > ~~~
> > {: .bash}
> >
> > But be careful! Running this command in the wrong directory, will remove
> > the entire Git history of a project you might want to keep. Therefore, always check your current directory using the
> > command `pwd`.
> {: .solution}
{: .challenge}
