# git-overlook

Sometimes there's stuff in my repo that I modify for personal tastes temporarily: say I hardcode the path to something in code in the repo or whatever as I'm iterating on things. 

It's very annoying in these cases for me to skip the file when I `git add -p` and stuff like that.
What would be great is if I could just ignore the file entirely until something changed in it.

This pretty much just uses `git update-index --skip-worktree` and its inverse to ignore the file and does the ugly thing of storing that information in the `$GIT_DIR/overlook/` directory with some rudimentary escaping. I don't have any exotically named files in my repos so this does the trick.

The final piece of this is that I a pre-commit hook to the repo so that when I try to commit something while these overlooked files have been changed and remain overlooked, the commit won't fire and you'll get an error message to affirm the overlooking or to bring the file back into consideration.

## Installation

1. Copy `./git-overlook` and `./git-relook` to somewhere in your `$PATH`.

2. Install the script in `./pre-commit` as a pre-commit hook into your `$GIT_DIR/hooks`. If you haven't done anything there before, this is just `cp ./pre-commit $YOUR_GIT_DIR/hooks`

Now, when you have a file you want to ignore for some time, do `git overlook path/to/file/in/repo`.

## Usage

### Overlooking

```
git overlook path/to/file/in/repo
```

### Un-overlooking

```
git relook path/to/file/in/repo
```

### Listing overlooked files

```
git overlook
```

## Warnings

I don't have spaces in my code filesystem as a matter of course, so I did not check to see if those are all handled correctly exhaustively
