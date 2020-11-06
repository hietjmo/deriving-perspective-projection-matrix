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
x' = m_{11} x + m_{12} y + m_{13} z + m_{14} w \\
y' = m_{21} x + m_{22} y + m_{23} z + m_{24} w \\
z' = m_{31} x + m_{32} y + m_{33} z + m_{34} w \\
w' = m_{41} x + m_{42} y + m_{43} z + m_{44} w \\
\end{aligned}$$

$\cdots$

Our goal is the perspective projection matrix $\mathbf M_\text{proj}$ defined as:
$$\mathbf M_\text{proj} = \begin{pmatrix}
\dfrac{2n}{r-l} & 0 & \dfrac{l+r}{l-r}  & 0 \\
0 & \dfrac{2n}{t-b}  & \dfrac{b+t}{b-t}  & 0 \\
0 & 0 & \dfrac{f+n}{n-f} & \dfrac{2fn}{f-n}  \\
0 & 0 & 1 & 0 \\
\end{pmatrix}$$

Here $n$ is the *near* clipping plane, $f$ the *far* clipping plane, $r$ the *right* clipping plane, $l$ the *left* clipping plane, $t$ the  *top* clipping plane, and $b$ the *bottom* clipping plane:
$\emph{left} \leq x \leq \emph{right}$,
$\emph{bottom} \leq y \leq \emph{top}$,
$\emph{far} \leq z \leq \emph{near}$.

The complete projection matrix is
$$\mathbf M_\text{proj} = \begin{pmatrix}
\dfrac{2n}{r-l} & 0 & \dfrac{r+l}{l-r} & 0 \\
0 & \dfrac{2n}{t-b} & \dfrac{t+b}{b-t} & 0 \\
0 & 0 & \dfrac{f+n}{n-f} & \dfrac{2fn}{f-n} \\
0 & 0 & 1 & 0 \\
\end{pmatrix}$$


If the viewing volume is symmetric, which is $r = -l$ and $t= -b$, then
$$\begin{aligned}
r+l &= 0 \\
r-l &= 2r
\end{aligned}
\qquad\qquad
\begin{aligned}
t+b &= 0 \\
t-b &= 2t
\end{aligned}$$
so the matrix can be simplified to
$$\mathbf {M}_\text{proj}' = \begin{pmatrix}
\dfrac{n}{r} & 0 & 0 & 0 \\
0 & \dfrac{n}{t} & 0 & 0 \\
0 & 0 & \dfrac{f+n}{n-f} & \dfrac{2fn}{f-n} \\
0 & 0 & 1 & 0 \\
\end{pmatrix}$$

\begin{figure}[H]
\begin{center}
\begin{tikzpicture} 
\begin{scope}[line width=0.6pt]
\coordinate (y-ax) at (0,2.0);
\coordinate (x-ax) at (2.5,0);
\draw[-latex] (0,-1.9) -- (y-ax);
\draw[-latex] (-2.4,0) -- (x-ax);
\node[below right] at (y-ax) {$y$};
\node[above left] at (x-ax) {$x$};
\draw (-2,1.5) -- (2,1.5) -- (2,-1.5) -- (-2,-1.5) -- cycle;
\node (minus-r) at (-2.0, 0.0) {$\bullet$};
\node[below right] at (minus-r) {$-r$};
\node (plus-r) at (2.0, 0.0) {$\bullet$};
\node[below left] at (plus-r) {$r$};
\node (minus-t) at  (0.0, -1.5) {$\bullet$};
\node[above left] at (minus-t) {$-t$};
\node (plus-t) at (0.0, 1.5) {$\bullet$};
\node[below left] at (plus-t) {$t$};
\node[above] (plus-t) at (2.0, 1.5) {\emph{near} plane $n$};
\end{scope} \end{tikzpicture}
\caption{The \emph{near} plane when the viewing volume is symmetric.}
\label{near-plane}
\end{center}
\end{figure}




