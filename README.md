## Git and Github Guide
Adapted from Hackers at Berkeley's Intro to Git (found at [https://github.com/hackberkeley/intro-git](https://github.com/hackberkeley/intro-git)

---

###About Git and Github
#### What is Git?
Git is a version control system.

#### What is a version control system (VCS)?

What is “version control”, and why should you care? Version control is a system that records changes to a file or set of files over time so that you can recall specific versions later.
It allows you to:
- revert files back to a previous state
- revert entire projects back to a previous state
- compare changes over time
- see who last modified something that might be causing a problem
- who introduced an issue, and when
- recover from screwed up or lost files

What if git wasn't used and a bug is discovered?
- Don't know when the bug was introduced and what code caused it
- Can't reset code to a previous version
- Don't know who introduced the bug
- Can't have different versions of code (production versus not-in-production)

<!-- Note to Kyle and others: include an illustration of branches/commits once prepared. -->

#### What is github?
Although git can be used to track your own personal files, github is what allows large teams to collaborate on a single project. Github is a web-based Git repository hosting service. It hosts and tracks the files in your projects.
It provides:
- access control (who can see what)
- wikis/documentation/READMEs for projects
- task management
- bug tracking
- feature requests

Which makes Github *excellent* for collaboration.  The open-source community especially loves using Github.  So do hackathon teammates, and technical recruiters.

---

### Getting Started
#### Downloads/Installs (Pre-requisite)
#### Mac:
Download from [http://git-scm.com/download/mac](http://git-scm.com/download/mac)
#### Windows:
Download from [http://git-scm.com/download/win](http://git-scm.com/download/win)
Two programs will install: Git BASH and Git GUI. Use Git BASH! Although the GUI can perform almost all the same functions as BASH, it's great to get experience working from the command line. You can use unix/linux commands within BASH.
#### Linux:
Ubuntu, Debian, and Mint users can run from their terminal: 
`sudo apt-get install git`
Fedora Users:
`sudo yum install git`

#### (Global) Config Settings
  There are some settings (such as your information, what editor you use, aliases, etc) on git that you'll definitely want to configure.
  Git has two files, `~/.gitconfig` and `~/.gitignore` located in your home directory. `~/.gitconfig` stores settings that you can configure. '~/.gitignore` stores information about what files git should not keep track of. (Maybe you don't want git to track any files with the extension ".catvideo").  You can also make repo-specific .gitignore files (for example, if you don't want to track .class files in a repo).
  
  You'll want to set your name, and email (attached to the commits you write):
  
  `$ git config --global user.name "John Doe"`

  `$ git config --global user.email johndoe@example.com`

  If you're unfamiliar with vim, change the default editor git uses:
  -Mac: `git config --global core.editor open`
  -Windows: `git config --global core.editor notepad`
  -Linux: `git config --global core.editor nano`

  If you want to make your git output be pretty and colorful, here's one way to do it:
  Open your git config: 
  -Mac: `open ~/.gitconfig`
  -Windows: `start ~/.gitconfig`
  -Linux: `nano ~/.gitconfig`
  -Add the following lines:
  ```
  [color]
    ui = true
  [color "branch"]
    current = yellow reverse
    local = yellow
    remote = green
  [color "diff"]
    meta = yellow bold
    frag = magenta bold
    old = red
    new = green
  ```
  
  As you use git more and more, you might be interested in aliasing commands (generally by making them shorter so you can type less!)  For more examples of ways to customize your git, you can look at an example gitconfig file under `git_resources`.

## Git Basics
#### Basic Unix Commands
You'll be working within the terminal, or git BASH if you're on Windows, and so it's handy to know some basic unix commands for navigation. Type a command, and then press enter.
-`pwd` tells you the directory (folder) you are currently in
-`ls` shows the files in the current directory
-`cd [FOLDER_NAME]` allows changes the current directory to FOLDER_NAME
-`cd ..` changes back to the parent directory (the folder that the *current* directory is inside of)

On Windows you can also right-click on the folder you want to be in and click `git Bash`. This will open git BASH with the current directory already at the folder you want. On Macs, you can type `cd ` and then drag the folder you want to the terminal window and it will fill in the pathname.

If this is confusing, ask for help! The command line can be daunting for beginners, but it will get easier with practice.
#### Getting a Git Repository
  - **Cloning an Existing Repository**
    - Most of the time in this club and elsewhere you'll be using git to work on projects already on github. Use the following command to clone the project to your computer
    
    `git clone https://github.com/dvcoders/intro-git.git`
    
    -This creates a new folder with a name matching the repository (Git name for project) name that you cloned from
    -`cd [REPOSITORY_NAME]` to change your current directory to the newly created folder
    
  - **Initializing a repository in an existing directory**
    - If you have a directory already on your computer that you want to start tracking with git, use `git init` to start tracking that folder with git.
    
    
    The `.git` directory allows git commands to be recognized within its parent directory (where you typed `git init`.)  
    If you are NOT Inside a git repo, you will get an error when you try to type a git command.
    ```
    $ cd ~
    $ git status
    fatal: Not a git repository (or any of the parent directories): .git
    ```

<!--> Note to Kyle: Edited up to this point -->

#### Making and Recording Changes to the Repo
Let's go back to temp.
`$ cd temp`

You tell git what to keep **track** of (does it care if you make changes to it or not?), and then git will tell you if any of your **tracked** files have been **modified**, whether they are **staged** for commit, and what **branch** you are on.

```
$ git status
On branch master

Initial commit

nothing to commit
```

We haven't done anything yet!  We're on the **master branch** by default, we haven't added/staged any files or committed any changes.
Create a file called `hello.txt` with the text `hello` in it.

```
$ git status
On branch master

Initial commit

Untracked files:
	hello.txt

nothing added to commit but untracked files present
```

So currently hello.txt is **untracked** by git.  Let's use the `git add` command to track it!

```
$ git add hello.txt
On branch master

Initial commit

Changes to be committed:
	new file:   hello.txt
```

Cool, now its **tracked** but you haven't **committed** any changes.

```
$ g commit -m "Created hello.txt which contains a greeting"
[master (root-commit) f6f7407] Created hello.txt which contains a greeting
 1 file changed, 1 insertion(+)
 create mode 100644 hello.txt
 ```
 
 Now git is tracking a file called hello.txt, and you have one commit with your initial changes to it.
 
 If you type `git status` again, you'll notice we're kind of back to where we started.  That's because we made and now git is tracking the changes between your most recent commit and now.  This is the typical flow of using git:
 
 1.  Create file/make changes to file
 
 2.  `git add <file>`
 
 3.  `git commit -m "changes to <file>`
 
 
 
 Make any change to `hello.txt`.  Now that `hello.txt` is already being tracked, instead of `new file`, it'll say that it has been `modified`.    
 
 ```
 $ git add hello.txt
 $ git commit -m "Changed text of hello.txt"
 [master 025aabe] Changed text of hello.txt
 1 file changed, 1 insertion(+), 1 deletion(-)
 ```
 
#### Looking at Changes, Commits, and Undoing Things

 If you want to see the commits you've made so far:
 ```
 $ git log
 Fri Jan 23 17:38:42 2015 -0800 025aabe (HEAD, master) Changed text of hello.txt  [Melanie Cebula]
 Fri Jan 23 17:35:13 2015 -0800 f6f7407 Created hello.txt which contains a greeting  [Melanie Cebula]
 ```
 
 If you haven't yet committed your changes, you can look at *what* you changed by performing `$ git diff`.  Go ahead and make some more changes to hello.txt.  In my case, my evil twin sister stole my laptop and furiously typed some things.  I want to know what she changed!!!
 
 ```
 $ git diff
 diff --git i/hello.txt w/hello.txt
 index 092bfb9..da5d515 100644
 --- i/hello.txt
 +++ w/hello.txt
 @@ -1 +1,3 @@
 -yo
 +Hahahahahaha I'm Melanie's evil twin Emily and I changed the text of this file!
 +Deal with it!!!!
 +-Emily
 ```
 She deleted yo (in red) and added a message (in green).  How do we undo this?
 Since this is unstaged, we basically need to **un-modify the modified changes**.
 
 Here's on way to do that (use with caution):
 `$ git checkout -- hello.txt`
 
 However, if you want to **undo something you've already committed (say your last commit)**:
 
 Undo commit with `git reset` (use with caution):
 `$ git reset --soft HEAD~1 `
 
Note: You can recover from undoing things (see [http://stackoverflow.com/questions/2510276/undoing-git-reset](http://stackoverflow.com/questions/2510276/undoing-git-reset))
 but you should be careful in general, because it can get complicated.
 
 Okay cool, so git can be used to keep track of modifications you make to the files that it tracks.
    
#### Pushing/Pulling Changes

So far, you've only dealt with a local git repo.  But nowadays, most people use Github to have a **remote** repository (the hosted on Github itself) in addition to their local repository.  This especially makes sense if you're working in teams.  Each teammate has their own **local** git repo, but they all push to the same project repo on Github.

Now:
  - Break into small groups of 2-4 people with 1 **Leader**.
  - **Leader**: Create a new directory, and initialize a git repo in it.  Let's do this with github:
  	1.  Create new repository with a README
  	2.  Go to the repo's Settings --> Collaborators and add your teammates
  - **Everyone**: clone the repo:
  `$ git clone https://github.com/[your-leader's-username]/[your-repository-name.git]`
  - **Leader**: `$ touch introductions.py`, add + commit the file.  Then type `$ git push`
  - **Everyone**: `$ git pull`
  
  Cool!  So you use `$ git push` to **update the Github repo** with your changes, and `$git pull` to **update your local repo** with the changes from the Github repo.
  Now add `introduce()` to `introductions.py`:
  ```
    def introduce():
      print "Hi! I'm <Your Name Here>."
   ```
   follow the add-commit-push flow, if you weren't the first person to push you'll see this:
   ``` 	
   $ git push
	To https://github.com/[your-leader's-username]/[your-repository-name.git]
 	! [rejected]        master -> master (non-fast-forward)
	...
   ```
   
   This means that your teammates successfully **pushed** and now you are **behind the remote** repo.  
   Pull in the changes: `$ git pull`
   
   You'll probably see this:
   ```
   $ git pull
   Auto-merging introductions.py
   CONFLICT (content): Merge conflict in introductions.py
   Automatic merge failed; fix conflicts and then commit the result.
   ```
   
   That means your changes are **conflicting** each other.  Open `introductions.py` and you'll see something like this:
   
   ```
   <<<<<<< HEAD
   def introduce():
     print "Hi! I'm Fred."
   =======
   def introduce():
     print "Hi! I'm George."
   >>>>>>> [really long string of letters and numbers]
   ```
   
   You'll have to manually fix this by removing the **conflict markers**.  
   
   Example:
   ```
   def introduceFred():
     print "Hi! I'm Fred."

   def introduceGeorge():
     print "Hi! I'm George."
   ```
   
   Sometimes conflicts are more complicated than removing the conflict markers as you'll only want to keep one version, or you'll need parts of both versions.
   
   Now do ye olde add-commit-push sequence again and all should be well.
   
   **Leader**:  Once everybody has collected their `introduceName()` functions and pushed up to the repositories, add these lines at the bottom.
```
def main():
    introducePersonA()
    introducePersonB()
    introducePersonC()

if __name__ == "__main__":
    main()
```

Basically, write a `function main()` that calls the introduce functions for everybody in your group, then add that last if statement at the bottom that calls main().

If you run
```
$ python introductions.py
"Hi my name is Ron!"
"Hi my name is Ginny!"
"Hi my name is Fred!"
"Hi my name is George!"
```
your program will introduce everybody. Hurray! Now add-commit-push it up to github so your entire group can git pull and enjoy your finished project.

## Other Topics:
#### Git Branching Summarized
- A branch in Git is simply a lightweight movable pointer to your latest commit
- The default branch name in Git is master
- Each branch points to the latest commit made on that branch (each time you commit, it moves forward automatically)

**Create** a new branch <branchName> with `$ git branch <branchName>`
- This creates a new pointer at the same commit you’re currently on.

**Switch** to branch <branchName> with `$ git checkout <branchName>`

**IMPORTANT: Switching branches CHANGES files in your working directory**:
- If you switch to an older branch, your working directory will be reverted to look like it did the last time you committed on that branch
- If Git cannot do this cleanly, it will not let you switch at all.

**Update** a branch: All you have to do is `checkout` the branch you wish to merge into and then use the `git merge` command:
```
$ git checkout master
Switched to branch 'master'
$ git merge hot-fix
```
This code switches to **branch** master, and then merges the changes from **branch** hot-fix into master.  Now master is up-to-date!

#### Remote Branches:
**Remote branches** are references (pointers) to the state of branches in your **remote** repositories.
- They take the form `(remote)/(branch)`
- **Add** a remote: `$ git remote add REMOTE-NAME REMOTE-LOCATION`
For example:  We add a **remote** called `origin` from the git repo `git://git.whatever.com`

`$ git remote add origin git://git.whatever.com`
- **List** remotes: `$ git remote -v`
- **Push** to a remote:  `$ git push (remote) (branch)`
For example, We push to a **branch** called `hot-fixes` on a **remote** called `origin`

`$ git push origin hot-fixes`

Git branching and remotes are confusing!  The main thing to remember is that **when you switch branches, your code changes**! Use `$ git log` liberally if you forget which changes are on which branches.

## Best Practices:

- Write a descriptive commit message.
- Break up commits into small changes.
- Keep master clean. Work on your own local branch and merge changes into master when you know they work.
- **Add your SSH key to github so you don't have to type in your user/password every time:** 			   
[https://help.github.com/articles/generating-ssh-keys/](https://help.github.com/articles/generating-ssh-keys/)
- git checkout [filename] to restore it to the state of the latest commit.
- git stash if you want to (temporarily) undo changes (git stash apply to re-apply it)
- **use a .gitignore file in each repo (ignore node_modules in javascript, *.class files in java, *pyc for python files, etc)**
- consider git pull with automatic rebase: [http://stevenharman.net/git-pull-with-automatic-rebase](http://stevenharman.net/git-pull-with-automatic-rebase)

## Parting Words:
Using Git takes practice!  Make sure you have the add-commit-(pull)-push workflow down and you're halfway there!

  
