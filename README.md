# Pushing Code with Git

## Learning Goals

- Create a local repository
- Create a remote repository
- Connect the local repository and the remote repository with `git remote`
- Push code up to the remote repo with `git push`

## Introduction

You've seen how valuable _remotes_ are for _getting_ software. Now we can take a
look at the other side of the transaction: how we synchronize our _local_
repository to a _remote_ repository using `git remote` and `git push`.

Once your code is on a _remote_, it's backed up — which is always a good
thing. Also, once you push to a remote, you can choose whether to let others
`fork` or `clone` and benefit from it. Let's learn how to `push` our code!

> **Note**: the workflow you've been using for labs also pushes code for you! When
> you run `learn test`, the `learn-co` gem automatically creates an `fis-wip`
> **branch**, saves the changes you've made to that branch, and pushes it up to
> your copy of the repo on GitHub. Once you have all the tests passing, the lab
> is registered as complete on Canvas _and_ you have a backup of your code saved
> on GitHub.

In this lesson, we'll learn how we can set up remote repositories on GitHub for
any projects we work on. Specifically, we'll learn how to get a new repo set up
on our local drive, create a remote repo for it on GitHub, connect the local and
remote repositories, and push our code up to the remote repo on GitHub.

## Create a Local Repo

Let's review the process for creating a local repository:

1. First, we want to create a folder for our repository, which we'll call
   `my_new_directory`. In the terminal, navigate to the `~/Development/code`
   directory (or wherever you are storing your code for the course) and type
   `mkdir my_new_directory`.

2. To navigate into this new folder, type `cd my_new_directory`. Your terminal
   should display `my_new_directory`, indicating that you are now inside of the
   new folder. Open the directory in VS Code by typing `code .`.

3. Next, we need to create a new file named `README.md`. You can do this in the
   terminal, by typing `touch README.md`, or in VS Code, by choosing
   `File -> New File`.

4. We can directly type in content for our README file in VS Code, but we can
   also use our terminal skills to add content. So, in the terminal, type
   `echo "This is my readme file" >> README.md`. If you've got the README file
   open in VS Code, the new text will appear!

5. Now that we've got some basic content, we can initialize our local
   repository. In your terminal, type `git init`. Your terminal should show that
   an 'empty Git repository' has been initialized.

6. Type `git add README.md` (or `git add .`) to stage the new `README.md` file
   so it will be tracked by `git`.

7. Now, type `git commit -m "Initialize git"`. This will create the first commit
   for this local repository.

## Create a Remote Repository on GitHub

There are a few steps to follow to create a _remote_ repository on GitHub.

1. Go to: [github.com/new](https://github.com/new), while logged in to GitHub.

2. Enter a name for your repository in the "Repository name" field. You can name
   it whatever you'd like; be creative! You can leave the remaining options as
   they are — the default options are fine. Click the green 'Create repository'
   button.

3. After you create the _remote_ repository, you should see a "Quick setup" box
   at the top of the page. Make sure the 'SSH' option is selected, then click
   the copy button next to the repo URL to copy the URL. (We'll use this in the
   next section.)

![github repo quick setup](https://curriculum-content.s3.amazonaws.com/phase-0/pushing-code-with-git/quick-setup.png)

Behind the scenes, GitHub has essentially `git init`'d a blank directory.

## Connect the Local Repository to the Remote Repository

We learned in the previous lesson that the `git remote` command will list the
**remotes** available to our Git repo. If you run that command now, ...nothing
happens. This is because we haven't set our remote repo as the **remote** for
our local repo yet. Doing so is a simple matter of assigning the URL we copied
above to a **remote name**.

We also learned that Git uses the remote name `origin` by default when we clone
an existing repo from GitHub. We verified that by running `git remote -v`, which
showed that the remote name `origin` was pointing to the repo on GitHub that we
cloned. We'll stick to that convention here.

You should still have your remote Git info copied from GitHub. To set the
remote, type `git remote add origin` followed by a space, then paste in the URL.
It will look something like this:

```console
$ git remote add origin git@github.com:your-github-username/my-new-repo.git
```

The command above creates a remote called `origin` and points it to your remote
repo on GitHub.

Let's use `git remote -v` (recall that the `-v` is for "verbose") to verify that
we successfully set our remote:

```console
$ git remote -v
View existing remotes
origin  git@github.com:your-github-username/my-new-repo.git (fetch)
origin  git@github.com:your-github-username/my-new-repo.git (push)
```

We did it! We're now set up to **_push_** our code.

## Send Code to the Remote Repo with `git push`

Now that we have added a remote repo, we need to send our latest work to it
using `git push`. This command will push all the local, committed work to the
remote repository.

The `git push` command takes two arguments. The first is the name of the remote
repo. Remember, `origin` is just an alias or "short name" that refers to the
repository name. You don't actually have to enter the repository name. Instead,
you can just use `origin`. The second argument is the name of the remote
**branch** you want to send code to. We're going to push to our remote
repository's **default branch**.

If you configured Git using the instructions given earlier in the prework, your
default branch's name will be `main`. You can verify this by running:

```console
$ git branch --show-current
```

Then, to push your code up to GitHub, run this command:

```console
$ git push -u origin main
```

The first time you push code up to a newly-added remote repository, using the
`-u` flag will tell Git to "save" the remote repository as the default push
destination for your current branch. What this means is that, for every
subsequent push from the `main` branch, you will only need to run `git push`.

## An Aside and a Small Shortcut

In this lesson, we've gone through the steps of both connecting a local
repository, and pushing code up to GitHub. During this course, you'll be
creating a few local repositories from scratch, but more often, you'll be
cloning existing repositories to your local machine. In these situations, you
won't need to use commands like `git init`, since the repo is already set up
with Git and will already have a remote configured.

However, you _will_ often need to add, commit and push work you've done locally
to the remote repository. The `learn test` command will do this for you for
labs, but for anything else you're working on — for example, the projects you'll
do at the end of each phase — you'll need to do the process by hand:

```console
$ git add .
$ git commit -m "commit message"
$ git push
```

Recall from earlier in this section that you can combine adding all **tracked**
files and committing by using an additional option flag, `-a`, with the commit
command:

```console
$ git commit -am "commit message"
$ git push
```

Note that the `-am` flags will work for adding and committing changes to files
that are **already being tracked**, but if you need to create a new file as part
of any lesson, you'll need to use `git add` to track that file before you can
commit it.

## Conclusion

Being able to add Git remotes allows you to back up your local repository to a
remote server. To review, the process is:

- create a local repo and run `git init` to start tracking it
- create a remote repo on GitHub
- run `git remote add origin your-remote-repository-URL` to tie your local repo
  to the remote repo on GitHub
- use `git add` and `git commit` to save your changes
- use `git push` to push the changes up to the remote repo

With these few steps, you'll be able to get your project up to GitHub in
minutes!

## Resources

- [GitHub guide on pushing](https://help.github.com/articles/pushing-to-a-remote/)
