Title: Principle Component Analysis (PCA; Proper Orthogonal Decomposition)
Date: 2021-01-11
Category: Machine Learning
Tags: phd, machine learning
Slug: principle-component-analysis
Authors: Adam Li
Summary: An overview of principle component analysis.

# Background
When i.i.d. vector data is collected, then it is generally of interest to 
represent the data in as low-dimension as possible. 

Given $x_k \in \mathbb{R}^d \sim X$ for k=1,...,n data points (e.g. 
if data are images, then d is the number of pixels), one would like to
simultaneously i) discover interdependencies within the data and ii) reduce dimensions. 
It is important to note here that the data is **sampled** from a distribution and so 
any downstream statistics (e.g. covariance) are **estimates** of the true 
underlying statistic.

Mathematically, this problem can be represented in many ways:

1. Minimizing Cost functions

    On the one hand we would like to find a lower-dimensional representation of our data, $x_k$. 
    We would like to find the minimization of the following cost function

    $$\argmin_P E[ x - Px ]^2$$

    where P is a projection operator of rank r. P takes the data points $x_k$ 
    and maps them from dimension d to r << d.

2. Maximizing Cost Functions
    
    On the other hand, we can view PCA as a method for maximizing the variance 
    observed in the data, subject to a constraint. If we stack our data samples, $x_k$ 
    column-by-column in a data matrix, X, we seek a linear combination of the columns 
    that give us the **maximal variance**. $Var(Xa) = a^T Var(X) a$, where a is a 
    vector of constants to provide linear combinations of X, and $Var(X)$ is the 
    covariance matrix of our data.
   
    In addition, we impose a constraint on the vector, a, such that it has unit norm. 
    Thus using the theory of Lagrange multipliers, we can write this as a 
    constrained optimization problem.
   
    $$\argmax_a a^T Var(X) a - \lambda(a^T a - 1)$$

    When differentiating with respect to a, and solving the equations, one 
    gets the analytical expression:
   
    $$Var(X) a = \lambda a$$

    which is simply an eigenvalue equation, where $\lambda$ is an eigenvalue of 
    Var(X) and a is an eigenvector. 

# Standard PCA and Algorithm
Standard PCA is commonly implemented in [sklearn](https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.PCA.html)
where the algorithm relies on the Singular Value Decomposition (SVD). Generally, 
it uses the ``LAPACK`` implementation, which supports full, truncated and randomized SVD. 
Conceptually the algorithm proceeds in 4 steps.

1. Standardization of variable scaling
    
    This step attempts to put all dimensions of the data in the same scale. 
    In the downstream step of the SVD, for variables that have a significantly larger 
    amplitude then other variables, then the variability in those variables will dominate. 
   
    Common standardizations include the z-scoring method:

    $$x_{k_i} = \frac{x_{k_i} - \mu(x_k)}{\sigma(x_k)}$$

2. Estimate covariance matrix

    The next step will compute the covariance matrix of the data. 
    If there are n samples of a d-dimensional data, then the covariance 
    matrix will be $d \times d$.

3. Matrix decomposition (SVD/EVD)

    Since the covariance matrix is a positive semi-definite (symmetric and 
    non-negative quadratic form), then its singular values are equivalent to 
    its eigenvalues. The singular/eigen vectors 
    of the covariance matrix are ordered by the values of the singular/eigen values.
   
4. Computing Principle Components
   
    The principle components of the data are obtained by multiplying the data 
    with the singular vector matrix. For example, the first 5 principle components corresponding to the 
    5 largest singular values can be used to obtain a 5-dimensional representation 
    of the original d-dimensional dataset. We simply take the $d \times 5$ truncated matrix 
    and multiply it with our data to obtain n samples now of a 5-dimensional data.

# Statistical Considerations
## Independence
If random variables are independent, then they have 0 correlation. Independence is a stronger 
assumption then non-correlated. Most of the times, independence is not fully realized; it is 
just a necessary assumption for mathematical modeling. However, when random variables are not necessarily independent, it is not necessary that 
they have non-zero correlation. In fact, they may have high correlation. 

When performing PCA on correlated data, most likely there will be a few principle components
in the data that are captured.

## Centering
When computing the principle components, it is in general common practice to 
center the columns of the data matrix first. 

Geometrically this centers all data points around the origin. PCA attempts at finding 
an orthogonal rotation to represent the data; note that this rotation occurs 
about the origin!

If the mean is not subtracted, then essentially the first principle component ends up being 
the mean vector of the data points, since rotating that mean would result in higher 
mean-squared error.

## Compressed Sensing (n < d) - "Robust PCA"
When dealing with high-dimension data with high-dimensional noise, PCA 
may become sensitive to outliers within the dataset. To combat this, 
we can instead model PCA as a convex optimization problem with the cost function

$$\min_{L,S} ||L||_* + \lambda ||S||_1$$

such that $X = L + S$, where L is a low-rank component and S is a sparse component.
This minimizes the sum of the singular values for the matrix L and the l1-norm of the
matrix S. The sparse matrix is associated with noise.

## Huge Dimensionality (n >> 1, d >> 1)
When you have a large number of samples with extremely high dimensions, the computational 
workhouse - SVD - becomes computationally expensive. Rather then take a full SVD, 
it has been shown that taking randomized SVD can capture the principle components of the data.

The randomized SVD approach essentially says that:

- choose a random unitary projection matrix ($d \times r$)
- multiply that with your data matrix and apply PCA
- the principle components of that data matrix has **high probability** of aligning 
with the principle components of the original large data matrix
  
Note: The important point here is that the unitary projection matrix must 
be chosen at random. Good choices are listed in [sklearn](https://scikit-learn.org/stable/modules/random_projection.html).

# Questions to Test Understanding
1. Given eigenvalues of the covariance matrix, what is one way to measure *variance explained* proportion for each component?

    Take the eigenvalues and sort them, then for each eigenvalue, divide it by the trace of the covariance matrix. This 
    results in a ratio between the corresponding jth eigenvalue and the total sum of all the eigenvalues, which gives 
    the proportion of variance explained in the principle components.

2. By performing z-score standardization of the data matrix, the covariance matrix of the data is now equivalent to the correlation matrix?

    By performing z-score standardization, the columns of the data matrix now all have sample variance equal to 1. Thus, the 
    correlation is defined as:
   
    $$\rho_{X, Y} = \frac{Cov(X, Y)}{\sigma_X \sigma_Y}$$
    
    which is equivalent to the covariance when the sample variances are unitary.

3. 

# References:
1. Jolliffe IT, Cadima J. (2016). Principal component analysis: a review and recent developments.Phil. Trans. R. Soc. A 374:20150202. http://dx.doi.org/10.1098/rsta.2015.0202