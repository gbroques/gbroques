---
layout: post
title:  "Linear Regression with One Variable"
permalink: 'linear-regression-with-one-variable'
date: 2017-08-21 00:00:00 -0500
categories: tutorials
excerpt_separator: <!--more-->
---

This post details the first week of Andrew Ng's excellent course, [Machine Learning](https://www.coursera.org/learn/machine-learning) on Coursera.

<!--more-->

Imagine your a CEO of a food-truck business considering a new city for a truck. You already have trucks in various cities and data on population and profit. Plotting the data gives the following graph.

![Food Truck Profits]({{ "/assets/img/food-truck-profits.png" | prepend: site.baseurl }})

The idea behind **linear regression** is to generate a line that best fits the data. Then, you can use that line to predict whether a new city will be profitable.

Implementing linear regression requires **three** main components:

1. The hypothesis function
2. The cost function
3. And Gradient Descent

### The Hypothesis Function

First you need a function that maps input values, population, to output values, profit. Conventionally this is called the **hypothesis function** and denoted with $$h_\theta(x)$$. For uni-variate linear regression (linear regression with one variable) the hypothesis function looks like this:

$$ h_\theta(x^{(i)}) = \theta_0 + \theta_1x^{(i)}$$

Where $$i$$ is an index into the training set and can take on the values $$1, 2, 3, ..., m$$ where $$m$$ is the total number of training examples.

Using different symbols and rearranging the right hand side&mdash;Its possible to form the familiar equation for a line $$y = mx + b$$.

Computing the hypothesis function for a given $$x$$ returns the *predicted value* and the corresponding $$y$$ is called the *actual value*. These terms will be used later.

### The Cost Function

Now you need a way to measure the accuracy of the hypothesis function. To do this, you'll use a function called the **cost function** denoted with $$J(\theta_0, \theta_1)$$. It looks like this:

$$J(\theta_0, \theta_1) = \dfrac {1}{2m} \displaystyle \sum _{i=1}^m \left (h_\theta (x_{i}) - y_{i} \right)^2$$

Another name for this function is the "mean squared error". Breaking apart the equation helps understand the reasoning behind this name.

Subtracting the actual value $$y_i$$, from the predicted value $$h_\theta(x_i)$$ gives the *error*, or how far off the prediction is from the actual value. Summing the *squared error* for each training example and dividing by the total number $$m$$, gives the "mean squared error".

The mean is halved $$(\dfrac {1}{2})$$ as a convienance for the computation of gradient descent (more on this soon), as differentiating the square function $$(h_\theta (x_{i}) - y_{i})^2$$ cancels out the $$\dfrac {1}{2}$$ term.

To recap, the **hypothesis function** predicts values of *y* based on values of *x*. For this problem, the hypothesis function predicts *profit* based on *population*. Then, the **cost function** calculates the accuracy of the hypothesis function. If the hypothesis function is *good* at predicting profit, then the cost will be **near zero**. Conversely, if the hypothesis function is *poor* at predicting profit, then the cost will be **very large**.

### Gradient Descent

Now you need a way to estimate $$\theta_0$$ and $$\theta_1$$ for the hypothesis function. To do this, you use **gradient descent**. [Gradient Descent](https://en.wikipedia.org/wiki/Gradient_descent) is an iterative optimization algorithm for minimizing a function. In machine learning, gradient descent is used to minimize the cost function.

Visualizing the cost function is helpful for understanding how gradient descent works. Plotting $$\theta_0$$ on the x-axis, $$\theta_1$$ on the y-axis, and $$J(\theta_0, \theta_1)$$ on the z-axis gives the following graph:

![Convex Function]({{ "/assets/img/convex-function.png" | prepend: site.baseurl }})

The cost function is shaped like a bowl or contact lense. This is called a *convex function*. Mathematically it means that there is only one minimum, the global minimum. Contrast this to a *non-convex* function:

![Non-Convex Function]({{ "/assets/img/non-convex-function.png" | prepend: site.baseurl }})

Where depending on the initial values of $$\theta_0$$ and $$\theta_1$$, gradient descent may converge on the global minimum or a local minimum. That's why it's important for the cost function to be *convex*.

The algorithm for gradient descent looks like this:


Repeat until convergence: {

$$\theta_j := \theta_j - \alpha \frac{\partial}{\partial \theta_j} J(\theta_0, \theta_1)$$

}

Where $$j = 0,1$$ and represents an index into the feature set. The colon-equals $$:=$$ means assignment. Alpha $$\alpha$$ represents the **learning rate**. The learning rate determines how big of a step you take down the gradient or "slope".

Picking the right value for $$\alpha$$ is important. If $$\alpha$$ is too small, then gradient descent will run very slow. If $$\alpha$$ is too large, then gradient descent will overshoot the minimum and fail to converge.

The swirly-d symbol, $$\partial$$, called "del", distinguishes **partial derivatives** from ordinary single-variable derivatives. It reads "take the partial derivative of $$J(\theta_0, \theta_1)$$ with respect to $$\theta_j$$".  See [Khan Academy](https://www.khanacademy.org/math/multivariable-calculus/multivariable-derivatives/partial-derivative-and-gradient-articles/a/introduction-to-partial-derivatives) for more details.

After calculating the partial derivative for $$J(\theta_0, \theta_1)$$ the gradient descent algorithm for linear regression with one variable looks like this:

Repeat until convergence: {

$$\theta_0 := \theta_0 - \alpha \dfrac {1}{m} \displaystyle \sum _{i=1}^m \left (h_\theta (x_{i}) - y_{i} \right)$$

$$\theta_1 := \theta_1 - \alpha \dfrac {1}{m} \displaystyle \sum _{i=1}^m \left ((h_\theta (x_{i}) - y_{i} \right) x_{i})$$

}

For gradient descent to properly work you must **simultaneously update** $$\theta_0$$ and $$\theta_1$$. This is because the calculation for $$\theta_1$$ depends on the value of $$\theta_0$$ and vise-versa. The following is a correct implementation:

$$temp_0 := \theta_0 - \alpha \dfrac {1}{m} \displaystyle \sum _{i=1}^m \left (h_\theta (x_{i}) - y_{i} \right)$$

$$temp_1 := \theta_1 - \alpha \dfrac {1}{m} \displaystyle \sum _{i=1}^m \left ((h_\theta (x_{i}) - y_{i} \right) x_{i})$$

$$\theta_0 := temp_0$$

$$\theta_1 := temp_1$$

Applying gradient descent on the data results in $$\theta_0 \approx -3.6303$$ and $$\theta_1 \approx 1.1664$$. This means the hypothesis function is:

$$ h_\theta(x) = -3.6303 +  1.1664x$$

Plotting the hypothesis function produces a best-fit line to the data:

![Best Fit Line]({{ "/assets/img/food-truck-profits-best-fit-line.png" | prepend: site.baseurl }})

For [St. Louis, Missouri](https://en.wikipedia.org/wiki/St._Louis) with a population of 317,419 the hypothesis function predicts a profit of $333,922.66. That's not bad for a food truck!

Next up is linear regression with multiple variables!