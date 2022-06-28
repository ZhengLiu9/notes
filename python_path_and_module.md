This document aims to provide a basic review of how and why we should structure our codebase when packaging python codes into modules/libraries. Specifically, we will go through:

* how path is determined in python, and 
* how modules are imported

## How path is determined in python

In python, modules/packages are imported via `import the_module` command. During importing, python will search for `the_module` (either as a folder, or as a .py file) in the following three locations:

* The *Current Working Directory*
* The folders specified in `PYTHONPATH` environment variable
* The directory holding installed packages (e.g. If you use `pip` to install packages, they will be installed in the `site-packages`  folder inside the lib folder of virtual environment).

For any active python kernel, you can check those three locations in `sys.path`. Among those three, the definition of *Current Working Directory* is the most confusing, and we try to explain as follows:

Suppose we have the following folder structure, and we are currently in `parent` folder.

```
parent
|- folder1
   |- __init__.py
   |- script1.py
```

1. When you run python as a script, e.g.  `python folder1/script1.py`, the *Current Working Directory* is the folder where the `script1.py` stays. In this example, it is the `folder1`.
2. When you run python as a module `python -m folder1.script1` , or directly through a string of commands `python -c "import folder1.script1"`, the *Current Working Directory* is where the command is executed. In this example, it is the `parent`.
3. The `os.getcwd()` will always give you the directory where `python` is executed. In both of the above two examples, it is the `parent`. But as we see above, this location is not necessary to be the same as *Current Working Directory*.
