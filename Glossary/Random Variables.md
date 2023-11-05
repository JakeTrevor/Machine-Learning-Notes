A Random variable is a mathematical description of an uncertain value; for example, if I flip a coin, and we assign $X$ to be the result - either `heads` or `tails` - then $X$ is a random variable.

With a random variable, we don't know the true value, but we do know the possible values and their associated probabilities.

Random variables are written with capital letters (e.g. $X, Y$); we use lower case letters to represent the values they take on (e.g. $x, y$).


# Discrete variables

Discrete variables take on a value from a finite, countable set. They are defined by the probabilities of different events taking place.
the probability of $X$ taking on the value $x$ for example is given by:
$$
P(X=x)
$$
The probabilities are constrained with the following:
$$
\begin{align}
0\leq P(Y=y)\leq 1 & & & \sum_{y}P(Y=y) = 1
\end{align}
$$
> All probabilities are in the range 0 - 1 and the sum of all probabilities is equal to 1.

# Continuous variables
Continuous variables come from a set with an uncountable number of values - you can't list out all the possible values. Take height - I can be 2 meters tall, but also 2.1m, 2.11m, 2.111m, and so on into infinite precision.

Instead of defining the probabilities of individual events, we define a density function, called $p(x)$. $p(x)$ tells us how likely different values are, but the value of $p(x)$ at a particular points is not a probability. It doesn't really make sense to ask about the probability of an individual value, since there are infinitely many of them and the probability of one in particular will always be 0.

Instead, we think about the probability of the value falling within a range. We compute this by taking the integral of the density function. For example:
$$
P(6\leq x\leq 8) = \int _{x=6}^{x=8} p(x)\, dx 
$$
Similar constraints also apply here, but they have to be reformulated for this new description: 
$$
\begin{align}
p(x) \geq 0&&\int _{-\infty}^{\infty}p(x) \, dx =1
\end{align}
$$

## Gaussian Random Variables
Gaussian random variables are a very common type of continuous random variable. If some $\epsilon$ is a gaussian random variable, we write:
$$
\epsilon \sim \mathcal{N}(\mu, \sigma^{2})
$$
The $\mathcal{N}$ here comes from the other name - the variable follows a **normal distribution** - values are most likely in the middle, and become less likely the further out you go.

The distribution is defined by two parameters; the mean $\mu$, and the variance $\sigma^{2}$. the mean tells you where the centre of the distribution is, and the variance tells you how  wide or 'stretched out' the distribution is.

The density function for Gaussian random variables looks like so:
$$
p(x) =\frac{1}{\sigma \sqrt{ 2\pi }} \exp \left\{ -\frac{1}{2\sigma^{2}} (x-\mu)^{2} \right\}
$$

# Joint probabilities

How do we describe two events coinciding? lets say $X$ takes on $x$ and $Y$ takes on $y$. We write this as:
$$
P(X=x, Y=y)
$$
This is called the joint probability of X and Y. For continuous variables, this idea also logically extends to create joint densities, which we write like this:
$$
p(x, y)
$$
## Independence
Much of the time $X$ and $Y$ are unrelated - take for example weather or not its raining currently and weather I had porridge for breakfast. These two things are **independent**. The value of one does not impact the value of the other.

In this case, the joint probability is found by simply multiplying together the probabilities of the individual events:
$$
\begin{align}
P(X=x, Y=y) = P(X=x)\cdot P(Y=y) \\
\text{If $X$ and $Y$ are independent}
\end{align}
$$

## Dependence
However, often the value of $X$ does have some impact on the value of $Y$. For example, weather or not its raining, and weather I'm using an umbrella. In this case, $X$ and $Y$ are **dependent** and we need to use a different set of rules to compute joint probability.

Instead of joint probabilities, we think in terms of conditional probabilities - The probability of some $x$ given some $y$. We write this as:
$$
P(X=x | Y=y)
$$
You read the vertical bar here as 'given'. You can take this and synthesize the joint probability from it:
$$
P(X=x, Y=y) = P(X=x|Y=y)\cdot P(Y=y)
$$
Pause for a moment and consider this - It's very natural. first we ask 'If $Y=y$, how likely is $X=x$?' Then we say 'How likely is $Y=y$?'. Combining these, its clear that you should get the probability of both.

Note also that this rule actually applies for independent variables too. With independent variables, we simply assume that the probability of $x$ is unaffected by $y$; in other words:
$$
\begin{align}
\text{If $X$ and $Y$ are independent:}\\
P(X=x | Y=y) = P(X=x)
\end{align}
$$

## Bayes rule
The conditional probability definitions above also lets us derive an extremely important rule for probability. Consider - we can decompose the joint probability in two ways - conditional on $X$ and conditional on $Y$:
$$
\begin{align}
P(X=x, Y=y)  \\
 & = P(X=x|Y=y)\cdot P(Y=y) \\
 & = P(Y=y|X=x)\cdot P(X=x)
\end{align}
$$
We can then use algebra to rearrange this as we wish:
$$
\begin{align}
P(X=x|Y=y)\cdot P(Y=y)  = P(Y=y|X=x)\cdot P(X=x) \\ \\
P(X=x|Y=y)  = \frac{P(Y=y|X=x)\cdot P(X=x)}{P(Y=y)}
\end{align}
$$
This is a bit noisy, so you will often see it written without the equals signs:
$$
P(x|y) = \frac{P(y|x)\cdot P(x)}{p(y)}
$$
This is called bayes rule, and it lets us construct a conditional probability. We will use it a lot later.