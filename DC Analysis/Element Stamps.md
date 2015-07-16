# Element Stamps

For the equation:
$$
Yv=J
$$

**TODO: Include diagrams**

## Resistor

A resistor between nodes $$i$$ and $$j$$ stamps into the $$Y$$ matrix:

$$
\begin{align*}

&
\begin{bmatrix}
\frac{1}{R} & \frac{-1}{R} \\
\frac{-1}{R} & \frac{1}{R} \\
\end{bmatrix}

\begin{matrix}
row\ i\\
row\ j\\
\end{matrix}
\\
&
\begin{matrix}
col\ i & col\ j
\end{matrix}

\end{align*}
$$

## Current Source

A current source from node $$i$$ to node $$j$$ stamps into the $$J$$ matrix:

$$
\begin{bmatrix}
-I \\
I
\end{bmatrix}
\begin{matrix}
row\ i\\
row\ j\\
\end{matrix}
$$

## Voltage Source

For an $$n$$-node circuit with $$x$$ voltage sources, we number the voltages sources from $$1$$-$$x$$. Voltage source $$k$$ from node $$i$$ to node $$j$$ stamps into the equation:

$$
\begin{align*}

&
\left[
\begin{array}{cc|c}
 &  & 1 \\
 &  & -1 \\
\hline
1\quad & -1\quad & 0
\end{array}
\right]
\begin{bmatrix}
 \\
 \\
i_{ij}
\end{bmatrix}
=
\begin{bmatrix}
 \\
 \\
V_{ij}
\end{bmatrix}
\begin{matrix}
row\ i\\
row\ j\\
row\ n\!+\!k
\end{matrix}
\\
&
\begin{matrix}
col\ i & col\ j & col\ n\!+\!k
\end{matrix}

\end{align*}
$$

## Controlled Sources

For controlled sources with a gain of $$\alpha$$.

### CCCS

$$
\begin{align*}

&
\left[
\begin{array}{cc|c}
 &  & 1 \\
 &  & -1 \\
 &  & \alpha \\
 &  & -\alpha \\
\hline
1\quad & -1\quad & 0
\end{array}
\right]
\begin{bmatrix}
 \\
 \\
 \\
 \\
i_{ij}
\end{bmatrix}
=
\begin{bmatrix}
 \\
 \\
 \\
 \\
0
\end{bmatrix}
\begin{matrix}
row\ i\\
row\ j\\
row\ l\\
row\ m\\
row\ n\!+\!k
\end{matrix}
\\
&
\begin{matrix}
col\ i & col\ j & col\ n\!+\!k
\end{matrix}

\end{align*}
$$

### CCVS

### VCCS

### VCVS


