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

What is the range of probabilities possible for eating pizza at least once over the weekend if eating pizza on Sunday is dependent on Saturday. Use inclusion-exclusion principle and bounds on the P(A \cup B) events given P(A) and P(B).

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

6. https://x.com/littmath/status/1769044719034647001?s=43&t=Ew8eS1seDjHua2vB1f40Tw
Flip a fair coin 100 times—it gives a sequence of heads (H) and tails (T). For each HH in the sequence of flips, Alice gets a point; for each HT, Bob does, so e.g. for the sequence THHHT Alice gets 2 points and Bob gets 1 point. Who is most likely to win?

Hint: First consider the expected value, and note that the expected number of points is
different from the probability of winning, where P(A wins) = P(A points > B points), and
P(B wins) = P(B points > A points).

Conceptually, consider the entropy of the game, and the fact that there are more states with
higher entropy (i.e. more combinations of a specific type, compared to another type).

Answer: Bob since there are more states in which Bob will win for a given sequence of flips.

b. Follow-up: What is the advantage that Bob has over Alice? I.e. What is the difference 
P(B wins) - P(A wins) for 100 flips? What about for n flips? Code it up.

Hint: As the number of flips increase, the advantage Bob has over Alice should decrease.
 
 https://stats.stackexchange.com/questions/643092/coin-flip-game-hh-vs-ht-in-a-sequence-of-flips


# Probability Brain Teasers

1. How many hershey kisses sold in USA last year?

Extrapolate starting from USA population: 330M. Now, we want to determine which subset
of the population would eat Hershey kisses, and which time periods of the year they would eat it.

- Population: Let's say people between ages 5-70 eat Hershey kisses because everyone else is too young or too old. This is maybe 80% of the population, so 0.8 * 330M = ~264M.

- Frequency: Let's say people eat Hershey kisses on average 1 time a week. This is 52 times a year. With double the amount during Halloween, Christmas, and Easter, we can say 52 + 3 * 52 = 208 times a year. 

Our final answer is somewhere around 208 * 264M, so more than 50B Hershey kisses sold in the USA last year.

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

## Jane Street Puzzles

1. Robot tug-of-war (https://www.janestreet.com/puzzles/robot-tug-of-war-index/)

Strategy: first calculate the probability of winning for first robot, which is a recursive function similar to heads/tails recursion.

Determine the probability of winning only up to 7 digits, as that would be the answer.


2. The 100 prisoners problem (https://www.janestreet.com/puzzles/100-prisoners-index/)

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

# Five Rings sample questions

How many pizzs sold in NYC every year?

How many coffee cups does the world dink in one day?

First round 1. Tenth root of 10 2. Log_{1.2}(3) 3. Water in a olympic pool 4. Weight of a baby elephant 5. Digits in 50 ! 6. Max slices of a pizza after 10 cuts Second round: 1. Roll 6 sided dice EV 2. Roll 2 6 sided dice, only get to roll the second one if you can't roll a sum over 10 (so first is 4 or lower). Find the EV 3. Now you can choose the number of sides, should the lower sided dice be rolled first or second 4. Find the optimal number of sides to maximize the EV Third Round: 1. Given a tournament of 8 teams, what's the probability that two teams will meet if they have .5 probability of advancing to the next round, assuming the matchups are randomly selected 2. Now there are 9 teams and every round one team is selected to advance at random at each level, what's the probability that the two teams will meet. Superday: Never made it this far

how much would you pay to enter a game (where you flip a coin, and get 5 dollars if it's a head, 0 dollar if it's a tail

Maximum number of régions you can devide a plane with 6 lines.

what is the expectation of the distance from X to the origin if X is uniformly drawn from the unit circle.

Deriving linear regression as a maximum likelihood estimator

Setting up calculus of variation for the brachistochrone curve problem

write linear interpolation from scratch, basic questions on lasso and ridge regression.

# Meta Interview Questions

Design a next-word prediction system for words that are being typed for instance.

# Tiktok Interview questions

Longest duplicated substring: need binary search + Rabin-Karp algorithm.

# Uber

1. Sort a list of numbers based on their squares. -> Two pointer approach in O(n)
2. Implement k-means algorithm from scratch
3. Implement library to compute eigenvalues of a 2x2 matrix and test it.
    - implement testing based on exact eigenvalues (e.g. diagonal matrices)
    - implement testing based on getting the corresponding eigenvectors and
        asserting that Av = \lambda v for \lambda eigenvalues and v eigenvectors.

System design:

1. Design recommendation system for Uber Eats.
- how to define inputs/outputs

# Virtu

Probability of making a basket in the next shot is the proportion of made baskets.
Initially, we make the first shot, and miss the second shot. What is the probability
that the score is even when we have shot 10 times?

Implement connect-four in Python from scratch. Simulation coding.

0. Which is more likely to have extreme values for the min? A mutually exclusive window of samples, or a sliding
window of samples?
-> The mutually exclusive window of samples are essentially sums of independent random variables, and thus
independent. The sliding window of samples are not independent, and thus the variance of the sum of the
sliding window of samples is higher.


1. Which is larger 99^100, or 100^99?
-> use contractive property of the log function

2. Number of digits in 100!?
-> use Stirling's approximation, or use the fact that the number of digits in a number
is given by \lfloor \log_{10} n \rfloor + 1.

3. Recursive probability questions with changing Geometric distribution to get all the possible cards.

4. How to sample in the uniform circle given a uniform sample in the unit square (X, Y)?
-> re-parametrize the circle in terms of the angle, and then sample the angle uniformly.
and then sample the radius in a manner that is proportional to the area of the circle.

# ART Advisors

Online Assessment questions:
1. Given an integer n > 0, implement method to find the closest fibonnaci number to n:
    - direct: O(log(n)) solution by iterating through fibonnaci numbers until we reach n or higher; keep track of f_n, f_n-1 and f_{n+1}
        until f_{n+1} > n. Then return the closest of f_n and f_{n+1}.
    - Binet formula: golden ratio phi = \frac{1 + \sqrt{5}}{2}, then f_n = \frac{\phi^n - (1 - \phi)^n}{\sqrt{5}}.
        We can use this formula to find the closest fibonnaci number to n.
        We can also invert and approximate the answer by recognizing that one term will go to 0 as n goes to infinity.

2. Given array of strings, each string has a nested string like "key1.key2.key3.key4=value", implement
a nested dict function that constructs and returns a nested Python dictionary form all the data items
in the data array argument.

build_nested_dict(['a.b=1', 'a.c=2']) will return {'a': {'b': 1, 'c': 2}}

3. Build a class to do Linear Interpolation, with __init__ and __call__ functions. It will
interpolate between two points (x1, y1) and (x2, y2) given a new x value.

The __init__(self, x, y) gets passed in data to be interpolated, and may or may not be sorted.
The __call__(self, x) function will return the interpolated value at x. If outside range, return np.nan

y_interpolated = y1 + (y2 - y1) * (x_new - x1) / (x2 - x1) = "mx + b".

- Do binary search to find x index O(log(n)) time complexity. Sort originally.
- Interpolate in O(1).

4. Consider the logistic map function f(x) = r * x * (1 - x), where r is a parameter, 0 < x < 1, and 0 <= r <= 4.
Implement a function to determine the smallest value of r at which chaos onsets to within 1% precision.
Assume n=100 iterations are suficient to determine chaos.

- Iterate through r values from 0 to 4, and for each r, iterate through x values from 0 to 1, and iterate through n iterations.
- estimate of lyapunov exponent: \sum_{i=1}^n \log |f'(x_i)| / n, where f'(x) = r - 2rx. We can monte carlo
estimate this value by averaging over many x_0 values within the range [0, 1].
- For each x value, we will monte carlo sample 100 instances to determine the lyapunov exponent andd whether 
or not it is positive.

1. If regression estimate of Y is highly sensitive to input X, then what's going on?
    - ill-conditioned matrix, multicollinearity, overfitting
    - solutions: regularization, applying PCA
    - how is PCA related to geometry of the solution?
        - projecting onto nullspace of the matrix, which is the direction of least variance

2. Bayes theorem question on probability of true positive when test is positive.

1. Given deck of unique cards, we play a game of: i) draw card, and ii) then put top card to bottom of deck, and then repeat until the entire deck is drawn.

Return the deck such that the cards are revealed in increasing order when they are drawn. For example:

Input: [3, 1, 2, 4]
Output: [1, 3, 2, 4]

2. What is the max rank of a matrix that A^2 = 0?

3. How to access `__property` in a Python class? Class mangling.


# Nvidia

1. Implement accumulate of elements in C++ using templates and iterators.
2. Implement function to compute einsum in Python.

# Genentech LLM ML Engineering

1. Coding: sequence to sequence transformation using valid sequences. Graph traversal.
2. Explain cross entropy loss
3. Explain difference between loss function and metrics: 
    - I needed to mention differentiability
4. Difference between 16 bit and 32 bit precision training in NVIDIA GPUs
5. Advantages of taking log after softmax?
6. Design a LLM RAG summary system.

# HRT

1. Return number of positive integers that are "fancy" with only 1's and 0's in its base-4 representation given a postivie integer n.
2. Simulate the Othello game.
3. Implement a function to construct a tree given a list of lists consisting of its keys, values
and optionally idx of its children nodes. The indices index into the list of lists. Then
print out the pre-order traversal.
4. Implement a function to merge trees using some criterion. Requires recursion.

# Amazon

1. What are the pros and cons of transformers vs LSTMs?
2. How does a transformer work?
3. Implement a function to return a list of all valid parentheses given "n" the number
of parentheses to use. Backtracking soln.

# Useful Review Links:
- Most helpful review, make sure you google/chat/read about each topic question and understand pros/cons/basic derivations/implementations https://huyenchip.com/ml-interviews-book/

- https://drive.google.com/drive/folders/1zxXNQKYrGk7fFnzaUb78VqVw-kv7Yy2B Stanford old midterms
- Stanford class notes: https://web.stanford.edu/class/cs109/
- Counting k balls in n boxes: https://tylerzhu.com/assets/handouts/ballsandboxes.pdf
- L1 regression solved in different ways: http://blog.omega-prime.co.uk/2020/04/01/l1-regression/


https://www.reddit.com/r/MachineLearning/comments/17u7b19/comment/k922w67/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button

Good luck with your interview

https://rentry.org/llm-training

Challenges and Applications of Large Language Models

https://github.com/bkitano/llama-from-scratch
https://github.com/rasbt/LLMs-from-scratch

https://github.com/mlabonne/llm-course

https://github.com/huggingface/alignment-handbook
https://huggingface.co/spaces/HuggingFaceFW/blogpost-fineweb-v1

https://www.philschmid.de/tags/generativeai

https://difficult-link-dd7.notion.site/Wei-Shen-s-LLM-Blog-dc1c32b03e0e4f84b368dbd09ee9479a

https://web.stanford.edu/class/cs224n/ and 224u, 224v

https://eugeneyan.com/writing/llm-patterns/ (many other good blogposts)

https://huyenchip.com/2023/04/11/llm-engineering.html

https://lilianweng.github.io

https://hamel.dev/notes/llm
https://github.com/underlines/awesome-ml/blob/master/llm-tools.md

RAG stuff(sentence embedding, vector db):
https://www.pinecone.io/learn/
https://www.sbert.net/
https://haystackconf.com/us2023/keynote/
https://www.latent.space/p/llamaindex#details