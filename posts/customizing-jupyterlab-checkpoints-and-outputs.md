<!--
.. title: JupyterLab - Multiple outputs and checkpoints
.. slug: jupyterlab-multiple-outputs-and-checkpoints
.. date: 2019-06-30 06:40:12 UTC
.. tags: Jupyter Lab, Python
.. category: 
.. link: 
.. description: 
.. type: text
-->

[Jupyter Lab](https://jupyterlab.readthedocs.io/en/stable/) is an excellent tool for data analysis. However, there are two default settings that, in my opinion, are a bit annoying. <!-- TEASER_END -->

## 1. Multiple outputs <sup>[\[1\]](https://ipython.org/ipython-doc/dev/config/intro.html)[\[2\]](https://stackoverflow.com/questions/36786722/how-to-display-full-output-in-jupyter-not-only-last-result)</sup>
The first one is that it is not possible to show multiple outputs from a cell using the default settings. This can be fixed in at least two ways. The easiest solution is to put the following code in a cell in the notebook:

```python
from IPython.core.interactiveshell import InteractiveShell

InteractiveShell.ast_node_interactivity = "all"
```
This is a good solution but it must be done in **every** notebook, i.e. it is not a global setting. If you want this to apply to all notebooks you create you must do the following:

1. Generate an ipython config file by running
   ```console
   ipython profile create
   ```
   Two files, *ipython_config.py*, and *ipython_kernel_config.py* are created in the *.ipython* folder in your home folder. On Linux, the full path is probably something like this: *~/.ipython/profile_default/*. On Windows, the path probably looks something like this: *C:\Users\my_account\\.ipython\profile_default*.
2. Open the *ipython_config.py* file in a text editor of your choice. Look for *#c.InteractiveShell.ast_node_interactivity = 'last_expr'*. At the time of writing this option was at row 147.
3. Remove the *#* and replace *last_expr* with *all*. Now jupyter always show multiple outputs.

## 2. Checkpoints <sup>[\[3\]]([hej](https://stackoverflow.com/questions/32625939/ipython-notebook-where-is-jupyter-notebook-config-py-in-mac))[\[4\]]([då](https://stackoverflow.com/questions/51887758/is-there-a-way-to-disable-saving-to-checkpoints-for-jupyter-notebooks))</sup>
The second one is that when you create a notebook Jupyter creates a folder in the current working directory called *.ipynb_checkpoints*. In this folder, a checkpoint file is stored. I do not mind checkpoints per se, but I do not want it in my current working directory. Below I show how to specify a separate folder to store all checkpoint files.

1. Generate a jupyter config file by running 
   ```console
   jupyter notebook --generate-config
   ```
   One file, *jupyter_notebook_config.py*, is created in the *.jupyter* folder in your home folder. On Linux, the full path is probably something like this: *~/.jupyter*. On Windows, the path probably looks something like this: *C:\Users\my_account\\.jupyter*.
2. Open the *jupyter_notebook_config.py* file in an text editor of your choice and write the following:
   ```python
   c.FileCheckpoints.checkpoint_dir = "/full/path/to/where/you/want/to/save/checkpoints"
   ```

[1] https://ipython.org/ipython-doc/dev/config/intro.html

[2] https://stackoverflow.com/questions/36786722/how-to-display-full-output-in-jupyter-not-only-last-result

[3] https://stackoverflow.com/questions/32625939/ipython-notebook-where-is-jupyter-notebook-config-py-in-mac

[4] https://stackoverflow.com/questions/51887758/is-there-a-way-to-disable-saving-to-checkpoints-for-jupyter-notebooks


