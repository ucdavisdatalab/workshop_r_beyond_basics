# Workshop: Intermediate R

_[UC Davis DataLab](https://datalab.ucdavis.edu/)_  
_Winter 2024_  
_Instructors: Nick Ulle, Wesley Brooks_  
_Maintainer: Nick Ulle <<naulle@ucdavis.edu>>_  

* [Reader](https://ucdavisdatalab.github.io/workshop_intermediate_r/)

This is the reader for all of UC Davis DataLab's Intermediate R workshop
series. The reader currently has four parts:

1. _Cleaning & Reshaping Data_

2. _Writing & Debugging R Code_

3. _Data Visualization & Analysis in R_

1. _Thinking in R_, which is about understanding how R works, how to diagnose
   and fix bugs in code, and how to estimate and measure performance
   characteristics of code.

Each part is independent and consists of approximately 2 workshop sessions.


## Contributing

The course reader is a live webpage, hosted through GitHub, where you can enter
curriculum content and post it to a public-facing site for learners.

To make alterations to the reader:

1.  Run `git pull`, or if it's your first time contributing, see
    [Setup](#setup).

2.  Edit an existing chapter file or create a new one. Chapter files are R
    Markdown files (`.Rmd`) at the top level of the repo. Enter your text,
    code, and other information directly into the file. Make sure your file:

    - Follows the naming scheme `##_topic-of-chapter.Rmd` (the only exception
      is `index.Rmd`, which contains the reader's front page).
    - Begins with a first-level header (like `# This`). This will be the title
      of your chapter. Subsequent section headers should be second-level
      headers (like `## This`) or below.
    - Uses caching for resource-intensive code (see [Caching](#caching)).

    Put any supporting resources in `data/` or `img/`. For large files, see
    [Large Files](#large-files). You do not need to
    add resources generated by your R code (such as plots). The knit step saves
    these in `docs/` automatically.

3.  Run `knit.R` to regenerate the HTML files in the `docs/`. You can do this
    in the shell with `./knit.R` or in R with `source("knit.R")`.

4.  Run `renv::snapshot()` in an R session at the top level of the repo to
    automatically add any packages your code uses to the project package
    library.

5.  When you're finished, `git add`:
    - Any files you added or edited directly, including in `data/` and `img/`
    - `docs/` (all of it)
    - `_bookdown_files/` (contains the **knitr** cache)
    * `renv.lock` (contains the **renv** package list)
<!--
    - `.gitattributes` (contains the Git LFS file list)
-->

    Then `git commit` and `git push`. The live web page will update
    automatically after 1-10 minutes.


### Caching

If one of your code chunks takes a lot of time or memory to run, consider
caching the result, so the chunk won't run every time someone knits the
reader. To cache a code chunk, add `cache=TRUE` in the chunk header. It's
best practice to label cached chunks, like so:

````
```{r YOUR_CHUNK_NAME, cache=TRUE}
# Your code...
```
````

Cached files are stored in the `_bookdown_files/` directory. If you ever want
to clear the cache, you can delete this directory (or its subdirectories).
The cache will be rebuilt the next time you knit the reader.

Beware that caching doesn't work with some packages, especially packages that
use external libraries. Because of this, it's best to leave caching off for
code chunks that are not resource-intensive.


<!--
### Large Files

If you want to include a large file (say over 1 MB), you should use git LFS.
You can register a large file with git LFS with the shell command:

```sh
git lfs track YOUR_FILE
```

This command updates the `.gitattributes` file at the top level of the repo. To
make sure the change is saved, you also need to run:

```sh
git add .gitattributes
```

Now that your large is registered with git LFS, you can add, commit, and push
the file with git the same way you would any other file, and git LFS will
automatically intercede as needed.

GitHub provides 1 GB of storage and 1 GB of monthly bandwidth free per repo for
large files. If your large file is more than 50 MB, check with the other
contributors before adding it.
-->

### Github Actions

GitHub Actions can be set up to automatically render your reader when you push 
new content to a repo. If you would like to use this function, download the 
materials in [datalab-dev/utilities/render_bookdown_site][render-site] and 
follow the instructions there.

[render-site]: https://github.com/datalab-dev/utilities/tree/main/render_bookdown_site

## Setup


<!--
### Git LFS

This repo uses [Git Large File Storage][git-lfs] (git LFS) for large files. If
you don't have git LFS installed, [download it][git-lfs] and run the installer.
Then in the shell (in any directory), run:

```sh
git lfs install
```

Then your one-time setup of git LFS is done. Next, clone this repo with `git
clone`. The large files will be downloaded automatically with the rest of the
repo.

[git-lfs]: https://git-lfs.github.com/
-->


### R Packages

This repo uses [**renv**](https://rstudio.github.io/renv/) for package
management. Install **renv** according to the installation instructions on
their website.

Then open an R session at the top level of the repo and run:

```r
renv::restore()
```

This will download and install the correct versions of all the required
packages to **renv**'s package library. This is separate from your global R
package library and will not interfere with other versions of packages you have
installed.

[Back to Top](#top)
