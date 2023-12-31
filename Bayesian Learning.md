---
next: 
previous: "[[Random Noise]]"
---
> [!info] Prerequisite
> Make sure you understand [[Glossary/Random Variables|Random Variables]], and [[glossary/Random Variables#bayes rule|Bayes rule]] in particular.


Previously, we talked about modelling noise in our data as a random variable. This is effective because there is some level of uncertainty in noise - we don't know what its value will be, more or less by definition. *Random variables and probability model uncertainty well.*

Well, what if there is some uncertainty in what model is best? Perhaps different values of $w$ or $\sigma^{2}$ are almost equally consistent with the data. A great example is when there are two clear trends within the data (the data is then known as multi-modal) - two different fits would perform almost equally well, but would give different predictions.

Bayesian methods can help us reason about different possible models in a way that captures this behaviour.

## combining models
Lets say that we create a bunch of different models. We ask each model to make a prediction for some $t_n$ based on some $x_n$.
$$
\sum_{a=1}^{A} q_{a f(X|w_{a})}
$$
where $q$ satisfies:
$$
\sum_{a=1}^{A}q_{a} = 1
$$
Intuitively, sampling more models should produce better results; so we can take this to the logical extreme. 
First, we make $w$ a random variable - this makes sense, since we are uncertain of the value of $w$. Now, we can integrate over all the possible values of $w$,. This lets us get an expected value for the 
$$
E\left\{ f(x, w) \right\} = \int f(x, w) p(w) \, dx 
$$