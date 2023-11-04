$$
\DeclareMathOperator*{\argmin}{argmin}
\DeclareMathOperator*{\argmax}{argmax}
$$If we have a model $t_{n}=f(x_{n}| w)$ there is a degree of uncertainty in $t$; we expect noise to be present. We can formalise this notion by saying that $t_{n}$ follows a random variable - which is a mathematical way to describe uncertainty.

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
L = p(T=t_{1},  \dots T=t_{n}| w, \sigma^{2}, x_{1}\dots x_{n}) = \prod_{n=1}^N p(T=t_{n}|w,\sigma^{2}, x_{n})
$$
We call this the likelihood of the model and its written as $L$. Now, our regression optimisation looks like this:
$$
\begin{align}
\argmax_{w, \sigma^{2}} L = \argmax_{w, \sigma^{2}} \left\{ \prod_{n=1}^N p(T=t_{n}|w,\sigma^{2}, x_{n})\right\}
\end{align}
$$
We can optimise this computation by computing the log likelihood instead; recall:
$$
\begin{align}
x \uparrow  \log x \uparrow\\
x \downarrow  \log x \downarrow
\end{align}
$$
So when $x$ is at a maximum, then so is $\log x$. This gives us:
$$
\begin{align}
\argmax_{w, \sigma^{2}} \ \log L = \argmax_{w, \sigma^{2}} \left\{ \log\prod_{n=1}^N p(T=t_{n}|w,\sigma^{2}, x_{n})\right\}
\end{align}
$$
