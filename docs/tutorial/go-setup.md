# Setting up a dev container for Go

* Primary author: [Daniel Zhang](https://github.com/D123aniel/) 

# Pre-requisites
These items are required to have in order to set up your devcontainer:
1. GitHub account
2. Install Git
3. Download and install Microsoft's Visual Studio Code (VS Code)
4. Install Docker

## Enabling extensions from Material for MkDocs

To begin, we will first enable some very useful (and basically required) markdown features. 

### Code Blocks
Code Blocks allows us to highlight code blocks in order for code to be easily readable and differentiable. To begin, simply paste the following source code directly into your `mkdocs.yml` file.

``` yaml
markdown_extensions:
  - pymdownx.highlight:
      anchor_linenums: true
      line_spans: __span
      pygments_lang_class: true
  - pymdownx.inlinehilite
  - pymdownx.snippets
  - pymdownx.superfences
```

To utilize the formatting, code blocks must be enclode with two separate lines of 3 backticks. A language "shortcode" must also be added to specify the language in which the formatting should be in. This shortcode is added right after the first 3 backticks. 

' ' ' shortcode  
      code  
' ' '

### Admonitions
Admonitions are known as "call-outs", as they allow the addition of side content without ruining the structure of the main content. To begin, paste the following source code directly into your 'mkdocs.yml' file. 

!!! tip "Tip"
  Admonitions are extremely useful in adding notes, tips, warnings, cautions, etc!

``` yaml
markdown_extensions:
  - admonition
  - pymdownx.details
  - pymdownx.superfences
```

## Installation 

### Part 1: Setting up the Repo

#### Step 1. Create a Local Directory and initialize Git

(A) Open your terminal 
 
(B) Create a new directory for your project with the following commands:

```
mkdir go-devcontainer-tutorial
cd go-devcontainer-tutorial
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

#### Step 2. Create a Remote Repo on GitHub

(A) Log in to your GitHub account and navigate to Create a New Repository Page

(B) Fill in the following details as follows: 

* **Repository Name**: ``` go-project ```
* **Descipriton**: "New Go Project"
* **Visibility**: Public

#### Step 3. Link your Local Repository to GitHub

(1) Add the GitHub Repository as a remote:

```
git remote add origin https://github.com/<your-username>/go-devcontainer-tutorial.git
```

Replace ```
<your-username>
``` with your GitHub username.

(2) Ensure your default branch is on ``` main ``` with the subcommand ``` git branch ```. If not, rename it to main with the following command: ``` git branch -M main ```.

(3) Push local commits to the GitHub Repository

``` 
git push --set-upstream origin main 
```

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

#### Step 2: Reopen the Project in a VS Code Dev Container

Reopen the project in a devcontainer by pressing ```Ctrl+Shift+P``` (```Cmd+Shift+P``` on Mac), and type "Dev Containers: Reopen in Container." Selecting the option will cause your VS Code to reload as the image is downloaded and requirements installed. Once your setup is complete, ensure in the ```go.mod``` file that the version is 1.23.4 (or the latest version at the time of completion).

### Part 3: Write your first program in Go

Now that your environment is set up within a devcontainer, we are going to write a simple program to begin. Our goal is to print out "Hello COMP423."

#### Step 1: Enable dependency tracking in your code.

Creating a go.mod file will enable dependency tracking in your code, allowing your code to keep track of other modules that provide packages your code might need. To do this, use the go mod command as follows: 

```
go mod init <github repository location>
```

### Step 2: File creation and code

In your root directory, create a file named ```hello.go```. Paste the following code into the file, and save it.

```
package main

import "fmt"

func main() {
  fmt.Println("Hello COMP423")
}
```

To run your code, use the command ``` go run .``` in your terminal to see the output (don't forget the dot at the end)!

We can also use the ```build``` subcommand to build the program into a binary file, similar to the ```gcc```command used mainly for C and C++ development. To do so, we run ```go build -o main``` in our terminal. This produces a binary file ```main```, which is an executable file that can be executed separately from Go's environment. To execute the file directly, run the command ```./main```.