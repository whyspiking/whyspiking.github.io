---
layout: default
---

Since the rise of Deep Learning, neural networks have become a household name.  Deep neural nets now achieve state of the art results in almost all areas of machine learning and computer vision.

So successful have they been that people sometimes forget their unloved and more homely cousins - spiking neural networks.  Spiking networks have a long history of being very promising, but not really working.  We believe this is about to change.  

This website came about because reviewers often questioned the basic reasons behind what we are doing.  Rather then repeatedly defend the ideas behind spiking networks, we will now refer to:

---

# The Spiking Manifesto

...

## What are spiking networks?

...

## Why should we use them?


1) Asynchrony

Imagine the following situation:

You have a robot, running on a conventional deep network, possibly with recurrent  or connections.  It has many sensors, and those sensors are running at different rates.  A gyroscope may be running at 1000Hz, and a camera may be running at 30Hz.  All of these signals are relavent to action, and we want to act on a signal from the moment it comes it.  

Presumably, we'll want to fuse these sensory signals into some kind of latent representation of the word.  We may, for instance, have the following architecture:

![multi-rate](https://docs.google.com/drawings/d/1fTgn1gKVK92OBBp6H8Muwpal7oVVCizpgPJ9APVbPog/pub?w=721&h=188)

The question arises: How often should we update the joint representation?  If we update at the rate of the fastest sensor, we're doing a huge amount of repeated computation, since we recompute the entire joint network for each new gyro signal, even though the image is fixed.  If we update at the rate of the slowest sensor, we have to wait for the next frame of the camera arrives before we're able to respond to something from the gyro.  Neither of these options is really satisfying.

What we want is a network that accepts data once it arrives, and can do a partial-update of its state to accomodate this new data.  In order to be computationally tractable, a partial update should cost substationally less than a full update of the network.

This is where spiking networks come in.


2) Efficiency


<iframe  title="Tiger Walk" width="480" height="390" src="https://youtu.be/1i9wgX_JN54" frameborder="0" allowfullscreen></iframe>



3) 


---

