### CKMS filter (or fast Chandrasekhar recursions)

When the [model](../model.md) is time invariant (which also implies that we don’t have missing values), it is usually much more efficient to use the Chandrasekhar recursions, which propagate the difference of the covariance matrix:

$$ \Delta P_t = - L_t M_t^{-1} L_t' $$

If we write:

$$ K_t = T P_t Z' $$ 

$$ F_t = Z P_t Z' + H $$

the CKMS recursions are:
$$  \Delta K_t = -T L_t M_t^{-1} L_t' Z'$$    
$$  \Delta F_t = -Z L_t M_t^{-1} L_t' Z'$$    
$$ L_{t+1} = \left( T - K_t F_t^{-1}Z \right) L_t$$  
$$ \Delta M_t = - Z L_t F_t^{-1} L_t'Z'$$  

It is clear that if we can take
$$ M_*=F_* $$
(see below for stationary models with their unconditional initial distribution), the last equation is redundant (
$$M_t=F_t$$
). Then, the recursions are 

$$  \Delta K_t = -T L_t F_t^{-1} L_t' Z'$$    
$$  \Delta F_t = -Z L_t F_t^{-1} L_t' Z'$$    
$$ L_{t+1} = \left( T - K_t F_t^{-1}Z \right) L_t$$  

In the case of stationary models, the usual (unconditional) distribution of the state is defined by the relationship:

$$ P_* = T P_* T' + V $$  

So, we have:
$$ \Delta P_* P_0 - P_* = T P_* T' - K F^{-1} K' + V = - K F^{-1} K'$$

and we can take:
$$ L_* = K_*, \: M_* = F_* $$  

It can be shown that the CKMS algorithm is also valid for non-stationary models, after their initialization period. 
