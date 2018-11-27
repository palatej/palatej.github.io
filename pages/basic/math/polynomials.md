$$ P(x)=a_0 + a_1 x^+ a_2 x^2 + \cdots +a_n x^n $$

The value of $P(X)$ at $z$ is computed by the formula:

$$ P(z) = a_0 + z (a_1+z(a_2+z(\cdots + z(a_n)))) $$

In other words it is computed by the recursion $f(i+1) = a_{n-i} + z f(i)$ with the initial condition $f(0)=a_n$

The value of $P'(X)$ at $z$ is computed by the formula:

$$ P'(z) = a_1 + z (2 a_2+z(\cdots + z(n a_n)))$$

It is not difficult to see that it corresponds to the recursion $g(i+1)=f(i)+z g(i),\; f(i+1) = a_{n-i} + z f(i)$ with the initial conditions $g(0)=0 ,\;f(0)=a_n$
