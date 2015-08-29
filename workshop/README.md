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
console.log("Luke, I am your father");
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

`git remote add origin https://github.com/YOUR_USERNAME/deathsar.git`



