# Obtaining Well Calibrated Probabilities Using Bayesian Binning

+ [code](https://github.com/pakdaman/calibration/)
+ [paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4410090/)

## Introduction

In this paper, the authors propose a novel calibration method for probabilistic
predictive models. Bayesian Binning into Qualities (BBQ), is a non-parametric
and post-processing calibration method. Their proposed method is a binary classifier calibration method is based on the histogram-binning calibration method ([Zadrozny and Elkan 2001](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.29.3039&rep=rep1&type=pdf)). It is important to note this method could be extended to
multi-class classification tasks, ([Zadrozny and Elkan 2002](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.13.7457&rep=rep1&type=pdf)).

## Problem Statement

In machine learning, classification problems are often solved by deploying a
a predictive model trained on some given data set but often under perform and
make miscalibrated predictions ("classifier score"). Statistically speaking, for
a calibrated prediction of i.e. 40%, there will be an occurrence of 40% for a
give test set that is 1) large enough with respect to solution space size, 2)
test data set is randomly selected (for more insight read on
 _Central Limit Theorem_).


Figure 1 is a reliability curve (DeGroot and Fienberg 1983; Niculescu-Mizil and
Caruana 2005) that is used as an example of a predictive model with poorly
estimated probabilities.

Figure 1:
![Fig 1](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4410090/bin/nihms679964f1.jpg)

## Related Work

Mainly, calibration is done two ways 1) _ab initio_, by modifying objective
function which increases computational cost. 2) It can be done as a
post-processing procedure. Post processing can be categorized into parametric
and non-parametric. Platt's method is an example of parametric calibration,
[Platt 1999). Non-parametric methods include histogram binning (Zadrozny and Elkan
2001), Platt scaling (Platt 1999), and isotonic regression (Zadrozny and Elkan
2002).

## Method

BBQ is an extension of simple histogram binning method ([Zadrozny and Elkan 2001](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.29.3039&rep=rep1&type=pdf)), with added capability to consider different binning models (different number
of bins) and their combinations under a Bayesian frame work ([Heckerman, Geiger,
 and Chickering,
1995](https://link.springer.com/content/pdf/10.1007/BF00994016.pdf)).
The generated Bayesian score is provides further insight into Bayesian network
structure and is used for combining binning models.

$$ \textit{Score}(M) ~=~ P(M)~.~P(D | M) $$

The marginal likelihood, $P(D | M)$, has a closed form solution under the
following 3 conditions,
([Heckerman, Geiger, and Chickering, 1995](https://link.springer.com/content/pdf/10.1007/BF00994016.pdf)):

1. All samples are under i.i.d. assumption and the class distribution $P(Z|B=b)$,
which is class distribution for bin b, with a binomial distribution with
parameter $θ_b$.
2. Bin distributions are independent.
3. The prior distribution over binning model parameters $θ$'s are modeled using a
Beta distribution.

Marginal likelihood closed form, ([Heckerman, Geiger, and Chickering, 1995](https://link.springer.com/content/pdf/10.1007/BF00994016.pdf)):

$$
P(D|M) = \prod_{b=1}^{B} \frac{\Gamma(\frac{N'}{B})}{\Gamma (N_b + \frac{N'}{B})}
\frac{\Gamma (m_b + \alpha_b)}{\Gamma (\alpha_b)}
\frac{\Gamma (n_b + \beta_b)}{\Gamma (\beta_b)}
$$

Where:

+ $\Gamma(n) = (n-1)!$
+ $N_b$ : total number of training instances in the $b$'th bin
+ $n_b$ : total instances of class *zero* among all training  instances $N_b$
+ $m_b$ : total instances of class *one* among all training instances $N_b$
+ P(M) : prior distribution of binning model M, uniform distribution for initial
 condition

The above equation is used for model averaging by BBQ, they point out that mentioned
Bayesian scores could be used for model selection. Per Hoeting (Hoeting et al. 1999),
model averaging is superior to model selection methods.

## BBQ
BBQ frame work defines calibrated prediction as:

$$
P(z=1|y) = \sum_{i=1}^{T} \frac{\textit{Score}(M_i)}{\sum_{j=1}^{T} \textit{Score}(M_j)}
~.~ P(z=1 | y, M_i)
$$

Where:

+ $T$ : total number of binning models considered
+ $P(z=1 | y, M_i)$ : probability estimate using model $M_i$ for uncalibrated
classifier output y.

## Calibration Measures

+ ECE: Expected Calibration Error is calculated over the bins
+ MCE: Maximum Calibration Error is calculated among the bins

$$
ECE = \sum_{i=1}^{K}P(i).|o_i - e_i| ~~,~~ MCE= \max\limits_{i=1}^{K}(|o_i-e_i|),
$$

Where:

+ $o_i$ : true fraction of positive instances in the i$^{th}$ bin
+ $e_i$ : mean of the post-calibrated probabilities in the i$^{th}$ bin
+ $P(i)$ : empirical probability (fraction) of all instances in the i$^{th}$ bin


## Empirical Results

+ Acc : accuracy
+ AUC : area under the ROC curve (receiver operator characteristic curve)
+ RMSE
+ ECE
+ MCE
