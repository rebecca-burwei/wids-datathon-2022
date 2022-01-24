# wids-datathon-2022
This repo contains the code for our team submission to WIDS Datathon 2022 [Kaggle Competition](https://www.kaggle.com/c/widsdatathon2022).

# Schedule 
Five weeks will go by very quickly! Here is a proposed schedule.
* Week 1: Set-up. Get organized as a team.
* Week 2: Explore the data. Do some preliminary preprocessing.
* Week 3: Build initial models.
* Week 4: Refine models.
* Week 5: Clean up the code base, submit predictions to the Kaggle competition, write a blog post or make a presentation about what you accomplished and learned.

Every week, each team member should aim to:
* Make at least one contribution to the codebase (open a pull request)
* Review a pull request from another team member

# Week 1
This week, you should download the data from Kaggle, set up your local computing environment in Python, and familiarize yourself with Git and GitHub.

## First time set up
We assume you already have Python 3 and Pip installed.

1. Clone the repo.
2. [Install jupyter notebook](https://jupyter.org/install) using pip.
3. [Install virtualenv](https://virtualenv.pypa.io/en/latest/installation.html#via-pip) using pip.
4. Create a new virtualenv using the requirements.txt file that is already in the repo. I called my virtualenv `wids-venv` and put it in the top-level of the repo. Instructions [here](https://towardsdatascience.com/create-virtual-environment-using-virtualenv-and-add-it-to-jupyter-notebook-6e1bf4e03415) for how to do this -- you have to scroll down quite a bit, but the entire article is good to read. 
5. Add the virtualenv you just created to jupyter notebook. Instructions [here](https://towardsdatascience.com/create-virtual-environment-using-virtualenv-and-add-it-to-jupyter-notebook-6e1bf4e03415), scroll down.
6. Download the data from [Kaggle](https://www.kaggle.com/c/widsdatathon2022/data) and unzip it into the data folder.

## Git standards
Here is how we will use Git and GitHub as a team.

The team version of the code is on the `main` branch. Team members should do work on their own branches. When you are ready to make a contribution to the team codebase, open a pull request on GitHub to merge the work on your branch into the `main` branch.

If you are new to Git and GitHub, here are some resources:
* [An Intro to Git and GitHub](https://medium.com/@abhishekj/an-intro-to-git-and-github-1a0e2c7e3a2f)
* [About Git](https://docs.github.com/en/get-started/using-git/about-git)
* Try opening a pull request on our repo and see what happens! :)
