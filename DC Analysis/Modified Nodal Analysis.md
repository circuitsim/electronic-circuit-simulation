# Modified Nodal Analysis

For independent voltage sources, simple nodal analysis isn’t enough. To solve circuits with these elements, Modified Nodal Analysis (MNA) is required. All controlled sources (except Voltage-Controlled Current Sources) consist of at least one independent voltage source, and MNA is needed to model these components too.

## Example

![Circuit requiring MNA](../imgs/MNA.jpg)

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

## Voltage Source Stamp

The *stamp* for a voltage source between nodes $$i$$ and $$j$$ for an $$n\!+\!1$$ node circuit is:

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
row\ n\!+\!1
\end{matrix}
\\
&
\begin{matrix}
col\ i & col\ j & col\ n\!+\!1
\end{matrix}

\end{align*}
$$

## Equation Conditioning

A consequence of MNA is the appearance one or more zeros on the diagonal of the $$Y$$ matrix, as seen above. This can cause problems when using simultaneous equation solvers.

It is possible to swap rows to move the zeros away from the diagonal, but a better method exists. This involves eliminating the unknown current values and rearranging the equations to closer resemble conventional nodal analysis. Doing this results in equations that are often:

- Better conditioned numerically
- More compact
- More efficient to solve than the original MNA equations.

For larger matrices, this is likely to have significant benefits.

*It would be interesting to show an example of how much more efficient this is to solve. E.g. Assume 10x10 matrix, one voltage source, turns to 8x8 matrix with two eliminated variables. O(n^3) to solve equation, O(1) to solve for eliminated variables. 10^3 = 1000, 8^3 = 512. Could be significantly faster? But how efficient is it to condition the matrix properly?*

### Example

A simple example of this procedure is shown in the following equations for a generic three-node circuit, with a voltage source $$V_{12}$$ between nodes 1 and 2.

The matrix equation is:

$$
\begin{bmatrix}
y_{11} & y_{12} & 1 \\
y_{21} & y_{22} & -1 \\
1 &-1 & 0
\end{bmatrix}
\begin{bmatrix}
v_{1} \\
v_{2} \\
i_{12}
\end{bmatrix}
=
\begin{bmatrix}
I_{1} \\
I_{2} \\
V_{12}
\end{bmatrix}
$$

Which represents the set of simultaneous equations:

$$
\begin{align}
y_{11}v_1 + y_{12}v_2 + i_{12} &= I_1 \\ 
y_{21}v_1 + y_{22}v_2 - i_{12} &= I_2 \\ 
v_1 - v_2 &= V_{12}
\end{align}
$$

Add row 2 to row 1 to eliminate $$i_{12}$$. $$i_{12}$$ can be calculated later by substituting $$v_1$$ and $$v_2$$ into one of the equations above.

$$
\begin{pmatrix}
y_{11}+y_{21} & y_{12}+y_{22} \\
1 &-1
\end{pmatrix}
\begin{pmatrix}
v_{1} \\
v_{2}
\end{pmatrix}
=
\begin{pmatrix}
I_{1}+I_{2} \\
V_{12}
\end{pmatrix}
$$

$$
\begin{align*}
(y_{11}+y_{21})v_1 + (y_{12}+y_{22})v_2 &= I_1+I_2 \\
v_1 - v_2 &= V_{12}
\end{align*}
$$

Since we know that $$v_2$$ is dependent on $$v_1$$, we can eliminate this variable too. Start by adding column 2 to column 1:

$$
\begin{pmatrix}
y_{11}+y_{21}+y_{12}+y_{22} & y_{12}+y_{22} \\
0 &-1
\end{pmatrix}
\begin{pmatrix}
v_1 \\
v_2-v_1
\end{pmatrix}
=
\begin{pmatrix}
I_1+I_2 \\
V_{12}
\end{pmatrix}
$$

$$
\begin{align*}
(y_{11}+y_{21}+y_{12}+y_{22})v_1 + (y_{12}+y_{22})(v_2-v_1) &= I_1+I_2 \\
-(v_2 - v_1) &= V_{12}
\end{align*}
$$

We then substitute $$V_{12}$$ into the first equation to get:

$$
\begin{align*}
(y_{11}+y_{21}+y_{12}+y_{22})v_1 + (y_{12}+y_{22})(-V_{12}) &= I_1+I_2
\end{align*}
$$

And rearrange:

$$
\begin{align*}
(y_{11}+y_{21}+y_{12}+y_{22})v_1 &= I_1+I_2+V_{12}(y_{12}+y_{22})
\end{align*}
$$

Finally, in matrix form:

$$
\begin{pmatrix}
y_{11}+y_{21}+y_{12}+y_{22} & y_{12}+y_{22}
\end{pmatrix}
\begin{pmatrix}
v_1
\end{pmatrix}
=
\begin{pmatrix}
I_1+I_2+V_{12}(y_{12}+y_{22})
\end{pmatrix}
$$

As shown above, with a bit of extra computation, the 3x3 matrix was reduced to a 1x1 matrix. For every voltage source, the matrix size can be reduced by two. For large circuits with many voltage sources, this can significantly reduce the size of the matrix, and reduce computation necessary to solve it.

An LU decomposition algorithm described in Numerical Recipes [5] has an efficiency of approximately $$O(N^3)$$, where N is the size of the matrix. An example circuit with a 15x15 matrix and two voltage sources could be reduced to an 11x11 matrix. Using the approximation above, this 11x11 matrix could be solved in approximately 40% of the time of the 15x15 matrix plus the additional time taken in conditioning the matrix and subsequent solution of the eliminated variables.

It should also be noted that most matrices for reasonable large circuits are sparse, meaning that there is a high number of zeros in the matrix. This can be taken advantage of using special methods. Use of these methods can increase the efficiency of solution for typical circuits from O(N3) to about O(N1.5) [3], a significant improvement. These methods have not been used in this project, so have not been considered in detail, but are worth keeping in mind for further work.

There are other techniques for building up a set of matrix equations for a circuit. Graph/tableau techniques are discussed in “Computer Methods for Circuit Analysis and Design” [4], but it mentions that MNA is usually preferred over this technique as it produces more compact, less sparse matrices that are easier to work with. A method called ‘two-graph MNA’ exists that performs even better, but this is not considered here as it would require too much modification of the existing code for too little benefit. Also, its main advantage is in switched networks, which are not a high priority.


