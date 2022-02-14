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

# Week 3-4
This week, we will build some initial models.

## Task -- Build a baseline model
Both in machine learning and in industry, you typically start by building a simple model (any model that's easy for you to build), and use it as a baseline to improve off of.

Here are some resources for building baseline models:
* [CatBoost model](https://www.kaggle.com/chryzal/wids2022-catboost/notebook): This notebook builds a CatBoost model off of the same data that we have. You may need to install the catboost library and change the paths to the data files. Pay attention -- the notebook uses Mean Absolute Error as an evaluation metric, but the Kaggle competition uses Mean Squared Error.
* [XGBoost or LightGBM](https://towardsdatascience.com/catboost-vs-light-gbm-vs-xgboost-5f93620723db): Nowadays, there are 3 popular implementations of gradient-boosted trees: CatBoost, XGBoost and LightGBM. (When I started back in 2016, there was only XGBoost! :P) This article describes the differences between them and includes some code for how to run each one. If the CatBoost model is not working well for you, or if you're already familiar with gradient-boosted trees and would like more of a challenge, then try seeing if XGBoost or LightGBM works better. Maybe ensembling together all 3 works even better!
* Multilayer Perceptron (MLP): This is the most basic type of neural network you can build. A good place to start with your first neural network. The Multilayer Perceptron (MLP) has many names. Some people call it a "feed forward neural network". This [implementation](https://scikit-learn.org/stable/modules/generated/sklearn.neural_network.MLPRegressor.html#sklearn.neural_network.MLPRegressor) from sklearn is an easy one to get started with, and here is a [tutorial](https://towardsdatascience.com/deep-neural-multilayer-perceptron-mlp-with-scikit-learn-2698e77155e).
* Fancier neural nets: One limitation of the sklearn implementation is that you can only build MLPs. You can't build fancier types of neural nets like recurrent neural nets (RNNs) or convolutional neural nets (CNNs). To build fancier neural nets, you have to use tensorflow/keras or pytorch. This [tutorial](https://www.kaggle.com/ulrich07/wids-2022-ann-tf-starter#TENSORFLOW-STUFFS) shows you how to build a simple MLP using tensorflow/keras on our dataset. Even though you can build the same MLP with much less code using sklearn, learning to use tensorflow/keras will allow you to build fancier neural nets in the future.

My suggestions:
* Try building one of the gradient-boosted trees or a simple neural net (MLP).
* Pay attention to the evaluation metric. We're using Root Mean Squared Error. Some of the tutorials use other evaluation metrics (aka loss functions).
* Use an out-of-time split instead of a random split.

  When you split train.csv into a "train set" and "test set", split the data based on Year_Factor as opposed to randomly. Put all of the rows with `Year_Factor = 6` into the "test set", and the rest of the rows with Years 1-5 into the "train set". 

  I recommend this because all the rows in test.csv have `Year_Factor = 7`, but train.csv only contains Years 1-6. This means we will be forecasting the future. To find the model that produces the best forecasts, we can pretend that we don't know about Year 6 in train.csv, train the models only on Years 1-5, and evaluate them on Year 6. This scenario is very common in industry -- for example, when we want to predict next year's revenue, we build a model to predict the current year's revenue to see which modeling algorithm generalizes the best to the future.

* I took a brief look at last year's Kaggle winners, and they built ensembles of gradient-boosted trees and MLPs. Based on their advice, we might consider building separate models for each building_class or State_Factor. But this can wait until next week.

### Resources for learning about neural nets

* Andrew Ng's [course on neural networks](https://www.coursera.org/learn/neural-networks-deep-learning)
* Andrew Ng's [course on machine learning](https://www.coursera.org/learn/machine-learning) -- Machine Learning 101: starts with the basics of machine learning and linear regression, but it shows you how neural networks are a generalization of things you already know like linear regression or support vector machines
* [Articles](https://github.com/therealsreehari/Learn-Data-Science-For-Free#25_-neural-networks) about the most important math behind neural nets (gradient descent, optimizers, etc)
* Once you are familiar with the basics of neural nets, [Deep Learning Weekly](https://www.deeplearningweekly.com/) is a good newsletter to keep up-to-date with the latest developments in deep learning, and also to learn about different applications of deep learning technologies.

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
