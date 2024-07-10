---
title: Computer Vision 001 - Neural Radiance Fields
description: An overview of NeRF, covering its theory and applications with a demo
date: 2024-07-07 20:00:00 -0800
categories: [Tutorials, Computer Vision]
tags: [view synthesis, 3d]     # TAG names should always be lowercase
toc: True
image: https://drive.google.com/thumbnail?id=1-0gFgIdimZyNOEAyzN9r97UZvFaJ8BRq&sz=w1000
---

# Introduction

Welcome to the first Computer Vision tutorial of my blog. While NeRF may be a bit advanced for a first post and not really a classical computer vision algorithm, I believe it is a great way to start off the series.

Neural Radiance Field, commonly known as NeRF, is a groundbreaking approach in the field of computer vision and graphics that was published in 2020. NeRF uses deep learning to synthesize novel views of 3D scenes, achieving photo-realisitc results that were previously unattainable with traditional methods. Moreover, follow-up works allow better performance or the ability to convert the network into a 3d model that can be used in application such as Blender. This blog post will overview the details of NeRF, explaining its core concepts, theory, and exploring its various applications. We'll also have a demo at the end of the post to show give a hands-on example of what we'll be discussing.

# What is NeRF?

Let's look at what the original ECCV 2020 Oral said about their method:

> [NeRF is] a method that achieves state-of-the-art results for synthesizing novel views of complex scenes by optimizing an underlying continuous volumetric scene function using a sparse set of input views. Our algorithm represents a scene using a fully-connected (non-convolutional) deep network, whose input is a single continuous 5D coordinate (spatial location (x, y, z) and viewing direction (θ, φ)) and whose output is the volume density and view-dependent emitted radiance at that spatial location.

Let's break this passage down. Essentially, NeRF allows us to query the RGB and volume density of a specific ray of light. The method takes in the viewing parameters of a "camera" in space from which beams of light are blasted into a scene. The key point of NeRF is that these beams of light "pass" through objects and don't stop when hitting a surface; instead, each point in space carries some density that "absorbs" the light from the ray passing through it. From these rays of light, we can query the color and density of the scene at any point. In combination with a volumetric rendering algorithm, we can then render a 3D scene from any viewpoint.

# NeRF Theory

Let's dive into the theory of NeRF. As discussed before, the goal of NeRF is to represent a continuous scene as a 5D function that takes in a spatial location and viewing direction and outputs the volume density and view-dependent emitted radiance at that spatial location. This 5D function is represented by a fully connected neural network, which is trained using a set of input views of the scene.

Using this representation, we can compute the color of a ray of light passing through the scene by using the following volume rendering equation:

$$
C = \int_{t_{near}}^{t_{far}} \tau(s) \rho(s) L_e(s) ds
$$

Where:


# Limitations

One of the main limitations of NeRF is its computational complexity. The original NeRF paper requires a large amount of memory and computation to train and render scenes. This is because the method requires a large number of input views to train the model, and the model itself is quite large (if you don't use the miny version like we did in the demo). This makes it difficult to scale NeRF to larger scenes or more complex scenes. However, there have been several follow-up works that aim to address these limitations, such as Mip-NeRF.

Another limitation is training. NeRF requires a large number of input views to train the model effectively. This can be time-consuming and computationally expensive, especially for complex scenes. Additionally, the NeRF model, being a filly connected network, is shown to be slow at learning high frequency details in the scene. The follow-up work "Fourier Features Let Networks Learn High Frequency Functions in Low Dimensional Domains" addresses this issue by using a Fourier feature mapping to allow the network to learn high frequency details more efficiently.

# Demo

Now that the theory is out of the way, let's dive in to the demo below. You'll be able to run this on colab, though you may need a gpu to run this in a reasonable amount of time.

https://colab.research.google.com/drive/1jdNBYahqNGEA9mXZKEoolOTKShXr1dhK#offline=true&sandboxMode=true