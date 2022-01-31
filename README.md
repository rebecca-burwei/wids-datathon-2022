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

# Week 2
This week, we will explore the data, understand what the fields mean, and look into different ways to preprocess the data.

## Task 1 -- Exploring the data
Take a look at the data and see if there is anything interesting or unusual about the data. Real world data is very messy and usually requires some cleaning up. I think this Kaggle dataset is quite clean, but it doesn't hurt to go through the exercise. Some questions to consider:

* Are there any fields with lots of missing values? What should we do about them (leave out, impute values, simulate values from a distribution, etc)?
* Are there any unusual distributions in the data? 
  * For example, I noticed that the distribution of elevations in test.csv is quite strange.
  * The distribution of the target variable is particularly important. Models will be biased towards mimicking the same distribution they are trained on.
  * It's important to notice when the distribution of the test and train data is different. We'll be evaluated on the test data, but only able to build models on the train data, so it's best when the two distributions are similar. If they are not similar, it may be helpful to weight the train data so it's more similar to the test data.
* Are there any outliers?

Resources:
* This [Kaggle notebook](https://www.kaggle.com/ccollado7/wids-complete-eda#3.-Analysis---Train-dataset) has some useful code for making lots of plots.
* This [Kaggle notebook](https://www.kaggle.com/farazrahman/bee-building-energy-efficiency-eda#2-|-EDA) has some interesting insights about the dataset.
 
## Task 2 -- Preprocessing by field type
There are 3 types of fields in this data: continuous (e.g., floor_area, avg_temp), categorical (e.g., building_class, facility_type) and ordered discrete (e.g., year_built, energy_star_rating, days_with_fog). A common interview question: What are some ways to preprocess each type of field, and what are the pros and cons of each preprocessing method?

Here are some common ways to preprocess each type of field:
* Continuous fields: use a log scale, normalize, no preprocessing
* Categorical fields: make dummy variables (and optionally apply a [dimension reduction](https://scikit-learn.org/stable/modules/unsupervised_reduction.html#pca-principal-component-analysis)), group some categories together or organize the categories into a hierarchy, use a pre-trained word embedding for longer text fields
* Ordered discrete: usually you just pretend these are either continuous or categorical

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
