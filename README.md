# intro-git

##Intro to Git

####Download/Install (Pre-requisite)
1.  Please follow instructions for your OS here: `http://git-scm.com/book/en/v2/Getting-Started-Installing-Git`
2.  type `$ git` into your terminal.  It should spit out a usage statement and list of commands.
3.  Create a `github` account.

####(Global) Config Settings
  `http://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup`
  There are some settings (such as your information, what editor you use, aliases, etc) on git that you'll definitely want to configure.
  Git has a global `~/.gitconfig` and `~/.gitignore` that will affect all of your git repos.  You can also make repo-specific .gitignore files (for example, if you don't want to track .class files in a repo)
  
  You'll want to set your name, and email (attached to the commits you write):
  
  `$ git config --global user.name "John Doe"`

  `$ git config --global user.email johndoe@example.com`
  
  If you don't use vim, you'll probably want to set your editor to nano or something.
  
  `$ git config --global core.editor nano`
  
  *If* you have `subl` as a command, you can set Sublime Text 2 as your default editor.
  
  `$ git config --global core.editor "subl -n -w"`
  
  If you want to make your git output be pretty and colorful, here's one way to do it:
  Open your git config: `vim ~/.gitconfig`
  Add the following lines:
  
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

####What is Git?

##Git Basics
####Getting a Git Repository
  - Initializing a repository in an existing directory
    - You have a directory that you want to track with git --> use `git init`
    
    ```
    $ mkdir temp
    $ cd temp
    $ git init
    Initialized empty Git repository in /Users/melaniecebula/temp/.git/
    $ ls -la
    .  ..  .git
    ```
    
    The `.git` directory allows git commands to be recognized within its parent directory (where you typed `git init`.)  
    If you are NOT Inside a git repo, you will get an error when you try to type a git command.
    ```
    $ cd ~
    $ git status
    fatal: Not a git repository (or any of the parent directories): .git
    ```
    
  - Cloning an Existing Repository
    - The git repository already exists on github (either you created or its public like this workshop repo!)
    
    `git clone git@github.com:HackBerkeley/intro-git.git`

####Making and Recording Changes to the Repo
Let's go back to temp.
`$ cd temp`

You tell git what to keep *track* of (does it care if you make changes to it or not?), and then git will tell you if any of your *tracked* files have been *modified*, whether they are *staged* for commit, and what *branch* you are on.

```
$ git status
On branch master

Initial commit

nothing to commit
```

We haven't done anything yet!  We're on the *master branch* by default, we haven't added any files or committed any changes.
Create a file called `hello.txt` with the text `hello` in it.

```
$ git status
On branch master

Initial commit

Untracked files:
	hello.txt

nothing added to commit but untracked files present
```

```
$ git add hello.txt
On branch master

Initial commit

Changes to be committed:
	new file:   hello.txt
```

```
$ g commit -m "Created hello.txt which contains a greeting"
[master (root-commit) f6f7407] Created hello.txt which contains a greeting
 1 file changed, 1 insertion(+)
 create mode 100644 hello.txt
 ```
 
 If you type `git status` again, you'll notice we're kind of back to where we started.  That's because we made and now git is tracking the changes between your most recent commit and now.
 
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
 
 If you haven't yet committed your changes, you can look at *what* you changed by performing git diff.  Go ahead and make some more changes to hello.txt.  In my case, my evil twin sister stole my laptop and furiously typed some things.  I want to know what she changed!!!
 
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
 Since this is unstaged, we basically need to un-modify the modified changes.
 
 Here's on way to do that (use with caution):
 `$ git checkout -- hello.txt`
 
 Undo commit (use with caution):
 `$ git reset --soft HEAD~1 `
 
 Note: You can recover from undoing things (see http://stackoverflow.com/questions/2510276/undoing-git-reset)
 but you should be careful in general, because it can get complicated.
 
 TODO
-untracked
-unmodified
-modified
-staged
    
####Pushing/Pulling Changes
TODO:
  - Break into small groups of 2-4 people.
  - One person should create a new directory, and initialize a git repo in it
  - Add a file
  - Push to github
  - Others should git clone, make changes, push/pull
  - Changes on different branches/fork/pull request
  - remotes

  add: add -a, add *, add *.java
  commit: -m "message"
  clone
  remote (add remote <branch>) (-v)
  pull: --rebase
  push: -f
  reset: --soft
  log:
  reflog
  branch:
  checkout:
  merge:
  forks
  rebase

####Merge Conflicts
TODO


  
