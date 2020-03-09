# AutoML-Zero

This directory contains the open source code for the paper:

\"**AutoML-Zero: Evolving Machine Learning Algorithms From Scratch**\" 
*E Real\*, C Liang\*, DR So, and QV Le \(\*equal contribution)*

## What is AutoML-Zero

AutoML-Zero aims at automatically discovering computer programs to solve supervised machine learning tasks, starting from empty or random programs and using only basic mathematical operations as building blocks. Despite the large search space, the evolutionary search demonstrates promising results by discovering linear regression, 2-layer fully connected neural networks with backpropagation, and even algorithms better than hand designed baselines of comparable complexity. Below is an example of a sequence of discoveries using binary classification tasks extracted from CIFAR-10: ![GIF for the experiment progress](progress.gif)

In our framework, an algorithm is represented as a triplet of component functions called ```Setup```, ```Predict```, and ```Learn```. To evaluate an algorithm, the ```Setup``` function is executed once at the beginning, the ```Predict``` and ```Learn``` functions are then executed once for each training example, and finally the ```Predict``` is executed once for each validation example to generate the predictions. All the instructions in the three functions are evolved: instructions can be inserted or removed, their arguments and output variables can be altered, and the operations used to combine those arguments can be modified. We also allow a variable number of instructions. The best evolved algorithm performs better than hand designed baselines of comparable complexity, e.g., logistic regression or two-layer fully connected neural networks, even when evaluating on other datasets. Most importantly, the evolved code is *interpretable*. Our paper analyzes the best evolved algorithm and finds that it applies techniques like bilinear interactions, weight averaging, normalized gradient and adding noise to inputs, which is shown below:

![GIF for the interpretation of the best evolved algorithm](best_algo.gif)

&nbsp;

## 5-Minute Demo: Rediscovering Linear Regression From Scratch

Considering the problem of linear regression provides a miniature version of the experiments in the paper. Confronted with this problem, a human designer might write the following algorithm:

```
TODO(ereal): write linear regression algorithm.
```

In this human-designed case, the ```Setup``` function establishes a learning rate, the ```Predict``` function applies a set of weights to the inputs, and the ```Learn``` function corrects the weights in the opposite direction to the gradient. In other words, a linear regressor trained with gradient descent.

*Can an evolutionary search discover linear regression?*

To answer this question, you can try the script below. It applies an experimental paradigm similar to that of our paper. The paradigm is to run evolution experiments on 10 linear *search tasks* (see paper). After each experiment, it evaluates the best algorithm discovered on 100 *selection tasks*. Once an algorithm attains a fitness (1 - RMS error) greater than 0.9999, it is selected for a final evaluation on 100 *unseen tasks*. To conclude, the demo prints the results of this one-time final evaluation and shows the code for the corresponding algorithm.

For the purposes of this demo, we use a much smaller search space: only the operations necessary to implement linear regression are allowed and the programs are constrained to a short, fixed length. This way, the demo will typically discover code similar to linear regression by gradient descent in under 5 minutes using 1 CPU.

First install `bazel` following instructions here, then run the demo with:

```
./run_demo.sh
```

Repeated runs will use different random seeds. Note that the runtime may vary
widely due to the random initial conditions and hardware.

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

&nbsp;

<sup><sub>
Search keywords: machine learning, neural networks, evolution,
evolutionary algorithms, regularized evolution, program synthesis,
architecture search, NAS, neural architecture search,
neuro-architecture search, AutoML, AutoML-Zero, algorithm search,
meta-learning, genetic algorithms, genetic programming, neuroevolution,
neuro-evolution.
</sub></sup>
