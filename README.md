# rrcf-weighted-


Based on the implementation of rrcf done by [kLabUM](https://github.com/kLabUM/rrcf.git), 
I only changed the def _cut_ in wrcf.py:

def _cut(self, X, S, parent=None, side='l')

        # Find max and min over all d dimensions

        xmax = X[S].max(axis=0)

        xmin = X[S].min(axis=0)

        # Compute l

        l = xmax - xmin

        l /= l.sum()

        # Determine dimension to cut

        q = self.rng.choice(self.ndim, p=l)

 

        __Determine value for split__

        p = self.rng.uniform(xmin[q], xmax[q])

 

        # Determine subset of points to left

        S1 = (X[:, q] <= p) & (S)

        # Determine subset of points to right

        S2 = (~S1) & (S)

        # Create new child node

        child = Branch(q=q, p=p, u=parent)

        # Link child node to parent

        if parent is not None:

            setattr(parent, side, child)

        return S1, S2, child

 

 

 

to (here, alpha=2)

 

 

def _cut(self, X, S, parent=None, side='l'):

        # Find max and min over all d dimensions

        xmax = X[S].max(axis=0)

        xmin = X[S].min(axis=0)

        # Compute l

        l = xmax - xmin

        l /= l.sum()

        # Determine dimension to cut

        q = self.rng.choice(self.ndim, p=l)

 

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

       

        # Determine subset of points to left

        S1 = (X[:, q] <= p) & (S)

        # Determine subset of points to right

        S2 = (~S1) & (S)

        # Create new child node

        child = Branch(q=q, p=p, u=parent)

        # Link child node to parent

        if parent is not None:

            setattr(parent, side, child)

        return S1, S2, child

 


Details are [Here](https://arxiv.org/abs/2202.01891)
