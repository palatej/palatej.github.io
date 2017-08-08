### State space form for the Cholette algorithm

See [SSf overview](../model.md)

The state vector is defined by

$$ \alpha_t= \begin{pmatrix}  {\omega_t y_t}^{\underline c} \\ y_t \end{pmatrix} $$

#### Dynamics 
$$ T_t = \begin{cases} \begin{pmatrix}0 &0  \\0&\rho \end{pmatrix},& {t+1} \mod {c} = 0\\ \begin{pmatrix} 0 & \omega_t\\ 0 & \rho\end{pmatrix},& {t} \mod {c} = 0\\\begin{pmatrix} 1 & \omega_t\\ 0 & \rho\end{pmatrix},&  otherwise\end{cases}$$
<br>
$$ V_t = \begin{pmatrix}0 &0  \\0&1 \end{pmatrix} ,\quad S_t = \begin{pmatrix}0 \\ 1 \end{pmatrix} $$

#### Measurement

$$ Z_t = \begin{cases} \begin{pmatrix} 0 & \omega_t\end{pmatrix},& {t} \mod {c} = 0 \\ \begin{pmatrix} 1 & \omega_t \end{pmatrix},& {t} \mod {c} \neq 0\end{cases}$$

<br>
$$ h_t = 0 $$

#### Initialization (not diffuse)

$$ \alpha_{-1} = \begin{pmatrix}  0 \\ 0 \end{pmatrix} $$

<br>

$$ P_{*} = \begin{pmatrix}  0  & 0 \\ 0 & \frac{1}{1-\rho^2} \end{pmatrix} $$