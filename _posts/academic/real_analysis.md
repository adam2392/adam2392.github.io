Title: Real Analysis (Lebesgue Integration, Differentiation and Measure)
Date: 2020-12-24
Category: Academic
Tags: math, phd, real-analysis
Slug: real-analysis
Authors: Adam Li
Summary: A short summary of important concepts in Real Analysis

# Summary
Real analysis is the study of real numbers in $\mathbb{R}^d$, with 
``d`` being the dimensionality. Although it is a pretty abstract topic 
that does not seem to have applications, it is a very fundamental 
in understanding other branches of applied mathematics. For example, in order
to define optimization algorithms, one is very interested in the ideas of convergence.
One then often uses theory of continuity. In computational neuroscience and 
control theory, one often deals with integrals when defining theory. In 
statistics, it is absolutely necessary to understand integrals (expectation 
is defined with an integral).

In this blog post, I'll review some of the basic concepts that one
needs to know in general. A great course sequence I took was both at UCSD with 
Professor Dragos Oprea (Math 140AB) and with Professor Sogge (Math 605) at Johns Hopkins.

Excellent references are:
- [Stein, E. M., Stein, E. M., & Shakarchi, R. (2005). Princeton lectures in analysis: 3. Princeton: Princeton Univ. Press.](http://www.cmat.edu.uy/~mordecki/courses/medida2013/book.pdf)

# Measurability
Measure is an abstract notion of "volume" of a set. In all "regular" 
examples, one can assume the sets in consideration are measurable. However,
using the [Axiom of Choice](https://en.wikipedia.org/wiki/Axiom_of_choice), one
can construct "unmeasurable" sets. This motivates the need to define Borel sets (sigma-algebras)
in probability theory, which denote measurable family of subsets of a set. This 
is beyond the scope of this post though. It suffices to know that unmeasurable 
sets ``do exist``.

Measure from first principles is defined in Stein starting from outer-measure. 
Outer-measure is simply the measure obtained by covering a set with a countable 
almost-disjoint union of rectangles (circles, squares also suffice). Outer-measure
is well-defined for any possible set. Lebesgue measure then is defined by 
the infimum over the possible outer-measures of a set.

Some important properties of measure of a set is non-negativity and 
countable sub-additivity. Countable additivity is obtained when 
they are pairwise disjoint sets in consideration.

# Convergence
For many interesting functions, and numbers, we are interested in 
the notion of convergence. That is, if we define a sequence enumerated 
by ``n`` of numbers, or functions using some rule that depends on ``n``, 
then what are conditions that these sequences converge? Generally, 
if a sequence does not converge, then it goes to $\infty$.

In real analysis, we generally consider the Euclidean metric space. 
In fact, these metric spaces are complete (i.e. all Cauchy sequences converge
inside the metric space).

## Important Integral Convergence Theorems
When defining convergence for integrals, there are three fundamental results 
that are useful:

- [Fatou's lemma](https://www.math3ma.com/blog/fatous-lemma)
- [Monotone convergence theorem](https://www.math3ma.com/blog/monotone-convergence-theorem)
- [Dominated convergence theorem](https://www.math3ma.com/blog/dominated-convergence-theorem)

I won't talk about them here because the above links actually provide 
a very nice reference (that is also accessible to beginners).

## Bolzano-Weirstrass Theorem For Sequences of Real Numbers
The main way of proving convergence relies on showing that a sequence 
is Cauchy. That is for every $\epsilon > 0$, we have:

$$|x_m - x_n| < \epsilon$$

for $m, n \ge N$, for some large number $N_\epsilon$. The "|...|" sign 
denotes the distance metric defined. This implies that even if 
the sequence $\{x_k\}$ potentially oscillates, the range of its oscillation
is decreasing as you take values further and further down the sequence.
Note that by construction any sequence that is Cauchy in a metric space 
is in fact ``bounded``.

The [Bolzano-Weirstrass theorem, or sequential compactness theorem](https://en.wikipedia.org/wiki/Bolzano%E2%80%93Weierstrass_theorem) 
states that any bounded sequence in finite-dimensional Euclidean space has 
a convergent subsequence. Then a sequence is convergent if and only if 
it has a convergent subsequence, and so every Cauchy sequence is convergent.

## Convergence In Norm
Note that convergence of a sequence of real numbers requires a specific 
component to emerge. In the space of integrable functions, $L^1(\mathbb{R}^d)$, 
one can define ``convergence in norm``. That is the sequence defined might not 
converge exactly element by element to a fixed component, but their difference in norm
converges. That is for every $\epsilon > 0$, and $\{f_k\} \in L^1$, we have:

$$||f_m(x) - f_n(x)||_{L^1} < \epsilon$$

where the distance metric is now defined as $||.||_{L^1} = \int_{\mathbb{R}^d} |f_m(x) - f_n(x)| dx$. 
Convergence in norm can then be extended in general to $L^p$ spaces, since 
$L^1 \supset L^2 \supset ... \supset L^\infty$, which follows from Holder's 
inequality.

## Other Convergences
Note that there are other notions of convergences as well! 
Weak convergence, strong convergence, etc.

# Integrability
Integration with respect to Lebesgue measure is defined by considering the 
convergence of the integral of the absolute value of the function:

$$\int |f(x)| dx < \infty$$

else, the function f is said to be not integrable. The space of 
Lebesgue integrable functions if formally known as the "L1" space. 
Note that by the Risz-Fisher theorem, we know that $L^p$ spaces for 
$1 \le p \le \infty$ is complete. 

# Differentiation
When considering differentiation in the context of integration, 
we are primarily interested in when the Fundamental Theorems of Calculus hold
in the Lebesgue measure theory. We learned in high school calculus the following:

## First Fundamental Theorem of Calculus:
If $F(x) = \int_a^x f(t) dt$ for $x \in [a, b]$ interval, then

$$F'(x) = f(x)$$

that is, we can reverse integration on f by taking the derivative of F.
This theorem holds in the space of Lebesgue integrable functions, when the 
function is ``locally integrable`` (i.e. Lebesgue's differentiation theorem).

## Second Fundamental Theorem of Calculus
The second part states that if we take the endpoints of the antiderivative, 
then we can obtain the integral of the function over those endpoints:

$$F(b) - F(a) = \int_a^b f(t) dt$$

The result holds when F is ``absolutely continuous``, which is a stronger 
notion then continuity. It essentially bounds the degree of variation and is 
actually introduced through the concept of Bounded Variation.

# Other Important Topics
This blog post is meant to be brief, but in the future, I'll probably 
try to cover Hilbert spaces (linear operators, orthogonality, compact operators, 
the Spectral Theorem, and Kernel integral operators), Fourier series and the Fourier transform, which are also 
broadly applicable across applied mathematics and engineering.