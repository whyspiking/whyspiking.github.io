---
layout: default
---

Since the rise of Deep Learning, neural networks have become a household name.  Deep neural nets now achieve state of the art results in almost all areas of machine learning and computer vision.

So successful have they been that people sometimes forget their unloved and more homely cousins - spiking neural networks.  Spiking networks have a long history of being very promising, but not really working.  We believe this is about to change.  

This website came about because reviewers often questioned the basic reasons behind what we are doing.  Rather then repeatedly defend the ideas behind spiking networks, we will now refer to:

---

# The Spiking Manifesto

In the last 5 years, the machine learning community has recognized that Deep Learning if going to be central to the future of the field. Deep Learning allows for the creation of models that can learn an arbitrary number of levels of abstraction. This appears to be important when trying to parse abstract concepts (e.g. the presence of a cat, a bird flapping it’s wings, or a car turning) from raw
data. In 2012, the ImageNet competition (a competition for recognizing objects in natural images) was won by Krizhevsky et al. with the use of a Deep Neural Network. Every year since then, ImageNet, as well as many other machine learning competitions, have been dominated by variations on Deep Neural Networks.  

## So, what's wrong with Deep Learning?

"If it ain't broke, don't fix it", they say.  Here's what's broke about Deep Learning:

### (mis-)Handling Multi-Rate Data


Let’s imagine we are trying to train a robot to perform some task. Typically, robotic systems have many sensors running at different rates. We assume that we want to merge all these sensory representations into some unified abstract representation of the world around our robot, and make decisions (via motor controls) based on this representation. 

![multi-rate](https://docs.google.com/drawings/d/1fTgn1gKVK92OBBp6H8Muwpal7oVVCizpgPJ9APVbPog/pub?w=721&h=188)

The above figure shows a schematic of how such a network may be structured. Various sensors, with vastly different update rates, are fed into the network, and it uses these sensory inputs, along with its previous state, to decide on some motor actions. The problem is how to update this system. We may chose to update the network at the rate of the fastest sensor - the gyro - but this involves doing many updates on our joint representation with a fixed set of features coming from the camera - a very redundant computation. Or we may chose to update at the rate of the slowest sensor - the camera - and process a temporally binned version of the recent gyro signal, but then lose the ability to update our motor signal quickly in response to changes in the gyro. So we have a tradeoff between efficiency and low-latency.  

### Inefficiency
Current approaches to deep learning can be obscenely inefficient when processing natural data.  Suppose we want to keep track of the some variable relating to the tiger in the following figure. You may, as a human, be trying to evaluate the threat posed by such an animal. How fast it is moving, whether it is coming towards you, and how hungry it looks, are important variables in this decision. Using the traditional way of doing deep learning, we would feed each individual frame into a neural network, and recompute our estimated variables. This, of course, involves doing a huge amount of redundant computation. It is much better to feed in sparse data that represents what has changed, and update our estimated variables based on that.

![tiger-walk](https://docs.google.com/drawings/d/1AbM0UFIwlQ1MNZyUKQWNxiDIIXFwqn4BCPMEEfeQdC8/pub?w=595&h=199)

The temporal sparsity may not be restricted to the raw input. Higher level features (for example, the presence of a triangular ear or a salivating feline tongue), will persist over time, and should not have to be continually re-reported through feedforward or recurrent connections in order to maintain a model of the state of the tiger.


## How can Spiking Help?

What we need is a way to efficiently implement a deep neural network in a setting with temporally sparse, variable-rate data.

### What is "spiking" anyway?
“Spiking Neural Network” is not a very strictly defined term. Loosely, it refers to a type of network that was inspired by biological neural networks. Such networks consist of neurons that have some persistent “potential’, and alter each-others’ potentials by sending “spikes” to one another. When unit i sends a spike, it increments the potential of each downstream unit j in proportion to the synaptic weight Wi,j connecting the units. If this increment brings unit j’s potential past some threshold, unit j sends a spike to its downstream units. Such systems therefore have the interesting property that the amount of computation done depends on the contents of the data, rather than the size of the network, since a neuron may be tuned to produce more spikes in response to some pattern of inputs than another.  Spiking networks allow us to circumvent the efficiency-latency tradeoff discussed in Section 2. If a spike is particularly important for predicting the variable of interest, the network will learn to give a higher weight to that event, and for it to propagate quickly through the network. Rather than have a global network update - data is simply pushed into the network as it arrives. Neurons will update their state only upon receiving input from other neurons, and can learn to fire spikes only when important data arrives.

Because of these properties, there has been a great deal of investment in hardware to efficiently run spiking neural networks. IBM’s TrueNorth, and University of Manchester’s Spinnaker are examples. But thus far, there has been no clear use for these technologies. The problem appears to be a lack of effective ways to train spiking neural networks.

### The Asynchrony Argument 
...


### The Efficiency Argument 
...


### The Hardware Argument 
...

### The Biological-Plausibility Argument
...

---