---
title: "Enhancing Dynamic CT Image Reconstruction with Neural Fields and Motion Models"
excerpt: "Brief description of results obtained in [this article](https://arxiv.org/abs/2406.01299v1)"
collection: portfolio
---

The ground truth is two squares moving around some background. 

Once WarpPINN has been trained, we can apply it on the nodes of a segmentation of the left ventricle to visualise how it performs and how it tracks the motion: 

<image src="/images/two_squares.gif" /> 

<image src="/images/full_batch_g_0.01.gif" /> 

<image src="/images/mb_g_0.01.gif" /> 

<image src="/images/full_batch_g_0.gif" /> 

