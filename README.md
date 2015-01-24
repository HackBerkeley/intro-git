# intro-git

##Intro to Git

####Download/Install (Pre-requisite)
1.  Please follow instructions for your OS here: `http://git-scm.com/book/en/v2/Getting-Started-Installing-Git`
2.  type `$ git` into your terminal.  It should spit out a usage statement and list of commands.

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
  As you git more and more, you might be interested in aliasing commands (generally by making them shorter so you can type less!)  For more examples of ways to customize your git, you can look at an example gitconfig file under `git_resources`.
  

####What is Git?
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


  
