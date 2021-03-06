                                                            
# Git Guide                                                 
                                                            
                                                            
## Setup                                                    
                                                            
    git config --global user.name "<insert username>"               # set username
    git config --global user.email "<insert e-mail>"                # set e-mail
    git config --global --unset user.password                       # delete user password
    git remote add origin "<repo url>"                              # Sets origin url
                                                                    
## New Install Workflow                                             
                                                                    
    git init                                                        # set git workspace here
    git clone "<insert url>"                                        # clone a repository 
                                                                    
## New Install Workflow                                             
                                                                    
    git pull origin master                                          # pull and merge remote repo with local
    git add .                                                       # add current workspace to repository
    git status                                                      # doublecheck this is what you expected
    git commit -m "<insert message about what you added>"           # commits changes, preparing to add to repo
    git push origin master                                          # pushes changes to repo
                                                                    
                                                                    
                                                                    
                                                                    
## Branching                                                        
                                                                    
    git clone -b <branch name> --single-branch <repo url>           # Clones branch of repo to this path
    git branch <branch name>                                        # Creates branch name
    git checkout <branch name>                                      # Moves to new branch
    git checkout -b <branch name>                                   # Creates branch and moves you to branch
                                                                    
                                                                    
## Versioning                                                       
    git log                                                         # See commit history
    git checkout <hash from log>                                    # Revert branch to just before last commit
    git revert <commit hash>                                        # Completely undo a commit
    git checkout -b <new branch name>                               # Create new branch for this version
                                                                    
    git reset --hard <remote name>/<branch name>                    # Resets branch to original position
    git clean -f -d                                                 # Cleans up branch, especially helpful after a reset
                                                                    
                                                                    
## Troubleshooting                                                  
                                                                    
    git push origin master --force                                  # sometimes you need to force 
                                                                    the push (I.E. changed local repo location)
    git remote -v                                                   # see where the remote origin is pointing
    git -rf .git                                                    # uninitiate local .git file
    git merge --abort                                               # abort merge    
                                                                    
    git fetch                                                       # Use these two lines if you run into trouble with committing before pulling
    git merge                                                       
                                                                    
    git reflog                                                      # See historical changes that you can rebase on
    git reset --hard HEAD@{<insert head number>}                    # Rebase on that head               
                                                                    
                                                                    
## Pull and overwrite local changes                                 
                                                                    
    git fetch --all                                                 # fetches (pulls without merging) all branch info
    git reset --hard origin/<branch>                                # overwrites local data
        
        
## Pushed to remote and just didn't get that last change in?    
    
    git add .                                                       # stages new changes
    git reflog                                                      # find the corresponding modification
    git reset --hard HEAD@{<insert head number>}                    # rebase on that head  
    git commit --amend -m "<input new message>"                     # ammends the new changes and comment to the old commit to the local repo
    git push --force <remote name> <branch name>                    # Overwrites the old commit with the new one on the remote repo
    
## Workflow transfer repo branches

    Setup
        Go to new path you want to user
        git remote add source <insert source URL>                   # Insert the remote repo link you want to copy from (I.E. github)
        git remote add dest <insert destination URL>                # Insert the remote repo link you want to copy to (I.E. bitbucket)
        
    Note: Use the branch that is the earliest version you want as a "trunk" for the branches to come from
        git clone -b <1st branch name> --single-branch <repo url>   # Clones branch of repo to this path
    
    Create and populate new branch
        git checkout -b <new branch name>                           # Creates branch and moves you to branch
        git reflog                                                  # look for the Head# that corresponds to your trunk
        git reset --hard HEAD@{<head#>}                             # Resets your history and version to the trunk version
        git pull source <new branch name> -q                        # pulls (and merges) branch quietly without requiring a message
    
    Note: repeat the last two steps for all branches you want to transfer
    
    Push all branches to destination repo
        git push dest --all                                         # Pushes all branches to destination repository
    

    