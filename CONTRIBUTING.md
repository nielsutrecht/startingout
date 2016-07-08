# Contributing

## The repository layout

This is a small repository with just a few files / directories. It’s kept simple on purpose so we can use this to practice Git as opposed to practice programming. The root contains the following files:

* README.md : the repository read
* CONTRIBUTING.md: the text you’re reading now
* LICENSE: A file that explains all this code is under the MIT license

Then there’s two directories:

* story/ : this contains our open source story. This is our ‘product’ and as a team we aim to together build the best product possible.
* scratch/ : this directory can be used to test things. I would suggest you add a file or make some changes in this directory first to practice using git and pull requests. Unlike changes in the story/ directory changes here will always be accepted unless they don’t follow our Code of Conduct.

## The workflow

So even though our project is really simple our goal is to practice a professional workflow so we are going to do just that. This means that we have two branches that will always keep existing:

* develop: this is the default branch. It represents the current on-going development and also is the branch you should create your own branches from and create pull requests against. 
* master: this is our release branch. You won’t make pull requests against this branch, the repo owners will be responsible for creating releases on this branch.

## Creating your first change

### Prereqs

You need the following

* Make sure you have git installed. If you open your terminal and type “git --version” you should see something like “git version 2.7.4” appear.
* Have a github account and make sure you’re logged in 

### Fork the repository

When you’re on the [repository](https://github.com/gitforgits/startingout) page you see a “Fork” button in the top right corner. If you want to contribute you first need to make a fork to your own github account. This basically creates a copy of the repository into your own account. With this copy you can do pretty much anything; you can even remove all the files if you’d want. However; just doing whatever you wants will just lead to people not accepting your pull requests. What you do in your copy does not affect the source in any way.

### Clone the repository

You could make changes directly in your repo online but you should clone it locally (since that is what you’d do when it would be an application). This is done through the “git clone” command. Git clone makes a local copy of the remote repository.

So open your command line, go to a directory where you want your repository and type:

    git clone https://github.com/<yourusername>/startingout.git

This will create a clone of the repository under the startingout/ subdirectory.

If you have SSH enabled you can also use the more convenient SSH url instead. For info on how to do this [check here](https://help.github.com/articles/generating-an-ssh-key/).

### Switch to the develop branch

Let’s see what branches we have. Type this:
```
    git branch
```
You should see something like this:
```
* master
  develop
```
By default git will be on the master branch. Since we base our work on the develop branch we need to switch. This is really simple:
```
   git checkout develop
```
If you now 