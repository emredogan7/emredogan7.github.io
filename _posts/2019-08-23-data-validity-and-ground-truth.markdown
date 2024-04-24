---
title: "Data Validity and Ground Truth"
layout: post
date: 2019-08-23 16:05
image: ../assets/post_images/data-validation-and-ground-truth/gt_scenario.png
headerImage: false
tag:
- academic
- machine learning
category: blog
author: emre dogan
description: About the ground truth definition on data
---

## TL;DR 
This post investigates the data validity and the ground truth definition. The motivation of this post comes from my first academic paper: _Investigating the Validity of Ground Truth in Code Reviewer Recommendation Studies_. You can access the full PDF version <a href="https://www.researchgate.net/publication/335078869_Investigating_the_Validity_of_Ground_Truth_in_Code_Reviewer_Recommendation_Studies">here</a>. 


## On Machine Learning and Data Validity

_Machine learning.._ I've had the chance to observe the hype of this term since 2015. In these years, everyone was trying to understand _what_ machine learning is all about. Almost 5 years have passed since that time. I don't know whether people have achieved to understand what it is all about, but nowadays everybody is trying to apply machine learning somehow. Without any concerns,  just by a few lines of code and a dataset. The necessity of learning the background of ML to use it is another issue to clarify, but not in this post (maybe later).


For the ones who don't know about _machine learning_, the best definition that I've encountered belongs to Tom M. Mitchell: 

>**A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P if its performance at tasks in T, as measured by P, improves with experience E**.

<img src="../assets/post_images/data-validation-and-ground-truth/ml_definition.png" alt="My image">
<p style='text-align: center;'><i>Figure: My illustration for Tom M. Mitchell's definition on machine learning</i></p>

<br><br>

__Experience__ in this definition corresponds to data instances used in training (learning) process. Machine learning is nothing but the process of making sense of these data instances so that new instances can be analyzed. For this reason, it can easily be concluded that __the reliability of a machine learning model is highly dependent on data.__ At this point, it becomes essential to define the term _ground truth_. 

<br>
Ground truth is a difficult phenomenon to explain. A clear definition from <a href="https://stackoverflow.com/questions/32182272/ground-truth-and-training-data-set">Stack Overflow</a> is given below:

> **Ground Truth is factual data that has been observed or measured, and can be analyzed objectively. It has not been inferred. If the data is based on an assumption, subject to opinion, or up for discussion, then, by definition, that is not Ground Truth data.**


As stated in the definiton, ground truth defines the reliability of data instances and their labels. To illustrate it better, let me give 2 different examples on the ground truth definition:

### 1- Cat and Dog Classifier:
With the recent improvements in computer vision and deep learning areas, image classification task has achieved great results in terms of accuracy. One of the most straightforward image classification application is __cat vs dog classifier__.  

<img src="../assets/post_images/data-validation-and-ground-truth/cat_dog.jpg" alt="cat_dog">
<p style='text-align: center;'><i>Figure: Data Instances from Cat and Dog Classifier Datasets</i></p>

Ground truth in this example refers to the correct labelling of data instances. _i.e.labelling cat images as CAT and dog images as DOG_.<br>

For this example, labelling is quite definite. Mislabelling occurs only when the person responsible for labelling (possibly Amazon Mechanical Turker) makes a mistake and labels a cat image as dog or vice versa. This kind of mistakes are known as _Label Noise_. Although these mistakes are crucial for the learning process, they can be ignored as they occur rarely.


### 2- Code Reviewer Recommendation:

This example is from a totally different area. In the software development teams, code review is an important best practice to examine the source code by highlighting bugs and enhancing the code quality. Recommeding the ideal reviwer for a pull request is a challenging task, especially in large development teams.

In the literature, there are different types of recommendation models to find the ideal reviewer. The table given below shows them:

<img src="../assets/post_images/data-validation-and-ground-truth/algos.png" alt="recommedation studies">
<p style='text-align: center;'><i>Table: Applied Methods of the Code Reviewer Recommendation Studies in the Literature</i></p>


As illustrated in the table, the majority of these recommendation models is based on several machine learning algorithms (kNN,SVM, genetic algorithm, bayesian, decision tree, etc.).In order to train these algorithms, some datasets collected from real life (proprietary or OSS projects) are used. These datasets consist of reviewer assignment instances from real life projects. 

Up to this point, everything is OK according to the definition of Tom M. Mitchell's definition. __Task(T)__ is to predict the ideal reviewer. __Experince(E)__ comes from the previous reviewer assignments and __the performance(P)__ is measured by different evaluation metrics _(top-k accuracy, precision, recall, etc.)_

What about the reliability of data? These recommendation models are trying to find and assign the _ideal_ reviewer for a pull request by using the previous reviewer assignments in real life. In other words, these models assume that real-life reviewer assignments are always ideal, __which is not the case!__

Consider the scenario given in the following figure. 
<p style='text-align: center;'><img src="../assets/post_images/data-validation-and-ground-truth/gt_scenario.png" width="400" alt="real life factors"><br><i>Figure: Non-ideal reviewer assignment scenario in real life</i></p>



The team leader selects the ideal code reviewer for a pull request. But due to several reasons, the ideal reviewer cannot complete the review and a new reviewer(non-ideal) has to be assigned. In the code reviewer assignment datasets collected from real life, there are many instances similar to this scenario. Non-ideal reviewer assignments are assumed to be ideal and used for training machine learning models. This flawed assumption reduces the reliability of reviewer recommendation models.


Several studies in real-life software projects reveal that code reviewer assignments are not usually done with the goal of finding the ideal reviewer. Here is a list of factors affecting the reviewer selection process in real life:


<p style='text-align: center;'><img src="../assets/post_images/data-validation-and-ground-truth/real-life.png" width="400" alt="real life factors"><br><i>Table: Factors Affecting the Reviewer Selection Process in Real Life</i></p>


### Conclusion

When we compare _the cat-dog classifier_ and _code reviewer recommendation models_, it is obvious that achieving a ground truth in cat-dog dataset is much more straightforward. The only factor threatening the ground truth is _label noise_ which can be ignored. In the case of code reviewer recommendation, the problem in data is more complicated to deal with. The recommendation models are claiming to find the ideal reviewer by using real-life data where the real-life reviewer assignments are not mostly ideal. There is a discrepancy between the claims of recommendation models and real life itself. I am currently working on this issue to solve this discrepancy in my research studies. 

Beyond these examples and the comparison, there is something to note on the current machine learning applications. People are trying to apply machine learning on every dataset they find without _investigating the validity of data_. __It must be noted that machine learning is nothing but the process of finding the patterns in data to make some predictions on the new data instances.__ It cannot think, sense or correct the faults in data. It simply mimics the actions in the dataset.

 __Don't expect an intelligent system when your data is dumb.__


_Emre Doğan_
<br>
_August 23, 2019_
