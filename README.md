# Ty Modding Wiki

To get set up to run the wiki as a local host you just need to do 3 things

1. Clone the repository
2. Run `pip install mkdocs`
3. Open a terminal window either in the folder you cloned the repo to or within visual studio (code) and run `mkdocs serve`, that will create a local host of the site at [localhost:8000](localhost:8000)

Now whenever you save any files it'll automatically reload the local host in your browser in less than a second (much better than waiting 30-45 seconds for github actions to build the site, and to not spam the repo with commits)

To close the local host just close visual studio or the terminal, when you want to setup the local host again just run `mkdocs serve` again