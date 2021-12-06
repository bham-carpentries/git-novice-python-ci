---
title: Collaborating - Branching and Pull Requests
teaching: 25
exercises: 0
questions:
- "How can I use version control to collaborate with other people more effectively?"
objectives:
- "Create a branch"
- "Push the branch to a repository"
- "Make a pull request to the repository"
keypoints:
- "`git checkout -b branchname` creates a branch that you can work on a set of changes"
- "`git checkout branchname` switches between branches"
- "Creating pull requests is the way most people work with Git and is good practice"
- "Before pull requests can be merged, there must be no merge conflicts"
---

Often, we want to work on a set of changes that are more complicated than what was shown in the last lesson, and without affecting other people's work. Think for example, what would happen if I made a change to code that someone else was using, but left it in a broken state. They would probably not be very happy with me! To this effect, we can use a concept called 'branches' to separate works-in-progress from the known 'good' copy of the code. In general, it's considered good practice to create a branch for every piece of work that you do, and to merge these into the 'good' version regularly.

To create a new branch, run the following command in your repository:
 
~~~
$ git checkout -b add-square-array-method
~~~
{: .bash}
~~~
Switched to a new branch 'add-square-array-method'
~~~
{: .output}

This creates a separate area for us to work in and add changes. It's a bit like how we cloned the repository in a separate place in the last lesson. However, we can also push our branch to the remote repository and keep it backed up.

We'll add a function that takes in a list, and squares all of the elements in it, returning a new array:
~~~
$ nano functions.py
$ tail -n 2 functions.py
~~~
{: .bash}

~~~
def square_array(list):
    return [item*item for item in list]
~~~
{: .output}

Then we'll commit it as normal:
~~~
$ git add functions.py
$ git commit -m "Add a method that squares a list"
~~~
{: .bash}

~~~
[add-square-array-method ea4141e] Add a method that squares a list
 1 file changed, 4 insertions(+)
~~~
{: .output}

Notice now that instead of saying 'master' here, it says 'add-square-array-method', showing us that our commit is on our branch. We've sort of glossed over it previously, but 'master' is the "default branch" in Git. In some newer git versions this has been renamed to "main", so you may see this instead.

Our commit is now saved in our local repository. If you want to, you can switch back to the "master" branch by doing:

~~~
git checkout master
~~~
{: .bash}
~~~
Switched to branch 'master'
~~~
{: .output}

If you now print the file, you'll see that our new method isn't there:

~~~
cat functions.py
~~~
{: .bash}
~~~

Then push the change to the *Owner's repository* on GitHub:

~~~
$ git push origin master
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


def sum_product(list):
    product = 1.0
    for item in list:
        product *= item
    return product
~~~
{: .output}

