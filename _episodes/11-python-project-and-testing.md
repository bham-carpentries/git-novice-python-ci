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
 
Generally, at a minimum, a Python project has the following structure:

~~~
planets/
  planets/
    functions.py
    __init__.py   # Often this is a 'blank' file.
  setup.py
  requirements.txt
  README.md
~~~

We'll take these elements one at a time:

# planets/
Inside the project, we normally have a folder which matches the name of the Python module, so that the module can be imported with:
~~~
import planets
~~~
{: .python}
You can see this for e.g. in the source repository of the [NumPy library](https://github.com/numpy/numpy).

Within this folder, we can store code files (e.g. functions.py) or further subdirectories. These will then be importable too.

## __init__.py
The __init__.py file is effectively as set of instructions that get run when you import a Python module. So with a blank __init__.py, nothing happens if you run `import planets` in a Python session. What is common is to import certain methods into the top level of the module, for e.g.:

~~~
from .functions import sum_function
~~~
{: .python}

Then, in a Python session, you would be able to do the following:

~~~
>>> import planets
>>> planets.sum_function([1, 2, 3, 4])
10
~~~
{: .python}