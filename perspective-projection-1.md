## Projection matrices

The vector $\mathbf v'$ is a result of multiplying the vector $\mathbf v$  with transformation matrix $\mathbf M$ ("postmultiplying"):
$$\mathbf v' = \mathbf M \mathbf v$$

For a three-dimensional vector 
$\mathbf v = \begin{pmatrix}
x & y & z \\
\end{pmatrix}^{\mathbf T}$
we use the four-dimensional homogenous coordinates
$\mathbf v =\begin{pmatrix}
x & y & z & w \\
\end{pmatrix}^{\mathbf T}$.

Now
$$\begin{pmatrix}
x' \\
y' \\
z' \\ 
w' \\
\end{pmatrix}
= \begin{pmatrix}
m_{11} & m_{12} & m_{13} & m_{14}\\
m_{21} & m_{22} & m_{23} & m_{24}\\
m_{31} & m_{32} & m_{33} & m_{34}\\
m_{41} & m_{42} & m_{43} & m_{44}\\
\end{pmatrix}
\begin{pmatrix}
x \\
y \\
z \\
w \\
\end{pmatrix}$$
where
$$\begin{aligned}
x' = x m_{11} + y m_{21} + z m_{31} + w m_{41}\\
y' = x m_{12} + y m_{22} + z m_{32} + w m_{42}\\
z' = x m_{13} + y m_{23} + z m_{33} + w m_{43}\\
w' = x m_{14} + y m_{24} + z m_{34} + w m_{44}\\
\end{aligned}$$

$\cdots$

Our goal is the perspective projection matrix $\mathbf M_\text{per}$ defined as:
$$\mathbf M_\text{per} = \begin{pmatrix}
\dfrac{2n}{r-l} & 0 & \dfrac{l+r}{l-r}  & 0 \\
0 & \dfrac{2n}{t-b}  & \dfrac{b+t}{b-t}  & 0 \\
0 & 0 & \dfrac{f+n}{n-f} & \dfrac{2fn}{f-n}  \\
0 & 0 & 1 & 0 \\
\end{pmatrix}$$

Here $n$ is the *near* clipping plane, $f$ the *far* clipping plane, $r$ the *right* clipping plane, $l$ the *left* clipping plane, $t$ the  *top* clipping plane, and $b$ the *bottom* clipping plane:
$\emph{left} \leq x \leq \emph{right}$,
$\emph{bottom} \leq y \leq \emph{top}$,
$\emph{far} \leq z \leq \emph{near}$.
