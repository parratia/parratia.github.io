---
title: "Enhancing Dynamic CT Image Reconstruction with Neural Fields and Motion Models"
excerpt: "Brief description of results obtained in [this article](https://arxiv.org/abs/2406.01299v1)"
collection: portfolio
---

The ground truth is two squares moving around some background. 

Once WarpPINN has been trained, we can apply it on the nodes of a segmentation of the left ventricle to visualise how it performs and how it tracks the motion: 

<image src="/images/two_squares.gif" /> 

The following image represents the Strain curves obtained:

![Alt text](/images/strain_curves-1.png)

Jacobian obtained by WarpPINN at end-systole with regularizer $\mu=10^{-5}$ for all volunteers. The wireframe represents the end-diastolic configuration.

![Alt text](/images/jacobian1e-05-1.png)
