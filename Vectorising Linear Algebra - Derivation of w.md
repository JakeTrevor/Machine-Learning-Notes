### Fist, some rules:
$$
\begin{align} \\
(1) &  & (\vec{a}+\vec{b})^\top &= \vec{a}^\top + \vec{b}^\top &  & \text{sum associativity} \\
(2) &  & \left(\vec{a} * \vec{b}\right)^\top &= \vec{b}^\top * \vec{a}^\top &  & \text{product associativity} \\  &  &  &  &  & \text{note that the order reverses}\\
(3) &  & \frac{ \partial  }{ \partial x } \vec{x}^\top a &= a \\ \\
(4) &  & \frac{ \partial  }{ \partial x } a\vec{x} &= a^\top \\ \\
(5) &  & \frac{ \partial  }{ \partial x } \vec{x}^\top\vec{x} &= 2\vec{x} \\ \\
(6) &  & \frac{ \partial  }{ \partial x } \vec{x}^\top a \vec{x} &= 2a\vec{x} \\ \\
\end{align}
$$
First, We need to expand the expression for loss into something we can work with:
$$
\begin{align}
\mathcal{L}

 & = \frac{1}{N} (T-X\vec{w})^\top (T-X\vec{w}) \\


 & = \frac{1}{N} (T^\top-(X\vec{w})^\top) (T-X\vec{w})  & \text{by (1)}\\


 & = \frac{1}{N} (T^\top-\vec{w}^\top X^\top) (T-X\vec{w})  & \text{by (2)}\\


 & = \frac{1}{N} \left( T^\top T - \vec{w}^\top X^\top T - T^\top X\vec{w} + \vec{w}^\top X^\top X\vec{w} \right) 
 
\end{align}
$$
Next, we need the derivative $\frac{ \partial \mathcal{L} }{ \partial \vec{w} }$
$$
\begin{align}
\frac{ \partial \mathcal{L} }{ \partial \vec{w} }  

 & =\frac{ \partial}{ \partial \vec{w} }  \frac{1}{N} \left( T^\top T - \vec{w}^\top X^\top T - T^\top X\vec{w} + \vec{w}^\top X^\top X\vec{w} \right) \\

 & = \frac{1}{N} \frac{ \partial }{ \partial \vec{w} } \left( T^\top T - \vec{w}^\top X^\top T - T^\top X\vec{w} + \vec{w}^\top X^\top X\vec{w} \right) \\
\end{align}
$$
Note that there are four terms added together. We can differentiate these separately:
$$
\begin{align}
\frac{ \partial  }{ \partial \vec{w} } (T^\top T) & = 0 \\
\frac{ \partial  }{ \partial \vec{w} } \left( -\vec{w}^\top X^\top T \right)  & = -X^\top T \\
\frac{ \partial  }{ \partial \vec{w} } (-T^\top X \vec{w}) &= (-T^\top X)^\top \\&= -X^\top T \\
\frac{ \partial  }{ \partial \vec{w} } \left( \vec{w}^\top X^\top X\vec{w} \right)  & = 2 X^\top X \vec{w}
\end{align}
$$
And then add the terms back together, so we get:
$$
\begin{align}
\frac{ \partial \mathcal{L} }{ \partial \vec{w} } 
&= \frac{1}{N}  \left( 0 - X^\top T   - X^\top T + 2X^\top X\vec{w} \right)\\
&= \frac{1}{N}  \left( 2X^\top X\vec{w} -2 X^\top T \right)\\
&= \frac{2}{N}  \left( X^\top X\vec{w} - X^\top T \right)\\
\end{align}
$$
### Finally, some simple algebra to solve:

$$
\begin{align}
\frac{ \partial \mathcal{L} }{ \partial \vec{w} }  & = 0 \\
\frac{2}{N}  \left( X^\top X\vec{w} - X^\top T \right)  & = 0\\
X^\top X\vec{w} - X^\top T  & = 0\\
X^\top X\vec{w} & = X^\top T  \\
\cancel{(X^\top X)^{-1}X^\top X}\vec{w} & = (X^\top X)^{-1}X^\top T  \\
\hat{w} & = (X^\top X)^{-1} X^\top T
\end{align}
$$
