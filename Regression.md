---
next: "[[Vectorising Linear Regression]]"
---

$$
\DeclareMathOperator*{\argmin}{argmin}
\DeclareMathOperator*{\argmax}{argmax}
$$
>[!info] Regression:
> Learning a continuous function from a set of known data points

Let's say that we have some data that comes in pairs of values ($x_{n}, t_{n}$). In regression, we assume it takes the form:
$$
t_{n} = f(x_{n} | w)
$$
Where $f$ is a continuous function, and $w$ is a collection of parameters to that function. $f$ and $w$ together form our model.

## Loss ($\mathcal{L}$)
We want a way of assessing how good our model is. To do we find the difference between the prediction of the model at some point $n$ and the true value:
$$
\mathcal{l}_{n} = t_{n} - f(x_{n}|w)
$$
This is called the loss. We want this value to be a measure of 'wrongness' - it should be positive if the prediction is either more or less than the true value. We can accomplish by just squaring the loss:
$$
\mathcal{L}_{n} = (t_{n} - f(x_{n}|w))^{2}
$$
Finally, we want to know how our model performs as a whole across all our data; so we take the mean of the loss:
$$
\mathcal{L} = \frac{1}{N}\sum_{n=1}^N (t_{n} - f(x_{n}|w))^{2}
$$
This is called the mean squared loss (often we just shorten it to 'loss'). This gives us a measure of how good the model is - the higher the loss, the worse the model.

## Optimising a model

We want to get the best model we can. Lets ignore how we would choose $f$ for now and focus only on $w$. We want to minimise the loss with respect to $w$. This is the principal question at the heart of regression, and it takes the form:

> [!tip] &nbsp; 
>  *Find the parameters $w$ to the model that minimises the loss*
> $$\argmin_{w}\ \mathcal{L} \left(w | x, t\right)$$

There are several ways to go about doing this. Often, its possible to find a perfect analytical solution; Checkout [[Linear Regression - Analytical Solution]] for a worked example.

However analytical solutions don't work in all cases - or they may be intractable. So we use imprecise-but-good-enough heuristic methods. The most famous is [[Gradient Descent]].
