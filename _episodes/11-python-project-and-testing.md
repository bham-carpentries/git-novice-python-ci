---
title: Setting up a Python project
teaching: 25
exercises: 0
questions:
- "How should I structure a Python project?"
- "How can I test my code to prevent bugs?"
objectives:
- "Make our repository follow a 'standard' Python project format"
- "Add a test and testing framework"
- "Run the tests and a linter on GitLab - using a branch and a Pull Request"
keypoints:
- "While there is often variation, most Python projects follow a similar structure for their code"
- "Doing so is beneficial because it allows components of your code to be reused more easily by yourself and others"
- "Testing can be 'automatic' rather than manual. This catches many issues before they become a problem - this is continuous integration"
- "The concepts here can be used for all programming languages - not just Python - and are pretty much universally used by professional software developers"
---

Most Python projects are structured in a similar way. There are very good reasons for this - if you follow the 'standard', other people who approach your code will recognise parts of it and will know by default how to install your code, run any tests that might exist, and where to look for source code or to change things like the dependencies that are required.
 
~~~
$ git clone
~~~
{: .bash}