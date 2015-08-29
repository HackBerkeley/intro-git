## Git Workshop

Lets practice git!

Following the main [README.md](../README.md) you should go through the installation process for your machine as well as the required `git config` commands.

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

Cool, but this is just a directory (or folder) without git! Lets **initialize git** in our directory:

```
$ git init
Initialized empty Git repository in /path/to/deathstar/.git/
$
```

Sweet! This entire directory is now being tracked by git.

**Important**: Your secret to using git will be `git status`, use it often!

### Adding Files

So, lets say we want to blow up Alderaan, well let's make a little `destory.js` file to do that:

```
$ touch destroy.js
$ ls
destory.js
$
```
Now open your text editor of choice and add the following lines to `destory.js`

If you're a Star Wars fan, [here's some fun Star Wars theme JavaScript](https://gist.github.com/thebearjew/19f670f9becb15bd12a7#file-destroy-js) to put into your `destroy.js` file for fun.

<small>Sticker for the first person to find the DBZ reference!</small>

Now that we have `destroy.js` with content we should our best friend **`git status`** to see what the state of the files are.

```
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	destory.js

nothing added to commit but untracked files present (use "git add" to track)
$
```

Our `destory.js` needs to be tracked by git so it will know when we make changes to it. Let's add it:

`$ git add -A` This command adds *all* new, modified, deleted, or untracked files. Use this often!

Now lets see what our status is after adding 

```
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   destory.js
$
```

Great, now we added the changes to `destory.js` to git's tracking. Next time you modify, create, or delete a file, git will tell you to add those changes.

### Committing
Great, we've made changes and added them, time to package them into commit with a description.

Note: first commits are always called "Initial commit:

```
$ git commit -m "Initial commit"
[master (root-commit) 21e1721] Initial Commit
 1 file changed, 56 insertions(+)
 create mode 100644 destory.js
$
```

We've just made a commit with everything we've done until this point and given it a description "Initial commit", which means we're starting off.

Next time you made changes to a file(s), go through the adding process and then this committing process. *Rinse, repeat*.

--

For this example, lets make another commit.

Open `destory.js` and add the following line to the end:

```js
console.log('Luke, I am your father!'');
console.log('I\'m not actually, my name is YOUR_NAME...')
```

Then go through the adding the changes (above), and the commit them like we just did. 

This time write a **different commit message**. It should describe what changes you've made.

### Linking to a Remote (Github)

Up until now, the work we've been doing has been on our local computer, nothing has left our little folder... time to change that.

We're going to assume you have a [Github](https://github.com/) account. Sign in now or make one.

Now, on Github **make a nee repo with the same name as our foler** - "deathstar"

[You should see something like this](./empty-repository.png)

Thankfully, Github has been nice and explained how we can link our folder and this one (remote) together.

First we'll add the URL of this repository to our local folder, and name it `origin` with this command:

`$ git remote add origin https://github.com/YOUR_USERNAME/deathsar.git`

### Pushing
Pushing is simply update your *remote repository* with the commits you've made on a branch.

We're on the master branch with two commits (the ones we just made). And we want to send this to our repository on Github. Lets `push` the commits to the corresponding branch:

```
$ git push -u origin master
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

Git is also telling us that the remote now has a new branch called `master`! The same one we were working on

**Note**: The `-u` is only used the first time to connect branches between local and remote repositories. Next time you push do so like this `$ git push origin branch-name`.

Refresh the page on your Github repo!

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
Congrats Dev B, you just clone Dev A's work! Now `cd` into the repo and open up `destory.js`... You should see Dev A's print statement at the end:

```js
console.log('I\'m not actually, my name is <DEV-A-NAME>...')
```

##### - Pushing to Dev A's Repo
Okay Dev B, your time to shine!

Edit the `destory.js` to print whatever you'd like (try to be nice :P)

- Add the changes
- Commit the changes
- Push the commits to the master branch on Dev A's repo

If you need help, there are mentors around the room ready to help you

##### - Pulling Dev B's Additions
Your turn Dev A. So your friend and made a commit to your repo, awesome! 

But how do you get those changes onto your local repository? With **pulling**. Pulling is simply the opposite of pushing (duh!) - it means there are things on the remote you don't have which you want, so you **pull them down to your computer**.

Here's a picture to visualize

![](https://illustrated-git.readthedocs.org/en/latest/_images/git-flows.svg)

Time to `pull`:

```
$ git pull 
# NOTE TO SELF, HAVE SOMEONE ELSE COMMIT TO DEATHSTAR THEN DO EXAMPLE PULL
``` 

Now, Dev A, open your `destory.js` file and you should see the additions that Dev B made!

### Todo

> Branching
> 
> Checking Out
> 
> Pull Requests
> 
> etc.
