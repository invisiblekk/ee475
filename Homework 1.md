## (a)

If we uniformly sample in [-1, 1] in each dimension, the number of whole sample points will be $P^N$. In (a), we set the number of sample points in each dimension fixed to P = 100. In each dimension, the sample point that is most close to 0 is the same, so the minimum value will be linear to the input dimension N (minimum value in dimension N = N $\times$ minimum value in dimension 1). Below I just draw N = 1, 2 because the number of points grows extremely quickly as dimension increases.

![](./2.1(a).png)

## (b)

As the number of sample points increases, there will be some points that are more closer to 0, which will make the minimum value smaller. And the relationship between minimum value and input dimension N remains linear.

 ```python
 def uniform_eval_for_Ps(g, N, nums_samples): 
    # loop over dimensions and evaluate
    min_evals = []
    for num_samples in nums_samples:
        m_eval = []
        for dim in range(1, N + 1):
            dim_eval = []
            grid = np.array(np.meshgrid(*[np.linspace(-1, 1, num_samples) for _ in range(dim)]))
            dim_eval.append(np.sum(g(grid), axis = 0))

            m_eval.append(np.min(dim_eval))
        min_evals.append(m_eval)

    # convert to array
    min_evals_global = np.asarray(min_evals)

    for k in range(len(nums_samples)):
        min_evals = min_evals_global[k, :]

        # draw minimum value for each numders of dimension N
        plt.plot(np.arange(N) + 1, min_evals, label = "P = " + str(nums_samples[k]))

    # set x y label
    plt.xlabel("input dimension N")
    plt.ylabel("minimum value")

    # draw horizontal axis
    plt.plot(np.arange(N) + 1, np.arange(N) * 0, linestyle = "dashed", color = "black")
    plt.title("Uniform Sample")
    plt.yscale("log")
    
    # draw legend
    plt.legend()
    
    plt.show()
    
# g = lambda w : np.dot(w.T, w)
g = lambda w : w**2
N = 2 # max input dimension
nums_samples = P = [100, 1000, 10000]
uniform_eval_for_Ps(g, N, nums_samples)
 ```

![](./2.1(b).png)
