# Our take on the PML exam questions

> Pala longa e pedalar.
\- Nereo Rocco 

___

## 1. Introduce the Empirical Risk Minimization principle

 Given a generic learning problem where we have an input space $X$ and an output space $Y$ we define the risk as a measure of the goodness of a certain model $h \in \mathcal{H}$ whith respect to a certain measure of error $l : \mathcal{H} \times X \times Y \rightarrow \mathcal{R}$, this quantity can be defined as $\mathbb{E}_{D \sim p(x,y)}[l(h,x,y)]$ and the estimation of this quantity from $N$ realizations from a datset is called the empirical risk. 
 
## 2. Define PAC Learning 

PAC Learning or Probably Approximately Correct Learning is a framework in which to formulate learning problems. A given hypothesis set $\mathcal{H}$, with the **realisability** property, meaning that the true data generating distribution is captured by a hypotesis inside $\mathcal{H}$. 

For binary classification we frame problem of training in terms of the learning algorithm being capable of achieving with probability $\epsilon$ a certain probability of error $\delta$: We assume that:
$$
	\mathrm{
		\forall \epsilon, \delta \in (0,1) \space \exists n \in \mathbb{N} \,.\, \forall m>n \ \forall D \sim p^N(X,Y) 
	}
$$
 **If the realizability assumption holds** (?)
$$
	\mathrm{
		Pr( R(h_D^*(x)) < \epsilon ) \geq 1 - \delta
	}
$$
## 3. Introduce the basic ideas of Probabilistic Inference

Marginalization and conditioning. For example given a distribution $p(x_1, x_2)$ one might want to condition, calculate $p(x1|x2)$ or vice versa. Conversely one might want to calculate $p(x_1)$ or $p(x_2)$.

## 4. Introduce Bayesian Networks and their factorization

Bayesian networks rapresent a way in which one can factorize a joint probability disitributions over a set of factors. For example $p(x_1, x_2, \ldots, x_n) = p(x_1)p(x_2|x_1)\ldots p(x_{n-1}|x_n)$ would correspond to the factorization:
```mehrmaid
graph LR
	T1 --> T2
	T2 --> T3 
	T3 -.-> TN
	
T1("$x_1$")
T2("$x_2$")
T3("$x_3$")
TN("$x_n$")
```


## 4. Conditional Independence in Bayesian Networks

We say that two random variables $A$ and $B$ are conditionally indipendent  given a third variable $C$ when $P(A|B,C)=P(A|C)$, written as $A \perp B \,|\, C$. For a node in a bayesian network a certain node, in this case $D$ is conditionally independent from the rest of the network when conditioned on the set of nodes that point to it, and the nodes it points to. So for $D$ would be $p(D|A,B,C,E) = p(D|C,E)$. 

$$ \mathrm{p(A,B,C,D,E)=p(A)\,p(B|A)\,p(C|A)\,p(B|C)\,p(E)\,p(D|C,E)} $$
```mehrmaid
graph LR
	E --> D
	A --> B
	B --> C 
	A --> C
	C --> D

A("A")
B("B")
C("C")
D("D")
E("E")
```


## 5. Introduce Random Markov Fields 

In markov random fields the factoring of the probability occurs in the following way, the factoring represents 

$$\mathrm{p(A,B,C,D,E)=p(A,B,C)\,p(D,E)\,p(C,D)}$$
```mehrmaid
graph LR
	E <---> D
	A <---> B
	B <---> C 
	A <---> C
	C <---> D

A("A")
B("B")
C("C")
D("D")
E("E")
```



## 6. Define Factor Graphs and How to convert Bayesian Networks and Markov Random Fields to Factor Graphs

In factor graphs i represent the probability density

$$\mathrm{p(A,B,C,D,E)=f_1(A,B,C)\,f_2(C,D)}$$
```mehrmaid
graph LR
	A <---> B
	B <---> C 
	A <---> C
	C <---> D

A("A")
B("B")
C("C")
D("D")
```

Becomes
```mehrmaid
graph LR
	A_ <---> f_1
	B_ <---> f_1 
	C_ <---> f_2
	C_ <---> f_1
	D_ <---> f_2
 
A_("A")
B_("B")
C_("C")
D_("D")
f_1("$f_1$")
f_2("$f_2$")

style f_1 fill:#bbbbbb
style f_2 fill:#bbbbbb
```



## 7. Describe the Sum Product algorithm

## 8. Describe the Max Plus algorithm

## 9. Define HMM and different Inference problems in HMM

## 10. Discuss closure properties of the Gaussian Distribution

## 11. How to transform a generic Gaussian Distribution to a Standard Gaussian via Principal components

## 12. Introduce the Bayesian Estimation Principles

## 13. Introduce Bayesian Linear Regression 

## 14. Prior and posterior over parameters in Bayesian Linear Regression

## 15. Predictive distribution in Bayesian Linear Regression

## 16. Discuss Model Evidence and hyper parameter optimization in Bayesian Linear Regression

## 17. Discuss Bayesian Model Comparison

## 18. Describe Laplace Approximation

## 19. Discuss Bayesian Information Content for Model Comparison

## 20. Introduce Bayesian Logistic Regression

## 21. Introduce the kernel trick and the dual formulation of linear regression

## 22. Introduce random functions and Gaussian Processes 

## 23. Present Gaussian Process regression

## 24. Rejection sampling

Given a sampling problem from a distribution $p(x) = \frac{1}{Z} q(x)$ rejection sampling employs the following schema
```julia
function rejection_sampling(q, g, M, N)
	# q = unnormalized distirbution density
	# g = sampling distribution
	# M = scale
	# N = number of samples
	samples = []
	
	while length(samples) != N
		x_c = sample(g)
		u   = sample(Uniform(0,1))
		tr  = q(x_c) / (M * g(x_c))
		if tr < u
			append!(samples, x_c)
		end
	end
	
	return samples
end
```

## 25. Importance sampling

## 26. Introduce Markov Chains and the Detailed Balance condition

## 27. Introduce Markov Chain Monte Carlo and the Metropolis Hastings criterion

## 28. Discuss issues of vanilla MCMC

## 29. Gibbs Sampling

## 30. Discuss  Convergence Diagnostics and the Rhat index

## 31. Introduce the ideas of effective sample size

## 32. Hamiltonian Monte Carlo

## 33. Introduce the problem that can be solved by EM and derive the  Evidence lower bound

## 34. Discuss the Expectation Maximization algorithm (both E-step and M-step)

## 35. Discuss convergence of the EM algorithm

## 36. Discuss EM algorithm for Gaussian Mixtures

## 37. Introduce  the problem formulation for Variational Inference

## 38. Introduce Mean Field Variational Inference

## 39. Example of Mean Field Variational Inference on Gaussian distribution

## 40. Variational Inference with direct and inverse KL

## 41. Variational Linear Regression 

## 42. Introduce Black box Variational Inference 

## 43. Discuss how to compute the gradient of the ELBO for a non-reparameterizable variational distribution

## 44. Discuss Rao-Blackwellization for variance reduction

## 45. Discuss Control variates for variance reduction

## 46. Discuss Bayesian Neural Networks

## 47. Introduce the generative modelling problem and present different models for generative AI

## 48. Introduce Autoencoding Variational Bayes

## 49. Introduce Denoising Diffusion Models


___
Hello from $M^E$
