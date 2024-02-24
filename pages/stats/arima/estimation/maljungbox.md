## LjungBox algorithm for pure MA models

### Short description

We consider the following stationary moving average model of order $q$ 

$$ 
y_t = \Theta \left(B \right) \epsilon_t 
$$

First, considering the initial innovations $\epsilon^*_t$ defined for $-q \leq t \lt 0$, we can write

$$\begin{pmatrix}
y^*_t \\
y_t
\end{pmatrix}
= A
\begin{pmatrix}
\epsilon^*_t \\
\epsilon_t
\end{pmatrix}
$$

where $A_{(n+q)\times (n+q)}$ is defined by 

$$  
\begin{pmatrix}
1 & 0 & \cdots & \cdots & \cdots & \cdots & 0 \\ 
\theta_1 & 1 & 0 & \cdots & \cdots & \cdots & \vdots \\ 
\theta_2 & \theta_1 & 1 & 0 & \cdots & \cdots & \vdots\\ 
\ddots & \ddots & \ddots & \ddots & \ddots & \ddots & \vdots \\ 
\cdots & \theta_q & \cdots & \theta_1 & 1 & 0 &  \vdots\\ 
\vdots & \ddots & \ddots & \ddots & \ddots & \ddots & 0 \\ 
0 & \cdots & 0 & \theta_q & \cdots & \theta_1 & 1 
\end{pmatrix} $$

Using the Pi-Weights of the model, we obtain $G=A^{-1}$

$$ G = \begin{pmatrix} 1 & 0 & \cdots & 0 \\ \pi_1 & 1 & \cdots & 0 \\ \pi_2 & \pi_1 & \cdots & \vdots\\ \vdots & \vdots & \vdots & \vdots \\ \pi_{n+q-1} & \pi_{n+q-2} & \cdots & \pi_{n} \end{pmatrix} $$

and we have that

$$\begin{pmatrix}
\epsilon^* \\
\epsilon
\end{pmatrix}
= G
\begin{pmatrix}
y^* \\
y
\end{pmatrix} 
= G_1 y^* + G_2 y
$$

Writing $(\epsilon^*, \epsilon)$ as $\bar{\epsilon}$ and $(y^*, y)$ as $\bar{y}$ , we have that 

$$p(\bar{\epsilon})=p(\bar{y})=p(y)p(y^*|y)$$

$$
p(\bar{\epsilon})=(2\pi\sigma^2)^{-(n+q)/2}e^{-(\bar{\epsilon}\bar{\epsilon}')/2\sigma^2}=(2\pi\sigma^2)^{-(n+q)/2}e^{-\bar{y}'G'G\bar{y})/2\sigma^2}
$$

Considering the equation $G_2 y = - G_1 y^* +\bar{\epsilon}$, by standard regression theory, we get:

$$
\begin{align}
\hat{y}^*=E(y^*|y) &= - (G_1'G_1)^{-1}G_1'G_2 y \\
var(y^*|y) &= (G_1'G_1)^{-1}\sigma^2
\end{align}
$$

We can now split $p(\bar{\epsilon})$ into

$$
\begin{align}
p(y^*|y) &= (2\pi\sigma^2)^{-q/2}|G_1'G_1|^{-1/2}e^{-(y^*-\hat{y}^*)'G_1'G_1(y^*-\hat{y}^*)/2\sigma^2} \\
p(y) &=  (2\pi\sigma^2)^{-n/2}|G_1'G_1|^{1/2}e^{-(G_1 y^* + G_2 y)'(G_1 y^* + G_2 y)/2\sigma^2}
\end{align}
$$

So, the different steps of the algoritm for computing the likelihood are:

* Compute $V=G_1'G_1$
* Compute L, the Cholesky factor of $V$
* 
* Solve $V=G'$

* Compute by Cholesky $G'G \hat z_* = G'a \quad and \quad \vert G'G \vert$ 

* Get by recursion the exact likelihood residuals
$\Theta\left(B\right)\begin{pmatrix}\hat a_* \\ \hat a_t \end{pmatrix}  = \begin{pmatrix}z_* \\ z_t \end{pmatrix}$

The processing defines the linear transformation 
$T z_t = \begin{pmatrix}\hat a_* \\ \hat a_t \end{pmatrix}$ and the searched determinant.

