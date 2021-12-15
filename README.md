# 1. How to change your git commit history #
  https://stackoverflow.com/questions/3042437/how-to-change-the-commit-author-for-one-specific-commit/3042512#30425120

# 2. Connecting to GitHub with SSH #

   If you are fed up with providing your username and PAT (Personal Authentication Token) every time you push your code to GitHub, you need to configure your Git      repo with SSH authentication. There are already plenty of documentations and stack overflow threads on how to do it. So, I am just leaving some links here that      worked for me.
   
   [Connecting to GitHub with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
   
   Go through the entire documentation above, step by step, to create your SSH key pair if you don't have them already. I did it on my Ubuntu 20.04.
   
   Once you have done that, you will have to initialize your local git repository. A local repo is a repo that's in your computer and is synced/connected to its        clone on GitHub or vice-versa. It's basically called a local-remote setup for your git repo. Assuming that you have a terminal open and you are inside the folder    of your local repo (you cd'd into it), run the command 
   
   <code>git init</code> 
   
   to initialize (or reinitialize in some cases) this repo with a <code>.git</code> folder.
   
   Now run the command 
   
   <code><git config remote.origin.url "git@github.com:your-GitHub-repo-name.git"</code> 
  
  where "your-GitHub-repo-name" is the name of the git repo your are trying to push code to (the same repo we are talking about here and that you have just cd'd       into). For example, if I want to remote to this git repo from my local Ubuntu desktop, then, I will execute 
  
  <code>git config remote.origin.url "git@github.com:python-deepdive.git"</code> .
  
  You can check if you have successfully configured this git repo by running the command
  
  <code>git config --get remote.origin.url</code>
  
  This command will display the git remote URL that you just configured your repository with.
  
  Now, whenever you do <code>git push</code>, you won't have to enter your GitHub credentials to push to this repo. However, if you have a SSH passphrase set up,   then you'll be asked to enter that passphrase before pushing. You'll see an option to disable this check on that pop-up window. Select it and you won't be         bothered again.
  
  ### Sources ###
  [Git asks for username every time I push](https://stackoverflow.com/a/34957424)
  
  [Git: Receiving "fatal: Not a git repository" when attempting to remote add a Git repo](https://stackoverflow.com/a/4630763)
  
