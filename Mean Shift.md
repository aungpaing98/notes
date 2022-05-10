# Mean Shift

![[mean_shift.png]]


![[hill_climbing.png]]

- Step 1 :  Set $m_i = f_i$ as initial mean for each pixel *i*.
- Step 2 : Repeat the following for each mean $m_i$:
	- Place window of size *W* around $m_i$.
	- Compute centriod m within the window. Set $m_i = m$.
	-  Stop if shift in mean $mi$ is less than a threshold $e$. $m_i$ is the mode.
- Step 3 : Label all pixels that have same mode as belonging to same cluster.


## Comments
- Simple but computationally expensive.
- Find arbitrary number of clusters. 
- NO initialization required.
- Robust to outliers.
- Clustering depends on window size W.