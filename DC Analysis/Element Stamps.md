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

For an $$n$$-node circuit with $$x$$ voltage sources, we number the voltages sources from $$1$$-$$x$$. Voltage source $$v$$ from node $$i$$ to node $$j$$ stamps into the equation:

$$
\begin{align*}

&
\left[
\begin{array}{cc|c}
 &  & 1 \\
 &  & -1 \\
\hline
-1\quad & 1\quad & 0
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
row\ n\!+\!v
\end{matrix}
\\
&
\begin{matrix}
col\ i & col\ j & col\ n\!+\!v
\end{matrix}

\end{align*}
$$

## Controlled Sources

For controlled sources with a gain of $$\alpha$$. The source is from node $$l$$ to node $$m$$, controlled by the current/voltage from node $$i$$ to node $$j$$.

### Current-Controlled Current Source

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
-1\quad & 1\quad & 0
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
row\ n\!+\!v
\end{matrix}
\\
&
\begin{matrix}
col\ i & col\ j & col\ n\!+\!v
\end{matrix}

\end{align*}
$$

### Current-Controlled Voltage Source

$$
\begin{align*}

&
\left[
\begin{array}{cccc|cc}
 & & & & 1 & 0 \\
 & & & & -1 & 0 \\
 & & & & 0 & 1 \\
 & & & & 0 & -1 \\
\hline
-1\quad & 1 & 0\quad & 0\quad & 0 & -\alpha \\
0\quad & 0 & -1\quad & 1\quad & 0 & 0
\end{array}
\right]
\begin{bmatrix}
 \\
 \\
 \\
 \\
i_{ij}\\
i_{lm}
\end{bmatrix}
=
\begin{bmatrix}
 \\
 \\
 \\
 \\
0\\
0
\end{bmatrix}
\begin{matrix}
row\ i\\
row\ j\\
row\ l\\
row\ m\\
row\ n\!+\!v_1 \\
row\ n\!+\!v_2
\end{matrix}
\\
&
\begin{matrix}
\ col\ i & col\ j & col\ l & col\ m
\end{matrix}

\end{align*}
$$

### Voltage-Controlled Current Source

$$
\begin{array}{cl}
\begin{bmatrix}
\alpha & -\alpha \\
-\alpha & \alpha
\end{bmatrix}
&
\begin{array}{l}
row\ l\\
row\ m
\end{array}
\\
col\ i \quad col\ j
\end{array}
$$

### Voltage-Controlled Voltage Source

$$
\begin{align*}

&
\left[
\begin{array}{cccc|c}
 & & & & 1 \\
 & & & & -1 \\
\hline
\alpha\quad & -\alpha\quad & -1\quad & 1\quad & 0
\end{array}
\right]
\begin{bmatrix}
 \\
 \\
i_{lm}
\end{bmatrix}
=
\begin{bmatrix}
 \\
 \\
0
\end{bmatrix}
\begin{matrix}
row\ l\\
row\ m\\
row\ n\!+\!v
\end{matrix}
\\
&
\begin{matrix}
\ col\ i & col\ j & col\ l & col\ m & col\ n\!+\!v
\end{matrix}

\end{align*}
$$



