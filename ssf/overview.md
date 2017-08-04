# State space framework of JD+ 

State space forms may represent many different models. On such forms we can apply the Kalman filter (KF), the Kalman smoother (KS) or some of the numerous variants/extensions of them. All those algorithms will generate/use different types of results.  
In such a situation, it is not easy to find a solution that is at the same time efficient and reusable. On the one hand, we can write dedicated algorithms for specific models; that will always provide the most efficient solution, but it will lead to much redundant code. On the other hand, we could use the general matrix representation that we can find in many papers; however, that approach will not be able to use the specificity of the considered model and will produce often rather slow solutions.  
Object-oriented programming can provide, through its polymorphic mechanism, a good solution; that is the avenue followed in JD+.

### Contents

* [General form](./model.md)
* Algorithms  
  * [Main algorithms](./algorithms.md)


### Bibliography