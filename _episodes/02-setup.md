---
title: Setting Up Git
teaching: 5
exercises: 0
questions:
- "How do I get set up to use Git?"
objectives:
- "Configure `git` the first time it is used on a computer."
- "Understand the meaning of the `--global` configuration flag."
keypoints:
-   "Use `git config` with the `--global` option to configure a user name, email address, editor, and other preferences once per machine."
---

When we use Git on a new computer for the first time,
we need to configure a few things. Below are a few examples
of configurations we will set as we get started with Git:

*   our name and email address,
*   what our preferred text editor is,
*   and that we want to use these settings globally (i.e. for every project).

On a command line, Git commands are written as `git verb`,
where `verb` is what we actually want to do. So here is how
Dracula sets up his new laptop:

~~~
$ git config --global user.name "Vlad Dracula"
$ git config --global user.email "vlad@tran.sylvan.ia"
~~~
{: .bash}

Please use your own name and email address instead of Dracula's. This user name and email will be associated with your subsequent Git activity,
which means that any changes pushed to
[GitHub](https://github.com/),
[BitBucket](https://bitbucket.org/),
[GitLab](https://gitlab.com/) or
another Git host server
in a later lesson will include this information.

> ## Line Endings
>
> As with other keys, when you hit <kbd>Return</kbd> on your keyboard,
> your computer encodes this input as a character.
> For reasons that are long to explain, different operating systems
> use different character(s) to represent the end of a line.
> (You may also hear these referred to as newlines or line breaks.)
> Because Git uses these characters to compare files,
> it may cause unexpected issues when editing a file on different machines.
>
> You can change the way Git recognizes and encodes line endings
> using the `core.autocrlf` command to `git config`.
> The following settings are recommended:
>
> On macOS and Linux:
>
> ~~~
> $ git config --global core.autocrlf input
> ~~~
> {: .bash}
>
> And on Windows:
>
> ~~~
> $ git config --global core.autocrlf true
> ~~~
> {: .bash}
> 
> You can read more about this issue 
> [on this GitHub page](https://help.github.com/articles/dealing-with-line-endings/).
{: .callout}

For these lessons, we will be interacting with the University of Birmingham's [GitLab](https://gitlab.com/) service, and so you should use your University account to log in. The ability to add external collaborators is not a problem, as you can invite people to use this with their personal e-mail address.If you/they elect to use a private email address with GitLab, then use that same email address for the `user.email` value, e.g. `username@users.noreply.gitlab.com` replacing `username` with your GitLab one. You can change the email address later on by using the `git config` command again.

Sometimes, operations in Git will require the opening of a text editor. You can choose your favourite editor, by copying and pasting the relevant command below, though I will demonstrate this course using "nano". 

| Editor             | Configuration command                            |
|:-------------------|:-------------------------------------------------|
| Atom | `$ git config --global core.editor "atom --wait"`|
| nano               | `$ git config --global core.editor "nano -w"`    |
| BBEdit (Mac, with command line tools) | `$ git config --global core.editor "bbedit -w"`    |
| Sublime Text (Mac) | `$ git config --global core.editor "/Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl -n -w"` |
| Sublime Text (Win, 32-bit install) | `$ git config --global core.editor "'c:/program files (x86)/sublime text 3/sublime_text.exe' -w"` |
| Sublime Text (Win, 64-bit install) | `$ git config --global core.editor "'c:/program files/sublime text 3/sublime_text.exe' -w"` |
| Notepad++ (Win, 32-bit install)    | `$ git config --global core.editor "'c:/program files (x86)/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"`|
| Notepad++ (Win, 64-bit install)    | `$ git config --global core.editor "'c:/program files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"`|
| Kate (Linux)       | `$ git config --global core.editor "kate"`       |
| Gedit (Linux)      | `$ git config --global core.editor "gedit --wait --new-window"`   |
| Scratch (Linux)       | `$ git config --global core.editor "scratch-text-editor"`  |
| Emacs              | `$ git config --global core.editor "emacs"`   |
| Vim                | `$ git config --global core.editor "vim"`   |

It is possible to reconfigure the text editor for Git whenever you want to change it.

> ## Exiting Vim
>
> Note that Vim is the default editor for many programs. If you haven't used Vim before and wish to exit a session without saving
your changes, press <kbd>Esc</kbd> then type `:q!` and hit <kbd>Return</kbd>.
> If you want to save your changes and quit, press <kbd>Esc</kbd> then type `:wq` and hit <kbd>Return</kbd>.
{: .callout}

The four commands we just ran above only need to be run once: the flag `--global` tells Git
to use the settings for every project, in your user account, on this computer.

You can check your settings at any time:

~~~
$ git config --list
~~~
{: .bash}

You can change your configuration as many times as you want: just use the
same commands to choose another editor or update your email address.

> ## Git Help and Manual
>
> Always remember that if you forget a `git` command, you can access the list of commands by using `-h` and access the Git manual by using `--help` (though practically, this is sometimes not very helpful...):
>
> ~~~
> $ git config -h
> $ git config --help
> ~~~
> {: .bash}
{: .callout}

[git-privacy]: https://help.github.com/articles/keeping-your-email-address-private/
