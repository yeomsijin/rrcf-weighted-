# rrcf-weighted-


Based on the implementation of rrcf done by [kLabUM](https://github.com/kLabUM/rrcf.git), 
I only changed some part of the def _cut_ in wrcf.py as follows:
(This is very simple and powerful)

**Determine value for split**

p = self.rng.uniform(xmin[q], xmax[q])




to (here, alpha=2)




def _cut(self, X, S, parent=None, side='l'):


#__Determine value for split

epsilon = ((xmax[q] - xmin[q])/(len(X[S][:,q])-1) )/2

num_nd =  1

iteration = 0

        while num_nd != 0 :

        p = self.rng.uniform(xmin[q], xmax[q])

        num_nd = sum((p-epsilon <= X[S][:,q]) &  ( X[S][:,q] < p+epsilon) )

        iteration +=1

        if num_nd < 2:

                break;__

    
 


Details are [Here](https://arxiv.org/abs/2202.01891)
