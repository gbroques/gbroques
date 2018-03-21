---
layout: post
title:  "Logistic Regression and Regularization"
permalink: 'logistic-regression-and-regularization'
date:   2017-06-25 00:00:00 -0500
categories: machine-learning
excerpt_separator: <!--more-->
---
Unsupervised learning is divided into two categories: **regression** and **classification**. The difference between these categories is whether the values your trying to predict are continuous or discrete. Regression models predict *continuous* values, while classification models predict *discrete* values.

<!--more-->

To illustrate the difference consider predicting housing prices versus predicting whether email is spam. Housing prices can take on a wide range of values, and is therefore continuous. Whereas predicting if email is spam or not results in only two possibilities, and is therefore discrete. This makes predicting whether an email is spam or not better suited to classification methods like **logistic regression**.

Classifying email as spam is an example of **binary classification** because only two possibilities exists, 0 or 1. By convention, 0 is called the *negative* class, and 1 is called the *positive* class. In this example, a non-spam email would be 0, and a spam email would be 1. Sometimes these are denoted with the symbols $$-$$ and $$+$$.

Also for each $$x^{(i)}$$ the corresponding $$y^{(i)}$$ is called the **label** for that training example.

### Hypothesis Representation
In regression models the hypothesis function $$\theta^T x$$ produces a wide range of values. You can use the same hypothesis function for binary classification, but should restrict the range to between 0 and 1. You can represent this mathematically with the following expression:

$$0 \leq h_\theta (x) \leq 1$$

A function that maps values to the range (0, 1) is called the [logistic](https://en.wikipedia.org/wiki/Sigmoid_function) or **sigmoid function** and is denoted by $$g(z)$$. The equation is as follows:

$$g(z) = \frac{1}{1+e^{-z}}$$

$$z = \theta^T x$$

$$h_\theta (x) = g ( \theta^T x )$$

Plotting the sigmoid function gives the following graph:
![Sigmoid Function]({{ "/assets/img/sigmoid.png" | prepend: site.baseurl }})

As you can see, there's horizontal asymptotes at $$y = 0$$ and $$y = 1$$ restricting the range to (0, 1). This makes the function perfect for binary classification.

$$h_\theta (x)$$ gives the probability that the output is 1. For example, $$h_\theta (x) = 0.7$$ means there's a 70% chance the output is 1. The probability that the output is 0 is the complement of the probability that it is 1. If the probability of the output being 1 is 70%, then the probability that the output is 0 is 30%. This rule is summarized in the following notation:

$$h_\theta(x) = P(y=1 | x ; \theta) = 1 - P(y=0 | x ; \theta)$$