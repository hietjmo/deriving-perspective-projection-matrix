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
\fill[gray!5] (-2,1.5) -- (2,1.5) -- (2,-1.5) -- (-2,-1.5) -- cycle;
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

\usetikzlibrary {perspective}
\begin{figure}[H]
\begin{center}
\begin{tikzpicture}[3d view={-30}{10}]
%\draw[-latex] (0,0,0) -- (1,0,0) node[pos=1.4] {$x$};
%\draw[-latex] (0,0,0) -- (0,1,0) node[pos=1.25] {$y$};
%\draw[-latex] (0,0,0) -- (0,0,1) node[pos=1.25] {$z$};
\coordinate (camera) at (0,0,0);
\coordinate (near-middle) at (4.5,0,0);
\coordinate (far-middle) at (9,0,0);
\coordinate (near-top-left) at (4.5,2,1.5);
\coordinate (near-top-right) at (4.5,-2,1.5);
\coordinate (near-bottom-right) at (4.5,-2,-1.5);
\coordinate (near-bottom-left) at (4.5,2,-1.5);
\coordinate (far-top-left) at (9,4,3);
\coordinate (far-top-right) at (9,-4,3);
\coordinate (far-bottom-right) at (9,-4,-3);
\coordinate (far-bottom-left) at (9,4,-3);
\fill[gray!5]  (near-top-left) -- (near-top-right) -- (near-bottom-right) -- (near-bottom-left) --cycle;
\fill[gray!5]  (near-top-left) -- (near-top-right) -- (far-top-right) -- (far-top-left) --cycle;
\fill[gray!5]  (near-bottom-right) -- (near-top-right) -- (far-top-right) -- (far-bottom-right) --cycle;
\draw (far-top-left) -- (far-top-right) -- (far-bottom-right) -- (far-bottom-left) --cycle;
\draw (near-top-left) -- (near-top-right) -- (near-bottom-right) -- (near-bottom-left) --cycle;
\draw (near-top-left) -- (far-top-left);
\draw (near-top-right) -- (far-top-right);
\draw (near-bottom-right) -- (far-bottom-right);
\draw (near-bottom-left) -- (far-bottom-left);
\begin{scope}[dashed]
\draw (near-top-left) -- (camera);
\draw (near-top-right) -- (camera);
\draw (near-bottom-right) -- (camera);
\draw (near-bottom-left) -- (camera);
\draw (camera) -- (near-middle) -- (far-middle);
\end{scope} 
\draw[-latex] (0,0,0) -- (1,0,0) node[pos=1.25,fill=white] {$z$};
\draw[-latex] (0,0,0) -- (0,-1,0) node[pos=1.4,fill=white] {$x$};
\draw[-latex] (0,0,0) -- (0,0,1) node[pos=1.25] {$y$};
\node[above left]  at (near-top-left)     {\emph{near-top-left}};
\node[below right] at (near-top-right)    {\emph{near-top-right}};
\node[above right] at (near-bottom-right) {\emph{near-bottom-right}};
\node[below left]  at (near-bottom-left)  {\emph{near-bottom-left}};
\node[above left]  at (far-top-left)      {\emph{far-top-left}};
\node[below right,align=left] at (far-top-right)     {\emph{far-}\\\emph{top-}\\\emph{right}};
\node[above right,align=left] at (far-bottom-right)  {\emph{far-}\\\emph{bottom-}\\\emph{right}};
\node[below left]  at (far-bottom-left)   {\emph{far-bottom-left}};
\node[below right,align=left,fill=gray!5] at (near-middle) {\emph{near-}\\\emph{middle}};
\node[below right,align=left,fill=gray!5] at (far-middle)  {\emph{far-}\\\emph{middle}};
\node[above left] at (camera)  {camera};
\node at (near-top-left)     {$\bullet$};
\node at (near-top-right)    {$\bullet$};
\node at (near-bottom-right) {$\bullet$};
\node at (near-bottom-left)  {$\bullet$};
\node at (far-top-left)      {$\bullet$};
\node at (far-top-right)     {$\bullet$};
\node at (far-bottom-right)  {$\bullet$};
\node at (far-bottom-left)   {$\bullet$};
\node at (camera) {$\bullet$};
\node at (near-middle) {$\bullet$};
\node at (far-middle)  {$\bullet$};
\end{tikzpicture}
\caption{The view frustum with a left-handed coordinate system. The $z$-axis to opposite direction would give us a right-handed coordinate system. Image is projected to \emph{near} plane.}
\label{view-frustum}
\end{center}
\end{figure}

\begin{figure}[H]
\begin{center}
\begin{tikzpicture}[3d view={-30}{10}]
\coordinate (origo) at (0,0,0);
\coordinate (near-middle) at (-2,0,0);
\coordinate (far-middle) at (2,0,0);
\coordinate (near-top-left) at (-2,2,2);
\coordinate (near-top-right) at (-2,-2,2);
\coordinate (near-bottom-right) at (-2,-2,-2);
\coordinate (near-bottom-left) at (-2,2,-2);
\coordinate (far-top-left) at (2,2,2);
\coordinate (far-top-right) at (2,-2,2);
\coordinate (far-bottom-right) at (2,-2,-2);
\coordinate (far-bottom-left) at (2,2,-2);
\fill[gray!5]  (near-top-left) -- (near-top-right) -- (near-bottom-right) -- (near-bottom-left) --cycle;
\fill[gray!5]  (near-top-left) -- (near-top-right) -- (far-top-right) -- (far-top-left) --cycle;
\fill[gray!5]  (near-bottom-right) -- (near-top-right) -- (far-top-right) -- (far-bottom-right) --cycle;
\draw (far-top-left) -- (far-top-right) -- (far-bottom-right) -- (far-bottom-left) --cycle;
\draw (near-top-left) -- (near-top-right) -- (near-bottom-right) -- (near-bottom-left) --cycle;
\draw (near-top-left) -- (far-top-left);
\draw (near-top-right) -- (far-top-right);
\draw (near-bottom-right) -- (far-bottom-right);
\draw (near-bottom-left) -- (far-bottom-left);
\draw[-latex] (0,0,0) -- (1,0,0) node[pos=1.25] {$z$};
\draw[-latex] (0,0,0) -- (0,-1,0) node[pos=1.3] {$x$};
\draw[-latex] (0,0,0) -- (0,0,1) node[pos=1.25] {$y$};
\node[above left]  at (near-top-left)            {\emph{near-top-left}};
\node[below left] at (near-top-right) {\emph{near-top-right}};
\node[below left] at (near-bottom-right)         {\emph{near-bottom-right}};
\node[above left]  at (near-bottom-left)         {\emph{near-bottom-left}};
\node[above right]  at (far-top-left)            {\emph{far-top-left}};
\node[above right] at (far-top-right)            {\emph{far-top-right}};
\node[below right] at (far-bottom-right)         {\emph{far-bottom-right}};
\node[above right]  at (far-bottom-left)         {\emph{far-bottom-left}};
\node at (near-top-left)     {$\bullet$};
\node at (near-top-right)    {$\bullet$};
\node at (near-bottom-right) {$\bullet$};
\node at (near-bottom-left)  {$\bullet$};
\node at (far-top-left)      {$\bullet$};
\node at (far-top-right)     {$\bullet$};
\node at (far-bottom-right)  {$\bullet$};
\node at (far-bottom-left)   {$\bullet$};
\end{tikzpicture}
\caption{Normalized device coordinates (NDC).}
\label{ndc}
\end{center}
\end{figure}

\begin{figure}[H]
\begin{center}
\begin{tikzpicture}
\coordinate (camera) at (0,0);
\coordinate (near-middle) at (4.5,0);
\coordinate (near-vert) at (4.5,-0.25);
\coordinate (near-top) at (4.5,1.5);
\coordinate (point-p) at (6,1);
\coordinate (p-horiz) at (6.25,1);
\coordinate (p-z-horiz) at (6.25,0);
\coordinate (point-p-z) at (6,0);
\coordinate (p-vert) at (6,-0.25);
\coordinate (p-prime) at (4.5,0.75);
\coordinate (far-middle) at (9,0);
\coordinate (far-vert) at (9,-0.25);
\coordinate (far-top) at (9,3);
\fill[gray!5] (near-top) -- (near-vert) -- (far-vert) -- (far-top) -- cycle;

\begin{scope}[dashed]
\draw (point-p) -- (camera);
\draw (point-p) -- (point-p-z) node [midway, right] {$y$};
\end{scope} 

\begin{scope}[densely dotted]
\draw (point-p-z) -- (p-vert);
\draw (near-middle) -- (near-vert);
\draw (far-middle) -- (far-vert);
\draw (point-p) -- (p-horiz);
\draw (point-p-z) -- (far-middle);
\draw (camera) -- (far-top);
\end{scope} 

\draw (1.1,0) -- (point-p-z); 
\draw (near-top) -- (p-prime);
\draw (p-prime) -- (near-middle) node [midway, right] {$y'$};
\draw (far-top) -- (far-middle); 
\node at (camera) {$\bullet$};
\node at (near-middle) {$\bullet$};
\node at (near-top)  {$\bullet$};
\node at (far-middle)  {$\bullet$};
\node at (far-top)  {$\bullet$};
\node at (point-p)  {$\bullet$};
\node at (point-p-z)  {$\bullet$};
\node at (p-prime)  {$\bullet$};
\draw[-latex] (0,0) -- (1,0) node[below left] {$z$};
\draw[-latex] (0,0) -- (0,1) node[below right] {$y$};
\node[below left] at (camera)  {camera $\mathbf o$};
\node[below,align=center] at (near-vert) {$\mathbf n$\\\emph{near}};
\node[below,align=center] at (far-vert)  {$\mathbf f$\\\emph{far}};
\node[above] at (near-top)  {\emph{near-top}};
\node[above] at (far-top)  {\emph{far-top}};
\node[above left] at (point-p)  {$\mathbf p$};
\node[above left] at (p-prime)  {$\mathbf p'$};
\node[below] at (p-vert)  {$\mathbf z$};
\end{tikzpicture}
\caption{Projection  $\mathbf p'$ of point $\mathbf p$ to \emph{near} plane (side view).}
\label{side-view}
\end{center}
\end{figure}

Here the triangles $\Delta \mathbf o \mathbf z \mathbf p$ and $\Delta \mathbf o \mathbf n \mathbf p'$ are similar.
Therefore $$\dfrac{|\mathbf n \mathbf p'|}{|\mathbf z \mathbf p|} = \dfrac{|\mathbf o \mathbf n|}{|\mathbf o \mathbf z|} \quad \Rightarrow \quad  \dfrac{y'}{y} = \dfrac{n}{z}$$

\begin{figure}[H]
\begin{center}
\begin{tikzpicture}
\coordinate (camera) at (0,0);
\coordinate (near-middle) at (4.5,0);
\coordinate (near-vert) at (4.5,0.25);
\coordinate (near-right) at (4.5,-2);
\coordinate (point-p) at (6,-1.5);
\coordinate (p-horiz) at (6.25,-1.5);
\coordinate (p-z-horiz) at (6.25,0);
\coordinate (point-p-z) at (6,0);
\coordinate (p-vert) at (6,0.25);
\coordinate (p-prime) at (4.5,-1.125);
\coordinate (far-middle) at (9,0);
\coordinate (far-vert) at (9,0.25);
\coordinate (far-right) at (9,-4);
\fill[gray!5] (near-right) -- (near-vert) -- (far-vert) -- (far-right) -- cycle;

\begin{scope}[dashed]
\draw (point-p) -- (camera);
\draw (point-p) -- (point-p-z) node [midway, right] {$x$};
\end{scope} 

\begin{scope}[densely dotted]
\draw (point-p-z) -- (p-vert);
\draw (near-middle) -- (near-vert);
\draw (far-middle) -- (far-vert);
\draw (point-p) -- (p-horiz);
\draw (point-p-z) -- (far-middle);
\draw (camera) -- (far-right);
\end{scope} 

\draw (1.1,0) -- (point-p-z); 
\draw (near-right) -- (p-prime);
\draw (p-prime) -- (near-middle) node [midway, right] {$x'$};
\draw (far-right) -- (far-middle); 
\node at (camera) {$\bullet$};
\node at (near-middle) {$\bullet$};
\node at (near-right)  {$\bullet$};
\node at (far-middle)  {$\bullet$};
\node at (far-right)  {$\bullet$};
\node at (point-p)  {$\bullet$};
\node at (point-p-z)  {$\bullet$};
\node at (p-prime)  {$\bullet$};
\draw[-latex] (0,0) -- (1,0) node[above left] {$z$};
\draw[-latex] (0,0) -- (0,-1) node[above right] {$x$};
\node[above left] at (camera)  {camera $\mathbf o$};
\node[above,align=center] at (near-vert) {\emph{near}\\$\mathbf n$};
\node[above,align=center] at (far-vert)  {\emph{far}\\$\mathbf f$};
\node[below] at (near-right)  {\emph{near-right}};
\node[below] at (far-right)  {\emph{far-right}};
\node[below left] at (point-p)  {$\mathbf p$};
\node[below left] at (p-prime)  {$\mathbf p'$};
\node[above] at (p-vert)  {$\mathbf z$};
\end{tikzpicture}
\caption{Projection $\mathbf p'$ of point $\mathbf p$ to \emph{near} plane (top view).}
\label{top-view}
\end{center}
\end{figure}

Here the triangles $\Delta \mathbf o \mathbf z \mathbf p$ and $\Delta \mathbf o \mathbf n \mathbf p'$ are similar.
Therefore $$\dfrac{|\mathbf n \mathbf p'|}{|\mathbf z \mathbf p|} = \dfrac{|\mathbf o \mathbf n|}{|\mathbf o \mathbf z|} \quad \Rightarrow \quad \dfrac{x'}{x} = \dfrac{n}{z}$$

