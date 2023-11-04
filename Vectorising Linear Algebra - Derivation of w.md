### Fist, some rules:
$$
\begin{align} \\
(1) &  & (\vec{a}+\vec{b})^\top &= \vec{a}^\top + \vec{b}^\top &  & \text{sum associativity} \\
(2) &  & \left(\vec{a} * \vec{b}\right)^\top &= \vec{a}^\top *\vec{b}^\top  &  & \text{product associativity} \\ \\
(3) &  & \frac{ \partial  }{ \partial x } \vec{x}^\top a &= a \\ \\
(4) &  & \frac{ \partial  }{ \partial x } a^\top\vec{x} &= a \\ \\
(5) &  & \frac{ \partial  }{ \partial x } \vec{x}^\top\vec{x} &= 2\vec{x} \\ \\
(6) &  & \frac{ \partial  }{ \partial x } \vec{x}^\top a \vec{x} &= 2a\vec{x} \\ \\
\end{align}
$$
### Then, some calculus:
$$
\begin{align}
\frac{ \partial \mathcal{L} }{ \partial w }  & = \frac{ \partial  }{ \partial w } \frac{1}{N} (T-X\vec{w})^\top (T-X\vec{w}) \\
 & = \frac{1}{N} \frac{ \partial  }{ \partial w } (T^\top-(X\vec{w})^\top) (T-X\vec{w})  & \text{by (1)}\\
 & = \frac{1}{N} \frac{ \partial  }{ \partial w } (T^\top-X^\top\vec{w}^\top) (T-X\vec{w})  & \text{by (2)}\\
 & = \frac{1}{N} \frac{ \partial  }{ \partial w } T^\top T - X^\top\vec{w}^\top T - T^\top X\vec{w} + X^\top\vec{w}^\top X\vec{w} & \text{expand}\\
 &=\frac{1}{N} \frac{ \partial  }{ \partial w } - X^\top\vec{w}^\top T - T^\top X\vec{w} + X^\top\vec{w}^\top X\vec{w} & \text{drop terms without $\vec{w}$}\\
 &= \frac{1}{N}  \left(  - X^\top T + \frac{ \partial  }{ \partial w }- T^\top X\vec{w} + X^\top\vec{w}^\top X\vec{w} \right) & \text{by (3 \& 4)}\\
&= \frac{1}{N}  \left(  - X^\top T  - T X^\top + \frac{ \partial  }{ \partial w } X^\top\vec{w}^\top X\vec{w} \right) & \text{by (4)}\\
&= \frac{1}{N}  \left(  - X^\top T  - T X^\top + 2X^\top X\vec{w} \right) & \text{by (6)}\\
&= \frac{1}{N}  \left( 2X^\top X\vec{w} - X^\top T  - T X^\top \right)\\
&= \frac{1}{N}  \left( 2X^\top X\vec{w} -2 X^\top T \right)\\
&= \frac{2}{N}  \left( X^\top X\vec{w} - X^\top T \right)\\
\end{align}
$$

### Finally,  some simple algebra to solve:
$$
\begin{align}
0 & = \frac{ \partial \mathcal{L} }{ \partial w }  \\
0 & = \frac{2}{N}  \left( X^\top X\vec{w} - X^\top T \right) \\
 & = X^\top X\vec{w} - X^\top T \\
X^\top X\vec{w} & = X^\top T  \\
\vec{w} & = (X^\top X)^{-1} X^\top T 
\end{align}
$$
