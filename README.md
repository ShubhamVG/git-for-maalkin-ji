# git-for-maalkin-ji
First let's get this clear: <b>What is the difference between Git & GitHub?</b>
So, Git, by definition, is a version control system but the way I like to say is that it is a tool to make <u>a collection of code (AKA a git repo)</u> so that migration, collaboration and branching (making different versions) is easy.
GitHub on the other hand is a platform where you can host and manage your Git repositories.

Now that we have this cleared, [download git](https://git-scm.com/downloads) or [build from source if you have too much chest hair or something](https://github.com/git/git/blob/master/INSTALL).

## What's in this lesson?
Let's dive right into the practical work. First I will tell you how to clone a repo and contribute (which is what we mostly do) and after that I will also tell you how to push your code that you have already been working on.

## Fork and Contribute (Practical work incl.)
Start with forking this repo. You should see a `Fork` button on top of this GitHub page.
A fork is a copy of a Git repo. When you fork this repo, the same repo is copied onto your GitHub profile. Forks are useful so that multiple people can contribute on the same repo even if they are not part of the project.

After forking, go to the forked repo and copy its url. It should look like `https://github.com/<your-name-or-org>/<repo-name>`.

Now that you have the url, open a terminal (i.e., command prompt or powershell for windows users) and type this command:
```
git clone <repo-url>
```
This will download the folder of your source code. If you wanna open this into VS Code directly using the terminal, use this command:
```
code <folder-name>
```

After that, just make the edits to the code as you like. Add file, delete file, do whatever you want. For this tutorial, I want you to open the [sign-here.txt](./sign-here.txt) file and add your name to the very end. After that, run the following commands, actually understand what it does first (each $ means a different line):
```
$ git add .
$ git commit -m "enter a message"
```
- The `git add <filename>` adds the file that you are ready to be commited or pushed. `add .` means add everything, alternatively you can also use `git add --all`.
- The `git commit -m "enter message"` will update your Git repo (not on GitHub directly) with the files you added before. `-m "message"` is very important as that is used to say what updates those specific commit provides. It can be single line or multiple line. Some use it twice like to add a title and description like:
```
git commit -m "Title" -m "Long description"
```

Now comes the part where you push it to GitHub. First off, you need to tell the Git locally installed on your PC that you really own (or are a member of) the GitHub repo that you're gonna push this repo on. To do that, we use something called tokens.

To be able to push code to github, [generate a GitHub token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens) by going to (assuming you are logged in) [https://github.com/settings/tokens](https://github.com/settings/tokens). I suggest the classic token. Don't forget to copy the token somewhere as it is only visible once.

Now look, since you have cloned this repo on step 1. Your Git files (some hidden files in the .git folder) already know the location where it came from. That location is called origin. We will talk more about this on the later section but for now, know that your origin is set to, well, in a read-only mode. To fix it, and this is only a one time thing, you have to edit the origin's url by adding your token so that Git knows that it is really you who is trying to push to GitHub.

You can change origin's url by opening a terminal; VS Code's terminal works too or any other terminal, just make sure that the location is the code directory that you are working on. Not gonna give any terminal tutorial here lol. Anyways, so this command:
```
git remote set-url origin https://<TOKEN>@github.com/<USER-OR-ORG>/<REPO>
```
e.g.,
```
git remote set-url origin https://ghp_oOgAB0oGaCaVeMaNBrA1n@github.com/maalkin/stinky-repo
```

After that, you are done. To push to GitHub run this command:
```
git push -u origin main
```
This `-u origin main` is a one time thing only. The `-u` sets the upstream origin to the `main` branch.
Once the upstream is set, just `git push` is enough.

Nowwwwwwww, go to your GitHub and to your repo and you will see that it has been updated and the new code has been added :)
Congrats on your first push ig hahaha.

## GitHub repo from scratch
Time to tell you how to push code that is already on your PC but not on your repo. By the way, you can also do this using the previous method. Just go to GitHub and create a new repo there. There should be a `New` button in bright green when you are on your profile page (whose url looks like `https://github.com/<your-name-or-org>`).

After that, clone the repo. Copy paste the files that you wanna push to that cloned folder. Push as I told you before.

But here's the new way; First go the folder where your code is present. Then run this command:
```
git init
```
This will initiate a repo with the necessary information it needs. After that:
```
$ git add .
$ git commit -m "enter message"
```
All this is familiar but here's the new step; create a new repo on GitHub. Copy its link. Come back to the terminal and type this command:
```
git remote add origin https://<TOKEN>@github.com/<USER-OR-ORG>/<REPO>
```
This will add the remote host like GitHub or GitLab's repo's link as the name origin. This is a one time thingy as expected.

After that the `git push -u origin main` (first time) or `git push` as usual to push.
Reload your GitHub repo now (on the browser) and the codes and files should be present now.

## Intro to branches, pull requests and merge.
### Branches
By default, a Git repo is on the main branch (or master branch depending on how you have configured the name to be). But sometimes, you need more branches. I make temporary branches frequently so that I can merge it to main if everyone works correctly or fall back to the last commit in case it doesn't. They have a lot of other uses too.

To check how many branches you have, use this command:
```
git branch
```

To make a new branch, use:
```
git branch <branch-name>
```

To delete a branch:
```
git branch -D <branch-name>
```

To switch between branches:
```
git checkout <branch-name>
```

When you make a branch, you should set a new upstream as well before pushing to GitHub;
```
git push -u origin <current-branch>
```
What this will do is create a new branch on your GitHub page so that you won't have to. One time thing only ofc.

### Pull request (practical work incl.)
After making a fork and adding changes, you can go to the original repo's link and then you will see a `Contribute` or `Compare & pull request` button. It appears when you have forked a repo and it has some changes from the original repo like some code addition or removal, files, etc etc.

I want you to create a pull request and I will merge it when I see your PR (pull request).

### Merging
When you get a pull request, which you get on GitHub so on your repo page, you check whether it is worth merging and if it is, approve it and merge it. After merging though, make sure to resync your git repo locally by using `git pull` or something (read about it below).

There is also `git merge <branch-to-merge>` command and this merge the branch you gave as input with the current branch you are on. Personally, I never do this and I just git pull instead.

### Sync with contributions (pull/fetch)
When multiple people are working on the same project, everyone is working on a different part of the program (at least sane teams do) and you wanna try to be as synced as possible and the way to do it is using:
```
git pull
```
By default, it will pull from YOUR repo/fork and from the same branch but sometimes you wanna pull from the upstream (AKA the original repo that you forked) or from a different branch. The way you do the latter (branch one) is like this:
```
git pull origin <branch-name>
```

For upstream, you gotta add it as a remote location first so like:
```
git remote add upstream https://github.com/<original-owner>/<original-repo>
```
and then pull like
```
git pull upstream <branch-name>
```

I suggest doing a pull everytime before you start editing your files (assuming you're on a team). There might be conflicts but they are a pain to solve and I rarely ever face 'em because I am a neat boi ;D
But yeah, I don't know how to deal with those. Learn from stackoverflow or youtube lol.

## Important commands
There are more important commands that you can read from the web. Imma mention some common ones here:
- `git pull`
- `git clone`
- `git branch`
- `git checkout`
- `git merge`
- `git stash`
- `git restore`:
- `git reset`: This is what you use to fall back to the last/given commit in case you f up. I do use `git reset --hard HEAD` often because I f up often :p

## That was it!
Open an issue on this repo if something is not working or if you have any questions that google could not answer. Star the repo and follow me if you appreciate me lol. k thx bye!
