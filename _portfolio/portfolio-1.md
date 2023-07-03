---
title: "WarpPINN"
excerpt: "Brief description of results obtained in [WarpPINN](https://arxiv.org/abs/2211.12549)"
collection: portfolio
---

Once WarpPINN has been trained, we can apply it on the nodes of a segmentation of the left ventricle to visualise how it performs and how it tracks the motion: 

<image src="/images/warpPINN.gif" /> 

The following image represents the Strain curves obtained:

![Alt text](/images/strain_curves.pdf)

Jacobian obtained by WarpPINN at end-systole with regularizer $\mu=10^{-5}$ for all volunteers. The wireframe represents the end-diastolic configuration.

![Alt text](/images/jacobian1e-05.pdf)
