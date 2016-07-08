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

### Configure the original as your upstream repository

You have forked and clone the repository but git now only knows of your own remote (on github) repository, not the one you forked from. Since others will be adding changes to that repository and your yours, and you need to incorporate these changes, you need to also tell git too add another remote:

```
git remote add upstream https://github.com/gitforgits/startingout.git
```

If we now list the remotes with “git remote -v” you should see something like this:

```
origin	git@github.com:<yourusername>/startingout.git (fetch)
origin	git@github.com:<yourusername>/startingout.git (push)
upstream	https://github.com/gitforgits/startingout.git (fetch)
upstream	https://github.com/gitforgits/startingout.git (push)
```

So to summarise: you have your local repository on your disk and you now have two remotes. Origin is the one in your github account and upstream is the original gitforgits repository.

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
Your develop branch might not be up to date with the upstream develop branch so we will pull that develop branch into our own:

```
git pull upstream develop
```

If there were changes you’d see something like this:

```
Updating 34e91da..16c56ad
Fast-forward
 README.md                 |    5 +++--
 1 file changed, 3 insertions(+), 2 deletions(-)
```

If you have just cloned the repository there is very little change you will have changes and you will get a “Already up-to-date.” message. 

If you get a warning that there was a merge conflict when merging upstream develop into your local develop this means that you made direct changes to your develop branch. So either you committed these changes locally or you accidentally merged a branch into your develop branch. Don’t do this! We’ll go into how to fix issues later.

### Create a working branch

So we want to learn how to use so called feature branches. A normal flow would be to do your work on your own branch. This way you can commit and push anything you want without impacting the work of others. Only when your own feature branch gets merged into develop do the other devs ‘see’ your changes.

A branch can have pretty much any name. It is common to agree on a naming scheme with the other developers. We’ll use a free form format that describes what you have been working on but keep in mind that every OS project has it’s own rules. For example it is very common to use the issue number in the branch name.

Let’s create a branch named my-first-change now:

```
git checkout -b my-first-change
```

This creates and checks out a new branch at the same time. Keep in mind that this branch is created from the state of your current branch. So typically if a feature is not related to one you have in development you should always do this from the develop branch.

If we now type “git branch” we should see something like this:

```
* my-first-change
  develop
  master
```

Nice! 

### Making our first change

So lets start with something simple. Let’s make a small introduction in the /scratch folder named hello-<yourusername>.md where you can tell something about yourself.

You can use any text editor of your choice. Create a file and add some text to it. When you’re done type “git status” in your command line. You should see something lik this:

```
On branch my-first-change
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	scratch/hello-username.md
```

As you can see git detected our changes correctly. 

### Adding your work

Unlike many older version control systems git separates a working set with your committed work. Your working set is your ‘bucket’ of work you want to commit. So first we add our file:

```
git add scratch/hello-username.md
```

It’s important to get this bit right. Check with git status again:
```
On branch my-first-change
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   scratch/hello-username.md
```

As you can see you just added on new file with can be committed. If there’s other files there make sure to remove them (using git reset). git add takes wildcards so it’s easy to just add the changes to the entire tree in one go. But this also makes it easy to add stuff you don’t want. And once changes are added and committed they can never be really removed again. No big deal with normal text but you don’t want to have for example your password in a public git repository. 

### Committing your work

Now we have added our new file we can commit our changes. Just type “git commit”.

Depending on your OS this will open a text editor. On MacOS / Linux this will be vi by default. You can configure this to a different editor if you want.

You can also just supply the commit message on the command line:

```
git commit -m “My first commit!”
```

And you can even add and commit with a message at the same time:

```
git commit -am “My first commit”
```

### Pushing your work to your repository

So our commits now only exist locally. They don’t exist on our own remote nor on the upstream. First we should push them to our own remote with “git push”. It won’t work the first time though; you get a message like this:

```
fatal: The current branch my-first-change has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin my-first-change
```

This is because your own remote (origin) doesn’t know the branch yet. So the easiest way is to just copy-paste the suggestion:

```
git push --set-upstream origin my-first-change
```

You will get a few lines reporting objects being sent ending with this:

```
Branch my-first-change set up to track remote branch my-first-change from origin.
```

Next time you type “git push” **on a known branch** it will just send over the changes.

### Creating a pull request

We now have our changes on github and we can click through our commits and see the changes. Now we can create a pull request to our upstream. This is done online on the github page. If you go to your repository (github.com/<youruser>/startingout) you should see a recent change to a branch a big green “Compare & pull request” button. Click it!

You will get a screen showing the creation options for the pull request.

You can create a PR on your own repository too but we want to get our changes into the upstream. So we should make sure that on the left hand side you have “base fork: gitforgits/startingout” selected together with the **develop** branch (**not master!**). The right hand side should have the “head fork: <your repo>” and the branch you just created selected.

Underneath you see the title of pull request together with some comments. Add a clear descriptive title there and a comment explaining what you did. Just to get you into the habit; a PR won’t be accepted without a clear description of the what and why of the change.

### So now what?

Now you wait :)

A pull requests gets reviewed by the maintainer. A pull (or merge) request is basically a review request. The maintainer can comment on it and ask you to make changes. When the maintainer of the repository is happy he will accept the pull request which will merge it into the develop branch.

We will pretty much always ask you to make changes on the pull requests (even if they don’t make sense) because it is important to practice this.  

## Common problems

### Merge conflicts