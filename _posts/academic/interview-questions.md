---
title: 'Collection of interview questions'
date: 2023-01-24
permalink: /posts/2024/01/interview-questions/
tags:
  - interview
  - academic
---

Summary: A short walkthrough of common interview questions.

Summary of interview questions

1. [Probability and Statistics]

It rains on saturday w/ 30% chance and sunday w/ 40% chance. What is the probability that it rains at least once over the weekend (i.e. Saturday and Sunday)? 

Say the event of rain is now correlated (i.e. not independent between sunday and saturday). Do we have any intuition on what is the range of probabilities possible for raining at least once over the weekend?

or alternatively

I eat pizza on saturday w/ 30% chance and sunday w/ 40% chance. What is the probability that I eat pizza at least once over the weekend (i.e. Saturday and Sunday)? 

What is the range of probabilities possible for eating pizza at least once over the weekend if eating pizza on Sunday is dependent on Saturday. Use inclusion-exclusion principle.

2. [Probability and Statistics + Coding]

You have a 52 card shuffled standard deck. You flip over cards and can stop at any point. You get $1 if a black card is flipped. You get $-1 if a red card is flipped. What is the optimal strategy and the expected value of the optimal strategy?

[Intuition 1] Realize that the expected profit at any point in time is a function of the current number of red and black cards.

[Intuition 2] Since you can choose stop at any time, you always have at least an expected value of 0 (i.e. playing the entire deck). Alternatively, if you get lucky and can flip over 26 cards, the maximum profit would be 26.

[Intuition 3] Since you can choose when to stop, you can choose to stop if your expected additional profit of playing is less than the additional profit of not playing. I.e. the additional profit of not playing is always 0 because you don't flip over a card. The additional profit of playing will then recurse down.

From this point on, you can write out a recurrence relationship to allow you to compute the
expected value starting from 26 R and B cards.

3. [Probability and Statistics - Coding]
https://math.stackexchange.com/questions/999290/probability-brainteaser-expected-value-of-these-two-games

You can toss a coin 100 times or stop earlier, you are paid the percentage of heads of your tosses, estimate the upper bound of the value of the game.

[Intuition 1] The game is a function of the number of heads and number of tails seen. The baseline pay is H / (T + H), whereas the expected value of playing is a recursive function that can be computed given the boundary of H/100 being the payout when H + T == 100.

[Intuition 2] What is the stopping condition? Well you should "play" if the expected value of playing is greater than the expected payout of H / (T + H) at the current step. As a result, the optimal playing strategy is a function of your luck and the current state of the game.

Sample code solution:

```Python
def expected_value(T, H, n, memo):
    if T + H == n:
        return H / (T + H)

    if (T, H) in memo:
        return memo[(T, H)]

    val_if_play = 1./2 * expected_value(T + 1, H, n, memo) + 1./2 * expected_value(T, H + 1, n, memo)

    if T + H > 0:
        val_if_not_play = H / (T + H)
    else:
        val_if_not_play = 0

    memo[(T, H)] = val_if_play
    if val_if_play > val_if_not_play:
        return val_if_play
    else:
        return val_if_not_play


memo = dict()
memo_max = dict()
ev = expected_value(0, 0, 100, memo)
print(ev)
```

4. [Probability and Statistics - Coding]
xref: https://math.stackexchange.com/questions/999290/probability-brainteaser-expected-value-of-these-two-games

There is a gambling machine with n-slots. You put balls one-by-one into the machine, each ball has equal probability to get inside each slot. You can stop the game anytime. In the end you will be rewarded like this: for each 1-ball slot, you are rewarded $1; for each k-ball slot (k>=2), you are penalized $k; for each 0-ball slot you are rewarded nothing. What is your strategy? What is the expected value of the game?

```Python
def expected_value(r, e, n, num_balls, memo):
    if e == 0:
        return 0
    if num_balls - r - e >= 0:  # we threw too many balls already
        return 0
    if (r, e, num_balls) in memo:
        return memo[(r, e, num_balls)]

    p_empty = e / n
    p_single_to_k = r / n
    p_already_filled = (n - r - e) / n

    val_if_play = (
        p_empty * expected_value(r + 1, e - 1, n, num_balls + 1, memo)
        + p_single_to_k * expected_value(r - 1, e, n, num_balls + 1, memo)
        + p_already_filled * expected_value(r, e, n, num_balls + 1, memo)
    )

    # value if we don't play is equal to the 1-slots minus the number of extra balls we've thrown
    num_extra = num_balls - r
    val_if_not_play = r - num_extra

    memo[(r, e, num_balls)] = max(0, val_if_play, val_if_not_play)
    if val_if_play > val_if_not_play:
        return val_if_play
    else:
        return val_if_not_play


n = 100
memo = dict()
arr = [0] * n
ev = expected_value(0, n, n, 0, memo)
print(ev)
```

5. https://jerryqin.com/posts/a-working-list-of-probability-problems-week-three


## DE Shaw Phone Interview

1. Algorithm for approximating square-root of any number

Review Newton Raphson and setting up an equation, where the roots of the equation provide the solution.

Given "n", where we wish to approximate sqrt (n), we desire to find a number x, such that x^2 = n. Thus, let our function be f(x) = x^2 - n. If we find the roots of f(x), we have solved the problem. This now boils down to Newton-Raphson 0 finding for f(x). 

The recursive algorithm for Newton-Raphson is provide an initial guess x_0. 

x(n+1) = x(n) - f(x(n)) / f'(x(n)) = x(n) - (x(n)^2 - n) / (2x(n))

We can iterate until x(n+1) - x(n) < THRESHOLD, where the threshold is some precision we are interested in.

2. What is the probability of X > 0 given X + Y > 0, where X and Y are iid N(0, 1).

P(X > 0 | X+Y>0) = P(X > 0 | X> -Y) = 1 - P(X < 0 | X > -Y)

Now P(X < 0 | X > -Y) = P(X < 0 | X > -Y, Y > 0)P(Y > 0) + P(X < 0 | X > -Y, Y < 0)P(Y < 0). However, if Y < 0, then -Y > 0, and thus P(X < 0 | Y < 0, X > - Y) = 0. On the other hand, P(X < 0 | Y > 0, X > -Y) is symmetric around 0, such that P(X < 0 | Y > 0, X > -Y) = P(X > 0 | Y > 0, X > -Y). 

Thus P(X < 0 | X > -Y) = 1/2 * 1/2 = 1/4

So our final answer for P(X > 0 | X+Y>0) = 1 - 1/4 = 3/4.

3. You are given a stock, which has an initial price of $100, i.e. r(0) = 100. Let r(1), r(2), r(30), denote the percentage difference in the stock price against the previous day. For example, if the stock price on day 1 is $110, then r(1) = 0.1 because it is 10\% higher than the previous day's price of $100.

If we know that the sum of all the returns $\sum_{i=1}^30 r(i) = 0$, then what can we say about the stock price on day 30?

- First, lower the dimensionality of the problem to 1, or 2 days. Note that if the return is 0.1 on day 1, it must be -0.1 on day 2 by the property that the sum of all returns is 0. Thus the final stock price on day 2 is $99. This is the case whether the returns start with -0.1 and then 0.1 on day 2. This pattern in general may hold?

- Let's see if holds in general: We can write down a pattern for the stock price as a function of the day. Let p(t) = stock price on day t, with p(0) = $100. Write down the recursive formulation.

p(t) = p(t-1) + r(t) * p(t-1)
p(t-1) = p(t-2) + r(t-1) * p(t-2)

=> p(t) = p(t-2) + r(t-1) * p(t-2) + r(t) * p(t-2) + r(t) * r(t-1) * p(t-2)

which gives rise to a recursive formula we can iterate until p(0):

p(t) = p(0) + \sum_{i=1}^30 r(i) * p(0) + \prod_{i=1}^30 r(i) * p(0)

By the assumption, we know that the summation term is equal to 0, so it can simplify to:

p(t) = p(0) + \prod_{i=1}^30 r(i) * p(0)

Note, we cannot say anything unless we know the sign of the \prod_{i=1}^30 r(i). It can be 0 if there is a day with return being equal to 0. This can be negative if there are an odd number of days with negative return. However, is that guaranteed?

For example, we could have a return of 0.4, -0.2, -0.2, 0.0, which sums up to 0, but also multiplies by 0, so the product is 0. If instead, 0.4, 0.1, -0.25, -0.25. We have actually that the product is positive. What if we consider six days? Say we have 0.4, -0.1, -0.1, -0.1, -0.1, 0.0, we have a product of 0. In addition, if we have 0.4, 0.1, -0.1, -0.1, -0.1, -0.2, we can have a product > 0. What about if we have three days? We can have 0.4, -0.4, 0.0, or 0.4, -0.1, -0.3. It seems that three days guarantees the product to be negative. What about five days? We have 0.4, -0.1, -0.1, -0.1, -0.1, which gives a positive product.

So in general, it is impossible to say anything about p(t) with respect to p(0) because we do not know the sign of the term \prod_{i=1}^30 r(i).

## Machine Learning
xref: https://medium.com/series/6c1e95b4b64a

1. Merge k (in this case k=2) arrays and sort them.
2. How best to select a representative sample of search queries from 5 million?
3. Three friends in Seattle told you it’s rainy. Each has a probability of 1/3 of lying. What’s the probability of Seattle is rainy?

4. Can you explain the fundamentals of Naive Bayes? How do you set the threshold?
5. Can you explain what MapReduce is and how it works?
6. Can you explain SVM?
7. How do you detect if a new observation is outlier? What is a bias-variance trade off ?
8. Discuss how to randomly select a sample from a product user population.
9. How do you implement autocomplete?
0.Describe the working of gradient boost.
11. Find the maximum of sub sequence in an integer list.
12. What would you do to summarize a twitter feed?
13. Explain the steps for data wrangling and cleaning before applying machine learning algorithms.
14. How to deal with unbalanced binary classification?
15. How to measure distance between data point?
16. Define variance.
17. What is the difference between box plot and histogram?
18. How do you solve the L2-regularized regression problem?
19. How to compute an inverse matrix faster by playing around with some computational tricks?
20. How to perform a series of calculations without a calculator. Explain the logic behind the steps.
21. What is a difference between good and bad Data Visualization?
22. How do you find percentile? Write the code for it.
23. Find max sum subsequence from a sequence of values.
24. What are the different regularization metrics L1 and L2?
25. Create a function that checks if a word is a palindrome.

https://github.com/ngavrish/coursera-machine-learning-1/tree/master/quiz

https://github.com/dingran/quant-notes

# Useful Review Links:
- https://drive.google.com/drive/folders/1zxXNQKYrGk7fFnzaUb78VqVw-kv7Yy2B Stanford old midterms
- Stanford class notes: https://web.stanford.edu/class/cs109/
- Counting k balls in n boxes: https://tylerzhu.com/assets/handouts/ballsandboxes.pdf
- L1 regression solved in different ways: http://blog.omega-prime.co.uk/2020/04/01/l1-regression/