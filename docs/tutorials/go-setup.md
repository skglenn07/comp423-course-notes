# Setting Up a Dev Container for Go

* Primary author: [Sarah Glenn](https://github.com/skglenn07)
* Reviewer: [Riley Chapman](https://github.com/rileyac)

## Introduction

In this tutorial, you will learn how to set up a basic project in Go. This guide will teach you how to set up a new dev container, create a new project, initialize git properly, and write, compile, and run a "Hello COMP423" program!

## Prerequisites

To get started, you will need the following:

* **A Github Account**: If you don't have one, sign up at [Github](https://github.com/)
* **Git Installed**: [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) if you haven't already 
* **Visual Studio Code**: Download it [here](https://code.visualstudio.com/)
* **Docker Installed**: Needed to run the dev container - get Docker [here](https://www.docker.com/products/docker-desktop/)
* **Command-line basics**: You'll need a basic knowledge of the command line!

## Part 1: Creating a Git Repository
(Adapted from [COMP 423 MkDocs Tutorial](https://comp423-25s.github.io/resources/MkDocs/tutorial/))

### Step 1: Create a Local Directory and Initialize Git
(1) Open your terminal or command prompt.

(2) Create a new directory for your project. (Note: Of course, if you'd like to organize this tutorial somewhere else on your machine, go ahead and change into that parent directory first. By default this will be in your user's home directory.):
```
mkdir go-tutorial
cd go-tutorial
```

(3) Initialize a new Git repository:
```
git init
```

!!! note
    This command creates a new Git Repository (repo). This Git repo will allow you to track versions and changed of your project.

(4) Create a README file:

```
echo "# Go tutorial set up" > README.md
git add README.md
git commit -m "Initial commit with README"
```

### Step 2: Create a Remote Repository on GitHub

(1) Log in to your GitHub account and navigate to the Create a New Repository page.

(2) Fill in the details as follows:

* **Repository Name:** go-tutorial
* **Description:** "Setting up a basic dev container for Go and writing a simple 'Hello COMP423' Program".
* **Visibility:** Public

(3) Do not initialize the repository with a README, .gitignore, or license.

(4) Click Create Repository.

### Step 3: Link your Local Repository to GitHub

(1) Add the GitHub repository as a remote:

```
git remote add origin https://github.com/<your-username>/go-tutorial.git
```
Replace <your-username> with your GitHub username.

(2) Check your default branch name with the subcommand ```git branch```. If it's not main, rename it to main with the following command: ```git branch -M main```.

(3) Push your local commits to the GitHub repository:

```
git push --set-upstream origin main
```

(4) Back in your web browser, refresh your GitHub repository to see that the same commit you made locally has now been pushed to remote. You can use ```git log``` locally to see the commit ID and message which should match the ID of the most recent commit on GitHub. This is the result of pushing your changes to your remote repository.

## Part 2. Setting Up the Development Environment
(Adapted from [COMP 423 MkDocs Tutorial](https://comp423-25s.github.io/resources/MkDocs/tutorial/))

### What is a Development (Dev) Container?

A dev container ensures that your development environment is consistent and works across different machines. In this tutorial, you will set up a dev container for Go!

### Step 1: Add Dev Container Configuration

(1) Open your project in VS Code (File > Open Folder)

(2) Install the Dev Containers extension

(3) Create a **.devcontainer** directory inside the project root with the following file inside: 

```
.devcontainer/devcontainer.json
```

(4) Add the following to **.devcontainer/devcontainer.json**:

```
{
     "name": "Go Development Container",
     "image": "mcr.microsoft.com/vscode/devcontainers/go:latest",
     "customizations": {
        "vscode": {
            "extensions": [
                "golang.go"
                ]
            }
        }
}

```

* **name:** A descriptive name for your dev container
* **image:** The Docker image to use is the latest version of a Go environment
* **customizations:** Adds configurations to VS code - in this case, the Go extension

### Step 2: Open the Project in the Dev Container

(1) Reopen the project in the container: In VS Code, press **Ctrl+Shift+P** or **Cmd+Shift+P** on Mac and select **Dev Containers: Reopen in Container**. This creates the container, and opens the project inside of the Go environment. 

(2) Once the dev container set up is complete, close the current terminal and open a new one in VS Code. Run this line in the terminal to verify the Go version running in your dev container:

```
go version
```

## Part 3: Creating a Go Program
(Adapted from [Getting Started With Go](https://go.dev/doc/tutorial/getting-started))

### Step 1: Create a "Hello, COMP423!" Program

Once your dev container is open, you can create a simple Go program in the environment!

(1) Initialize a Go module for this project:

```
go mod init example/go-tutorial
```

This creates a go.mod file to manage and track dependencies in your project. For an actual project, the module path will likely be the repository location where your source code is kept. For this tutorial, we used ```example/go-tutorial``` as an example.

(2) Right click inside of the "File Explorer" on the left-hand side of VS Code and select "New File" - Name this ```"hello.go"```

(3) Add the following code to the ```hello.go``` file

```
package main
import "fmt"
func main() {
    fmt.Println("Hello, COMP423")
}
```
Here's what you're doing with this Go code:

* Declaring a main pacakge
* Importing the fmt pacakge which contains the function that allows you to print to the console
* Implementing a main function where you print your message. This executes by default when the main package is run. 

### Step 2: Run Your Program!
Learn more about go commands [here](https://pkg.go.dev/cmd/go#hdr-Compile_and_run_Go_program)

(1) Use the ```go run``` command to run the program:

```
go run hello.go
```

This will compile and run the main Go package from the program you've named ```hello.go``` quickly without creating a seperate binary, so it is helpful for testing programs! You should see this output: 

```
Hello, COMP423
```

(2) Build and Run using the ```go build``` command: 
!!! note
    ```go build``` is used in Go similarly to the ```gcc``` command in C. Both compile code into binary executables that can be used to run programs. 

```
go build hello.go
```

This will compile the hello.go file and create a executable binary file called ```hello```.  

Now, you can run this binary with the following command:

```
./hello
```
You should see this output:

```
Hello, COMP423
```

??? question
    **What's the difference between ```build``` and ```run```?**
    
    * The Go ```run``` command compiles and immediately runs your code without creating a binary file.
    * The Go ```build``` command compiles dependencies and files to create an executable binary which is run independently of the Go source file. 

## Summary
In this tutorial, you have completed the basic tasks to help you set up a Go dev container using Docker, build a Go project, and understand some simple go commands. Thanks for following along and congratulations on your first Go project!