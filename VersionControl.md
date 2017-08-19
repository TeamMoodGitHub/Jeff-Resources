# Version Control

## What is Version Control?
Version control is a way programmers create checkpoints in their programming projects. It is useful whether you are working by yourself, or in larger groups as modern developed version control systems have the ability to allow multiple users to work on a project simultaneously. They also handle for cases where you may have submitted flawed code, allowing you to reset the version of your project to a working checkpoint. You may imagine this to be useful if you are developing a product used by thousands of people and you release a version of your project that breaks this product -- you would want to restore functionality as quick as possible to your users by resetting your checkpoint to a working time and then locally debugging the issues you have introduced.

### Vocabulary
There are some terms that can be important to understand moving forward in Git. These include but are not limited to:
`branch` - A project can have multipled `branches`. Think of a branch as a copy of the project that you intend to move in a specific direction. Like in a tree, branches originate from one main origin, but can diverge in different directions. The difference here is that for our purposes, branches that have moved in different directions can still later be merged back into its origin, changing the origin to match the direction of that branch. Suppose for example that you are developing a website and want to add the ability to play music. The website (origin) is already working as is, but you can create a branch and work in the direction of adding music. Once that is completed, we merge that branch back into the origin, and voila -- our website can now play music

`remote` - A remote is a reference to an online location or endpoint. When we say we are "working remote", we generally mean that we are working elsewhere. This concept is important because sometimes the project we are working on can exist in multiple locations. Consider Github, a cloud service used for storing code. We know that Github's servers that store our code are obviously not in the same location as a copy of our project located on our own machine. When we type a command such as `git push origin master`, `origin` is a remote that stands for a specific location on the cloud that we are attempting to copy our code into. Understanding remotes is important because our code could be hosted in multiple locations. Consider working on a project where it is important to our clients that our local code is uploaded online in order for them to check for satisfaction. Maybe one remote copy of our code exists on Github in our private repository, and one copy exists on a separate repository maintained by our employers. In this case, we have two separate remotes and thus it is important to distinguish between them when we are pushing our code.

`commit` - Commiting a file simply means saving the file in the current state it is in.

`staging area` - The staging area represents a collection of files (one or more) that you are ready to commit. When we are ready to push parts of our project, we `add` these files to the staging area. We then `commit` those files with a helpful message highlighting the changes that were made as a part of that commit.

`push` - Uploading a version / commit of our project to a remote repository (such as Github). The key idea for pushing is that we are taking local files and code changes and uploading that to an online repository, which would in turn allow other users or programmers to see those changes

`pull` - The converse to pushing, to pull is to grab the latest set of changes from a remote repository and integrate them into our own copy of those files. For example, if you were working with a friend on a two man project and s/he added a file that enabled some functionality important to your own part, you would want to pull those files first so that those changes would appear locally on your computer.

`merge` - Merging is a complex idea performed by version control systems whereby two separate branches and their respective changes are merged together. The version control system does a `diff`, or often a line by line comparison of the versions of the same two files on these two different branches (remember with branches that two separate branches can have the same file but at different points in time) and attempts to create a single file. This is relevant because if you are developing a specific feature on your own branch, and you want to integrate those changes with the released version of your main project (often on a branch called `master`), you would want to merge your branch with master.

`merge conflict` - I mentioned in the previous definition that the version control system will __attempt__ to merge your branch with another. I say attempt because there are times when the version control system may be confused by changes that have happened in two versions of the same files and will be unable to understand which changes should take precedence. Assume for example in one file that I have changed a variable's value like:

```
let versionNumber = '1.0.1'
```

Now let us say I am attempting to merge my version of this file with a coworker's, who has gone ahead with developing his own featuers on the same file and has labeled the variable as 

```
let versionNumber = '1.0.2'
```

When the version control system is attempting to combine these changes, we have both made separate changes on the same variable. How could the system possibly know which version is correct? Such an issue is called a merge conflict, and it is always the developer's responsibility to fix these conflicts and re-commit his or her files in order to maintain the state of the project.

### Workflow for Getting Started
What happens when we want to start working on a project that is already hosted on the cloud, such as on Github? If you navigate to a repository that hosts code such as this [one](https://github.com/TeamMoodGitHub/Jeff-Resources), you'll see that there is a green button that prompts you to __Clone or Download__. Clicking on this yields two URLs, one for HTTP and one for SSH. While out of the scope for this writeup, the real difference for retrieving code with these URLs is the setup and authentication methods for granting access to clone. Speaking of `cloning`, what does that even mean?

Cloning is merely the act of downloading or making a copy of a remote repoistory onto our own computers. When you find a repository you wish to work on locally, you can merely copy the HTTPS url, and, assuming Git is installed on your computer's command line, type in the command `git clone [HTTPS_URL]` and the repository will be downloaded to wherever you are located in your computer's directory. 

What about if you have already written a bunch of code on your computer and want to upload it to a repository? You can always navigate into that folder that you have been working on, run `git init` to tell Git to start watching that repository for changes, and start your workflow as you normally would to manage that project. When you feel the time is right to upload those files, it's time to set a `remote`! Remember, you have your project working locally on your computer, but how could you upload it to Github unless you instruct Git first the location of where your repository is located on the Cloud? Remember also that when I say location on the cloud, I am merely referring to an endpoint provided by Github's servers.

To see the remotes (or repositories on the Cloud in this specific analogy) that already exist for your project, simply type in `git remote -v` to your command line. To add a remote (which we will need to do), run `git remote add [NAME] [HTTPS_URL]`. What exactly is `name`? It's simply a helpful keyword that you can use to distinguish between remotes. When you clone a repository, a remote by the name of `origin` is automatically added using the HTTPS URL that you cloned with.

So, to repeat, I have a project that I have already been working on that I would like to upload to a Git repository. I run `git init` to start tracking those files. I `add` and `commit` the files I wish to upload to move them to the staging area. I set up a remote by navigating on my web browser to the repository I wish to upload to and copying the HTTP URL. Then, I add a remote that I will name origin to my project by running `git remote add origin [URL]`. Now, I can run `git push origin master` to push the master branch of my project to Github. Note that if you had named your remote something else, like `home` or `work`, you would run instead `git push work master` and so on and so forth.

### Basic Commands
`git add` - Used to add files to the staging area. Can work with modifiers such as `git add singleFile.cpp`, `git add directoryName/`, `git add -A` which adds all the files in the directory, or `git add *.java` which is a wildcard that adds all files that end in `.java`. There are probably more combinations of git add. It is typically dangerous to use `git add -A` because often times in a project there are user specific files with sensitive data that should not be uploaded to a location such as Github.

`git commit -m "Your commit message here"` - This is a specific command but one that is so often used that I include it in a specific form. Using commit will take all the files that you have added to the staging area along with a helpful description of that commit and save it as a specific version in the history of your project -- think of commit as making a checkpoint in a game that you can always return to.

`git push [REMOTE_NAME] [BRANCH_NAME]` - Used to upload a branch's commited files to a remote, which is explained above

`git pull [REMOTE_NAME] [BRANCH_NAME]` - Used to download a remote branch's most recent state of files to your local version of the project

`git branch` - Used to see what branch you are currenty working on

`git checkout [BRANCH_NAME]` - Used to switch what branch you are working on to that specified by `BRANCH_NAME`. Note that this new branch must already exist or you should instead run:

`git checkout -b [BRANCH_NAME]` - Creates a new branch and automatically switches you to it

`git stash` - When you have modified a bunch of files but want to switch branches, Git will usually yell at you to save your changes first otherwise it cannot properly track what files you have changed. If you feel, however, that your current state is not yet ready to be saved, you can first stash your changes, which temporarily removes them from your files. When you later want to re-apply those changes, you should run `git stash apply`

`git remote -v` - See the names of existing remotes registered for your project

`git add remote [REMOTE_NAME] [REMOTE_URL]` - See above section on remotes to understand the use case of this command

`git status` - See what files Git has noticed that you have changed since your last commit, useful to figure out what files you will need to `add` to the staging area

`git log` - Take a look at the history of the commits you have made along with their specifc hashed IDs. You can use these IDs later to return your project to an earlier "checkpoint"

