#### Workflow

When working in team you do the following steps

**Assumption: You are not added in as collaborator in the project repo, but are contributing to it. This means you don't have write access to the original project repo but can copy the project repo and make changes to it and request for those changes to be added in to the original project**

  1. Fork the repo of the project you want to work on in case you are not added in as a collaborator.

  2. Clone the repo to your local machine from your forked copy and **not from the original repo**

  3. Add the original repo as a remote to your local git repo.

  4. Pull the changes from original repo to your system from the newly added remote to make sure you have the latest changes to the repo.

  5. Create a new branch to make your changes.

  5. Make changes that you want to add to the project.

  6. Again do a pull request to master branch, to make sure everything is up to date there.

  7. add and commit the changes you made the project in your checked out branch.

  8. Push the changes to your repo online using the remote you got when cloning it.

  9. Create a pull request on github, asking for the project manager to merge your changes.

  10. Wait till you get a reply.

  11. Rejoice on successful merge of your code or update the code in case its rejected and try again.

  12. Do a git pull to master to update your copy of the project to now added copy of the project in master branch.

  13. Delete the development branch used to make changes from your local machine and git push to your copy of the repo to make sure everything is up to date.

  note: I know this is quite a dance to do, but you don't have to do it for every commit. Just the commit which you feel is a major one like solves an issue or is completed adding a new feature or solves a bug etc.

  Personally, I've got custom commands for doing it all in one or two lines. Depending on your OS you can make em too, just google it.

  Now for a detailed explanation of how to do it all using git, checkout the notes on git commands below.


# Fork The repository

Forking means making a copy of the repository you want to work on. This is something you do using GitHub and not git. I believe you understand that git and github are different, github or github.com is one of the few platforms to store your repositories online and git is the tool you used to do it.

Anyways moving along just click on the 'Fork Button' on the repository you wan't to work on and bam! You have a working copy of the code same as the original project.


# Clone the repository

Simple as

```
  git clone <repo-url>
```
note: the repo url can be https or git protocol based.

Cloning would create a new local copy of the project in your system.

# Remotes

Remotes are gits way of tracking the multiple urls you'll be sending and getting your data from in a sane manner, both for you and git itself but mostly for you.

following are some of the common git remote commands, I'll  explain one and the rest should be self-explanatory

```
  git remote add <custom-remote-name> <repo url>
```

This will add the repo-url as one of the **endpoint** *(A fancy term you'll be hearing a lot in software development which simply means where you request will eventually come to, as in its final destination)* named as <custom-remote-name>.

eg,

```

  git remote add myPersonalUrl https://github.com/presidentObama/killTheInfidels

```
where myPersonalUrl will become the name of the remote

Other remote commands
```
  git remote rm myPersonalUrl
```

For more git remote related commands type
```
  git help remote
```
# Branches

### A good team is like a tree, it has ever-growing new branches!!

Always create a new branch locally on your system when you start working on a new feature/issue.

You can do this by typing

```
  git checkout -b <branch-name>
```
note:This will also switch you to the new brnach automatically

To switch to a different branch type the following

```
  git checkout <branchname>
```

To get a list of branches in the current project local to your system

```
  git branch
```
This will also highlight with a * to tell you the branch you are currently on.

```
  git branch -d <branch-name>
```

removes the branch

```
  git branch -m <old-branch-name> <new-branch-name>
```

will rename an already existing branch to something new

# Merging

Merging is the process of combining code from one branch to another, such that latter will have code from both the branches. This may or may not result in **merge-conflicts** aka *problems combining code from both branches*.

You merge branches locally using the following command

```
  git merge <changes-branch> <branch-to-merge-to>
```

# Pull and Fetch

These are two commands that you'll be running a lot in your system.

### Pull

Pull command as in

```
  git pull <repo-url>
```

or if you are already on a branch to get its latest changes, just types

```
  git pull
```

pulls the latest change from the corresponding repository and **merges** the new changes in the current branch.

### Fetch

Fetch command as in

```
  git fetch <repo-url>
```

will fetch the latest changes but will not merge them

### Merge Conflicts and how to resolve them

So lets talk about a scenario where I modify the code in one branch or have merged my custom branch with master and you've also modified your custom branch and we both somehow modified the same line of code, this will result in a **merge conflict**.

Its how git tells the developers of the project, bruh I'm not sure which changes to keep!! So how to we go about solving this. Well there are couple of ways these can be tackled but we will talk about the scenario where you are working on a forked repo and not as a collaborator( more on this soon, but for keep it simple silly!).

So first step is to make sure you have the latest repo, so change to your teams working branch(we'll assume its master here to keep things simple, assuming you don't have **multiple <u>branches</u>** for different types of development such as mobile and web-app) and merge the changes to the working branch(from now on I'll just call it master so don't get confused).

This will make sure you have the latest code in the master branch merged to your local copy of the code. Then you can commit your changes.
Git will give you an error saying you have merge conflicts since you and I have modified the same line of codes individually and may be even differently. To resolve this

- Open the file(s), git is telling you the merge conflicts are in

```
<<<<<<<HEAD
  My Line of code I uploaded the last time I commited
=====
  Your line of code that you added which you want to commit
<<<<<<<name of your working branch
```

- **Now this can be solved in 4 ways**

  1. Solve by deleting my code, running the app and if everything works and is how you want to keep things, keep your code.,***keep yourcode and delete my code alogn with <<<<HEAD,=====,and <<<< name of your working branch.***

  2. Solve by deleting your code, running hte app and if everything works and is how you want to keep things,***keep my code and delete yours along with <<<<HEAD,=====,and <<<< name of your working branch.***

  3. Delete both our codes include <<<HEAD,=== and <<<working branch

  4. Keep both our codes and delete <<HEAD,=== and << working branch

- save your changes and commit

- check status to make sure everything is committed

- push **working branch** <not master > to your forked repo in your id

- send me a pull request **using github** for your working branch

- After trying your solution on my system( assuming we don't have a CI system), I'll accept or delete your pull request and the merge accordingly thus bringing the main repo to a coherent change.

- again do a git pull after my merging to make sure you have the latest changes.

- Delete your working branch

- Start working on a new branch as desired

# Issues

### We re working in a team dammit! Work on the issues first!!

No they are not issues related to team members or team performance but related to the project the team is working on.

Though in agile development, the one we are following for our project. Issues will just become our tasks for the project that we need to get done, any actual issues will also be considered as a task as its suppose to be fixed to move on to other tasks.

To create a new issue click on the Issues tab on the github page of the project, give it a good title and a body, as in everything else on github you can format the text using Markdown!
Click on submit new issue to create an issue(hehehe, :P)


Here is the reason for using issues for tracking tasks, you can close an issue by making a commit or a pull request with the following words anywhere in it, "fixes #1" where #1 is the first issue created on github.

But here's the awesome part, it closes the issues only after the code is merged with the main/master branch. And all of it happens automatically!

You can also use close(s|d),resolve(s|d),fixe(s|d) as the keyword instead of just fixes.

You can close multiple issues with one commit using "fixes #1,#4,#6". But this is not suggested, especially in an agile project.
