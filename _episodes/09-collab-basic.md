---
title: Collaborating - Basic
teaching: 25
exercises: 0
questions:
- "How can I use version control to collaborate with other people?"
objectives:
- "Clone a remote repository."
- "Collaborate pushing to a common repository."
- "Describe the basic collaborative workflow."
keypoints:
- "`git clone` copies a remote repository to create a local repository with a remote called `origin` automatically set up."
---

To mimic collaborating with other people, please open a second terminal window.
This window will represent your collaborator, working on another computer.

The 'Collaborator' needs to download a copy of the Owner's repository to her
 machine. This is called "cloning a repo". To clone the Owner's repo, enter
 the following into the second terminal window:
 
~~~
$ git clone https://gitlab.bham.ac.uk/elvidgsm-dasp/planets-pepperr.git ~/Desktop/planets-pepperr.git
~~~
{: .bash}

Replace the URL with your own one. You can now make changes to this completely separate version of the repository
to model another collaborator working on it. So just as you've done before, add a change to the file - write a new Python functon at the bottom that computes a product

~~~
$ cd ~/Desktop/planets-pepperr.git
$ nano functions.py
$ tail -n 5
~~~
{: .bash}

~~~
def sum_product(list):
    product = 1.0
    for item in list:
        product *= item
    return product
~~~
{: .output}

~~~
$ git add functions.py
$ git commit -m "Add a product method to functions.py"
~~~
{: .bash}

~~~
 1 file changed, 7 insertions(+)
 create mode 100644 pluto.txt
~~~
{: .output}

Then push the change to the *Owner's repository* on GitHub:

~~~
$ git push origin master
~~~
{: .bash}

~~~
Counting objects: 4, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 306 bytes, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://gitlab.bham.ac.uk/elvidgsm-dasp/planets-pepperr.git
   9272da5..29aba7c  master -> master
~~~
{: .output}

Note that we didn't have to create a remote called `origin`: Git has already
setup this as default from the original `clone` that we did.

Take a look at thes repository on the GitLab website now (maybe you need
to refresh your browser.) You should be able to see the new commit made by the
'Collaborator' (though in this case it's still you!).

To download the changes from GitLab, switch back to your original terminal and enter::

~~~
$ git pull origin master
~~~
{: .bash}

~~~
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0)
Unpacking objects: 100% (3/3), done.
From https://gitlab.bham.ac.uk/elvidgsm-dasp/planets-pepperr.git
 * branch            master     -> FETCH_HEAD
Updating 9272da5..29aba7c
Fast-forward
 pluto.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 pluto.txt
~~~
{: .output}

Now the three repositories (Owner's local, Collaborator's local, and Owner's on
GitLab) are back in sync.

> ## A Basic Collaborative Workflow
>
> In practice, it is good to be sure that you have an updated version of the
> repository you are collaborating on, so you should `git pull` before making
> our changes. The basic collaborative workflow would be:
>
> * update your local repo with `git pull origin master`,
> * make your changes and stage them with `git add`,
> * commit your changes with `git commit -m`, and
> * upload the changes to GitHub with `git push origin master`
>
> It is better to make many commits with smaller changes rather than
> of one commit with massive changes: small commits are easier to
> read and review.
{: .callout}

> ## Comment Changes in GitLab
>
> The Collaborator has some questions about one line change made by the Owner and
> has some suggestions to propose.
>
> With GitLab, it is possible to comment the diff of a commit. Over the line of
> code to comment, a blue comment icon appears to open a comment window.
>
> The Collaborator posts its comments and suggestions using GitLab interface.
{: .challenge}

> ## Version History, Backup, and Version Control
>
> Some backup software can keep a history of the versions of your files. They also
> allows you to recover specific versions. How is this functionality different from version control?
> What are some of the benefits of using version control, Git and GitLab?
{: .challenge}
