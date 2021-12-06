---
layout: lesson
root: .
---

You might be a researcher, PhD student or something else that has to work with software. You'll often have to work on a set of software or documents in collaboration with other people, often at the same time. If you do this naively, like working on Dropbox, or Google Drive, you can often run into problems. If you take it in turns, you end up taking a lot of time waiting to finish. Working on your own copies and then e-mailing changes back and forth is inelegant and can lead to things being lost, overwritten or duplicated. 

A way of working around this is to use [version control]({{ page.root }}/reference/#version-control) to
manage your work. Version control is better than mailing files back and forth:

*   Nothing that is committed to version control is ever lost, unless
    you work really, really hard at it. Since all old versions of
    files are saved, it's always possible to go back in time to see
    exactly who wrote what on a particular day, or what version of a
    program was used to generate a particular set of results.

*   As we have this record of who made what changes when, we know who to ask
    if we have questions later on, and, if needed, revert to a previous
    version, much like the "undo" feature in an editor.

*   When several people collaborate in the same project, it's possible to
    accidentally overlook or overwrite someone's changes. The version control
    system automatically notifies users whenever there's a conflict between one
    person's work and another's.

Teams are not the only ones to benefit from version control: lone
researchers can benefit immensely.  Keeping a record of what was
changed, when, and why is extremely useful for all researchers if they
ever need to come back to the project later on (e.g., a year later,
when memory has faded). This is especially useful if, for e.g. you write
a paper in the first year of your PhD, and need to reuse the data and
regenerate a figure slightly differently for your thesis, such as to 
incorporate new data, change the style, etc.

Version control is the lab notebook of the digital world: it's what
professionals use to keep track of what they've done and to
collaborate with other people.  Every large software development
project relies on it, and most programmers use it for their small jobs
as well.  And it isn't just for software: books,
papers, small data sets, and anything that changes over time or needs
to be shared can and should be stored in a version control system.

> ## Prerequisites
>
> In this lesson we use Git from the Unix Shell, and we expect trainees to be famliar with Python.
> Some previous experience with the shell is expected.
{: .prereq}

