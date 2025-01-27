# Setting up a dev container for Go

<<<<<<< HEAD
* Primary author: [Daniel Zhang](https://github.com/D123aniel/)
=======
* Primary author: [Daniel Zhang](https://github.com/D123aniel/)
* Reviewer: [Mann Barot](https://github.com/MannBarot)

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
>>>>>>> edits/admonitions
