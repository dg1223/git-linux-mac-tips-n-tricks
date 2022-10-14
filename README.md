# Intro
If you are new to Git or have not had to use Git too much before but now your dev world is getting heated up, this guide is for you. It's a collection of Git-related tips and tricks (some Linux tricks as well) that helped me to significantly cut down the time spent on executing repetitive Git operations on a daily basis. My original intention was to create a repository for myself and only jot down rough notes so that I can come back to these tips-n-tricks whenever I need to. However, I think writing these down in a documentation format will not only benefit me but also other people who are on the same boat as I am.

If the notes below have helped you in any way, please give this repo a star :) <br><br>

# 1. How to change your git commit history
https://stackoverflow.com/questions/3042437/how-to-change-the-commit-author-for-one-specific-commit/3042512#30425120 <br><br>

# 2. Connecting to GitHub with SSH

If you are fed up with providing your username and PAT (Personal Authentication Token) every time you push your code to GitHub, you need to configure your Git repo with SSH authentication. There are already plenty of documentations and stack overflow threads on how to do it. So, I am just leaving some links here that worked for me.
   
[Connecting to GitHub with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
   
Go through the entire documentation above, step by step, to create your SSH key pair if you don't have them already. I did it on my Ubuntu 20.04.
   
Once you have done that, you will have to initialize your local git repository. A local repo is a repo that's in your computer and is synced/connected to its clone on GitHub or vice-versa. It's basically called a local-remote setup for your git repo. Assuming that you have a terminal open and you are inside the   folder of your local repo (you cd'd into it), run the command 
   
<code>git init</code> 
   
to initialize (or reinitialize in some cases) this repo with a <code>.git</code> folder.
   
Now run the command 
   
<code><git config remote.origin.url "git@github.com:your-GitHub-repo-name.git"</code> 
  
where "your-GitHub-repo-name" is the name of the git repo your are trying to push code to (the same repo we are talking about here and that you have just cd'd into). For example, if I want to remote to this git repo from my local Ubuntu desktop, then, I will execute 
  
<code>git config remote.origin.url "git@github.com:python-deepdive.git"</code> .
  
You can check if you have successfully configured this git repo by running the command
  
<code>git config --get remote.origin.url</code>
  
This command will display the git remote URL that you just configured your repository with.
  
Now, whenever you do <code>git push</code>, you won't have to enter your GitHub credentials to push to this repo. However, if you have a SSH passphrase set up, then you'll be asked to enter that passphrase before pushing. You'll see an option to disable this check on that pop-up window. Select it and you won't be bothered again.
  
### Sources
[Git asks for username every time I push](https://stackoverflow.com/a/34957424)
  
[Git: Receiving "fatal: Not a git repository" when attempting to remote add a Git repo](https://stackoverflow.com/a/4630763) <br><br>
  
# 3. Push code with a single command
  
The usual way to push your code to a remote Git repository is to follow the **git add-commit-push** cycle. But that's three commands. You can reduce this repetitive task to two or even a single command.

[ **JUMP below if you 'just want the single command'** ]

  
If you want to bundle add and commit only for more control over the commit command, you can just add this simple alias to your git config file by running this command in the terminal inside your local git repository:
  
<code>git config --global alias.add-commit '!git add . && git commit'</code>

[ **JUMP here for single command git push** ]
  

Bundling all three together is a more involved task and takes away your freedom of choosing different parameters for the commands but you basically have one command to execute. I think that's pretty neat!

To do this, open your .bashrc file (if you are using Linux) or its equivalent and add the following function. Although you can use Vim (the default VI editor) to edit the file in your terminal, which many Linux pros do, as a millenial, I hate using it most of the time. It's old and cumbersome. I do it the easy way.
  
  - Open the terminal (<code>Ctrl + Alt + T</code>)
  - Open the **.bashrc** file for editing with: <code>gedit ~/.bashrc</code>
  - Add the following function at the end of the file:
  
        function gitpush() {
            git add .
            git commit -a -m "$1"
            git push
        }
  - Save the file (<code>Ctrl + S</code>)
  - Run this command in the terminal: <code>source ~/.bashrc</code>

Now you can push your code to your remote repository with this single command: <code>gitpush "your commit message"</code>
  
### Source
[git add, commit and push commands in one?](https://stackoverflow.com/a/23328996) <br><br>

# 4. Shorten the current directory path shown on terminal
   
When you are deep into a directory structure that has many folders, your terminal may show your current directory path like this:
   
<code>shamir@dg:~/Documents/Software/php-app$</code>

It makes running long commands a messy situation, especially when you have the terminal window downsized for convenience. To shorten the path name so that the terminal only shows your current directory, you can do the following:
   
  - Open the terminal (<code>Ctrl + Alt + T</code>)
  - Open the **.bashrc** file for editing with: <code>gedit ~/.bashrc</code>
  - Add the following line at the end of the file: <code>PS1="\u@\h: \W:\$"</code>
  - Save the file (<code>Ctrl + S</code>)
  - Run this command in the terminal: <code>source ~/.bashrc</code>

Now the path name should look like this:
   
<code>shamir@dg: php-app:$</code>
   
### Source
[How do I shorten the current directory path shown on terminal?](https://unix.stackexchange.com/questions/381113/how-do-i-shorten-the-current-directory-path-shown-on-terminal)


# 5. Enable remote connection to MariaDB

If MariaDB connector does not work, use the MySQL connector.

