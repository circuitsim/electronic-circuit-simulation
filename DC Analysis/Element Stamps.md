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

## Controlled Sources

### CCCS

### CCVS

### VCCS

### VCVS