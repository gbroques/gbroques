---
layout: post
title:  "Partially Differentiate the Mean Squared Error"
permalink: 'partially-differentiate-the-mean-squared-error'
date:   2017-06-25 00:00:00 -0500
categories: notes
excerpt_separator: <!--more-->
---

In the first week of [Stanford's machine learning course from Coursera](https://www.coursera.org/learn/machine-learning),  Andrew Ng introduces the algorithm for **gradient descent**. Gradient descent finds parameters theta $$\theta$$ that minimize the *cost function* by using partial differentiation. While providing a great explanation of gradient descent, he fails to give an adequate explanation of the differentiation step.

<!--more-->

This post aims to provide a detailed explanation of how to partially differentiate the mean squared error and derive the formula for gradient descent yourself.

Recall the following formulas:

##### The Hypothesis Function
<p>$$ h_\theta(x^{(i)}) = \theta_0 + \theta_1x^{(i)}$$</p>

##### The Cost Function

<p>$$J(\theta_0, \theta_1) = \dfrac {1}{2m} \displaystyle \sum _{i=1}^m \left (h_\theta (x_{i}) - y_{i} \right)^2$$</p>

##### Gradient Descent

Repeat until convergence:

$$\theta_j := \theta_j - \alpha \frac{\partial}{\partial \theta_j} J(\theta_0, \theta_1)$$

Where $$j = 0,1$$ and represents the feature index number.

If your familiar with derivatives, but not partial derivatives, read this [article](https://www.khanacademy.org/math/multivariable-calculus/multivariable-derivatives/partial-derivative-and-gradient-articles/a/introduction-to-partial-derivatives) from Khan Academy first. 

Begin by partially differentiating $$J(\theta_0, \theta_1)$$ with respect to $$\theta_0$$:

$$\frac{\partial}{\partial \theta_0} J(\theta_0, \theta_1)$$

Substitute $$J(\theta_0, \theta_1)$$ for its value:

$$\frac{\partial}{\partial \theta_0} (\dfrac {1}{2m} \displaystyle \sum _{i=1}^m \left (h_\theta (x_{i}) - y_{i} \right)^2)$$

Apply the [constant factor rule](https://en.wikipedia.org/wiki/Constant_factor_rule_in_differentiation) to move the $$\dfrac {1}{2m}$$ term outside the derivative:

$$\dfrac {1}{2m} \frac{\partial}{\partial \theta_0} (\displaystyle \sum _{i=1}^m \left (h_\theta (x_{i}) - y_{i} \right)^2)$$

The [sum rule](https://en.wikipedia.org/wiki/Sum_rule_in_differentiation) states:

$$\frac{\partial}{\partial \theta_0} (\displaystyle \sum _{i=1}^m \left (h_\theta (x_{i}) - y_{i} \right)^2)$$

Is **equivalent** to

$$\frac{\partial}{\partial \theta_0} (h_\theta(x_1) - y_1)^2 + \frac{\partial}{\partial \theta_0} (h_\theta(x_2) - y_2)^2 + ... + \frac{\partial}{\partial \theta_0} (h_\theta(x_m) - y_m)^2$$

Focusing on one derivative of the summation:

$$\dfrac {1}{2m} \frac{\partial}{\partial \theta_0} (h_\theta(x) - y)^2$$

Apply the [chain rule](https://en.wikipedia.org/wiki/Chain_rule) and the [power rule](https://en.wikipedia.org/wiki/Power_rule).

$$\dfrac {1}{m} (h_\theta(x) - y) \times \frac{\partial}{\partial \theta_0} (h_\theta(x) - y)$$