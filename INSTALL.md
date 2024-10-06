<details>

<summary>TODO</summary>

## Ideas for this tuto
- [ ] Complet [Install-Visual-Studio-Code](#install-visual-studio-code)
- [ ] Add advantage/disadvantage jupiter/vs code
- [ ] Add the setup : WSL, ect. so it can be used for this project
</details>

# Jupyter Notebook Setup

This guide will walk you through setting up a Jupyter Notebook on a machine using Mambaforge and WSL.

## Prerequisites for Windows Users

### 1. Install WSL (Windows Subsystem for Linux)

- **Install Windows Terminal:**
  - Download from the [Windows Store](https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701?hl=fr-ch&gl=ch&rtc=1) (already installed on Windows 11).
  
- **Set up WSL:**
  - Run Windows Terminal as *administrator* and execute:  
    ```bash
    wsl --install
    ```
  - Restart your computer, set up your Ubuntu user (username and password).

- **Update Linux Distribution:**
  ```bash
  sudo apt-get update
  sudo apt-get install wget ca-certificates
  ```

### 2. Configure Ubuntu Terminal

- **Set Ubuntu as Default Shell (optional):**
  - In Terminal settings, under *Startup*, set Ubuntu as the default profile to always start with the correct terminal.

## Installing Python with Mambaforge

### 1. Verify Existing Python Installation

- Check if Python is already installed:
  ```bash
  which python
  ```
  - If Python is present, you might want to uninstall it before proceeding.

### 2. Download and Install Mambaforge

- **Download Mambaforge:**
  - Go to the [Mambaforge GitHub page](https://github.com/conda-forge/miniforge?tab=readme-ov-file#miniforge3), find the appropriate installer for your CPU, and copy the download link in the table.
> [!IMPORTANT] Do not select an installer under *Miniforge-pypy3* but *Miniforge3*.
- Check the directory
  ```bash
  pwd
  ```
  Should return `/home/<username>`
  - Create a `downloads` folder
  ```bash
  mkdir downloads
  ```

- **Install Mambaforge:**
  ```bash
  wget <Miniforge3_download_link>
  bash <name_sh_file>.sh
  ```
  - Agree to the terms, press `Enter` for default options, and type `yes` when prompted to initialize conda.
--------------------------------------------------------------------------------------------------------------------
### 3. Verify Installation

- Ensure Mambaforge is correctly installed:
  ```bash
  which python
  ```
  - It should point to the Mambaforge directory : `home/<username>/miniforge3/bin/python`

## Install important basic packages

### 1. Install JupyterLab and Essential Libraries

- **Install necessary packages:**
  ```bash
  mamba install ipython jupyterlab ipywidgets
  ```
  - Accept prompts with `Y`.

### 2. Update Mambaforge

- **Keep Mambaforge up to date:**
  ```bash
  mamba update mamba
  ```

### 3. Register Python Environment in Jupyter

- **Set up the environment in Jupyter:**
  ```bash
  python3 -m ipykernel install --user --name=python3
  ```

### 4. Start JupyterLab

- **Launch JupyterLab:**
  ```bash
  jupyter lab --no-browser
  ```
  - Use the provided link to access JupyterLab from your browser.
## Install Visual Studio Code
VS Code is a source-code editor, it include usefull features like debugging suport, code completion, code refactoring, syntax highlighting and embedded git control.

Use this installation [help](https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-vscode) to guide you through the installation and configuration with WSL, stop before the section **_Install Git (optional)_**.

> Go to [Developing in WSL](https://code.visualstudio.com/docs/remote/wsl) for more information about the installation and operation.

## Jupyter lab or VS code
For working on a Notebook, the two methods works and have advantages, few difference between the two methods :

| VS code               |                              | Jupyter                                             |                                                                    |
|-----------------------|------------------------------|-----------------------------------------------------|--------------------------------------------------------------------|
| +                     | -                            | +                                                   | -                                                                  |
| Can be set as we want | Must be configured correctly | Avoid setting conflict (folder where data are, etc) | Underdeveloped modules (black formatter, git, github copilot, etc.) |
| Autocomplete          |                              | IDE easy to install                                 | No autocomplete                                                    |
| Powerful modules  |                              |                                                     |                                                                    |

## Git Setup

Be sure git is installed correctly on your computer by following [this quick tutorial](https://linuxhint.com/add-git-bash-windows-terminal/).

### 1. Configure Git

- **Set up your Git identity:**
  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "your.name@example.ch"
  ```
-Confirm that the Git username is set correctly:
  ```bash
  $ git config --global user.name
  > Your Name
  $ git config --global user.email
  > your.name@example.ch
  ```
### 2. Set Up SSH for GitHub

- **Generate SSH Key:**
  ```bash
  ssh-keygen -t ed25519 -C "your_email@example.ch"
  eval "$(ssh-agent -s)"
  ssh-add ~/.ssh/id_ed25519
  ```

- **Add public SSH Key to GitHub:**
  - Copy the public key:
    ```bash
    cat ~/.ssh/id_ed25519.pub
    ```
  - Paste it into your GitHub account under *Settings > SSH and GPG keys*.

### 3. Clone Repository

- **Clone the project repository:**
  ```bash
  mkdir git 
  cd git
  git clone git@github.com:heig-vd-iese/rht.git
  ```

### 4. Install Dependencies

- **Install packages from `environment.yml` into the `(base)` environnement:**
  ```bash
  cd rht
  mamba env update -n base --file environment.yml
  ```
---

### Commiting your work with Git
<details>
<summary> Commiting your work with Git </summary>

To add all the changes you've made:

```bash
git add .
```

To commit them:

```bash
git commit -m "MY MESSAGE HERE"
```

> [!NOTE]
> `-m` is the message flag here. The message is really important in order for tracking your work via git.

You can also put those steps together like this:

```bash
git commit -a -m "MY MESSAGE HERE"
```

To push your committed changes from your local repository to your remote repository:

```bash
git push origin master
```

It is possible to get some type in your username/password for github. Unless you have configured [SSH keys correctly](#section-ssh-key)..

More information about these steps:

- [How to commit and push?](https://stackoverflow.com/questions/19576116/how-to-add-multiple-files-to-git-at-the-same-time)

> [!IMPORTANT]
> You are done with the setup.
> If you did not get any trouble, you can continue with the tutorials for this course [github.com's notebook viewer](./index.ipynb).

If you get many problems with your git branch or repo, please get in touch with [Luca](mailto:luca.tomasini@heig-vd) or [Antoine](mailto:antoine.giraldi@heig-vd.ch).
</details>

---

## Troubleshooting in the setup guide

This section is designed to help you solve problems before contacting support directly. Try one of the following steps, depending on which part of the guide is giving you trouble.

---

<details>

<summary>Installation automation (to optimize later on)</summary>

### Install an isolated Python environment with `setup-conda.sh` (not necessary to follow)

We are going to run the following script from the terminal `setup-conda.sh`. Don't worry, we will guide you through the all process.

Go to your download folder by typing the following command in your terminal:

```bash
cd downloads
wget https://github.com/fastai/fastsetup/blob/master/setup-conda.sh
```

Then, you can type the following command into the terminal:

```bash
chmod u+x setup-conda.sh
```

In a nutshell, those commands help to change the permissions to add executable permission to the current user (yourself). Then type:

```bash
 ./setup-conda.sh
```

The installation is starting...

- Restart terminal for Ubuntu.
- You should see `(base)` at the beginning of prompt.

> [!NOTE]
> Everytime you open a new Ubuntu terminal, you should see `(base)` environment. That means your configuration setup works well for this course and labs.

At this point, we have to check if your configuration works fine:

- Run `which python`, you should see that the python you are running is in the mambaforge directory: `home/<username>/miniforge3/bin/python` on Linux/WSL and `/Users/<username>/miniforge3/bin/python`.
- This means everything was just setup correctly.

</details>

---

<details>

<summary>Only if you encounter difficulties with WSL</summary>

### Troubleshooting with WSL

There is no need to enable 'Windows Subsystem for Linux' in the `Turn Windows features on or off` settings unless you get in trouble with your installation setup. In such case, it is recommended to follow this [tutorial](https://learn.microsoft.com/en-us/windows/wsl/troubleshooting) or get back to assistance.

- [Enable WSL correctly for Windows 10](https://code.visualstudio.com/docs/remote/wsl-tutorial#_enable-wsl)

</details>

<details>

<summary>Only if you encounter difficulties with Mambaforge</summary>

### Troublehsooting with Mambaforge

- `rm -rf mambaforge`
- Remove conda initializing commands from `\\wsl.localhost\Ubuntu\home\<username>`: `.bashrc` file (with a text editor). Delete everything at the end of the script between these commands:

```bash
# >>> conda initialize >>>
__conda_setup=
...
# <<< conda initialize <<<
```

---

> [!NOTE]
> Uncollapse these section depending where you need more help to solve troubleshootings.

</details>

<details>

<summary>Only if you encounter difficulties with GitHub</summary>

### Troubleshooting with GitHub

We regularly update the notebooks to fix issues and add support for new librarires. So make sure you update this project regularly.

For this, open a terminal, and run the following:

```bash
cd $HOME # or whatever development directory you chose earlier
cd rht # go to this project's directory
git pull
```

If you get an error, it's probably because you modified a notebook. In this case, before running `git pull` you will first need to commit your changes. I recommend doing this in your own branch, or else you may get conflicts:

```bash
git checkout -b my_branch # you can use another branch name if you want
git add -u
git commit -m "Describe your changes here"
git checkout main
git pull
```

Next, let's update the libraries. First, let's update `mamba` itself:

```bash
mamba update -c defaults -n base mamba
mamba activate base
jupyter lab --no-browser
```

</details>

---

## Further references for the setup (not necessary to follow)



<details>

<summary>References (not necessary to follow – backup)</summary>

> [!NOTE]
> Notice that it is however using `conda install`, which we will replace with `mamba install`.

### For the complete setup from scratch

> [!WARNING]
> More information about it can be found [here](https://github.com/conda-forge/miniforge/pull/277) and [here](https://github.com/conda-forge/miniforge/releases/tag/23.3.1-0).
> *Mambaforge (Discouraged as of September 2023)*, that means "the packages and configuration of Mambaforge and Miniforge3 are now identical. The only difference between the two is the name of the installer and, subsequently, the default installation directory."

1. [Beginner's Guide to Mambaforge Installation](https://qbiwan.github.io/fastpages/mamba-installation)
2. [Mambaforge setup page](https://github.com/conda-forge/miniforge#mambaforge)
3. [Fastsetup script](https://raw.githubusercontent.com/fastai/fastsetup/master/setup-conda.sh)
4. [Jeremy Howard's Live Coding Sessions](https://forums.fast.ai/t/official-course-walk-thrus/96617)
5. [Mamba Installation](https://mamba.readthedocs.io/en/latest/mamba-installation.html)
6. [Mamba Installation with Docker](https://hub.docker.com/r/condaforge/mambaforge)
7. [Miniforge3 23.3.1-0](https://github.com/conda-forge/miniforge/releases/tag/23.3.1-0)

### For VS Code and WSL details

1. [Windows Subsystem for Linux Documentation](https://learn.microsoft.com/en-us/windows/wsl/)
2. [Open a WSL project in Visual Studio Code](https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-vscode#open-a-wsl-project-in-visual-studio-code)
3. [Open a remote folder or workspace](https://code.visualstudio.com/docs/remote/wsl#_open-a-remote-folder-or-workspace)
4. [Install Ubuntu on WSL2 and get started with graphical applications](https://ubuntu.com/tutorials/install-ubuntu-on-wsl2-on-windows-11-with-gui-support#1-overview)
    * [How to install Windows Subsystem for Linux (WSL) on Windows 11](https://pureinfotech.com/install-wsl-windows-11/)
5. [Install Ubuntu on WSL2 on Windows 10](https://ubuntu.com/tutorials/install-ubuntu-on-wsl2-on-windows-10#1-overview)
    * [How to install WSL2 (Windows Subsystem for Linux2) on Windows 10](https://pureinfotech.com/install-windows-subsystem-linux-2-windows-10/)
6. [How to get access to your Linux (WSL) Files in Windows 10 or 11](https://www.howtogeek.com/426749/how-to-access-your-linux-wsl-files-in-windows-10/)
7. [What're the differences between these 2 ways of launching WSL?](https://superuser.com/questions/1765100/whatre-the-differences-between-these-2-ways-of-of-launching-wsl)
8. [Get started with Docker remote containers on WSL 2](https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-containers)
9. [Advanced: Opening a WSL 2 folder in a container](https://code.visualstudio.com/docs/remote/wsl#_advanced-opening-a-wsl-2-folder-in-a-container)
10. [Get started tutorial for Python in VS Code](https://code.visualstudio.com/docs/python/python-tutorial#_configure-and-run-the-debugger)
11. [Add User to WSL Linux Distro in Windows 10](https://winaero.com/add-user-wsl-linux-distro-windows-10/)
12. [Switch user in WSL Linux Distro in Windows 10](https://winaero.com/switch-user-wsl-linux-distro-windows-10/)
13. [How to set default user, switch user, and remove a user for WSL](https://www.thewindowsclub.com/how-to-set-default-user-switch-user-and-remove-a-user-for-wsl)

### For Git and SSH

1. [Quickstart with GitHub](https://docs.github.com/en/get-started/quickstart/set-up-git)
2. [What is a Git SSH Key?](https://www.atlassian.com/git/tutorials/git-ssh)
3. [Checking for existing SSH keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys)
4. [Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
5. [Generating a new SSH key for a hardware security key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent?platform=linux#generating-a-new-ssh-key-for-a-hardware-security-key)
6. [Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
7. [Multiple SSH Keys settings for different github account](https://gist.github.com/jexchan/2351996)
8. [Working with SSH key passphrases](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases)
9. [About commit signature verification](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification)
10. [Do I need authentication as well as signing keys on GitHub?](https://stackoverflow.com/questions/73673920/do-i-need-authentication-as-well-as-signing-keys-on-github)

### JupyterLab Desktop and Python environment

1. [Connect to an existing JupyterLab server](https://github.com/jupyterlab/jupyterlab-desktop/blob/master/user-guide.md#connecting-to-an-existing-jupyterlab-server) (with the link you just copied from your terminal session)
2. [The python requirements file and how to create it](https://learnpython.com/blog/python-requirements-file/)
3. [Conda install requirements](https://linuxhint.com/conda-install-requirements-txt/)
4. [Introducing the new JupyterLab Desktop!](https://medium.com/jupyter-blog/introducing-the-new-jupyterlab-desktop-bca1982bdb23)

</details>
