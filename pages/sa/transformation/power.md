## Power transformation (with sign)

We write $Y$ the variable in original scale and $y$ the transformed variable. the transformation and its reciprocal are defined by:

$$ y=f(Y)=sign(Y) \lvert{Y}\rvert^{\lambda}$$

$$ Y=f^{-1}(y)=sign(y) \lvert y\rvert^{1/ \lambda}$$


We define the operator $\oplus$ between two variables as follows:

$$A \oplus B = f^{-1}(f(A)+f(B))$$

When $\lambda = 1$, this is the usual sum. 

When $f(Y)=\log{Y}, f^{-1}(y)=e^y$, $A \oplus B = A \times B$

When $\lambda=0.5$, $A \oplus B= sign(c) c^2$ where $c=sign(A)\sqrt{\lvert A \rvert}+ sign(B)\sqrt{\lvert B \rvert}$. 

If we omit the signs, $A \oplus B= {\left(\sqrt A + \sqrt B \right)}^2$

We define the same way the operator $\ominus$ between two variables as follows:

$$A \ominus B = f^{-1}(f(A)-f(B))$$


#### Seasonal adjustment

We consider now the decomposition computed on the transformed model

$$ y = sa + s$$

As usual, if the log transformation has been applied, the decomposition in the original scale becomes

$$ Y = SA \oplus S = e^{sa}*e^s=SA*S$$

After a square root transformation, we have (we suppose to simplify the notations that $sa \gt 0$ and $sa+s\gt 0$):

$$ Y = SA \oplus S =  \left(sa + s \right)^2 = SA  + \lvert S \rvert + 2 sign(s) \sqrt{\lvert SA \times  S \rvert } $$

$$ = SA + S +2 \sqrt{S*SA} \quad ,S \ge 0$$

$$ = SA - (S + 2 \sqrt{-S*SA}) \quad ,S \lt 0 $$

We can define in a similar way $sa = y - s$ ,  $t=sa-i$  ...
