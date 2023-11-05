---
next: "[[Bayesian Learning]]"
previous: "[[Validation]]"
---
$$
\DeclareMathOperator*{\argmin}{argmin}
\DeclareMathOperator*{\argmax}{argmax}
$$
> [!info] Prerequisite
> To understand this chapter, its a good idea to make sure you understand [[Glossary/Random Variables|Random Variables]].

If we have a model $t_{n}=f(x_{n}| w)$ there is a degree of uncertainty in $t$; we expect noise to be present. We can formalise this notion by saying that $t_{n}$ follows a random variable - which is a mathematical way to describe uncertainty.

To do this, we create a model that encodes our uncertainty:
$$
t_{n} = f(x_{n}|w) + \epsilon
$$
Where $\epsilon$ is a random variable describing the noise:
$$
\epsilon \sim \mathcal{N}(0, \sigma^{2})
$$
This propagates to $t$; It's now a gaussian random variable, so that we can say it follows a distribution $T$:
$$
T \sim \mathcal{N}(f(x|w), \sigma^{2})
$$
$T$ is described by the probability density:
$$
p(T=t_{n} |w, x_{n}, \sigma^{2}) = \frac{1}{\sigma \sqrt{ 2\pi}}\exp\left\{ -\frac{1}{2\sigma^{2}} (t-f(x|w)) \right\}
$$
The density of $T$ at some point $t_n$ is called the **likelihood** of $t_n$. Now, instead of minimising the loss, we are going to try and maximise the likelihood of our data.

We want to do this not just for a single point $x_n, t_n$, but for all the data in our model. To do this, we need to compute the joint likelihood of all our data points, which we can do like this:
$$
L = p(T_{1}=t_{1},  \dots T_{n}=t_{n}| w, \sigma^{2}, x_{1}\dots x_{n}) = \prod_{n=1}^N p(T_{n}=t_{n}|w,\sigma^{2}, x_{n})
$$
We call this the likelihood of the model and its written as $L$. Now, our regression optimisation looks like this:
$$
\begin{align}
\argmax_{w, \sigma^{2}} L = \argmax_{w, \sigma^{2}} \left\{ \prod_{n=1}^N p(T_{n}=t_{n}|w,\sigma^{2}, x_{n})\right\}
\end{align}
$$
This is actually quite hard because of the $\exp$ operation in there. But we can make it easier optimising the log likelihood instead. recall:
$$
\begin{align}
x \uparrow  \log x \uparrow\\
x \downarrow  \log x \downarrow
\end{align}
$$
So when $x$ is at a maximum, then so is $\log x$. This allows us to safely optimise the log instead, which gets rid of the inconvenient $\exp$. This gives us the epxression:
$$
\begin{align}
\argmax_{w, \sigma^{2}} \ \log L = \argmax_{w, \sigma^{2}} \left\{ \log\prod_{n=1}^N p(T=t_{n}|w,\sigma^{2}, x_{n})\right\}
\end{align}
$$
Writing this out in full we get:
$$
\argmax_{w, \sigma^{2}} \left\{ \log \prod_{n=1}^{N} \frac{1}{\sigma \sqrt{ 2\pi}}\exp\left\{ -\frac{1}{2\sigma^{2}} (t-f(x|w)) \right\} \right\}
$$
$$
\begin{align}
\log L  \\
 & = \log \prod_{n=1}^{N}\left( \frac{1}{\sigma \sqrt{ 2\pi}}\exp\left\{ -\frac{1}{2\sigma^{2}} (t_{n}-f(x_{n}|w))^{2} \right\} \right) \\ \\
& = \sum_{n=1}^{N} \log \left( \frac{1}{\sigma \sqrt{ 2\pi}}\exp\left\{ -\frac{1}{2\sigma^{2}} (t_{n}-f(x_{n}|w))^{2} \right\} \right) \\
 & = \sum_{n=1}^{N}\log \frac{1}{\sigma \sqrt{ 2\pi}} + \sum_{n=1}^{N}\cancel{\log\exp}\left\{ -\frac{1}{2\sigma^{2}} (t_{n}-f(x_{n}|w))^{2} \right\}  \\
 & = -N \log \left(\sigma \sqrt{ 2\pi} \right)+ \sum_{n=1}^{N } -\frac{1}{2\sigma^{2}} (t_{n}-f(x_{n}|w))^{2}  \\
& = -N \log \left(\sigma \sqrt{ 2\pi} \right) -\frac{1}{2\sigma^{2}}\sum_{n=1}^{N } (t_{n}-f(x_{n}|w))^{2} 
\end{align}
$$
The same value of $\hat{w}$ works as before:
$$
\hat{w} = (X^\top X)^{-1} X^\top t
$$
We also get a new equation for $\hat{\sigma^{2}}$:
$$
\hat{\sigma^{2}} = \frac{1}{N}(t-X\hat{w})^\top (t-X\hat{w})
$$

## likelihood not loss
You should note that when we use this formalism, we don't compute loss - likelihood replaces it. the higher the likelihood of the model the more likely it is - and therefore, the better the model fits the data.

You use this idea to help with choosing a model function too - instead of using validation loss, use validation likelihood. All the same ideas apply.

How do we use a model like this? This produces a distribution, so its not really good at producing exact, direct predictions. Instead, you can ask what range a value is likely to fall into. This is outside the scope of the course, but for instance you can ask what range 95% of values fall into, and use that to set bounds on a prediction - or you can use it to give you some notion of 'confidence' in a prediction without the noise.


