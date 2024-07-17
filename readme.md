## Git vs GitHub and version control
### New Information
#### What is Git?

![](./images/git_2x.png)

(with apologies to [xkcd.com](https://xkcd.com))

[Git](https://git-scm.com/) is:

- A program you run from the command line
- A distributed version control system

Programmers use Git so that they can keep the history of all the changes to their code. This means that they can rollback changes (or switch to older versions) as far back int time as they started using Git on their project.

A codebase in Git is referred to as a **repository**, or **repo**, for short.

Git was created by [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds), the principal developer of Linux.

#### What is Github?

[Github](https://github.com/) is:

- A hosting service for Git repositories
- A web interface to explore Git repositories
- A social network of programmers
- We all have individual accounts and put our codebases on our Github account
- You can follow users and star your favorite projects
- Developers can access codebases on other public accounts
- GitHub *uses* Git

#### Can you use git without Github?

Yes!

# So how does all of this work?

Git can be somewhat difficult to grasp conceptually. The basics are all you need to get started. With a bit of practice, the basic workflow will become second nature and you will be able to gradually pick up the more advanced features of git, although you don't need to be an expert to take advantage of git as a version control tool.

# Git versus Github

One thing to keep in mind is that we'll be interacting with git on our local machines and Github online. Make sure that you are thinking about 1) where you are (local or on GitHub), and 2) how that relates to other "versions" of that code. It takes some practice, but the more you practice, the easier it will get.

## Staging and Committing

The simplest way to think about git is to imagine it as a series of entries in a journal. Each of those entries is a saved state of the code. As we code, we make frequent saves of that code. We can then go back and return to different versions of the code, see how it has changed from different versions (and who made those changes), and take advantage of a bunch of other benefits.

### Key Concepts

Git operates under a few concepts:

First, we have to consider the *working directory*: git tracks a specific working directory and all folders contained within it. This means that if we navigate out of the root working directory, changes we make are no longer tracked. However, anything within the working directory (and every folder within it) are tracked.

Once we've made some changes that we are happy with, we need to add these to a *staging area* (this is known as the index within git parlance). This indicates to git which files we would like to save the current state of. At this point, nothing has been committed to history yet.

Finally, we want to *commit* the changes to long-term memory. Once we've committed the changes, they are part of the history of our repository forever (except for certain extreme cases).

### What's under the hood?

> What git is actually doing is that instead of saving individual copies of each file, they are saving the difference between each successive version of the file. This helps keep the speed and size of the saved records dramatically but until we commit the changes in our files to the repository, the *HEAD* (most current commit) will not reflect anything new. That said, keeping in mind the fact that a git history is a chain of successive differences between files will help you make sense of various things going on.

### Installation

Let's start by getting some basic stuff installed and ready to go.

#### For Mac Install:

_1) Install Homebrew_

[Homebrew](http://brew.sh/) is a package manager for OS X that installs packages using the command line. It is very useful for us in general. To install it, go to [Homebrew homepage](http://brew.sh/) and run the line of code under the heading "Install Homebrew" in Terminal. As of 7/11/2024, this was the latest:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

_2) Install git_

OS X generally has a (fairly old) installation of git ready to go. However, we want to (re-)install git through homebrew to keep it up to date. To do so, run the following:

```bash
brew install git
```

_3) Set Up a Github Account_

Go to  https://github.com/ and create an account.


#### For Windows Install:

_1) Install Git for Windows_

Go to [Git for Windows](https://git-scm.com/download/win) to start the download. The download should start automatically, but you can select to manually download if it doesn't. Once installed, you should have a program called "GitBash" on your machine. You will use this terminal to use git.

### So how do we use it?

Let's run through a basic example of using git. In this example, we are going to create our own repository, add and commit a file, and *push* it up to github. *Pushing* a repository refers to taking the git log that you have created locally and sending it to GitHub. The commands are below:

```bash
cd ~
mkdir my_first_git_repository
cd my_first_git_repository
touch readme.md
echo "hello world!" >> readme.md
```

What have we done here?

1. Navigate to your "home" directory
```bash
cd ~
```

2.  Create a new directory called "my_first_git_repository"
```bash
mkdir my_first_git_repository
```

3. Change your working directory to the one you created in step 2
```bash
cd my_first_git_repository
```

4. Create a file called "readme.md"
```bash
touch readme.md
```

5. Add content into the `readme.md` file
```bash
echo "hello world!" >> readme.md
```

The last command `echo "hello world!"` repeats the string `hello world!`. When followed by `>>` we can append the result of a previous command (such as `echo`) into a file (in this case, `readme.md`). So now, we have a file called `readme.md` that has the text `hello world!` inside of it. We can check it with the following command:

```bash
cat readme.md
```

You should see all of the text in the file! Awesome!

Let's set up our repository, add `readme.md` to it, and commit!

```bash
git init
git status
git add readme.md
git commit -m "Hello world -- our first commit"
```

What did we do here? In order:

- `git init`: This command initializes a git repository in your working directory. This means that everything in the `my_first_git_repository` folder is now ready to be tracked by git.
- `git status`: This tells you 1) what files, if any have changed and 2) if they have been added to the staging area yet. When we run this, we should see that we have one file that is not added yet (`readme.md`)
- `git add readme.md`: This command adds a specific file to the index so that its changes will be tracked (in this case, it adds `readme.md` to the index)
- `git commit -m "Hello world -- our first commit"`: Here we commit our changes, saving the current state of our files to the git log. Every commit must have a message associated with it. This commit message should describe briefly whatever changes you've made (very helpful if you're looking in the past for a specific change!)

Let's make a couple of other changes before we send this up to GitHub proper:

```bash
git log
echo "this is a great file" >> readme.md
git status
git add readme.md
git commit -m "My second commit"
```

Can you explain what we've done at each step?

At this point, we have a file (`readme.md`) with that looks like this:

```bash
cat readme.md
hello world!
this is a great file
```

We'd like to take this repository and *push* it to GitHub. What's *pushing* you ask?

- *Push*: To take a local repository and move it up to a remote repository (i.e., on GitHub, etc.)
- *Pull*: To take a remote repository (i.e., on GitHub) and download it to your local machine

You might wonder how we push and pull without overwriting our code or losing data. We won't get into that at this point, but rest assured that there is a robust set of ways to avoid that exact situation (in fact, GitHub will not overwrite *anything* unless you are very explicit that you want data to be overwritten and lost).

Before we push we need to create a repository on GitHub and sync the repository to our local repository (so it knows where to send it). Go ahead and create a repository on GitHub with the name `my_first_git_repository` (see [here](https://guides.github.com/activities/hello-world/#repository) to do that). Then, run the following command on your command line:

```bash
git remote add origin https://github.com/my_first_git_repository.git
git push -u origin master
```

Let's walk through what we're going to do before we do it.

- `git remote add origin` -- this adds a remote (i.e., not on our computer) repository. Origin is the name of that remote (we may have multiple remotes). Why origin? Convention, mostly.
- `https://github.com` -- This is the user through which we are sending our data (we are talking to another computer after all!) The user is `git` (this is standard) and the address of that computer is `https://github.com` (this is exactly what we type into the web browser when we connect!)
- `my_first_git_repository.git` -- this is the specific repository that we are adding. You'll have to switch my user ID out for yours
- `git push -u origin master` -- this does two things. 1) it pushes the `master` branch (don't worry about that yet) of this repository up to the `origin` remote (which we just set up) and 2) the `-u` flag sets this remote to be upstream. Essentially that means that our local repository knows that what's up on the remote is something it will probably want to pull down at some point (in case you were working with multiple people and they had made changes).

Once you've ran it successfully, navigate back to your repository on GitHub and you should see _everything_ in your local repository, online!

# Hello World Guide

There are many, many ways to use Github and git effectively. GitHub provides a ton of resources for common situations. The guide below is an excellent "hello world" example to reinforce the examples provided in this document. If you're able to follow along this guide and understand the steps, then you're at a level that's capable of using Git and GitHub effectively!

https://guides.github.com/activities/hello-world/

# Questions and Feeback

 Please feel free to submit an Issue or reach out to me with questions or feedback.
