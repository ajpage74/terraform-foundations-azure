# Terraform Foundations on Azure

## 👋 Introduction
Welcome to Terraform Foundations on Azure. Follow the instructions on this page to complete all your lab assignments. You may use the navigation menu on the left to jump to a particular lab exercise.

## 👩🏾‍🔬 Your Lab Environment
Your lab environment is running on the <a href="https://instruqt.com" target="_blank">Instruqt</a> platform. Instruqt provides sandbox cloud environments where you can experiment and learn how to use HashiCorp tools like Terraform. You have four tabs in your learning environment:

* **Instructions** - All your lab instructions are contained on this page, which opens in a new tab or window. If you have enough room on your desktop we recommend dragging the instructions tab into a separate window for easy reference.
* **Text Editor** - This tab contains a simple programmer's text editor. Use the file navigation menu on the left side of the editor to browse to files that you wish to edit.
* **Shell** - This is the bash shell for your Ubuntu 18.04 workstation. We've pre-installed a bunch of popular devops tools such as terraform, git, docker, and the `az` Azure CLI tool.
* **Azure Portal** - This tab contains a link and credentials for your Azure sandbox subscription.

Note: You can increase or decrease the text size in your lab environment with the `CTRL +` or `CTRL -` keyboard shortcuts Windows/Linux). Use the `CMD` key instead if you are on MacOS.

Warning: Use an incognito window when you log onto the Azure portal. You can do this by right-clicking the link on the Azure Portal page and selecting "Open in Incognito Mode" or "Open in Private Mode". Using an incognito/private window for all your lab exercises will ensure that you don't accidentally log on with your company or personal account.

![incognito_mode](images/incognito_mode.png)

## ⚙️ Lab 0: A Taste of Git
<a href="https://en.wikipedia.org/wiki/Git" target="_blank">Git</a> is the worlds most popular version control system (VCS). We'll be using Git to download all the lab exercises and example code for this workshop. Before we begin working with Terraform let's review some basic Git commands.

### **Exercise 1:** Fork and clone the terraform-azure git repository.

You'll need a GitHub.com account to do the lab exercises. Visit github.com in a new browser tab and sign in. Visit the following URL and click the **Fork** button in the upper right corner. You can right-click the link to open it in a new window or tab:

https://github.com/hashicorp/terraform-azure-labs

Run the following command to download (clone) a copy of the training repo to your workstation.

```bash
git clone https://github.com/YOURGITUSERNAME/terraform-azure-labs
```

Now change into the directory you just downloaded and run the `ls -l` command:

```bash
cd terraform-azure-labs
ls -l
```

Note that your prompt changes when you change into a Git repository. The git-enabled prompt adds additional information about your git repository including the branch name and any changes that haven't been committed yet.

Note: If you know your way around the Git command line you may skip the rest of this section and proceed on to the next lab, Terraform Basics.

### **Exercise 2:** Git Basics
#### Set Up Your Username and Email
Before we start working with the Git command line we need to run two housekeeping commands. These commands identify you so that your code commits can be tagged. Run these two commands in your Shell tab, replacing the name and email with your own:

```bash
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

#### Git Status
The first git command you should learn is `git status`. You can always get a summary of the status of your repo with this command. Try it now in your Shell tab:

```bash
git status
```

Note that the current status message says there is nothing to commit. This is known as a clean working tree. It means you don't have any files that have changed from the last checkpoint. The little green checkmark on your prompt also indicates a clean working tree.

Now let's add a file and see how the status changes. Run the following commands:

```bash
touch myfile.txt
git status
```

Now you'll see your prompt change and the status message change to show the untracked file that you just created. Since Git has never seen this file before it is marked as untracked.

Next let's try editing a file. Go into your text editor and open the README.md file inside the terraform-azure-labs directory. Add your name or a short message on the last line of the file. Save the file by clicking the little disk icon on the file tab. CTRL-S or CMD-S keyboard shortcuts may not work here.

![Edit Files in Instruqt](images/edit_readme.png)

Go back to your Shell tab and check the status again:

```bash
git status
```

Now you have one untracked file, and a modified file. Git keeps track of all changes, additions and deletions to the entire repository.

#### Git Add
Let's add that untracked file so Git can keep track of it. Run the following command:

```bash
git add .
```

The `.` is a shortcut that means "Add all my changes from this directory on downward." You'll be using this shortcut a lot. You can also add individual files by specifying the filename directly.

Run the status command again to see what's different:

```bash
git status
```

Now you'll see your two changes sitting in a 'ready to commit' state. This is known as **staging**. Staged items are changes that you want to make but haven't committed yet. It's a bit like a shopping cart at the grocery store. You can add and remove items to your cart before you make the final decision what to purchase.

#### Git Commit
The next step is to **commit** your pending changes. Use the following command to create a new commit along with a short message explaining what you did:

```bash
git commit -m "Added a file, edited README.md"
```

You'll see some output that looks like this:

```
[main 45d303a] Added a file, edited README.md
 2 files changed, 1 insertion(+)
 create mode 100644 myfile.txt
```

Note the short commit hash next to the branch name, `45d303a`. Every single commit you make to the git repo has an identifier like this. You can use these hashes to refer to specific commits if you need to go back in time.

Run the status command again and see how it has returned back to a clean working tree.

```bash
git status
```

Your bash prompt now has a green checkmark again but there's a new symbol `↑·1` that indicates you have changes that have not been pushed to the main repo.

### **Exercise 3:** Remote Repositories - Credentials Config
GitHub passwords are no longer supported for command line access so you'll need to create a Personal Access Token. Visit this link in a web browser and click on the **Generate New Token** button:

https://github.com/settings/tokens

In the Note section you can enter "Terraform Azure Lab". Under the Select Scopes section check the box next to **repo**.

![Git Token Creation](images/git_token.png)

Click on **Generate Token** at the bottom of the page. GitHub will generate you a new personal access token. Save this token in a text file as you'll need it in a moment.

![Personal Access Token](images/personal_access_token.png)

Configure the Git Credential Helper so you won't have to copy your token in every time you make a change. Run this command to set up the credential helper to store your creds for 4 hours.

```bash
git config credential.helper 'cache --timeout 14400'
```

### **Exercise 4:** Remote Repositories - Push and Pull
#### Git Remote
When you collaborate with others on the same codebase you'll want a shared main repository that everyone can contribute to. This is known as a remote repository. Check your remote URL with the following command:

```bash
git remote -v
```

You'll see a remote named `origin` which is the default name for remote repos, with entries for both **fetch** and **push**. This is the same repo you forked earlier.
#### Git Push
Let's push our local changes to the remote repo. Run the following command.

```bash
git push origin main
```

This command means "Push all my local commits to the main branch on the origin repo."

Note: You can also abbreviate this command by simply typing `git push` which uses the default remote repo and branch names, **origin** and **main**.

You'll be prompted to log onto GitHub to authorize the push. Use your GitHub username along with the personal access token you created in the previous step. Your credentials are now safely cached on the workstation for future commands.

#### Git Pull
Now let's make a change on the remote repo and pull it into our local copy. Visit your repo fork in a browser and click on the README.md file. 

Next click on the little pencil shaped icon ✏️ on the upper right side of the preview pane. This will allow you to edit the README.md file in place.  Add some more text to the file using the built in text editor. Enter an optional commit message and click on the **Commit changes** button on the bottom of the page.

![Git Commit GUI](images/git_commit_gui.png)

Go back to your Shell tab and run a git status command:

```bash
git status
```

Your local repo doesn't know anything about the changes on the remote. Let's run another command to fetch the change we just made:

```bash
git fetch
```

Look at how your prompt changed: `↓·1`. This means there is one new commit on the remote repo that we can merge into our local copy. Run this command to merge the change:

```bash
git merge FETCH_HEAD
```

You can combine the fetch and merge steps into a single command, `git pull`. Try it now:

```bash
git pull
```

Note: Advanced git users run `git fetch` and `git pull` often to ensure that they have the latest changes to the codebase.

### **Exercise 5:** Git Log
You can output the log for your Git repository with the `git log` command. Try it now. 

```bash
git log
```

You can exit the log viewer by typing capital `ZZ` or `:q`.

This log will show all the commits to your repository since you forked it from the main repo. You can control the log output with various flags. Here's an example that creates a more compact, colorized log with a graph:

```bash
git log --oneline --color --graph
```

### **Exercise 5:** Git Command Reference
Here's a quick overview of the most commonly used Git commands:

* `git status` - Shows the current status of your local repo.
* `git clone` - Make a local copy of a remote repo.
* `git log` - Outputs the log to your terminal. Escape with `ZZ`.
* `git add .` - Add all files in the current directory and below to staging.
* `git rm filename` - Removes a file from the staging area.
* `git commit` - Commits all local changes. Use the `-m` flag to append a message.
* `git push` - Push local changes to remote repo.
* `git fetch` - Pull changes from a remote repo.
* `git merge` - Merge changes to current branch.
* `git pull` - Fetch and merge at the same time.
* `git branch` - Show which branch you are currently on.
* `git config` - Alter the Git configuration file.
* `git remote` - Work with remote repositories.
* `git checkout` - Use to switch branches or revert changes to a file.

## ⚙️ Lab 1: Terraform Basics
### What is Terraform?
Terraform is an Infrastructure-as-Code (IaC) software tool created by HashiCorp and released in 2014. Terraform allows users to define and provision infrastructure using a declarative configuration language known as HashiCorp Configuration Language (HCL). Terraform manages infrastructure such as public and private cloud instances or VMs, network appliances, Software-as-a-Service (SaaS) and Platform-as-a-Service (PaaS) resources.

### Modular and Extendible
Terraform uses a catalog of providers to communicate with different cloud platforms and APIs. The rich provider ecosystem supports a wide variety of different types of cloud and on-premise resources.

### Declarative Infrastructure
The Terraform language, or HCL, is a Domain Specific Language (DSL) that uses a declarative syntax. Declarative configuration allows you to define the desired final state of your resources without having to define the logic necessary to get there. Terraform determines the order that resources need to be provisioned in based on dependencies. For instance, a network needs to be built before a server can be assigned to it. 




Terraform is a command line tool that is written in Golang. Here is an example of some Terraform code that builds an Azure Resource Group:

<!-- We had to use the php syntax highlighter because hcl isn't available. -->
```php
resource "azurerm_resource_group" "example" {
  name     = "example"
  location = "Central US"
}
```

## ⚙️ Lab 2: The Azure Provider

## ⚙️ Lab 3: Build a Resource Group

## ⚙️ Lab 4: Add a Virtual Network

## ⚙️ Lab 5: Create a Subnet

## ❓ Appendix A: The Answers