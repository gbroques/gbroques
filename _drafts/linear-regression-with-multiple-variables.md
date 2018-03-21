---
layout: post
title: "Linear Regression with Multiple Variables"
permalink: 'linear-regression-with-multiple-variables'
date: 2017-06-25 00:00:00 -0500
categories: notes
excerpt_separator: <!--more-->
---

This post details the second week of Andrew Ng's fantastic [Machine Learning](https://www.coursera.org/learn/machine-learning) course on Coursera. I recommend reading [Linear Regression with One Variable]({{ "/linear-regression-with-one-variable" | prepend: site.baseurl }}) before reading this article.

<!--more-->

Linear regression with multiple variables, also known as "multi-variate linear regression", requires the following notation:

$$x_j^{(i)} = \text{value of feature } j \text{ in the }i^{th}\text{ training example}$$

$$x^{(i)} = \text{the input (features) of the }i^{th}\text{ training example}$$

$$m = \text{the number of training examples}$$

$$ n = \text{the number of features} $$

The multi-variable form of the hypothesis function is:

$$h_\theta (x) = \theta_0 + \theta_1 x_1 + \theta_2 x_2 + \theta_3 x_3 + \cdots + \theta_n x_n$$

Vectorizing the hypothesis function for one training example looks like:

$$h_\theta(x) =\begin{bmatrix}\theta_0 \hspace{2em} \theta_1 \hspace{2em} ... \hspace{2em} \theta_n\end{bmatrix}\begin{bmatrix}x_0 \newline x_1 \newline \vdots \newline x_n\end{bmatrix}= \theta^T x$$

Where $$x_{0}^{(i)} =1 \text{ for } (i\in { 1,\dots, m } )$$ making $$x$$ the same dimension as $$\theta$$ for easier matrix operations.

Gradient descent now accounts for $$n$$ features:

Repeat until convergence: {

$$\theta_j := \theta_j - \alpha \frac{1}{m} \sum\limits_{i=1}^{m} (h_\theta(x^{(i)}) - y^{(i)}) \cdot x_j^{(i)}$$

}

Where $$j = 0, 1, 2, \cdots, n$$

With notation covered, how do you achieve optimal results with gradient descent in practice?

### Gradient Descent in Practice
Two strategies improve gradient descent's performance in practice: **feature scaling** and **choosing the learning rate**.

###### Feature Scaling

[Feature scaling](https://en.wikipedia.org/wiki/Feature_scaling) speeds up gradient descent by scaling each feature into roughly the same range. With uneven input values certain parameters or *weights* update quicker than others resulting in less efficiency.

Scaling the inputs to roughly the same range creates efficient minimization.

Two techniques transform input values into roughly the same range: **standardization** and **min-max scaling**. Standardization involves subtracting the average value from the input value, and then dividing by the standard deviation:

$$x_i := \dfrac{x_i - \mu_i}{\sigma_i}$$

Where $$\mu_{i}$$ is the **average** of feature $$i$$ and $$\sigma_{i}$$ is the standard deviation. This gives the input values the properties of a standard normal distribution where $$\mu = 0$$ and $$\sigma = 1$$. This is important because you can apply the [empirical rule](https://en.wikipedia.org/wiki/68%E2%80%9395%E2%80%9399.7_rule) to the data.

The empirical rule states 68% of the data lies within the range [-1, 1], 95% of the data lies within [-2, 2], and 99.7% lies within [-3, 3]. Therefore most of the input values lie in roughly the same range. Below is a standard normal distribution:

![Standard Normal Distribution]({{ "/assets/img/std-normal-dist.png" | prepend: site.baseurl }})

**Min-max scaling**, also called *normalization*, involves subtracting the minimum from the input value, and then dividing by the range (the maximum value minus the minimum value):

$$x_i := \dfrac{x_i - min_i}{max_i - min_i}$$

Where $$min_i$$ the minimum value of feature $$i$$, and $$max_i$$ is the maximum value. Compared to standardization, min-max scaling maps input values to a tighter range [0, 1], which suppresses the effects of outliers.

For more information, read this [excellent article](http://sebastianraschka.com/Articles/2014_about_feature_scaling.html) by Sebastian Raschka.

###### Choosing the Learning Rate
Choosing the learning rate also affects the performance of gradient descent. Too small and gradient descent runs slowly. Too large and gradient descent diverges.

Creating a plot with the number of iterations on the x-axis, and cost function $$J(\theta)$$ on the y-axis helps determine the value for the learning rate. You should see the cost function decreasing as the number of iterations increase.

Picking a learning rate to start with is arbitrary. Start with a sufficiently small value like 0.1, and then experiment with values increasing and decreasing by roughly $$\frac{1}{3}$$. Consider the following graph:

![Learning Rates]({{ "/assets/img/learning-rates.svg" | prepend: site.baseurl }})

The graph shows five different learning rates minimizing the cost function at different speeds. The <span style="color: #FF00FF">magenta line</span> represents a learning rate of **1** and minimizes the cost function the quickest. A larger value for the learning rate, like **1.33**, causes gradient descent to diverge:

![Large Learning Rate]({{ "/assets/img/large-learning-rate.svg" | prepend: site.baseurl }})

### Improving Features

Sometimes creating new features out of existing ones improves model performance. For example, imagine your predicting housing prices and you have two features: the width of the property and the length. Multiplying these features together for a new feature area, may improve model performance.

### Polynomial Regression

Some data sets are too complex for straight lines. You can modify the hypothesis function by making it quadratic, cubic, a square root function, or any other form.

For example consider the hypothesis function:

$$h_\theta(x) = \theta_0 + \theta_1 x_1$$

This can be made quadratic:

$$h_\theta(x) = \theta_0 + \theta_1 x_1 + \theta_2 x_1^2$$

Or cubic:

$$h_\theta(x) = \theta_0 + \theta_1 x_1 + \theta_2 x_1^2 + \theta_3 x_1^3$$

Or a square root function:

$$h_\theta(x) = \theta_0 + \theta_1 x_1 + \theta_2 \sqrt{x_1}$$

Feature scaling becomes *very important* when choosing features this way. For example, if $$x_1$$ lies within the range [1, 1000], then $$x_1^2$$ lies within the range of [1, 1000000], and $$x_1^3$$ lies within [1, 1000000000]!

### The Normal Equation
Another way of minimizing the cost function is the **normal equation**. Unlike gradient descent the normal equation is *non-iterative*, meaning it minimizes the cost function in one calculation. Below is the formula:

$$\theta = (X^T X)^{-1}X^T y$$

Since there's no iteration, there's **no need** for feature scaling. You also don't need to choose a learning rate. Why use gradient descent then? Because the normal equation is more computationally expensive due to calculating the inverse of $$X^T X$$.

As a general rule, use the normal equation when $$n < 10,0000$$, and gradient descent when $$n \geq 10,000$$. Below is a table comparison of the two methods:

| **Gradient Descent** | **Normal Equation** |
|:------------- | ------------- |
| Need to choose alpha | No need to choose alpha |
| Iterative | Non-iterative |
| $$\mathcal{O}(kn^2)$$ | $$\mathcal{O}(n^3)$$ |
| Works well when $$n$$ is large | Slow when $$n$$ is very large |

<p></p>

##### Non-invertibility
In linear algebra, a matrix $$A$$ is said to be **non-invertible** (also singular or degenerate) if and only if $$A^{-1}$$ does not exist.

Two factors may cause $$X^T X$$ to be non-invertible:

1. Feature redundancy - Two features are closely related (linearly dependent)
2. Too many features ($$m \leq n$$) - Either delete features or use regularization 

When calculating $$(X^T X)^{-1}$$ use **pinv()** in GNU Octave and NumPy to calculate the [pseudo-inverse](https://en.wikipedia.org/wiki/Moore%E2%80%93Penrose_pseudoinverse), which has some of the same properties as the actual inverse, but always return a valid result.