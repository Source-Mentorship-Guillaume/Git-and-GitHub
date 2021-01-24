# Life of a change - A typical way to modify a code base.

In this exercise, we'll see how we can modify a file, track the history of this change, and ask for this change to be part of the main code base.

### Creating our own branch - how to isolate your work.

Git's whole idea is to allow for different people to work together on the same code base in parallel. For this we "branch" out of the main repository before making any changes. 
- Create a new branch with 
  ```
  git branch mybranch-<your-name>
  ```
  >***Note***: Everytime you see `<your-name>` in a command, please remember to replace it with your actual name! For example `git branch mybranch-guillaume`
- Type the command `git branch` to make sure that your current branch is `mybranch-<your-name>` - it should have a `*` before it.

That's it, now everything we change will be changed in this branch, not the `main` one, so we can do what we want!


### Make changes and record them
- Change the last two lines in the poem from:
  ```
  I've changed this file
  And you can too.
  ```
  to:
  ```
  You've changed this file
  And I can too
  ```
- Now in the terminal (console), type 
  ```
  git diff
  ```
  This will show you the difference between the *HEAD* - in this case the last commit, and your current version of the file - in your *working tree*. To exit, type press the `q` key.
  
  You can also show the state of the files in your repository by typing:
  ```
  git status
  ```
  Here, `poem.txt` will be list as having been modified.

- Let's commit these changes. Committing is like setting a *save-point* in our work. After we commit, we can make any changes we can always go back to this point in time, and see our files as they are now. We'll see this later. For now:
  - First we *stage* the changes with `git add`, which tells git which files we want in our next commit. In this case we have only `poem.txt`. But we might, for example, also have a file `poem2.txt`, which we changed too but don't want to commit yet.
    ```
    git add poem.txt
    ```
  - Now we commit, which means that we tell git to remember the state of the files we stagedw at this moment in time.
    ```
    git commit -m "Changed the last two lines of this poem"
    ```
    > ***Note***: the `-m` option allows us to pass in the commit message. If we type `git commit` alone, a text editor will open in the console to let us write a message.


### Let's take a moment to look back at what we just did.
- We created our own new branch on the repository with `git branch` and worked on it with `git checkout`
- We made a change to the poem file.
- We committed this change to our new branch with `git add` and `git commit`


### Great but now I want those changes to be in the main branch!
If you were alone working on this repository, you could simply move back to the main branch with `git checkout main` and tell Git to pull the changes that you made in your branch to the `main` branch. 

However, if you work in a team, your teammates might want to review your changes before they are accepted and merged into the common code base.
Since we're working with GitHub, we'll create what is called a **Pull Request** (**PR** for short). For this, we first need to upload this new branch on Github. It's important to understand that right now, all the changes we have made only exist on our local machine, and were tracked with Git. Git created some files in the `.git` folder to keep track of the history, and it can also help us put all this online, in this case on Github.

- First let's check what our `remote` is. The `remote` is the *online* repository, which Git can `push` to (upload) or `pull/fetch` from (download). Here we will want to upload, or `push`, our changes. First let's check what the `remote` by typing:
  ```
  git remote -v
  ```
  It should print out:
  ```
  origin	git@github.com:Source-Mentorship-Guillaume/Git-and-GitHub.git (fetch)
  origin	git@github.com:Source-Mentorship-Guillaume/Git-and-GitHub.git (push)
  ```
  which is where you cloned this project from, remember? It automatically set the `origin` remote to it.
  >***Note***: `origin` is the default online repository, so typing `git push` or `git fetch` or `git pull` without specifying a remote will assume you want the `origin` remote.

- Now let's try to push our new branch and its changes to this Github repo. Type `git push`. You should have a message saying:
  ```
  fatal: The current branch mybranch-<your-name> has no upstream branch.
  To push the current branch and set the remote as upstream, use

    git push --set-upstream origin mybranch-<your-name>
  ```
  Let's read this carefully: `The current branch mybranch-<your-name> has no upstream branch`. Git is telling us that right now there is no branch with this name on our Github repo, so it cannot push the changes. Indeed, when we created our branch we only created locally, Github has no idea it exists! But it's giving us a solution:
  ```
   To push the current branch and set the remote as upstream, use
     git push --set-upstream origin mybranch-<your-name>
  ```
  Let's break down this command: 
    - `git push` - upload to the remote
    - `--set-upstream` - upstream meaning "on the remote". So "create on the remote"
    - `origin` this specifies which remote we want to create this branch on.
    - `mybranch-<your-name>` the name of the local branch we want to create on the remote.

  Great, let's run this command now!

  This should give us an output like:
  