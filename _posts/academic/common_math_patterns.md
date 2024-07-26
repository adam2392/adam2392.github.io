---
title: 'Math Patterns'
date: 2024-07-26
permalink: /posts/2024/07/math-patterns/
tags:
  - interview
  - math
---

Summary: A short walkthrough of common math patterns that are useful for solving algorithmic problems.

# Math Patterns

## Numerical Programming

### Taylor Series

The Taylor series is a representation of a function as an infinite sum of terms that are calculated from the values of the function's derivatives at a single point. The formula for the Taylor series is:

$$f(x) = f(a) + f'(a)(x-a) + \frac{f''(a)}{2!}(x-a)^2 + \frac{f'''(a)}{3!}(x-a)^3 + ...$$

### Power Series (Exponential Function)

A power series is a series of the form:

$$\sum_{n=0}^{\infty} a_n(x-c)^n$$

where $a_n$ are the coefficients of the series, $x$ is the variable, and $c$ is the center of the series. The series converges to a function of $x$ in some interval around $c$. It is useful to know that the exponential function can be represented as a power series:

$$e^x = \sum_{n=0}^{\infty} \frac{x^n}{n!}$$

This converges rather quickly since the factorial term in the denominator grows very quickly.

### Newton's Method

Newton's method is an iterative method for finding the roots of a twice-differentiable function. It is a popular method for finding the minimum of a function. The formula is:

$$x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)}$$

Example: Finding the square root of a number $x$.

The derivation follows from the following intuition of framing the problem as finding a 0 to the function $f(x) = x^2 - a = 0$, where $a$ is the given number we are trying to find a square root of, and $x$ is our unknown solution. We start with an initial guess point $x_0$, and now the problem can be rewritten as follows: what is the value of h, such that $f(x) = f(x_0 + h) = 0$? Here, $x$ and $x_0$ are known, but h is unknown.

We can now write things in terms of the Taylor expansion of $f(x_i + h)$ around $h = 0$:

$$0 = f(x_i + h) = f(x_i) + f'(x_i)h + \frac{f''(x_i)}{2}h^2 + ...$$

If we ignore the higher terms, we get the following approximation:

$$0 \approx f(x_i) + f'(x_i)h$$

So therefore $h = -\frac{f(x_i)}{f'(x_i)}$. This is the update rule for Newton's method. The
new $x_{i+1} = x_i + h = x_i - \frac{f(x_i)}{f'(x_i)}$, which gives us Newton's method.


## Inequalities

### Jensen's Inequality
Value of a convex function $f$ of an integral is related to the integral of the convex function.

In other words, the function of the average of two points is less than or equal to the average of the values of the function at the two points.

$$f(\frac{x+y}{2}) \leq \frac{f(x) + f(y)}{2}$$

In the context of how it is used in machine learning, we commonly relate the function of an expectation to the expectation of the function.

$$f(E[X]) \leq E[f(X)]$$
