---
layout: post
title:  "Naive Bayes Classifier"
permalink: 'naive-bayes-classifier'
date: 2017-08-21 00:00:00 -0500
categories: tutorials
excerpt_separator: <!--more-->
---

Naive Bayes classifiers are a simple model based upon [Bayes' theorem](https://en.wikipedia.org/wiki/Bayes%27_theorem) where you naively assume conditional independence between the features. Naive Bayes classifiers remain popular for [document classification](https://en.wikipedia.org/wiki/Document_classification), like categorizing email as spam or not spam. This post aims to thoroughly explain how these models work starting from Bayes theorem.

<!--more-->


### Bayes' Theorem
To properly understand how naive bayes classifiers work, one must first understand Bayes' theorem. Let's derive Bayes' theorem, by first discussing the probability of two events occurring. Consider the event of drawing a **jack** out of a deck of cards. Since there are **4** jacks, and **52** cards, the probability of this event occurring is $$\frac{4}{52}$$. This is expressed by the following notation:

$$P(Jack) = \frac{4}{52}$$

Now consider the event of drawing another **jack**. You already drew 1 jack, which leaves **3** remaining jacks, and **51** remaining cards. The probability of this event occurring is $$\frac{3}{51}$$. The probability of both events occurring is equal to the probability of drawing a jack, *times* the probability of drawing another jack. This is expressed as:

$$P(Jack \space and \space Jack) = \frac{4}{52} \cdot \frac{3}{51}$$

In general for any two events, **A** and **B**, the probability of A and B occurring is equal the probability of A occurring *times* the probability of B occurring, given that A occurred. We can express this using notation as:

$$P(A \space and \space B) = P(A) \cdot P(B|A)$$

$$P(B \vert A)$$ can be read as the probability of B occurring, *given* that A occurred. This is known as the [multiplication rule](https://www.khanacademy.org/math/ap-statistics/probability-ap/probability-multiplication-rule/a/general-multiplication-rule) and is the building block for Bayes' theorem.
