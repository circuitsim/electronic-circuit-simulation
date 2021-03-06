# AC analysis

AC analysis shows a circuit’s response in magnitude and phase for different frequencies. It is possible to do this as a transfer function for a single AC input. Alternatively, the output response can be taken on its own, which works for any number of inputs. All DC sources are shorted for this analysis.

## Linear AC Analysis

For LTI circuits, AC analysis is relatively simple. Frequency domain equations are used for energy storage elements, such as capacitors and inductors. These equations are then stamped into the Y matrix using complex admittances, in much the same way as resistors. This matrix equation can then be solved for any number of frequencies required.

Most circuit elements are modelled as complex admittances for AC analysis. For example, a capacitor’s admittance is $$j\omega C$$. However, the admittance for an inductor is:

$$
G_L=\frac{1}{j\omega L}
$$

As $$\omega \rightarrow 0$$, it is possible that numerical problems could arise as the admittance approaches infinity. To solve this, inductors are modelled as impedances. The inductor current $$I_L$$ is added as a new variable and an auxiliary equation is added, much the same as the technique used for voltage sources in MNA. For an inductor from node $$a$$ to node $$b$$, the auxiliary equation is:

$$
v_a-v_b-j\omega LI_L=0
$$

It is interesting to note that that is not a particularly efficient method. For 100 frequency points, it is necessary to solve for 100 complex-valued circuits, which for large circuits can be a lengthy task.

## Nonlinear AC Analysis

For nonlinear circuits, the procedure is more complicated.  Nonlinear DC analysis is used to find the bias point and the circuit linearised around this point. Linear AC analysis can then be used to analyse the resulting linear circuit.

## Alternative Methods

An alternative, useful, method of finding the frequency response of a circuit is pole/zero analysis. This is only an optional objective so has not been considered in detail, but again this is not very efficient. A more efficient method does exist, and this approximates the frequency response using dominant pole analysis, based upon a method called ‘moment-matching’. It is also noteworthy that pole/zero analysis can cause problems when circuits contain more than about 20 charge storage elements, as noted in [The SPICE Book](http://www.amazon.co.uk/The-Spice-Book-Andre-Vladimirescu/dp/0471609269).

Another technique can be used, using a simple FFT of the output signal when a broadband signal is input to a circuit. This, of course, relies on the time domain simulation being linear and accurate, which may not be the case.
