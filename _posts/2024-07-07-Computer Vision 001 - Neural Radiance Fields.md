---
title: Computer Vision 001 - Neural Radiance Fields
description: An overview of NeRF, covering its theory and applications with a demo
date: 2024-07-07 20:00:00 -0800
categories: [Tutorials, Computer Vision]
tags: [view synthesis, 3d]     # TAG names should always be lowercase
toc: True
image: ./image 1.png
---

# Introduction

Neural Radiance Field, commonly known as NeRF, represents a groundbreaking approach in the field of computer vision and graphics. NeRF uses deep learning to synthesize novel views of complex 3D scenes, achieving high-quality results that were previously unattainable with traditional methods. This blog post will overview the details of NeRF, explaining its core concepts, theory, and exploring its various applications. We'll also have a demo at the end of the post to show give a hands-on example of what we'll be discussing.

# What is NeRF?

Let's look at what the original EECV 2020 Oral said about their method:

'''
[NeRF is] a method that achieves state-of-the-art results for synthesizing novel views of complex scenes by optimizing an underlying continuous volumetric scene function using a sparse set of input views. Our algorithm represents a scene using a fully-connected (non-convolutional) deep network, whose input is a single continuous 5D coordinate (spatial location (x, y, z) and viewing direction (θ, φ)) and whose output is the volume density and view-dependent emitted radiance at that spatial location.
'''

# Demo

Now that the theory is out of the way, let's dive in to the demo below. You'll be able to run this on colab, though you may need a gpu to run this in a reasonable amount of time.

https://colab.research.google.com/drive/1jdNBYahqNGEA9mXZKEoolOTKShXr1dhK#offline=true&sandboxMode=true