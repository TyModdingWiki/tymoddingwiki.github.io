# Ty Modding Wiki

## Setting up a local host
To get set up to run the wiki as a local host you just need to do 3 things:  
(Required to already have python installed)
1. Clone the repository
2. Run `pip install mkdocs-material`
3. Open a terminal either in the folder you cloned the repo to or within visual studio (code) in the root folder for the repo, and run `mkdocs serve`, that will create a local host of the site at [http://localhost:8000/](http://localhost:8000/)

Now whenever you save any files it'll automatically rebuild and reload the local host in your browser in less than a second, to quickly make sure everything looks right. (Much better than waiting 30-45 seconds for github actions to build the site, and to not spam the repo with commits)

To close the local host just close visual studio or the terminal, when you want to setup the local host again just run `mkdocs serve` again

## Creating pages and resources
To create any pages just add a .md file to the folder for the game you want to create the page for in the docs folder.   
Any resources you want to use for a page typically are put in the docs folder too, anything mkdocs specifically uses has the docs folder as the base directory (mainly just the mkdocs.yml file).

## Mkdocs documentation
The mkdocs material documentation is really good to follow to find out how to use the huge amount of features mkdocs has [https://squidfunk.github.io/mkdocs-material/](https://squidfunk.github.io/mkdocs-material/)

## Page not updating after commit
If after pushing a commit and the build actions are complete in the actions tab, but the website hasn't updated for you, you can use the hotkey `ctrl + f5` in your browser to force it to clear the cache and completely reload the site which usually fixes it
