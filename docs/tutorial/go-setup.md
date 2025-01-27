# Setting up a dev container for Go

* Primary author: [Daniel Zhang](https://github.com/D123aniel/)
* Reviewer: [Mann Barot](https://github.com/MannBarot)

## Introduction

Dev Containers are a powerful way to ensure all team members in a project have the same dependencies and environment without having to locally download everything, risking version mismatches and conflicts on personal machines. Dev Containers also provide a way to quickly get team members up and running by pre-defining dependencies, versions, tools, and configurations in a single file. They also work in isolation from your host machine, allowing developers to prevent conflicts between versions and dependencies. 

These benefits provided by Dev Containers ensure a smooth and reliable development experience, especially in collaborative settings. In this tutorial, we go over how to start up a Go project using Dev Containers in VS Code. 

## Pre-requisites
These items are required to have in order to set up your devcontainer:

1. [GitHub](https://github.com/) Account
2. Install [Git](https://github.com/git-guides/install-git)
3. Download and install Microsoft Visual Studio Code ([VS Code](https://code.visualstudio.com/download))
4. Install [Docker Desktop](https://docs.docker.com/desktop/)


## Installation 

### Part 1: Setting up the Repo

#### Step 1. Create a Local Directory and initialize Git

(A) Open your terminal 
 
(B) Create a new directory for your project with the following commands:

```
mkdir go-tutorial
cd go-tutorial
```

(C) Initialize new Git repository

``` 
git init
```

(D) Create a README file:

```
echo "# New Go Project" > README.md
git add README.md
git commit -m "Initial commit w/ README"
```
!!! tip "Commit Early and Often"

    Committing early and often like this, even after small changes, helps users track their progress and changes much easier.

#### Step 2. Create a Remote Repo on GitHub

(A) Log in to your GitHub account and navigate to Create a New Repository Page

(B) Fill in the following details (example shown below): 

* **Repository Name**: ```go-tutorial```
* **Description**: "Go Project Setup Tutorial"
* **Visibility**: Public

#### Step 3. Link your Local Repository to GitHub

(1) Add the GitHub Repository as a remote:

```
git remote add origin https://github.com/<your-username>/go-tutorial.git
```

Replace ```
<your-username>
``` with your GitHub username.

(2) Ensure your default branch is on ``` main ``` with the subcommand ``` git branch ```. If not, rename it to main with the following command: ``` git branch -M main ```.

(3) Push local commits to the GitHub Repository

``` 
git push --set-upstream origin main 
```

!!! warning "Check Remote URL"
    Double-check your remote URL to ensure it points to the correct repository. This can be useful when working on multiple repositories/projects at once.

### Part 2: Setting up the Development Environment

#### Step 1: Add Development Container Configuration

(1) In VS Code, open your ``` go-devcontainer-tutorial ``` directory. 

(2) Install the **Dev Containers** extension for VS Code.

(3) Create a ``` .devcontainer ``` directory in the root of your project.

(4) Add the following file inside the ``` .devcontainer ``` directory you just created:

``` .devcontainer/devcontainer.json ```

The ``` devcontainer.json``` file defines the configuration for your development environment. Here, we are specifying the following:

* ```name ```: Descriptive name for your container.
* ```image```: The Docker image to use. Here, we use the latest base image for Go by Microsoft.
* ```customization```: Adds useful customizations to VS Code. In this case, we are installing the Go lang extension from the VS Code marketplace. 
* ```postCreateCommand```: Upon creation of the devcontainer, we run the command "go version" automatically. This will ensure that the devcontainer is configured with the correct (latest) version of Go lang. 

``` json
{
    "name": "Example Go Project",
    "image": "mcr.microsoft.com/vscode/devcontainers/go:latest",
    "customizations": {
      "vscode": {
        "settings": {},
        "extensions": ["golang.Go"]
      }
    },
    "postCreateCommand": "go version"
  }
```

#### Step 2: Reopen the Project in a VS Code Dev Container

Reopen the project in a devcontainer by pressing ```Ctrl+Shift+P``` (```Cmd+Shift+P``` on Mac), and type "Dev Containers: Reopen in Container." Selecting the option will cause your VS Code to reload as the image is downloaded and requirements installed. Once your setup is complete, the terminal should print out the version of Go installed. Ensure the version is 1.23.4 (or the latest version at the time of completion).

!!! warning "Wrong Version"
    If the version is incorrect, ensure that the ```:latest``` tag is attached to the end of the image link. Then, press ```Ctrl+Shift+P``` (```Cmd+Shift+P``` on Mac) and type "Dev Containers: Rebuild Container" and run it.

### Part 3: Write your first program in Go

Now that your environment is set up within a devcontainer, we are going to write a simple program to begin. Our goal is to print out "Hello COMP423."

#### Step 1: Enable dependency tracking in your code.

Creating a go.mod file will enable dependency tracking in your code, allowing your code to keep track of other modules that provide packages your code might need. To do this, use the go mod command as follows: 

```
go mod init <github repository location>
```

!!! warning "Correct Module Path"
    Ensure that the GitHub remote repository is the same one as you are currently working in, and remove the "https://" at the beginning.

### Step 2: File creation and code

In your root directory, create a file named ```hello.go```. Paste the following code into the file, and save it.

```
package main

import "fmt"

func main() {
  fmt.Println("Hello COMP423")
}
```

!!! note "What does this do?"
    - We declare the main package, a required step for Go programs. 
    - ```import "fmt"``` imports the ```fmt``` package, a standard Go library used for formatted I/O. 
    - Then, we create a ```main``` function as an entry point to our program, and use the ```Println``` function from the ```fmt``` library to print the string "Hello COMP423". 

To run your code, use the command ``` go run .``` in your terminal to see the output (don't forget the dot at the end)!

We can also use the ```build``` subcommand to build the program into a binary file, similar to the ```gcc```command used mainly for C and C++ development. To do so, we run ```go build -o main``` in our terminal. This produces a binary file ```main```, which is an executable file that can be executed separately from Go's environment. To execute the file directly, run the command ```./main```.

!!! info "```run``` vs ```build```"
    ```go run``` automatically compiles and executes the program. ```go build``` compiles but doesn't execute the program, instead creating a separate binary file. This is an executable file that can be run later independent of the GO environment. This allows for more portable binary files for sharing, and ensuring they work outside of this particular environment.

Credits and Acknowledgements: [https://comp423-25s.github.io/resources/MkDocs/tutorial/](https://comp423-25s.github.io/resources/MkDocs/tutorial/)