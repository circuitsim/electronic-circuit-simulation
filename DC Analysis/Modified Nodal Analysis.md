# Modified Nodal Analysis

For independent voltage sources, simple nodal analysis isn’t enough. To solve circuits with these elements, Modified Nodal Analysis (MNA) is required. Since current-controlled sources use a zero-valued voltage source as the control element, all controlled sources (except VCCSs) consist of at least one independent voltage source, and MNA is needed to model these components.

![Circuit requiring MNA](./MNA.jpg)

A circuit which requires MNA is shown above. Since the voltage between nodes $$1$$ and $$2$$ is known, the voltages at those nodes are not independent of each other. An extra independent variable and equation is needed. The current through the voltage source is added as an independent variable, and the following equation added.

$$
v_2-v_1=V_s
$$

The resulting circuit equation is shown below.

$$
\begin{bmatrix}
\frac{1}{R_1} + \tfrac{1}{R_2} & \tfrac{-1}{R_2} & 1 \\
\tfrac{-1}{R_2} & \tfrac{1}{R_2} & -1\\
1 & -1 & 0
\end{bmatrix}
\begin{bmatrix}
v_{1}\\
v_{2}\\
i_{12}
\end{bmatrix}
=
\begin{bmatrix}
I_{1}=0\\
I_{2}=0\\
V_{12}
\end{bmatrix}
$$

The 'stamp' for a voltage source between nodes $$i$$ and $$j$$ for an $$n\!+\!1$$ node circuit is:

$$
\begin{align*}

&
\begin{bmatrix}
 &  & 1 \\
 &  & -1 \\
1\quad & -1\quad & 0
\end{bmatrix}
\begin{bmatrix}
 \\
 \\
i_{12}
\end{bmatrix}
=
\begin{bmatrix}
 \\
 \\
V_{12}
\end{bmatrix}
\begin{matrix}
row\ i\\
row\ j\\
row\ n+1
\end{matrix}
\\
&
\begin{matrix}
col\ i & col\ j & col\ n\!+\!1
\end{matrix}

\end{align*}
$$

A consequence of MNA is the appearance one or more zeros on the diagonal of the $$Y$$ matrix, as seen above. This can cause problems when using simultaneous equation solvers.

It is possible to swap rows to move the zeros away from the diagonal, but a better method exists which involves eliminating the unknown current values and rearranging the equations to closer resemble conventional nodal analysis. This method results in equations that are often:

- Better conditioned numerically
- More compact
- More efficient to solve than the original MNA equations.

For larger matrices, this is likely to have significant benefits.

A simple example of this procedure is shown in the following equations for a generic three-node circuit, with a voltage source $$V_{12}$$ between nodes 1 and 2.
