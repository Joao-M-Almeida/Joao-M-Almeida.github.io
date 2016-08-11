---
layout: post
title: Genetic Algorithms in one night
tldr:  Tonight I decided to implement a genetic algorithm to take care of the parameter optimization for my master thesis.
---

## __TL;DR__

Tonight I decided to implement a genetic algorithm to take care of the parameter optimization for my master thesis. I wanted to do it in one night, but ended up spending a couple of hours on the following day fixing some stuff. You can find the resulting code [here](https://gist.github.com/Joao-M-Almeida/06972e6a4c005a3f9c37f36e9892bcf9).

## Why? How?

I have to optimize 5 models, each with more than 4 continuous parameters for my master thesis and I got tired of hand tuning them.

So I decided to spend one night trying to implement a Genetic algorithm to optimize the parameters for me. Up until now I had been doing a mix of a grid search and hand picking parameter values to try to improve on the RMSE score of my models.

I have been working in Python 2.7 on my thesis so I decided to use and to make the implementation generic so it could be used in other projects.

## What do I need from the models to optimize?

- __Objective function__: The function that we want to maximize.
  - _input_: parameter tuple;
  - _output_: score from 0 to 1;


- __List of valid values for each parameter__: Let's consider only discrete values, a continuous parameter can be discretized;

## What do I need to implement?

### Individual Class


#### Attributes

An individual consists of:

- __Genome__: parameter tuple;
- __score__: Objective function value if already known;

#### Methods

- __get_score__: Returns score of Individual
- __set_score__: Sets score of Individual
- __to_string__: Represents Individual in string format


### Genetic algorithm class



#### Methods

- __generate_individual__: Sample parameter space to generate element for population;
  - _output_: One valid parameter tuple to add to test population;


- __crossover__: Mix two individuals to create next generation individual;
  - _input_: 2 parameter tuples, score of each individual;
  - _output_: New individual;

For the crossover instead of just giving equal probability to the parameters of each individual I decided to give a probability based on their score:

$$P_a = \frac{s_a}{s_a + s_b}$$

- __mutate__: Change one individual to replicate the mutation mechanism that exists in nature;
  - _input_: Individual to be mutated;
  - _output_: New individual;


## Notes

I used tuples to represent genomes to guarantee same length
