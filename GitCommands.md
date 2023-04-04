# List of Commonly used git commands

### Clone repository with limited history
    git clone --depth=1
    git log

### Add something to previous commit => Amending your commit
     git add .
     git commit --amend

    or

     git commit --amend -m "Incase you want to rename the message"

    or
    git commit --amend --no-edit

###  Check who changed what

    > git blame <filename>
    -s would give only commit id not name
    -l 1,3 just 3 lines
    -l 1,+5 start from 1st line and include next 5 lines

### Send changes to more than 1 repo

    git remote add origin <URL>
    git remote add working <NEW URL>


### Get concise history

    Generally git log  is used

    git log --oneline => shorter version

    git log --oneline --after="yesterday"
    git log --oneline --after="last week"
    git log --oneline --after="6 months ago"
    git log --oneline --grep="animation"

### Track down bugs

    git bisec start
    git bisect bad

    git log
    git checkout <commit id>

### Working more than one branch

    git worktree add <foldername>

### Send specific folder of specific branch to share with colleagues

        git archive
        git archive -o ../whatevername.zip = would put it one folder above

### Get rid of quick fixes
Take last 4 commit and merge it into single commit

    git rebase -i HEAD~4

### Marking items without branching

    git tag
    git tag v1014.1.1
    git tag v10.01.00.0 <commit id>
### Remove untracked documents

        git checkout . => remove staged files from stage
        git clean -ndf =>(for preview and d for directory)


### Renaming a branch

        git branch -mv master main
        git config --global init.defaultBranch main

### Remove all extra branch and only keep main branch

            git branch | grep -v "main|master" | xargs git branch -D

### Bring specific commits from on branch to other (Cherry picking)

            git checkout main
            git cheerry-pick commitID1 commitID2 commitID3 -n

### Undo a hard reset

    git reset --hard commitID
    git reflog



### Head
 It will show last commit and its changes

        git show HEAD
        git show <commit ID>
        git show HEAD~<[123]> based on number it would fetch last numbered commit


### Creating, Switching, Renaming and Deleting branch

        git branch -b <New branch name>
        git switch <Branch name>
        git branch -m <new name to branch> => Change current branch name
        git branch -D <Deleting branch name which should not be current branch>
        git checkout <branch name>

### Removing folder and file

            git clean -fD <file or folder>

### Undo changes to existing files

        git checkout <filename> would go to its previous state would loose all its changes
        git checkout -- <filename>




### Revert, Reset and Restore

Create a new commit that match state of previous commit

        git revert <commit ID> latest commit only undo latest commit, adds one more commit
        git revert --mixed => remove commits from history and move files to unstaged
        git revert --soft  => commits message removed from history files still maintained not staged
        git revert --hard

Remove prior commit and head as the given commit ID

        git reset <commit ID> makes this commit ID as head
        git reset . = Staged files will be unstaged
        --soft will remove commit but not file
        --hard will remove commit and files
        --medium will remove commit and move files to unstaged

Undo changed edited file

            git restore {{file name}}
            git restore --source HEAD~N {{filename}}
            git restore --staged {{filename}}



### Fetch and Pull

        git fetch  => Gets latest data from remote doesn't change working files

        git pull => git fetch + git merge
        Download changes and merge to current branch

### Cherry pick
        git cherry-pick <commit ID>

### Tags

Used to mark versioning or a particular state freeze

        git tag -a "Release v1.0" -m "Marking the tag version of release 1.0"
        git tag -l => Lists the available tags
        git tag -d <Tag name> => Would delete tag locally
        git push --delete origin <Tag name> => Would delete in remote

### Rebase vs Merge
* Incase of head is differnce between branch merge would create a commit
* For rebase irrespective of head the merge would not create a commit for merging


### Setting remote for local repo

        git remote add name http://url.git
        git remote add url https://url.git


