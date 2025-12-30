---
title: Atom IDE Installation Guide
toc: true
breadcrumbs: false
date: 2022-04-29
---

{{< callout type="caution" >}}
Atom has been officially sunset and is no longer maintained. I do not recommend following this guide for new setups — prefer modern, actively maintained editors such as [VS Code](https://code.visualstudio.com/). This post is retained for archival purposes (it never migrated from my old site); I originally wrote it to help move my research group off vim — they now use VS Code.
{{< /callout >}}

## What is Atom?
*Atom* is a hackable text editor created by GitHub

## Why Atom?
A dedicated code editor offers many advantages over pure command-line editors (vim, emacs) or SSH clients (MobaXterm, PuTTY)
- modern editing tools are *magic*
  - code completion, customizable shortcuts, etc.
  - if you're really attached to vim/emacs, you can still use those within Atom as well!
- highly customizable, well documented
- ability to easily run/debug code and manage files within your editor

Why specifically Atom, over other alternatives like [VS Code](https://code.visualstudio.com/) or [Sublime](https://www.sublimetext.com/)?
- completely free
- thousands of open-source packages
- convenient Git integration for version control

Even if you prefer one of these options over Atom, it's a major improvement over slow, rigid tools like MobaXterm and its default text editor.

{{< callout type="caution" >}}
I've only learned about many of these topics in the past few months, and I'm by no means an expert. I just wanted to make a tutorial to document a system for remote access and editing in the clusters. If I find out that something implemented here isn't best practices, I'll change it. If I find there are vulnerabilities, I'll update it and notify anyone who's used this tutorial.
{{< /callout >}}

# Installation

## Inital setup

- Download and run the installer from [https://atom.io/](https://atom.io/)

{{< callout type="note" >}}
This tutorial is done on Windows using Atom 1.60.0. OS X/Linux or different Atom versions may differ slightly
{{< /callout >}}

One of the first things to do after installing Atom would be set up your workspace.

Atom uses **projects** to manage different workspaces. For example, you might have a project for [Bell](https://www.rcac.purdue.edu/compute/bell), another for [nanoHUB](https://nanohub.org/), and another for local runs.

- After opening Atom, create a new project by clicking **Open a Project** on the right pane
- Choose (or create) a folder where you want your workspace to be stored
- For this example, we'll create a new folder called 'Gilbreth' we'll use to connect to the [Gilbreth cluster](https://www.rcac.purdue.edu/compute/gilbreth)

# Creating a git repository

If you've never used Git before, it's a tool used for version control. Instead of only saving the most recent version of each file, Git can track its history.

{{< callout type="caution" >}} 
Why go through the hassle of Git?
It's a fail safe - if your code breaks something, or files become corrupted, Git can save the day
{{< /callout >}}

While this tutorial will focus on individual uses of Git, it's primary appeal is as a coding collaboration tool. To learn more about why Git is useful, see the explanation provided [here](https://www.practicaldatascience.org/html/git_and_github.html). In short, here's a few relevant terms useful to know
- **repository**: The location where all of your files and changes are stored. Rather than just a folder, think of it as a history of different states of your folder
- **stage**: After editing a file, you can *stage* the changes you made to indicate that you want them tracked. There are some changes which you don't want to track (passwords, API keys, large files)
- **commit**: To *commit* adds all of the staged changes to your repository, saving this state
- **push**: To tell your repository that this commit/series of commits is the most updated version of your code
- **pull**: To *pull* is to take the latest pushed commit and update your files to reflect these changes. While it doesn't have a huge meaning here, when working on teams it's essential for sharing code.

## Setting up a Git Repository
In the last step, we created a new project called 'Gilbreth,' now we'll initialize a Git repository in this directory. Press `CTRL-SHIFT-8` to open the GitHub panel.

- Click 'Login' and continue
- Copy the OAuth token to Atom to login
- Click 'Initialize and publish on GitHub'
- Enter a repository name and set visibility (most likely private)

In addition, we want to set up the Git panel, which we open using `CTRL-SHIFT-9`.
- Enter your name and email address
- If you intend to use this login for all repositories, click 'Use for all repositories'

You should now see a panel with three sections: unstaged changes, staged changes, and commit message. This will keep track of the changes you make and allow you to push them to Git.

{{< callout type="note" >}}
Any changes you don't with to track on Git can be untracked by creating a file named '.gitgnore' and adding these file names (i.e. test.py or outVASP)
{{< /callout >}}

Create the .gitignore file by selecting the 'Gilbreth' folder in the left pane and pressing `a`, then type '.gitignore' and add whichever files names you don't want to track

We can now make an initial commit

- In the Git panel, press 'Stage All' to stage your changes (creating the .gitignore file)
- Add a Commit message in the text box below, describing the changes this commit contains
- Click 'Create detached commit'
- Click 'Publish' to set up a remote tracking branch

Congrats! You should be able to view your repository on GitHub, and have the system in place to stage, commit, and push your changes from within Atom.

{{< callout type="note" >}}
Atom has some pretty cool integrations with Git. See which changes were made between commits, merge branch conflicts, easily switch between branches, etc.
{{< /callout >}}

# Remote FTP
Atom describes itself as a 'hackable' text editor because it has thousands of community-made packages which greatly extend the utility of Atom. We're now going to install some useful packages

**Remote FTP** is a package that transfers files between local and remote servers. This is useful when connecting to RCAC clusters or nanoHUB. In this exmaple, we'll demonstrate how to connect to the Gilbreth cluster.

Press `CTRL + ,` to open the Settings menu. From here, click 'Install.' This lets you query and install packages for Atom.

Locate and install the 'remote-ftp' package (by icetee). After it's done installing, you can select 'Packages → Remote FTP → Toggle' from the menu bar. This will open a new tab in your left pane.

{{< callout type="note" >}}
The left tab labeled 'project' is your local project folder - the right 'remote' tab is your remote file manager. Remote FTP will sync any remote changes locally
{{< /callout >}}
To connect to the  Gilbreth cluster, we need to create an .ftpconfig file. This is done by selecting 'Packages → Remote FTP → Create SFTP config file'

In this file, there are a few settings we need to change.
- host: 'gilbreth.rcac.purdue.edu'
- user: '[[YOUR USERNAME]]'
- pass: '[[YOUR PASSOWRD]]' (we'll set up SSH keys later)
- remote: 'home/[[YOUR USERNAME]]'

{{< callout type="caution" >}}
Add '.ftpconfig' to your .gitignore file! You should never commit your .ftpconfig file, it contains your password
{{< /callout >}}
TODO: write a more complete SSH key setup guide (Atom is a lil janky to set up)

With this setup, you'll still have to use 2FA each time you connect. Following the guide [here](https://www.rcac.purdue.edu/knowledge/scholar/accounts/login/sshkeys), you can connect without 2FA

# Platformio IDE Terminal

In addition to managing and editing files, it's often useful to have a command line interface directly connected to the clusters. For this, we'll use a package called **platformio-ide-terminal**

Similarly to Remote FTP, search for this package in settings and install

{{< callout type="note" >}}
Ensure that you are installing the correct *terminal* package, not the other platformio-ide tools (though those can be useful as well)
{{< /callout >}}

To automatically connect to a cluster by default, open Settings (`CTRL + ,`), then select 'Packages → platformio-ide-terminal → Settings'. Within these settings, set 'Auto Run Command' to your ssh connection line. For example,

    ssh [[YOUR USERNAME]]@gilbreth.rcac.purdue.edu

{{< callout type="note" >}}
If you set up SSH keys in the previous step, those should let you connect automatically without the need of a password or 2FA
{{< /callout >}}

If you want to files in the cluster directly from the Atom editor, change your SSH command to use port-forwarding, as below

    ssh -L[[1234]]:localhost:[[1234]] [[YOUR USERNAME]]@gilbreth.rcac.purdue.edu

Where [[1234]] is some arbitrary 4-digit number you'll use as a port

{{< callout type="note" >}}
Within these same settings, you can assign some shortcuts to phrases you type a lot (squeue ..., cd /scratch..., etc.). You can assign these shortcuts to hotkeys using the 'keybindings' section under settings
{{< /callout >}}

# Hydrogen

**Hydrogen** is an Atom package which lets you run Jupyter-like Python files within your Atom editor. This gives you the benefits of instantaneous code feedback, without being restricted by clunky Jupyter Notebooks.

Installation is similar to the previous steps - search for 'Hydrogen' (by nteract) and install.

## Running local Python files
To run Hydrogen kernels locally, you'll need to install [Python](https://www.python.org/downloads/). After installing Python, install the ipykernel package locally

    pip install ipykernel
    python -m ipykernel install

Let's start by testing out Hydrogen using a simple python file. In your Gilbreth directory, create a new file called **hydrogen.py**

{{< callout type="caution" >}}
If you edit a file in your remote directory, you'll be editing a local copy that updates the remote copy when you save. Therefore, when running local Hydrogen kernels, you won't have access to the cluster's environment or file system.
{{< /callout >}}

Hydrogen uses Python (.py) files to simulate Jupyter Notebooks. Similarly, it has markdown and code cells, which can be separated in the following way

    # %% markdown

    This is the content of the Markdown cell. $$H|\psi\rangle = E|\psi\rangle$$

    # %% codecell

    fish = 2+2
    print("Wow Kat, thank you for writing this tutorial!")

Try copying the above cells into your **hydrogen.py** file, and typing `ALT-SHIFT-ENTER`. This should run the cell your cursor is in, then move down to the next cell

This system takes a little getting used to, but it's essentially equivalent to cells in Jupyter notebooks

## Running remote Python files

Running files locally is cool, but it's often desired to run Python files directly in the cluster.

1. Connect to a cluster using ssh port forwarding (this should be done from the previous step)

```python
ssh -L[[1234]]:localhost:[[1234]] [[YOUR USERNAME]]@gilbreth.rcac.purdue.edu
```

2. Setup config file in the cluster (you can do this using the platformio-ide-terminal)

```python
pip install jupyter
jupyter notebook --generate-config
```

{{< callout type="caution" >}}
By default, the RCAC clusters use Python v2.7.5. Yuck, but it's as simple as typing **module load anaconda** to use a newer version. If you add 'module load anaconda' to a file named '.bashrc' in your home directory, it will automatically load anaconda every time you connect
{{< /callout >}}

3. In config file (~/.jupyter/jupyter_notebook_config.py), uncomment

```
    #c.NotebookApp.token = ''
```
and set the string to some arbitrary phrase (i.e. 'katnyp')

4. Run a Jupyter server using

```python
jupyter notebook --port=[[1234]] --no-browser
```

You should now see a Jupyter Notebook server running in the terminal!

{{< callout type="note" >}}
If you're using multiple terminals, this will only work on the first connection you make. This shell will now be 'unusable', but you can just open a new terminal and use that
{{< /callout >}}

5. If you just want to use your local Jupyter in-browser in the cluster environment, copy the output of the previous command into a browser

```python
# it should look something like this
http://127.0.0.1:[[1234]]/?token=...
```

This is Jupyter notebook server connected to the RCAC clusters. Cool! But we want more, we want it *within Atom*

6. From Hydrogen package settings, set 'Kernel Gateways' to the following

```python
[{
  "name": "Gilbreth",
  "options": {
    "baseUrl": "http://localhost:[[1234]]",
    "token": "[[your chosen token]]"
  }
}]
```

7. To connect, we there's a few steps we need to take.

{{< callout type="note" >}}
Instead of using the Menu bar, we'll introduce the **command palette**. It's a convenient way to access commands within Atom without using the mouse or scrolling through menus.
{{< /callout >}}

To connect to a remote kernel, open the command palette using `CTRL-SHIFT-P`
- type 're k' to select 'Hydrogen: Connect to Remote Kernel'
- select Gilbreth
- choose 'Authenticate with a token'
- type in your chosen token
- choose [new session] (or connect to an existing one)
- choose your desired Python kernel

Congrats, you're now connected to the clusters! As a check, try adding the following code cell to your Python file

```python
# %% codecell
import os
os.getcwd()
```

You should see that you're in the cluster!

# Other useful packages

That's the gist of the tutorial, I hope you found it useful! Feel free to reach out if you have any questions, email or slack works best.

Atom has tons of open-source packages. This is great, but it also means that you need to be careful with installing random packages. I tend to only install packages with large user bases and active communities to check for vulnerabilities.

Cool packages that didn't warrant their own pages:
- **atom-beautify**: adjusts your code to fit proper code formatting standards
- **highlight-selected**: highlights the current word selected (everywhere it appears) when double clicked
- **jumpy**: navigate around your code with dynamic hotkeys
- **minimap**: preview your full code in your scroll bar
- **pp-markdown**: live preview Markdown files (useful for writing this tutorial!)
- **split-diff**: compare differences between two files
- **todo-show**: finds all TODOs, FIXMEs, etc. in your project and compiles them into a list
- **zentabs**: sets a maximum on the number of opened tabs