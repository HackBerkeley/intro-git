## Git Workshop

Lets practice git!

Following the main [README](../README.md) you should go through the installation process for your machine as well as the required `git config` commands.

**Note**: You'll see `$` these a lot. Don't actually type them in! They just mean you're entering a command!

### Configuring Git to Know "You"
Git needs to know two things about you to associate you with your commits. **Name** and **email address** - don't worry, you will never be emailed. Also, *this is not making an account*, just setting variables in a configuration file.

Do so like this:

`$ git config --global user.name "Lord Vader"`

`git config --global user.email lordvader@deathstar.mil`

The `--global` flag tells git that you want your **name** and **email address** to be the same across all of the repositories you work in, not just the current one.

### Creating a Repo
Quick review, a **repo** is simply a *directory (folder) being tracked* by git.

So to make a repo, we first need a directory, lets make one:

`$ mkdir deathstar`, then `$ cd deathstar`, now we should be inside our deathstar directory, check by using print working directory `pwd`.

Cool, but this is just a directory (or folder) without Git! Lets **initialize Git** in our directory:

```
$ git init
Initialized empty Git repository in /path/to/deathstar/.git/
```

Sweet! This entire directory is now being tracked by Git.

**Important**: Your secret to using Git will be `git status`, use it often!

### Adding Files

So, lets say we want to blow up Alderaan, well let's make a little `destroy.js` file to do that:

```
$ touch destroy.js
$ ls
destroy.js
```
Now open your text editor of choice and add the following lines to `destroy.js`

If you're a Star Wars fan, [here's some fun Star Wars theme JavaScript](https://gist.github.com/thebearjew/19f670f9becb15bd12a7#file-destroy-js) to put into your `destroy.js` file for fun.

<small>Sticker for the first person to find the DBZ reference!</small>

Now that we have `destroy.js` with content we should our best friend **`git status`** to see what the state of the files are.

```
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	destroy.js

nothing added to commit but untracked files present (use "git add" to track)
```

Our `destroy.js` needs to be tracked by Git so it will know when we make changes to it. Let's add it:

`$ git add -A` This command adds *all* new, modified, deleted, or untracked files. Use this often!

Now lets see what our status is after adding 

```
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   destroy.js
```

Great, now we added the changes to `destroy.js` to Git's tracking. Next time you modify, create, or delete a file, Git will tell you to add those changes.

### Committing
Great, we've made changes and added them, time to package them into commit with a description.

Note: first commits are always called "Initial commit:

```
$ git commit -m "Initial commit"
[master (root-commit) 21e1721] Initial Commit
 1 file changed, 56 insertions(+)
 create mode 100644 destroy.js
```

We've just made a commit with everything we've done until this point and given it a description "Initial commit", which means we're starting off.

Next time you made changes to a file(s), go through the adding process and then this committing process. *Rinse, repeat*.

--

For this example, lets make another commit.

Open `destroy.js` and add the following line to the end:

```js
console.log('Luke, I am your father!');
console.log('I\'m not actually, my name is YOUR_NAME...')
```

Then go through the adding the changes (above), and the commit them like we just did. 

This time write a **different commit message**. It should describe what changes you've made.

### Linking to a Remote (Github)

Up until now, the work we've been doing has been on our local computer, nothing has left our little folder... time to change that.

We're going to assume you have a [Github](https://github.com/) account. Sign in now or make one.

Now, on Github **make a new repo with the same name as our directory** - "deathstar"

[You should see something like this](./empty-repository.png)

Thankfully, Github has been nice and explained how we can link our folder and this one (remote) together.

First we'll add the URL of this repository to our local folder, and name it `origin` with this command:

`$ git remote add origin https://github.com/YOUR_USERNAME/deathsar.git`

Now we check to see if it was successfully by asking git to show us our remote URLS:

```
$ git remote -v 
origin https://github.com/YOUR_USERNAME/deathstar.git (fetch)
origin https://github.com/YOUR_USERNAME/deathstar.git (push)
```

Hooray!

### Pushing
Pushing is simply updating your *remote repository* with the commits you've made on a branch.

We're on the master branch with two commits (the ones we just made). And we want to send this to our repository on Github. Lets `push` the commits to the corresponding branch:

```
$ git push -u origin master # <--- First time only! After do $ git push origin master
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 804 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:YOUR_USERNAME/deathstar.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
```

This means push to the `origin` (https://github.com/YOUR_USERNAME/deathstar.git) branch called `master` (the same one we're on). If we were on another branch, we would push to the branch with the same name.

Git is also telling us that the remote now has a new branch called `master`! The same one we were working on.

**Note!**: The `-u` is only used the first time to connect branches between local and remote repositories. Next time you push do so like this **`$ git push origin branch-name`**.

Refresh the page on your Github repo and see your commit!

### Working Together (Cloning, Pushing, Pulling)
In order to practice pulling, you need to work with another person. So turn to the person next to you, say hi, ask their name, and their Github username.

One person will be called "Developer A" and the other "Developer B".

Dev A should **add Dev B as a collaborator** on their Github repository (https://github.com/DEVELOPER-A/deathstar.git).

You can do that by going to Settings > Collaborators > Then add Dev B's username.

##### - Cloning Someone Else's Repository
Dev B should now `clone` Dev A's repository on Github.

```
$ cd /where/you/want/to/clone/it

$ git clone https://github.com/DEVELOPER-A/deathstar.git
Cloning into 'deathstar'...
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
Checking connectivity... done.
```
Congrats Dev B, you just clone Dev A's work! Now `cd` into the repo and open up `destroy.js`... You should see Dev A's print statement at the end:

```js
console.log('I\'m not actually, my name is <DEV-A-NAME>...')
```

##### - Pushing to Dev A's Repo
Okay Dev B, your time to shine!

Edit the `destroy.js` to print whatever you'd like (try to be nice :P)

- Add the changes
- Commit the changes
- Push the commits to the master branch on Dev A's repo

If you need help, there are mentors around the room ready to help you

##### - Pulling Dev B's Additions
Your turn Dev A. So your friend and made a commit to your repo, awesome! 

But how do you get those changes onto your local repository? With **pulling**. Pulling is simply the opposite of pushing (duh!) - it means there are things on the remote you don't have which you want, so you **pull them down to your computer**.

Here's visualization:

![](https://illustrated-git.readthedocs.org/en/latest/_images/git-flows.svg)

Time to pull:

```
$ git pull 
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (1/1), done.
remote: Total 4 (delta 2), reused 4 (delta 2), pack-reused 0
Unpacking objects: 100% (4/4), done.
From github.com:thebearjew/deathstar
   c6ff65f..9b39773  master     -> origin/master
Updating c6ff65f..9b39773
Fast-forward
 destroy.js | 2 ++
 1 file changed, 2 insertions(+)
``` 

Now, Dev A, open your `destroy.js` file and you should see the additions that Dev B made!

Pulling worked!

### Branching and Checking Out
Branching is actually the most important feature of Git. It allows 2 or 2,000 developers work on the same code without writing over or deleting each other's work.

So we just learned the ins-and-outs of pulling and pushing our changes (or commits) to a repository.

However, **what happens if Dev A decides to rename `destroy.js` to `peace-and-love.js`**?

Dev B will still have their file named `destory.js`. After they edit `destory.js`, add the changes, commit them, and push them, they might get this error.

```
$ git push origin master
To git@github.com:DEVELOPER-A/deathstar.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'git@github.com:DEVELOPER-A/deathstar.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

Dev B is unable to push because Dev A made changes and pushed them before Dev B did. 

Now Dev B should try to `$ git pull` and see what happens -> a **merge error**.

**A merge conflict is the same as two people trying to write on the same line of paper at the same time**. We can avoid this by giving each person a copy of the paper and let them work on their own, this is **branching**.


##### - Practice Branching
Both Dev A and Dev B should make their own branches:

```
# Dev A
$ git checkout -b feature/<DEVELOPER_A_NAME>           <-"jake" for example
Switched to a new branch 'feature/<DEVELOPER_A_NAME>'
```

```
# Dev B
$ git checkout -b feature/<DEVELOPER_B_NAME>
Switched to a new branch 'feature/<DEVELOPER_B_NAME>'
```

The command `$ git checkout -b branch-name` creates a branch and simultaneously switch to it.

`checkout` allows you to jump between branches. Do so later by using `$ git checkout branch-name`

We can see that we made the branch successfully by asking Git to list the branches

```
$ git branch -a 
*feature/<YOUR_NAME>
master
remote/origin/master
```

Dev A Add the following to `destroy.js`

```js
console.log('You really shouldn\'t blow up planets Vader');
```

Dev B add the following to `destroy.js`

```js
console.log('Blowing up planets is FUN! Give me another one!');
```

Both Devs add, commit, and push like so `$ git push origin feature/<YOUR_NAME>`

Now check the Github repo and you should see `3 branches` at the top.

--
### Merging, Pull Request, and Forking Demo
Speakers give demo on merging branches, Github Flow, and Forking.

These are features unique to Github, so demoing them on Github makes a lot of sense!


