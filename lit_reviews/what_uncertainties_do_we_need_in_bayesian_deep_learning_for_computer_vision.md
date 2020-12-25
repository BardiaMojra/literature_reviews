# What Uncertainties Do We Need in Bayesian Deep Learning for Computer Vision?

By Alex Kendall and Yarin Gal

[paper](https://arxiv.org/abs/1703.04977)

## In a Nutshell

The paper focuses on quantifying two major types uncertainty in machine
learning models, aleatoric and epistemic. Such capabilities are features
of using Bayesian Neural Networks in **Deep Learning** which was 
introduced in [Uncertainty in Deep Learning](http://www.cs.ox.ac.uk/people/yarin.gal/website/blog_2248.html).

For analyzing uncertainty, authors present a Bayesian framework that
combines input-dependent aleatoric uncertainty with epistemic uncertainty.

Moreover, using their new framework they studied models with per-pixel
semantic segmentation and depth regression applications. This led to the
development of new loss functions (**loss attenuation**) for which it is 
more robust to noisy data and is comparable to state-of-the-art.

## Definitions

**Epistemic uncertainty** is what a model does not know due to the 
incompleteness of training data. Epistemic uncertainty decreases (but it 
will never be equal to zero) as training data is expanded. It is also 
referred to as **model uncertainty**.

**Aleatoric uncertainty** is the uncertainty caused by the natural stochasticity of observation. It can be further categorized into two groups, **homoscedastic**, and **heteroscedastic**.

**Homoscedastic uncertainty** is a type of **aleatoric uncertainty** that is constant with respect to model input.

**Heteroscedastic Uncertainty** is a type of **aleatoric uncertainty** 
that depends on model input. For example, for depth regression, different 
textures and vanishing lines can result in different degrees of certainty 
in the model.  

![Uncertainty](https://miro.medium.com/max/700/1*5vj9r-scd3fEKHRXnqqurg.png)



## Bayesian Neural Network - BNN 
Bayesian neural networks use PDF's (probabilistic distribution function) 
for network weight parameters and then average over all possible 
parameters, this is also referred to as **marginalization**. This is in 
comparison to classical neural networks and CNN's where we use 
deterministic weight parameters and then optimize network weights for the 
best output prediction. 

"Bayesian nets are easy to formulate yet difficult to perform inference 
in." 

"Dropout variational inference is a practical approach for approximating 
inference in large and complex models." This was presented in [Bayesian Convolutional Neural Networks with Bernoulli Approximate Variational Inference](https://arxiv.org/abs/1506.02158).




