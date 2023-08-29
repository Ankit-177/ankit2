---
layout: post
title: Linux Shell and Bash
description: A Tech Talk on Linux and the Bash shell.
toc: True
comments: True
categories: ['5.A', 'C4.1']
courses: {'csse': {'week': 1}, 'csp': {'week': 0, 'categories': ['6.B']}, 'csa': {'week': 0}}
type: devops
---

## Bash Tutorial
> A brief overview of Bash, on your way to becoming a Linux expert.  When a computer boots up, a kernel (MacOS, Windows, Linux) is started.  This kernel provides a shell that allows user to interact with a most basic set of commands.  Typically, the casual user will not interact with the shell as a Desktop User Interface is started by the computer boot up process.  To activate a shell directly, users will run a "terminal" through the Desktop. VS Code provides ability to activate "terminal" while in the IDE.

## Prerequisites
> Setup bash shell dependency variables for this page.

- Hack: Change variables to match your project.


```python
%%script bash

# Dependency Variables, set to match your project directories

cat <<EOF > /tmp/variables.sh
export project_dir=$HOME/vscode  # change vscode to different name to test git clone
export project=\$project_dir/ankit2  # change teacher to name of project from git clone
export project_repo="https://github.com/Ankit-177/ankit2.git"  # change to project of choice
EOF
```


```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

# Access the variables
echo "Project dir: $project_dir"
echo "Project: $project"
echo "Repo: $project_repo"
```

    Project dir: /home/ankitp/vscode
    Project: /home/ankitp/vscode/ankit2
    Repo: https://github.com/Ankit-177/ankit2.git


## Setup Project
> Pull code from GitHub to your machine. This script will create a project directory and add "project" from GitHub to the vscode directory.  There is conditional logic to make sure that clone only happen if it does not (!) exist.


```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Using conditional statement to create a project directory and project"

cd ~    # start in home directory

# Conditional block to make a project directory
if [ ! -d $project_dir ]
then 
    echo "Directory $project_dir does not exists... makinng directory $project_dir"
    mkdir -p $project_dir
fi
echo "Directory $project_dir exists." 

# Conditional block to git clone a project from project_repo
if [ ! -d $project ]
then
    echo "Directory $project does not exists... cloning $project_repo"
    cd $project_dir
    git clone $project_repo
    cd ~
fi
echo "Directory $project exists." 
```

    Using conditional statement to create a project directory and project
    Directory /home/ankitp/vscode exists.
    Directory /home/ankitp/vscode/ankit2 exists.


### Look at files Github project
> All computers contain files and directories.  The clone brought more files from cloud to your machine.  Review the bash shell script observe the commands that show and interact with files and directories.

- "ls" lists computer files in Unix and Unix-like operating systems
- "cd" offers way to navigate and change working directory
- "pwd" print working directory
- "echo" used to display line of text/string that are passed as an argument


```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Navigate to project, then navigate to area wwhere files were cloned"
cd $project
pwd

echo ""
echo "list top level or root of files with project pulled from github"
ls

```

    Navigate to project, then navigate to area wwhere files were cloned
    /home/ankitp/vscode/ankit2
    
    list top level or root of files with project pulled from github
    Gemfile
    Gemfile.lock
    LICENSE
    Makefile
    README.md
    _config.yml
    _data
    _includes
    _layouts
    _notebooks
    _posts
    _site
    compsci.md
    images
    index.md
    indexBlogs.md
    indexHelp.md
    scripts


### Look at file list with hidden and long attributes
> Most linux commands have options to enhance behavior

[ls reference](https://www.rapidtables.com/code/linux/ls.html)


```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Navigate to project, then navigate to area wwhere files were cloned"
cd $project
pwd

echo ""
echo "list all files in long format"
ls -al   # all files -a (hidden) in -l long listing
```

    Navigate to project, then navigate to area wwhere files were cloned
    /home/ankitp/vscode/ankit2
    
    list all files in long format
    total 100
    drwxr-xr-x 12 ankitp ankitp 4096 Aug 28 01:53 .
    drwxr-xr-x  4 ankitp ankitp 4096 Aug 28 01:36 ..
    drwxr-xr-x  8 ankitp ankitp 4096 Aug 28 01:57 .git
    drwxr-xr-x  3 ankitp ankitp 4096 Aug 28 01:36 .github
    -rw-r--r--  1 ankitp ankitp  104 Aug 28 01:36 .gitignore
    -rw-r--r--  1 ankitp ankitp  122 Aug 28 01:36 Gemfile
    -rw-r--r--  1 ankitp ankitp 7293 Aug 28 01:53 Gemfile.lock
    -rw-r--r--  1 ankitp ankitp 1081 Aug 28 01:36 LICENSE
    -rw-r--r--  1 ankitp ankitp 3120 Aug 28 01:36 Makefile
    -rw-r--r--  1 ankitp ankitp 5798 Aug 28 01:36 README.md
    -rw-r--r--  1 ankitp ankitp  451 Aug 28 01:36 _config.yml
    drwxr-xr-x  2 ankitp ankitp 4096 Aug 28 01:36 _data
    drwxr-xr-x  2 ankitp ankitp 4096 Aug 28 01:36 _includes
    drwxr-xr-x  2 ankitp ankitp 4096 Aug 28 01:36 _layouts
    drwxr-xr-x  2 ankitp ankitp 4096 Aug 28 01:44 _notebooks
    drwxr-xr-x  2 ankitp ankitp 4096 Aug 28 01:53 _posts
    drwxr-xr-x  8 ankitp ankitp 4096 Aug 28 01:53 _site
    -rw-r--r--  1 ankitp ankitp   91 Aug 28 01:36 compsci.md
    drwxr-xr-x  2 ankitp ankitp 4096 Aug 28 01:36 images
    -rwxrwxrwx  1 ankitp ankitp 2838 Aug 28 01:43 index.md
    -rw-r--r--  1 ankitp ankitp   53 Aug 28 01:36 indexBlogs.md
    -rw-r--r--  1 ankitp ankitp   50 Aug 28 01:36 indexHelp.md
    drwxr-xr-x  3 ankitp ankitp 4096 Aug 28 01:36 scripts



```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Look for posts"
export posts=$project/_posts  # _posts inside project
cd $posts  # this should exist per fastpages
pwd  # present working directory
ls -l  # list posts
```

    Look for posts
    /home/ankitp/vscode/ankit2/_posts
    total 68
    -rw-r--r-- 1 ankitp ankitp   704 Aug 28 01:36 2023-08-15-Tools_Plans_Sample.md
    -rw-r--r-- 1 ankitp ankitp  4447 Aug 28 01:36 2023-08-16-Tools_Hacks_Sample.md
    -rw-r--r-- 1 ankitp ankitp   549 Aug 28 01:36 2023-08-16-Tools_Help.md
    -rw-r--r-- 1 ankitp ankitp 25923 Aug 28 01:53 2023-08-16-linux_shell_IPYNB_2_.md
    -rw-r--r-- 1 ankitp ankitp  3751 Aug 28 01:53 2023-08-17-Markdown_Table_Code_Hack_IPYNB_2_.md
    -rw-r--r-- 1 ankitp ankitp  2052 Aug 28 01:36 2023-08-21-GitHub_Pages_Plans.md
    -rw-r--r-- 1 ankitp ankitp  1003 Aug 28 01:36 2023-08-21-GitHub_Pages_Tangibles.md
    -rw-r--r-- 1 ankitp ankitp  6356 Aug 28 01:53 2023-08-21-HTML_Image_Hack_IPYNB_2_.md
    -rw-r--r-- 1 ankitp ankitp  2448 Aug 28 01:36 2023-08-26-GitHub_Sync.md



```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Look for notebooks"
export notebooks=$project/_notebooks  # _notebooks is inside project
cd $notebooks   # this should exist per fastpages
pwd  # present working directory
ls -l  # list notebooks
```

    Look for notebooks
    /home/ankitp/vscode/ankit2/_notebooks
    total 60
    -rwxrwxrwx 1 ankitp ankitp 35278 Aug 28 01:45 2023-08-16-linux_shell.ipynb
    -rw-r--r-- 1 ankitp ankitp  5506 Aug 28 01:36 2023-08-17-Markdown_Table_Code_Hack.ipynb
    -rw-r--r-- 1 ankitp ankitp  8948 Aug 28 01:36 2023-08-21-HTML_Image_Hack.ipynb
    -rwxrwxrwx 1 ankitp ankitp  2240 Aug 28 01:44 quiz.py



```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Look for images in notebooks, print working directory, list files"
cd $notebooks/images  # this should exist per fastpages
pwd
ls -l
```

    Look for images in notebooks, print working directory, list files
    /home/ankitp/vscode/ankit2/_notebooks
    total 60
    -rwxrwxrwx 1 ankitp ankitp 35278 Aug 28 01:45 2023-08-16-linux_shell.ipynb
    -rw-r--r-- 1 ankitp ankitp  5506 Aug 28 01:36 2023-08-17-Markdown_Table_Code_Hack.ipynb
    -rw-r--r-- 1 ankitp ankitp  8948 Aug 28 01:36 2023-08-21-HTML_Image_Hack.ipynb
    -rwxrwxrwx 1 ankitp ankitp  2240 Aug 28 01:44 quiz.py


    bash: line 6: cd: /images: No such file or directory


### Look inside a Markdown File
> "cat" reads data from the file and gives its content as output


```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Navigate to project, then navigate to area wwhere files were cloned"

cd $project
echo "show the contents of README.md"
echo ""

cat README.md  # show contents of file, in this case markdown
echo ""
echo "end of README.md"

```

    Navigate to project, then navigate to area wwhere files were cloned
    show the contents of README.md
    
    ## Blog site using GitHub Pages and Jekyll
    > This site is intended for Students.   This is to record plans, complete hacks, and do work for your learnings.
    - This can be customized to support computer science as you work through pathway (JavaScript, Python/Flask, Java/Spring)
    - All tangible artifact work is in a _posts or in a _notebooks.  
    - Front matter (aka meta data) in ipynb and md files is used to organize information according to week and column in running web site.
    
    ## GitHub Pages
    All `GitHub Pages` websites are managed on GitHub infrastructure. GitHub uses `Jekyll` to tranform your content into static websites and blogs. Each time we change files in GitHub it initiates a GitHub Action that rebuilds and publishes the site with Jekyll.  
    - GitHub Pages is powered by: [Jekyll](https://jekyllrb.com/).
    - Publised teacher website: [nighthawkcoders.github.io/teacher](https://nighthawkcoders.github.io/teacher/)
    
    ## Preparing a Preview Site 
    In all development, it is recommended to test your code before deployment.  The GitHub Pages development process is optimized by testing your development on your local machine, prior to files on GitHub
    
    Development Cycle. For GitHub pages, the tooling described below will create a development cycle  `make-code-save-preview`.  In the development cycle, it is a requirement to preview work locally, prior to doing a VSCode `commit` to git.
    
    Deployment Cycle.  In the deplopyment cycle, `sync-github-action-review`, it is a requirement to complete the development cycle prior to doing a VSCode `sync`.  The sync triggers github repository update.  The action starts the jekyll build to publish the website.  Any step can have errors and will require you to do a review.
    
    ### WSL and/or Ubuntu installation requirements
    - The result of these step is Ubuntu tools to run preview server.  These procedures were created using [jekyllrb.com](https://jekyllrb.com/docs/installation/ubuntu/)
    - Run scripts in scripts directory of teacher repo: setup_ubuntu.sh and activate.sh.  Or, follow commands below.
    ```bash
    ## WSL/Ubuntu commands
    # sudo apt install, installs packages for Ubuntu
    echo "=== Ugrade Packages ==="
    sudo apt update
    sudo apt upgrade -y
    #
    echo "=== Install Ruby ==="
    sudo apt install -y ruby-full build-essential zlib1g-dev
    # 
    echo "=== Install Python ==="
    sudo apt-get install -y python3 python3-pip python-is-python3
    #    
    echo "=== Install Jupyter Notebook ==="
    sudo apt-get install -y jupyter-notebook
    
    # bash commands, install user requirements.
    echo "=== GitHub pages build tools  ==="
    export GEM_HOME="$HOME/gems"
    export PATH="$HOME/gems/bin:$PATH"
    echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
    echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
    echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
    echo "=== Gem install starting, thinking... ==="
    gem install jekyll bundler
    head -30 ./teacher/scripts/activate.sh
    echo "=== !!!Start a new Terminal!!! ==="
    ```
    
    ### MacOs installation requirements 
    - Ihe result of these step are MacOS tools to run preview server.  These procedures were created using [jekyllrb.com](https://jekyllrb.com/docs/installation/macos/). Run scripts in scripts directory of teacher repo: setup_macos.sh and activate_macos.sh.  Or, follow commands below.
    ```bash
    # MacOS commands
    # brew install, installs packages for MacOS
    echo "=== Ugrade Packages ==="
    brew update
    brew upgrade
    #
    echo "=== Install Ruby ==="
    brew install chruby ruby-install xz
    ruby-install ruby 3.1.3
    #
    echo "=== Install Python ==="
    brew install python
    #    
    echo "=== Install Jupyter Notebook ==="
    brew install jupyter
    
    # bash commands, install user requirements.
    export GEM_HOME="$HOME/gems"
    export PATH="$HOME/gems/bin:$PATH"
    echo '# Install Ruby Gems to ~/gems' >> ~/.zshrc
    echo 'export GEM_HOME="$HOME/gems"' >> ~/.zshrc
    echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.zshrc
    echo "=== Gem install starting, thinking... ==="
    gem install jekyll bundler
    head -30 ./teacher/scripts/activate.sh
    echo "=== !!!Start a new Terminal!!! ==="
    ```
    
    ### Preview
    - The result of these step is server running on: http://0.0.0.0:4100/teacher/.  Regeneration messages will run in terminal on any save.  Press the Enter or Return key in the terminal at any time to enter commands.
    
    - Complete installation
    ```bash
    bundle install
    ```
    - Run Server.  This requires running terminal commands `make`, `make stop`, `make clean`, or `make convert` to manage the running server.  Logging of details will appear in terminal.   A `Makefile` has been created in project to support commands and start processes.
    
        - Start preview server in terminal
        ```bash
        cd ~/vscode/teacher  # my project location, adapt as necessary
        make
        ```
    
        - Terminal output of shows server address. Cmd or Ctl click http location to open preview server in browser. Example Server address message... 
        ```
        Server address: http://0.0.0.0:4100/teacher/
        ```
    
        - Save on ipynb or md activiates "regeneration". Refresh browser to see updates. Example terminal message...
        ```
        Regenerating: 1 file(s) changed at 2023-07-31 06:54:32
            _notebooks/2024-01-04-cockpit-setup.ipynb
        ```
    
        - Terminal message are generated from background processes.  Click return or enter to obtain prompt and use terminal as needed for other tasks.  Alway return to root of project `cd ~/vscode/teacher` for all "make" actions. 
            
    
        - Stop preview server, but leave constructed files in project for your review.
        ```bash
        make stop
        ```
    
        - Stop server and "clean" constructed files, best choice when renaming files to eliminate potential duplicates in constructed files.
        ```bash
        make clean
        ```
    
        - Test notebook conversions, best choice to see if IPYNB conversion is acting up.
        ```bash
        make convert
        ```
    
    end of README.md


### Env, Git and GitHub
> Env(ironment) is used to capture things like path to Code or Home directory.  Git and GitHub is NOT Only used to exchange code between individuals, it is often used to exchange code through servers, in our case deployment for Website.   All tools we use have a behind the scenes hav relationship with the system they run on (MacOS, Windows, Linus) or a relationship with servers which they are connected to (ie GitHub).  There is an "env" command in bash.  There are environment files and setting files (.git/config) for Git.  They both use a key/value concept.

- "env" show setting for your shell
- "git clone" sets up a director of files
- "cd $project" allows user to move inside that directory of files
- ".git" is a hidden directory that is used by git to establish relationship between machine and the git server on GitHub.  


```python
%%script bash

# This command has no dependencies

echo "Show the shell environment variables, key on left of equal value on right"
echo ""

env
```

    Show the shell environment variables, key on left of equal value on right
    
    SHELL=/bin/bash
    PYTHONUNBUFFERED=1
    WSL2_GUI_APPS_ENABLED=1
    APPLICATION_INSIGHTS_NO_DIAGNOSTIC_CHANNEL=1
    WSL_DISTRO_NAME=Ubuntu
    ELECTRON_RUN_AS_NODE=1
    VSCODE_AMD_ENTRYPOINT=vs/workbench/api/node/extensionHostProcess
    NAME=Code
    PWD=/home/ankitp/vscode/ankit2/_notebooks
    LOGNAME=ankitp
    PYDEVD_IPYTHON_COMPATIBLE_DEBUGGING=1
    HOME=/home/ankitp
    LANG=C.UTF-8
    WSL_INTEROP=/run/WSL/311968_interop
    LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.zst=01;31:*.tzst=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.wim=01;31:*.swm=01;31:*.dwm=01;31:*.esd=01;31:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.webp=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:
    WAYLAND_DISPLAY=wayland-0
    CLICOLOR=1
    VSCODE_L10N_BUNDLE_LOCATION=
    LESSCLOSE=/usr/bin/lesspipe %s %s
    VSCODE_HANDLES_SIGPIPE=true
    TERM=xterm-color
    LESSOPEN=| /usr/bin/lesspipe %s
    USER=ankitp
    GIT_PAGER=cat
    PYTHONIOENCODING=utf-8
    DISPLAY=:0
    SHLVL=2
    PAGER=cat
    VSCODE_CWD=/mnt/c/Users/ankit/AppData/Local/Programs/Microsoft VS Code
    MPLBACKEND=module://matplotlib_inline.backend_inline
    XDG_RUNTIME_DIR=/run/user/1000/
    WSLENV=ELECTRON_RUN_AS_NODE/w:
    
    VSCODE_WSL_EXT_LOCATION=/mnt/c/Users/ankit/.vscode/extensions/ms-vscode-remote.remote-wsl-0.81.0
    XDG_DATA_DIRS=/usr/local/share:/usr/share:/var/lib/snapd/desktop
    PATH=/bin:/home/ankitp/.local/bin:/home/ankitp/.vscode-server/bin/6c3e3dba23e8fadc360aed75ce363ba185c49794/bin/remote-cli:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/lib/wsl/lib:/mnt/c/Windows/system32:/mnt/c/Windows:/mnt/c/Windows/System32/Wbem:/mnt/c/Windows/System32/WindowsPowerShell/v1.0/:/mnt/c/Windows/System32/OpenSSH/:/mnt/c/Program Files/dotnet/:/mnt/c/Program Files (x86)/NVIDIA Corporation/PhysX/Common:/mnt/c/Program Files/Git/cmd:/mnt/c/Users/ankit/AppData/Local/Microsoft/WindowsApps:/mnt/c/Users/ankit/AppData/Local/Programs/Microsoft VS Code/bin:/snap/bin:/home/ankitp/.vscode-server/bin/6c3e3dba23e8fadc360aed75ce363ba185c49794/bin/remote-cli:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/lib/wsl/lib:/mnt/c/Windows/system32:/mnt/c/Windows:/mnt/c/Windows/System32/Wbem:/mnt/c/Windows/System32/WindowsPowerShell/v1.0/:/mnt/c/Windows/System32/OpenSSH/:/mnt/c/Program Files/dotnet/:/mnt/c/Program Files (x86)/NVIDIA Corporation/PhysX/Common:/mnt/c/Program Files/Git/cmd:/mnt/c/Users/ankit/AppData/Local/Microsoft/WindowsApps:/mnt/c/Users/ankit/AppData/Local/Programs/Microsoft VS Code/bin:/snap/bin
    DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/1000/bus
    VSCODE_NLS_CONFIG={"locale":"en","osLocale":"en","availableLanguages":{}}
    HOSTTYPE=x86_64
    PULSE_SERVER=unix:/mnt/wslg/PulseServer
    VSCODE_HANDLES_UNCAUGHT_ERRORS=true
    VSCODE_IPC_HOOK_CLI=/run/user/1000/vscode-ipc-47c8a699-049a-4bbd-90ac-a52f25e66c32.sock
    _=/bin/env



```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

cd $project

echo ""
echo "show the secrets of .git"
cd .git
ls -l

echo ""
echo "look at config file"
cat config
```

    
    show the secrets of .git
    total 60
    -rw-r--r--  1 ankitp ankitp   13 Aug 28 01:57 COMMIT_EDITMSG
    -rw-r--r--  1 ankitp ankitp   95 Aug 28 01:57 FETCH_HEAD
    -rw-r--r--  1 ankitp ankitp   21 Aug 28 01:36 HEAD
    -rw-r--r--  1 ankitp ankitp   41 Aug 28 01:57 ORIG_HEAD
    drwxr-xr-x  2 ankitp ankitp 4096 Aug 28 01:36 branches
    -rw-r--r--  1 ankitp ankitp  260 Aug 28 01:36 config
    -rw-r--r--  1 ankitp ankitp   73 Aug 28 01:36 description
    drwxr-xr-x  2 ankitp ankitp 4096 Aug 28 01:36 hooks
    -rw-r--r--  1 ankitp ankitp 4450 Aug 28 01:57 index
    drwxr-xr-x  2 ankitp ankitp 4096 Aug 28 01:36 info
    drwxr-xr-x  3 ankitp ankitp 4096 Aug 28 01:36 logs
    drwxr-xr-x 13 ankitp ankitp 4096 Aug 28 01:57 objects
    -rw-r--r--  1 ankitp ankitp  112 Aug 28 01:36 packed-refs
    drwxr-xr-x  5 ankitp ankitp 4096 Aug 28 01:36 refs
    
    look at config file
    [core]
    	repositoryformatversion = 0
    	filemode = true
    	bare = false
    	logallrefupdates = true
    [remote "origin"]
    	url = https://github.com/Ankit-177/ankit2.git
    	fetch = +refs/heads/*:refs/remotes/origin/*
    [branch "main"]
    	remote = origin
    	merge = refs/heads/main


### Student Request - Make a file in Bash
> This example was requested by a student (Jun Lim, CSA). The request was to make jupyer file using bash, I adapted the request to markdown.  This type of thought will have great extrapolation to coding and possibilities of using List, Arrays, or APIs to build user interfaces.  JavaScript is a language where building HTML is very common.

> To get more interesting output from terminal, this will require using something like mdless (https://github.com/ttscoff/mdless).  This enables see markdown in rendered format.
- On Desktop [Install PKG from MacPorts](https://www.macports.org/install.php)
- In Terminal on MacOS
    - [Install ncurses](https://ports.macports.org/port/ncurses/)
    - ```gem install mdless```
    
> Output of the example is much nicer in "jupyter"


```python
%%script bash

# This example has error in VSCode, it run best on Jupyter
cd /tmp

file="sample.md"
if [ -f "$file" ]; then
    rm $file
fi

tee -a $file >/dev/null <<EOF
# Show Generated Markdown
This introductory paragraph and this line and the title above are generated using tee with the standard input (<<) redirection operator.
- This bulleted element is still part of the tee body.
EOF

echo "- This bulleted element and lines below are generated using echo with standard output (>>) redirection operator." >> $file
echo "- The list definition, as is, is using space to seperate lines.  Thus the use of commas and hyphens in output." >> $file
actions=("ls,list-directory" "cd,change-directory" "pwd,present-working-directory" "if-then-fi,test-condition" "env,bash-environment-variables" "cat,view-file-contents" "tee,write-to-output" "echo,display-content-of-string" "echo_text_>\$file,write-content-to-file" "echo_text_>>\$file,append-content-to-file")
for action in ${actions[@]}; do  # for loop is very similar to other language, though [@], semi-colon, do are new
  action=${action//-/ }  # convert dash to space
  action=${action//,/: } # convert comma to colon
  action=${action//_text_/ \"sample text\" } # convert _text_ to sample text, note escape character \ to avoid "" having meaning
  echo "    - ${action//-/ }" >> $file  # echo is redirected to file with >>
done

echo ""
echo "File listing and status"
ls -l $file # list file
wc $file   # show words
mdless $file  # this requires installation, but renders markown from terminal

rm $file  # clean up termporary file
```

    
    File listing and status
    -rw-r--r-- 1 ankitp ankitp 809 Aug 28 01:59 sample.md
     15 132 809 sample.md
    
    [0m[0;1;47;90mShow Generated Markdown [0;2;30;47m========================================================[0m
    
    This introductory paragraph and this line and the title above are generated
    using tee with the standard input (<<) redirection operator.
    [0;1;91m- [0;1;91m[0;97mThis [0;97mbulleted [0;97melement [0;97mis [0;97mstill [0;97mpart [0;97mof [0;97mthe [0;97mtee [0;97mbody.
    [0;1;91m- [0;1;91m[0;97mThis [0;97mbulleted [0;97melement [0;97mand [0;97mlines [0;97mbelow [0;97mare [0;97mgenerated [0;97musing [0;97mecho [0;97mwith [0;97mstandard
    [0;97moutput [0;97m(>>) [0;97mredirection [0;97moperator.
    [0;1;91m- [0;1;91m[0;97mThe [0;97mlist [0;97mdefinition, [0;97mas [0;97mis, [0;97mis [0;97musing [0;97mspace [0;97mto [0;97mseperate [0;97mlines. [0;97mThus [0;97mthe [0;97muse [0;97mof
    [0;97mcommas [0;97mand [0;97mhyphens [0;97min [0;97moutput.
          [0;1;91m- [0;1;91m[0;97mls: [0;97mlist [0;97mdirectory
          [0;1;91m- [0;1;91m[0;97mcd: [0;97mchange [0;97mdirectory
          [0;1;91m- [0;1;91m[0;97mpwd: [0;97mpresent [0;97mworking [0;97mdirectory
          [0;1;91m- [0;1;91m[0;97mif [0;97mthen [0;97mfi: [0;97mtest [0;97mcondition
          [0;1;91m- [0;1;91m[0;97menv: [0;97mbash [0;97menvironment [0;97mvariables
          [0;1;91m- [0;1;91m[0;97mcat: [0;97mview [0;97mfile [0;97mcontents
          [0;1;91m- [0;1;91m[0;97mtee: [0;97mwrite [0;97mto [0;97moutput
          [0;1;91m- [0;1;91m[0;97mecho: [0;97mdisplay [0;97mcontent [0;97mof [0;97mstring
          [0;1;91m- [0;1;91m[0;97mecho [0;97m"sample [0;97mtext" [0;97m>$file: [0;97mwrite [0;97mcontent [0;97mto [0;97mfile
          [0;1;91m- [0;1;91m[0;97mecho [0;97m"sample [0;97mtext" [0;97m>>$file: [0;97mappend [0;97mcontent [0;97mto [0;97mfile
    
    [0m

## Hack Preparation.
> Review Tool Setup Procedures and think about some thing you could verify through a Shell notebook.
- Come up with your own student view of this procedure to show your tools are installed.
- Name and create notes on some Linux commands you will use frequently.
- Is there anything we use to verify tools we install? Review versions checks.
- Is there anything we could verify with Anaconda?  or WSL?  
- How would you update a repository?  Could you do that in script above?

