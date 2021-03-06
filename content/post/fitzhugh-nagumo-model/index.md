---
title: FitzHugh-Nagumo model
subtitle: "This two-dimensional system of PDE models an excitable system such as
  electric signals on heart tissue. It is solved by means of a finite
  differences scheme. Also, an inverse problem is established and partially
  solved: reconstruct cardiac tissue properties by using measurements available
  from an ECG. Code available on github upon request."
date: 2021-02-15T16:24:21.868Z
summary: "This two-dimensional system of PDE models an excitable system such as
  electric signals on heart tissue. It is solved by means of a finite
  differences scheme. Also, an inverse problem is established and partially
  solved: reconstruct cardiac tissue properties by using measurements available
  from an ECG. Code available on github upon request."
draft: false
featured: false
image:
  filename: featured
  focal_point: Smart
  preview_only: false
---
## Overview

Heart disease is one of the leading causes of death in the world, thus it is necessary a fully-understanding of its biomechanical behaviour. One attempt to do so is the FitzHugh-Nagumo model, one of the most successful mathematical models that describe excitable media, that is, materials consisting of elementary segments with well-defined rest state, a threshold for excitation and a diffusive-type coupling to its nearest neighbours. Hence, this model is useful for modelling different phenomena such as nerve pulses, spreading of forest fires or certain types of chemical reactions. In particular, it is used in cardiac electrophysiology to qualitatively describe the voltage propagation through the cardiac tissue. Consequently, from this model, it is possible to gain some insights about heart imparities such as arrhythmias.  

The most important characteristic of excitable media is the almost immediate damping out of signals below a certain threshold. On the other hand, signals exceeding this threshold propagate without damping. In cardiac cells, ions move through small pores in the cellular membrane which can be either open (excited) or closed (rest) making the heart muscle pumping blood in and out.

In what follows, the equation is described, a direct model is solved with a finite differences scheme and an inverse problem is established to reconstruct properties of the heart tissue from measurements given by an ECG

## The equation

The FitzHugh-Nagumo model is a system of two variables and two PDEs. The variables are an **activator** (the electric potential $V$) and an **inhibitor** (a variable $R$ that describes the voltage-dependent probability of the pores in the membrane being open and ready to transmit ionic current). The potential follows a diffusion process with a non-linear term.     

$$\begin{array}{ll}\dfrac{\partial V}{\partial t}= div(\sigma\nabla V)+\nu V(\alpha-V)(V-1)- R + I & \text{, in }\Omega\times[0,T] \\\\
\dfrac{\partial R}{\partial t}=\delta (V-Rd) & \text{, in } \Omega\times[0,T] \\\\
\dfrac{\partial V}{\partial n}= 0 & \text{, on } \partial \Omega \times [0,T] \\\\
V(x,0) = V\_0 & \text{, for } x\in\Omega \\\\
R(x,0) = R\_0 & \text{, for } x\in\Omega
\end{array}$$
where
- $V(t,x)$: the voltage or transmembrane potential in the point $x\in\Omega$ and time $t\in[0,T]$. 
- $R(t,x)$: inhibitor or recovery variable.
- $\sigma(x)$: conductivity of the tissue that may depends on $x\in\Omega$. Moreover, $\sigma(x)\geq0$ and if $\sigma(x)=0$ then the tissue on the point $x\in\Omega$ is dead and no diffussion may occur.
- $\nu$: excitation rate, with $\nu>0$.
- $\alpha$: threshold for excitation, with $0<\alpha<1/2$.
- $\delta$: excitation decay, with $0<\delta$.
- $d$: recovery decay, with $d>0$.
- $I$: stimulating current. 

## Direct problem. Solving the equation with finite differences

A Crank-Nicolson scheme is used to numerically solve the system, i.e., a convex comibination between the explicit and implicit schemes with parameter $\theta$:

$$\begin{array}{cll}
 \dfrac{V^{n+1}\_{i,j}-V^n\_{i,j}}{\Delta t}&=&\theta\sigma\_{i,j} \left(\dfrac{V^{n}\_{i,j+1}-2V^{n}\_{i,j}+V^{n}\_{i,j-1}}{h\_x^2}+\dfrac{V^{n}\_{i,j}-2V^{n}\_{i,j}+V^{n}\_{i-1,j}}{h\_y^2}\right) \\\\
 &&+\theta\left((\sigma\_x)\_{i,j}\dfrac{V^n\_{i,j+1}-V^n\_{i,j}}{h\_x}+(\sigma\_y)\_{i,j}\dfrac{V^n\_{i+1,j}-V^n\_{i,j}}{h\_y}\right) \\\\
 &&+(1-\theta)\sigma\_{i,j} \left(\dfrac{V^{n+1}\_{i,j+1}-2V^{n+1}\_{i,j}+V^{n+1}\_{i,j-1}}{h\_x^2}+\dfrac{V^{n+1}\_{i,j}-2V^{n+1}\_{i,j}+V^{n+1}\_{i-1,j}}{h\_y^2}\right) \\\\
 &&+(1-\theta)\left((\sigma\_x)\_{i,j}\dfrac{V^{n+1}\_{i,j+1}-V^{n+1}\_{i,j}}{h\_x}+(\sigma\_y)\_{i,j}\dfrac{V^{n+1}\_{i+1,j}-V^{n+1}\_{i,j}}{h\_y}\right) \\\\
 &&+\nu V^{n}\_{i,j}(V^{n}\_{i,j}-\alpha)(1-V^{n}\_{i,j})- \theta \delta R^{n}\_{i,j}-(1-\theta)\delta R^{n+1}\_{i,j} \\\\
\dfrac{R^{n+1}\_{i,j}-R^n\_{i,j}}{\Delta t}&=&\theta\delta (V^{n}\_{i,j}-R^{n}\_{i,j}d)+(1-\theta)\delta (V^{n+1}\_{i,j}-R^{n+1}\_{i,j}d) \end{array}$$ 

### Simulations

#### Normal heart   

{{< video library="true" src="Corazon_sano.mp4" controls="yes" >}}

#### Reentrant waves

{{< video library="true" src="Corazon_no_sano.mp4" controls="yes" >}}

#### Ventricular fibrilation  

{{< video library="true" src="Fibrilacion.mp4" controls="yes" >}}

### Code and Poster

{{% staticref "media/Poster_EDPN.pdf" "newtab" %}}You can download a poster here{{% /staticref %}}. 

## Inverse problem

For this toy model, we could suppose as known the parameters $\num \alpha, \delta$ and $d$ while $\sigma$ remains unknown. This function contains information about the properties of the cardiac tissue, hence, it would be helpful to know it and make a good prognosis. The inverse problem proposed is to reconstruct this function $\sigma$ from measurements obtained from an ECG.

An ECG is a graph of voltage versus time that describes the electrical activity in the heart from electrodes located in the skin. 
