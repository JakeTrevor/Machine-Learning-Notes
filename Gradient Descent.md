
# Gradients
Lets say we have some function $f$ on some set of values $w_{1}, w_{2}, \dots w_{n}$. 
Then its gradient ($\nabla f$) is given by:
$$
\nabla f = \begin{pmatrix}
\frac{ \partial f }{ \partial w_{1} }  \\
\frac{ \partial f }{ \partial w_{2} }  \\
\dots \\
\frac{ \partial f }{ \partial w_{n} } 
\end{pmatrix}
$$
> [!info] notice: 
> $f$ is a function that operates on a list (or a vector) of values, so its gradient is also a list (or a vector) of values.

The gradient of $f$ points in the direction of steepest ascent. and therefore, the opposite direction is direction of steepest descent.

## Gradient Descent

The idea of gradient descent is to descend the curve as quickly as possible, hopefully moving towards its minimum.

Gradient descent isn't an exact, analytical solution. It's imprecise and iterative. Ideally, each iteration of gradient descent will get you closer and closer to the exact solution, even if you never actually reach it.

One iteration or 'pass' of gradient descent looks like this:
$$
w = w - \alpha \nabla f
$$


```pa
w = [1, 3, /* ... */]
alpha = 0.01 // learning rate
while notConverged {
		for i in [0 to w.length] {
			g = (d Loss(w)/ d w[i])
			w[i] = w[i] - alpha * g
		}
}
```
