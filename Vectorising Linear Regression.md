---
next: "[[Validation]]"
previous: "[[Regression]]"
---
Earlier I said that $w$ represents a collection of parameters to the model. We can represent this mathematically as a vector:

$$
\vec{w} = \begin{bmatrix}
w_{0} \\
w_{1} \\
\end{bmatrix}
$$
I've marked it here as $\vec{w}$ to make it clear that it is a vector.

Doing this, its logical to try and also represent our $x_{n}$ as a vector so we can represent the whole model as a vector calculation. To do this, we need to get $x_{n}$ into a vector form that multiplies with $\vec{w}$ correctly. For a linear model with $t=w_{0}+w_{1}x$, this gives us the vector:

$$
\vec{x}_{n} = \begin{bmatrix}
1 \\
x_{n} \\
\end{bmatrix}
$$
This is called a design vector, because it controls the 'design' (i.e. the underlying function) of our model. Our model can then be written:
$$
t_{n} = \vec{x}_{n}^\top \vec{w}
$$
What if we wanted to compute all of our values of $t$ at once? We can combine our values for $t_{n}$ into a single large vector, called $t$:
$$
t=\begin{bmatrix}
t_{1} \\
t_{2} \\
\vdots \\
t_{n}
\end{bmatrix}
$$
Our vector $\vec{w}$ is fine, but our $\vec{x}$ needs to be changed - although not by much! Just like with $T$, we just stack up all our design vectors to get a single **design matrix** - we'll call it $X$:

$$
X = \begin{bmatrix}
1 & x_{1} \\
	1  & x_{2} \\
\vdots & \vdots\\
1 & x_{n}
\end{bmatrix}
$$
Note that we transposed $\vec{x}$ so that we can now write our whole model:
$$
t = X\vec{w}
$$
## Vectorised loss
We'd also like to vectorise our loss; Recall that it looks like;

$$
\mathcal{L} = \frac{1}{N}\sum_{n=1}^N (t_{n} - w_{0}-w_{1}x_{n})
$$
We can re-write this a bit with our vectorized form for $t_{n}$:
$$
\mathcal{L} = \frac{1}{N}\sum_{n=1}^N (t_{n} - \vec{x}^\top w)^{2}
$$

> [!info] A nice mathematical fact:
> Let $q_{n}$ be a row in matrix $Q$ with $D$ rows.
> $$\sum_{n=1}^D(q_{n})^{2} = Q^\top Q$$


In our expression for loss,  it looks like we have a row in the following matrix:
$$
(t_{n} - \vec{x}^\top w) \in t - X\vec{w}
$$
This allows us to re-write loss in a nice vector form:
$$
\mathcal{L} = \frac{1}{N} (t-X\vec{w})^\top (t-X\vec{w})
$$

## Minimising loss:

Remember, we want to minimise the loss to get the optimal value. This in general fulfils the equation:
$$
\frac{ \partial \mathcal{L} }{ \partial w }  = \nabla_{w}\mathcal{L} = 0
$$

Through the power of *don't worry about it* and *maths*, we can find optimal $w$:
$$
\hat{w}=(X^\top X)^{-1} X^\top t
$$
Don't worry about deriving this; its outside the scope of the course. If you're interested, there's a derivation [[Vectorising Linear Algebra - Derivation of w|here]].


## More advanced regression
I worked through this example with simple linear regression, but this formula for loss works on anything you can put into your design matrix.

You can choose to stick simply to polynomial models; for a polynomial in $x^n$, we have $\vec{w}$ and $X$ in the forms:
$$
\begin{align}
\vec{w}=\begin{bmatrix}
w_{0} \\
w_{1} \\
\vdots \\
w_{n}
\end{bmatrix}
 &  &  X = \begin{bmatrix}
1, &x^1_{1}, & \dots, & x^n_{1} \\
1, &x^1_{2}, & \dots, & x^n_{2} \\
\vdots  & \vdots  & \ddots & \vdots\\
1, &x^1_{n}, & \dots, & x^n_{n} \\
\end{bmatrix}
\end{align}
$$
But actually, we can generalise this even further. We can choose arbitrary functions on $x$ to put into our design matrix:
$$
X = \begin{bmatrix}
h_{0}(x_{1}), &h_{1}(x_{1}), & \dots, & h_{n}(x_{1}) \\
h_{0}(x_{2}), &h_{1}(x_{2}), & \dots, & h_{n}(x_{2}) \\
\vdots  & \vdots  & \ddots & \vdots\\
h_{0}(x_{n}), &h_{1}(x_{n}), & \dots, & h_{n}(x_{n}) \\
\end{bmatrix}
$$
These functions $h$ on $x$ are called the **basis functions** of our design matrix.

You might notice a critical limitation of this representation of regression: we cannot optimise any parameters within a basis function $h$. We can only scale its contribution. In mathematical terms, we say that this the model optimises a **linear combination** of the basis functions.

Essentially, those parameters become design decisions, much like choosing which functions to include.



my model is a linear combination of the features in the design matrix.