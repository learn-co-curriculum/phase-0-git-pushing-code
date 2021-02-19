# Pushing Code with Git

## Learning Goals

- Create a remote repository on GitHub
- Connect a local repository to a remote repository
- Set the destination of a repo with `git remote`
- Send code to the remote repo with `git push`

## Introduction

You may have heard of [GitHub](https://github.com) before. In the previous
lesson, you used it to get Facebook's code for the React framework. For all
the amazing power that GitHub provides (Microsoft thought it was so powerful
that they bought GitHub for a cool \$7.5 billion), as far as Git is concerned
they're just a big old server that hosts a whole bunch of remote repositories
("remotes").

You've seen how valuable
_remotes_ are for _getting_ software. Now we can take a look at the other side
of the transaction: how we mirror our _local_ repository to a _remote_ repository
using `git push` and `git remote`.

Once your code is on a _remote_, it's backed up &mdash; which is always a good
thing. Also, once you push to a remote, you can choose whether to let
others `fork` or `clone` and benefit from it. Let's learn how to `push` our code!

## Create a Remote Repository on GitHub

There are a few steps to follow to create a _remote_ repository on GitHub.

1. Go to: [github.com/new](https://github.com/new), while logged into GitHub.

2. Enter a name for your repository in the "Repository name" field. You can name
   it whatever you'd like; be creative! The default options are fine as-is — don't
   initialize the new repository with a `README` or add a `.gitignore` or license.
   Click the green 'Create repository' button.

3. After you create the _remote_ repository, you should see a "Quick setup"
   page. Make sure the 'SSH' option is selected, then click the "Copy to clipboard"
   symbol next to the repo URL (pictured) to copy the URL. (We'll use this in the
   next section.)

![github repo quick setup](https://curriculum-content.s3.amazonaws.com/web-development/enough-git-for-learn-co/github_quick_setup.png)

Behind the scenes, GitHub has essentially `git init`'d a blank directory.

## Connect a Local Repository to a Remote Repository

After you've created your _remote_ GitHub repository, you'll want to get your
local repository uploaded to GitHub. Follow the steps below:

1. First, we want to create a folder for our repository, which we'll call
   `my_new_directory`. In the terminal, type `mkdir my_new_directory`. The folder
   will appear in the tree on the left of the IDE. Alternatively, you can use the
   'Create New' button at the bottom of the IDE.

2. To navigate into this new folder, type `cd my_new_directory`. Your terminal
   should display `my_new_directory`, indicating that you are now inside of the new
   folder.

3. Next, we need to create a new file named `README.md`. In the terminal, type
   `touch README.md`. In the file tree, if you expand the folder
   `my_new_directory`, you should now see your `README.md` file. Click on it to
   open it in the text editor.

4. We can directly type in content here, but we can also use our terminal skills
   to add content. So, in the terminal, type `echo "This is my readme file" > README.md`. If you've got the README file open, the new text will appear!

5. Now that we've got some basic content, we can initialize our local
   repository. In your terminal, type `git init`. Your terminal should show that an
   'empty Git repository' has been initialized.

6. Type `git add README.md` to stage the new `README.md` file so it will be tracked by
   `git`.

7. Now, type `git commit -m "Initialize git"`. This will create the first commit
   for this local repository, which will allow us to push our work to the remote
   repository we created earlier.

## Set the Destination of a Repo with `git remote`

To connect your local repository to the newly created GitHub repository, you
must add a new remote to a remote name. Adding a remote involves giving `git` a "short name" and
a "repository path." You copied the repository path from GitHub a few steps
above.

The repository path is a long bunch of technical words. The creators of Git
thought it would be easier to type a "nickname" or a "short name" that points to
that long repository path. It's common to have a "default" remote. The default
remote short name is called `origin`. So we're going to create a new remote with a
short name of `origin`.

Make sure you still have your remote Git info copied from GitHub, and type the
following into the terminal:

```bash
my_new_directory $ git remote add origin your-copied-remote-repository-url
```

This sets the remote so you can now **_push_** your code.

You can use `git remote -v` (the `-v` is for "verbose") to view the remote(s).

```bash
my_new_directory $ git remote -v
# View existing remotes
# origin  git@github.com:OWNER/REPOSITORY.git (fetch)
# origin  git@github.com:OWNER/REPOSITORY.git (push)
```

## Send Code to the Remote Repo with `git push`

Now that we have added a remote repo, we need to send our latest work to the
remote. We use this command when we want to send some code from the local
repository to the associated remote repository. Git will push all the local,
committed work to the remote repository.

The `git push` command takes two arguments. The first is the name of the remote
repo. Remember, `origin` is just an alias or "short name" that refers to the
repository name. You don't actually have to enter the repository name. Instead,
you can just use `origin`. The second is the name of the remote branch you want
to send code to. In the example below, we're pushing to our remote repository's
_default_ branch, `master`. We're still going to hold off on discussing branching
until later, but it's important to remember that `master` is special; it's
the default branch.

```bash
my_new_directory $ git push -u origin master
```

This will push your code up to the remote repo/branch. The first time you push
code up to a newly-added remote repository, use the `-u` flag to tell Git to
"save" the remote repository as the default push destination.

For every subsequent push, you only need to enter `git push`.

## An Aside and a Small Shortcut

In this lesson, we've gone through the steps of both connecting a local repository,
and pushing code up to GitHub. During this course, you'll be creating a few local
repositories from scratch, but more often, you'll be cloning existing repositories
to your local machine. In these situations, you won't need to use commands like
`git init`, since the repo is already set up with Git and will already have a remote
configured. However, you _will_ often need to add, commit and push work you've done
locally to the remote repository. In these situations, you should be able to just run
the following commands:

```
git add .
git commit -m "commit message"
git push
```

As a small shortcut, you can also combine adding and commiting by using an additional
option flag, `-a`, with the commit command:

```
git commit -am "commit message"
git push
```

## Conclusion

Being able to add Git remotes allows you to back up your local repository to a
remote server. If you remember `git init`,
`git remote add origin your-remote-repository-URL`, add, and push your changes,
you'll be able to get your project up to GitHub in minutes!

## Resources

- [GitHub guide on pushing](https://help.github.com/articles/pushing-to-a-remote/)
