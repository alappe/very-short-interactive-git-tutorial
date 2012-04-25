# Very Short Interactive Git Tutorial

This repository should give you an easy way to play around with several
features of the git-scm and to try to branch, merge and resolve
conflicts without actually working in a real-life project.

That being said, working in a real project would give you more, so
consider this option seriously before proceeding.

## Commit

First let's start by committing some changes to this repository, simply
to get us going and warm up the keyboard.

While this should give you a chance to play with, this is no replacement
for documentation, so if you don't know that I talk about in here, go
read the man-pages to git, the documentation available on
[the git homepage](http://www.git-scm.com) or any other stuff you like to get your
knowledge.

All commands are entered from within the root of the tutorial directory
structure if not otherwise noted.

### Status

Open up `Data/SimpleCommit.json` in your favorite text editor (from now on
called `$EDITOR`) and fill out the three fields name, email and date.

With `git status` you should now see that the file `Data/SimpleCommit.json`
has changed and is not staged for commit. Yay!

### Simple commit

So let's commit this changes to the file by calling `git commit
Data/SimpleCommit.json` (Note that `git commit -a`, `git commit Data` and `git
commit .` would also work but would not be the same. Read up on it to
know when to use what…!).

This opens `$EDITOR` to let you write a commit message. The style of the
message differs from project to project, so refer to the CGL of the
project you will be working on the future to start using the correct
syntax now. If in doubt read
[tpopes blog entry](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
on this topic.

After saving the message, your commit is done.

### Read the log

A simple way to see what changed over time in your project is to read
the log with `git log`. Scroll down to see older commit messages.

Use this method to verify that the previous commit has been saved. If it
didn't work, write a hate-mail to git-tutorial@example.net to calm down.

### Partial commit

Well, this was easy, wasn't it? It certainly should have been, because
this is what you'll do several dozen times a day. Get used to it. Now
let's do something a bit more fancy:

Let's do several changes to a file and commit them in several logical
parts. For this, fire up `$EDITOR` to edit `Data/PartialCommit.json` and
again fill out the three parts with data of imaginary friends, your
favorite stuffed toys or whatever you like.

Now we'll assume that it's important to split this change into three
commits, one for the names (a commit message would be something along
the lines of »Adding names of imaginary friends.«), one for the email
(…) and one for the date (you're still reading these texts in the
brackets, aren't you?).

This is done (one way, at least) with the command `git add --patch
Data/PartialCommit.json` which starts an interactive way to stage hunks
(partial changes). Use `s` to split the big hunk into three parts, then
use the `e` command to change the hunks so that you end up with a staged
version of `Data/PartialCommit.json` that only changes the name. To
check this, use `git diff --cached`, it should result in something
similar to:

	diff --git a/Data/PartialCommit.json b/Data/PartialCommit.json
	index c224230..e518abb 100644
	--- a/Data/PartialCommit.json
	+++ b/Data/PartialCommit.json
	@@ -1,16 +1,16 @@
	 [{
		// One
	-       name: '',
	+       name: 'Aasubsioh',
		email: '',
		date: ''
	 },{
		// Two
	-       name: '',
	+       name: 'hdoihdoih',
		email: '',
		date: ''
	 },{
		// Three
	-       name: '',
	+       name: 'oidhiohd',
		email: '',
		date: ''
	 }]
 
Commit this staged change with `git commit` and use a descriptive commit
message. Repeat this process for email and date. Read the log and be a
little bit proud…

## Amend

With software, there a several ways to screw up. If you didn't already
push out your changes you can adjust your last commit to fix a bug you
introduced (or simply change the message).

For this, let's reuse one of the previous commits: `git commit -amend`.
This is a very simple case, so read the `git-commit` manpage to get a
more thorough understanding of what happens here and what more complex
stuff can be done.

## Branch

Everybody loves trees, right? So let's play with branches…

### Add a branch

A branch is easily added with `git branch myFirstBranch` which uses your current
branch (master) as a base. Then switch over to the new branch with `git 
checkout myFirstBranch` (or show-off to your coworkers by combining
those two steps into one with `git checkout -b myFirstBranch master`).

### Use branches

Switch back to your master with `git checkout master` and clean up the
unused (but still first and cool) branch with `git branch -d
myFirstBranch`.

## Merge

Branches only make sense if you work on them and often you will want to
get changes and features from a branch back into your master (or any
other branch for that matter).

Head off to a branch with `git checkout -b validJson master` and adjust
`Data/SimpleCommit.json` to be a valid json-file by surrounding the keys
with double-quotes (") as well as changing all single-quotes to
double-quotes. Commit as usual.

Now to get this back into your master, switch to it (I could list the
command here, but I won't… you should know that by now!) and use `git
merge validJson` to get those changes in. Read the log to verify the
changes.

## Conflicts

Merging can produce conflicts that have to be resolved by you. Right,
you. So practice how to do that:

Add a branch called »movieStars« and adjust
`Data/PartialCommit.json` to three movie-stars you recently stalked (or
use your fantasy) and commit that.

Head back to your master branch and adjust `Data/PartialCommit.json` to
three Teletubbies you like most (and yes, commit it… riight).

Merge in your movieStars-branch and you shall get a nice conflict. Fix
it so that Teletubbies win.

## Reset (this tutorial)

Read the log back to the point before you started to commit to it, then
use `git reset --hard $SHA` with the original SHA1 hash to reset it to
the beginning. Rinse and repeat.

## License

This tutorial, as small as it is, shall have a license too—therefor:


