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
 
# 4. Convert local directory to a Git repo and link it to a remote GitHub repo

For this to work, your remote GitHub reposity **MUST** have the same name as your current local directory.

Add the following function to your .bashrc file in the same way as [#3](https://github.com/dg1223/tips-n-tricks/edit/main/README.md#3-push-code-with-a-single-command) above:
   ```
   function gitremote() {
    dirName=$(basename "$(pwd)")
    echo "# ${dirName}" >> README.md
    git init
    git add .
    git commit -a -m "initial commit"
    git branch -M main
    git remote add origin https://github.com/[your-github-username]/${dirName}.git
    git push -u origin main
}
```
Replace [your-github-username] (including the square brackets) with your GitHub username. This will create a README.md file in your current directory, initialize the directory as a Git repository and push everything to your remote GitHub repository that has the same name as your current directory.
   
Note that this code does not create a .gitignore file.

# 5. Shorten the current directory path shown on terminal
   
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


# 6. Enable remote connection to MariaDB

If MariaDB connector does not work, use the MySQL connector.

# 7. Upgrade to Python 3.9 on Ubuntu 18.04 LTS
This is mainly for AWS Cloud9 IDE because it only provides Ubuntu 18.04.

Add the deadsnakes repository
   
<code>sudo add-apt-repository ppa:deadsnakes/ppa</code>

<code>sudo apt-get update</code>

Install Python 3.9
   
<code>sudo apt-get install python3.9</code>

Check installed Python versions (optional)
   
<code>ls /usr/bin/python3.*</code>

Tell Ubuntu that it can now use either of the installed Python 3 versions. Option 1: Python 3.6; option 2: Python 3.9
   
<code>sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 1</code>

<code>sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.9 2</code>

Set Python 3.9 as primary Python 3 version. Enter the option number (probably #2) to set Python 3.9 as default.
   
<code>sudo update-alternatives --config python3</code>

Check default Python 3 version
   
<code>python3 --version</code>

The regular Python version still probably points to Python 2.x
   
<code>python --version</code>

If so, you can uset Python 2.x from being default for anything (optional)
   
<code>sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.9 1</code>

Now, everything should point to Python 3.9
   
<code>python --version</code>

<code>python3 --version</code>
   
You may have to reinstall the apt package manager so that it correctly points to Python 3.9
   
<code>sudo apt-get install python3-apt --reinstall</code>
   
Recreate symbolic link to the apt package
   
<code>cd /usr/lib/python3/dist-packages</code>

Check which apt_pkg.cpython-{version_number} your system has
   
<code>ls apt_pkg.cpython-*</code>
   
Link to this package file by replacing {your-version-number}, including replacing the braces, with your installed version number
   
<code>sudo ln -s apt_pkg.cpython-{your-version-number}-x86_64-linux-gnu.so apt_pkg.so</code>

For example,
   
<code>sudo ln -s apt_pkg.cpython-36m-x86_64-linux-gnu.so apt_pkg.so</code>
   
If you have more than one package installed, you can also do this. Keep the braces this time.
   
<code>sudo ln -s apt_pkg.cpython-{36m, 37m}-x86_64-linux-gnu.so apt_pkg.so</code>

You may also have to install the distutils package for Python 3.9

<code>sudo apt install python3.9-distutil</code>

Check if its installed correctly. You should see no traceback calls

<code>python3 -c "from distutils import sysconfig"</code>
   
   
### Sources
[How to upgrade to Python 3.9.0 on Ubuntu 18.04 LTS](https://www.itsupportwale.com/blog/how-to-upgrade-to-python-3-9-0-on-ubuntu-18-04-lts)

[Change the Python3 default Version in Ubuntu](https://dev.to/meetsohail/change-the-python3-default-version-in-ubuntu-1ekb)

[python-dev installation error: ImportError: No module named apt_pkg](https://stackoverflow.com/questions/13708180/python-dev-installation-error-importerror-no-module-named-apt-pkg)

[ImportError: cannot import name 'sysconfig' from 'distutils' ](https://askubuntu.com/questions/1292972/importerror-cannot-import-name-sysconfig-from-distutils-usr-lib-python3-9)

# 8. Update tailwind.config.css file to enable TailwindCSS CLI
In <code>module.exports</code>, content should be <code>content: ["*"],</code>

You can replace the <code>*</code> with more granular file paths but do not use the default code from Tailwind's installation instructions.

# 9. Change origin for a newly initialized local Git repository to a new remote GitHub repository
Everything from <code>git init</code> to <code>git push -u origin main</code> remains the same except for the following line:

<code>git remote set-url origin git@github.com:[your_github_account_name]/[your_github_repo_name].git</code>

For the URL, copy the SSH URL of the Git remote repository.


### Sources
[How to Change Git Remote Origin(URL)](https://linuxhint.com/change-git-remote-origin-url)

# 10. Set your GitHub credentials for VSCode from Linux terminal

In the command line, enter <code>gh auth login</code>, then follow the prompts. 
