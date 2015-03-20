---
layout: post
title: Kullback Leibler Divergence
date: 2015-03-20 13:37
categories: science
comments: false
---

# Concept

The Kullback-Leibler (KL) divergence is a statistical concept used to measure how similar are two probabilities distributions. Considering two probability density functions (PDF), *f* and *g*, the KL divergence satisfies these properties:

1. Self similarity: D(f\|\|f) = 0;
2. Self identification: D(f\|\|g) = 0 only if f = g;
3. Positivity: D(f\|\|g) >= 0 for all f, g.

# Divergence using GMM

The KL divergence does not have a closed form expression for all cases. In this post I will focus on gaussians PDF, more specifically on Mixture of Gaussians (GMM). In the literature, one may find methodologies to estimate the KL divergence for this kind of PDF, but there is no closed form to achieve an exact value. The equations bellow describe *f* and *g* as mixture of gaussians:
<img class="large-img" src="/assets/posts/kl/description.png">

The most common technique to estimate the KL divergence between  two GMM is using Monte Carlo (MC). This a technique is based on  sampling points randomly, and applying some computation based on these samples.

Consider that we can sample *n* points to cover the GMM *f*, the KL divergence by MC is computed by the equation bellow. The intuition of this equation is that we sample points in one gaussian *f*, then we compute the probability of this point for the gaussian *f* and the gaussian *g*. So, basically we are analysing how the function *f* overlaps function *g* by an approximation.
<img class="large-img" src="/assets/posts/kl/kl_mc.png">

One can imagine that the MC approach is time consuming, as the quality of the estimation relies on the amount of samples. Some more recent methodologies to estimate the divergence are available. I will present one of them: the variational approach, that has this definition:
<img class="large-img" src="/assets/posts/kl/kl_var.png">

The fist equation is the variational divergence itself, and the second equation is the definition of the KL divergence between two simple gaussians (not a GMM, i.e. not a mixture of gaussians, just a single gaussian distribution function). The intuition of this approach is a little trick. There is no necessity to sample points, because this is a direct formulation.

For each gaussian component of *f*, it is computed the divergence of this component with all other components of *f* and also with all components of *g*, using the entropy concept as a logarithmic function. This will provide a lower bound divergence.

# Coding
I am working in a Mathematica CDF file to provide an interactive way to explain the KL concept. For now you can get on my github the Mathematica notebook files for the [Monte Carlo](https://github.com/tibaes/motion/blob/master/clustering/symbolic%20divergence/KL%20Divergence%20by%20MC.nb) and [Variational](https://github.com/tibaes/motion/blob/master/clustering/symbolic%20divergence/KL%20Divergence%20by%20Aprox.nb) approaches; and also the C++ code for the [variational](https://github.com/tibaes/motion/blob/master/clustering/compKLVar.cpp) KL. Remember that these codes are experimental, use at your own risks.

# Final remarks
If you need to code something with Kullback Leibler divergence, I strongly recommend you to read the article I used as reference. However, sometimes it is hard to understand all the statistical concepts, so I wrote this article to provide an overview of the problem. I am not a pro in statistics, but if you need some assistance to understand the equations or the code, don't hesitate to contact me. Also, this is my first draw about this subject, but I plan to improve this post+

# References
1. Hershey, J. and Olsen, P. (2007). Approximating the kullback leibler divergence between gaussian mixture models. In Acoustics, Speech and Signal Processing, 2007. ICASSP 2007. IEEE International Conference on, volume 4, pages IV–317–IV–320.

