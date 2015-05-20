Clone a repository. I have created a test repository for us to play with.

If you have set up your ssh keys use SSH. Otherwise just switch it to HTTPS. For setting up SSH reference here https://confluence.atlassian.com/display/BITBUCKET/Set+up+SSH+for+Git

git clone git@bitbucket.org:punsarn/playground.git


Create a branch. Please do not work on “master” branch as it should contained reviewed/tested code only. 

cd playground
git branch (to check the current branch)
git branch than/new-text-123 (create a new branch named than feature)
git checkout than/new-text-123 (switch branch to than-feature)

Please name your branch with this convention. {YourName}/{Short-Description}-{#TrackingNumber}. For the tracking number it is the number from Issue Tracker.
Make changes to your branch

nano notes.txt
git status (to check modified files)
git add notes.txt (this will add the changed file to the staging)    
git commit -m 'Added feature 123 adding a new line in notes.txt'
(repeat adding files and committing if there’s more than one changed file)


Pushing your branch to Bitbucket
git push origin than/new-text-123
Creating a pull request for your branch

Click on “Create pull request” and select your branch on the left one. On the right one select “master” branch. Add title and description if you have any.
Once submitted your pull request will be checked and merged into the “master” branch by whoever managing the repository. 
If you want to fix another new bug or add a new feature you should pull updates from the Bitbucket first. Run
git checkout master (switch to master branch)
git pull origin master (pull updates from master branch)


Create a branch for your new feature or bug fix following steps 2. Rinse and repeat. 


General Notes
You might want to set up your git email and name if you haven’t.
git config --global user.email "your_email@example.com"
git config user.name "Billy Everyteen"
git config user.email (Checking if email is set correctly)
git config user.name (Checking for username)
Nice links
Learn Git Basics https://try.github.io/levels/1/challenges/1 
Learn Git Branching https://try.github.io/levels/1/challenges/1 
Pull Requests Documentation https://help.github.com/articles/using-pull-requests/#article-platform-nav 
Git tips http://rypress.com/tutorials/git/tips-and-tricks 
Sample branches and pull requests on edx-platform https://github.com/edx/edx-platform/branches 


