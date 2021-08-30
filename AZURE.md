# Terraform Foundations on Azure

## 👋 Introduction
Welcome to Terraform Foundations on Azure. Follow the instructions on this page to complete all your lab assignments. You may use the navigation menu on the left to jump to a particular lab exercise.

## 👩🏾‍🔬 Your Lab Environment
Your lab environment is running on the <a href="https://instruqt.com" target="_blank">Instruqt</a> platform. Instruqt provides sandbox cloud environments where you can experiment and learn how to use HashiCorp tools like Terraform. You have four tabs in your learning environment:

* **Instructions** - All your lab instructions are contained on this page, which opens in a new tab or window. You should return to this link whenver you need to review the instructions or move on to a new lab exercise. If you have enough room on your monitor we recommend opening the instructions in a separate window for easy reference.
* **Text Editor** - This tab contains a simple programmer's text editor. Use the file navigation menu on the left side of the editor to browse to files that you wish to edit.
* **Shell** - This is the bash shell for your Ubuntu 18.04 workstation. We've pre-installed a bunch of popular devops tools such as terraform, git, docker, and the `az` Azure CLI tool.
* **Azure Portal** - This tab contains a link and credentials for your Azure sandbox subscription.

Warning: Use an incognito window when you log onto the Azure portal. You can do this by right-clicking the link on the Azure Portal page and selecting "Open in Incognito Mode" or "Open in Private Mode". Using an incognito/private window for all your lab exercises will ensure that you don't accidentally log on with your company or personal account.

![incognito_mode](images/incognito_mode.png)

## ⚙️ Lab 0: A Taste of Git
<a href="https://en.wikipedia.org/wiki/Git" target="_blank">Git</a> is the worlds most popular version control system (VCS). We'll be using Git to download all the lab exercises and example code for this workshop. Before we begin working with Terraform let's review some basic Git commands.

**Exercise 1:** Clone the terraform-azure git repository.

Run the following command to download a copy of the training repo to your workstation.

```bash
git clone https://github.com/scarolan/terraform-azure-labs
```

Now change into the directory you just downloaded and run the `ls -l` command:

```bash
ls -l
```

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