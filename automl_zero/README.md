# AutoML-Zero

Open source code for the paper: \"[**AutoML-Zero: Evolving Machine Learning Algorithms From Scratch**](https://github.com/google-research/google-research/tree/master/automl_zero)"

| [Introduction](#what-is-automl-zero) | [Quick Demo](#5-minute-demo-discovering-linear-regression-from-scratch)| [Reproducing Search Baselines](#reproducing-search-baselines) | [Citation](#citation) |
|-|-|-|-|

## What is AutoML-Zero?

AutoML-Zero aims at automatically discovering computer programs to solve machine learning tasks, starting from empty or random programs and using only basic math operations. The goal is to simultaneously search for all aspects of an ML algorithm (e.g., the model structure and the learning strategy), while employing *minimal human bias*. Despite the challenging search space for AutoML-Zero, evolutionary search showed promising results by discovering linear regression, 2-layer neural network with backpropagation, and even algorithms better than hand designed baselines of comparable complexity. An example sequence of discoveries is shown below.  

![GIF for the experiment progress](progress.gif)

More importantly, the evolved algorithms can be *interpreted*. Below is an analysis of the best evolved algorithm, which "invents" techniques like bilinear interactions, weight averaging, normalized gradient and adding noise to inputs.

![GIF for the interpretation of the best evolved algorithm](best_algo.gif)



&nbsp;

## 5-Minute Demo: Discovering Linear Regression From Scratch

As a miniature "AutoML-Zero" experiment, let's try to automatically discover programs to solve linear regression tasks. 

To get started, first install `bazel` following instructions [here](https://docs.bazel.build/versions/master/install.html), then run the demo with:

```
./run_demo.sh
```


This script runs evolutionary search on 10 linear tasks (*T<sub>search</sub>* in the paper). After each experiment, it evaluates the best algorithm discovered on 100 new linear tasks (*T<sub>select</sub>* in the paper). Once an algorithm attains a fitness (1 - RMS error) greater than 0.9999, it is selected for a final evaluation on 100 *unseen tasks*. To conclude, the demo prints the results of the final evaluation and shows the code for the automatically discovered algorithm.

For the purposes of this demo, we use a much smaller search space: only the operations necessary to implement linear regression are allowed and the programs are constrained to a short, fixed length. This way, the demo will typically discover code similar to linear regression by gradient descent in under 5 minutes using 1 CPU (Note that the runtime may vary due to the random seeds and hardware). We saw similar discoveries in the unconstrained search space, although at a higher compute costs. 

Compare that with the solution from a human ML researcher (one of the authors):

```
TODO(ereal): write linear regression algorithm.
```

In this human-designed case, the ```Setup``` function establishes a learning rate, the ```Predict``` function applies a set of weights to the inputs, and the ```Learn``` function corrects the weights in the opposite direction to the gradient. In other words, a linear regressor trained with gradient descent.

&nbsp;

## Reproducing Search Baselines

The following command can be used to reproduce the results in Supplementary
Section 9 ("Baselines") with the "Basic" method on 1 process (1 CPU):

*[To be continued, ETA: March, 2020]*

If you want to use more than 1 process, you will need to code a way to
parallelize the computation based on your particular distributed-computing
platform. A platform-agnostic description of what we did is given in our paper.

We left out of this directory upgrades for the "Full" method that are
pre-existing (hurdles) but included those introduced in this paper (e.g. FEC
for ML algorithms).

## Citation

If you use the code in your research, please cite:

`TODO`

&nbsp;

<sup><sub>
Search keywords: machine learning, neural networks, evolution,
evolutionary algorithms, regularized evolution, program synthesis,
architecture search, NAS, neural architecture search,
neuro-architecture search, AutoML, AutoML-Zero, algorithm search,
meta-learning, genetic algorithms, genetic programming, neuroevolution,
neuro-evolution.
</sub></sup>
