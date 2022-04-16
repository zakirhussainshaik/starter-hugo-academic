---
title: " Channel Hardening and Favorable Propagation"
subtitle: Technical jargons made simple
date: 2022-04-04T07:31:54.876Z
draft: false
featured: false
categories:
  - Technical
image:
  filename: featured
  focal_point: Smart
  preview_only: false
---
5G is around the corner and soon will be deployed worldwide. If one has been following the technical community closely, we may know that “Massive MIMO” is one of the key enabling technology in 5G. If someone is not aware what the acronym MIMO stands for, MIMO actually stands for multiple-input-multiple-output. Here, the multiple input corresponds to the multiple-transmit antennas that can send various signals by multiplexing, and multiple-output corresponds to multiple users to which the base station will be serving. The word “Massive” indicates that the base station has very large number of antennas, practically 64 antennas and more. For more information, refer to: https://ma-mimo.ellintech.se/2020/05/13/how-massive-are-the-current-massive-mimo-base-stations/

One may wonder what makes Massive MIMO so special than its pioneering technology MIMO, except that it has a massive number of antennas rather than four to eight antennas. One immediate benefit that one can easily guess is that with a very large number of antennas, the various gains and benefits Massive MIMO networks can provide over standard MIMO networks (4-8 antennas) will be significant. However, two key important features of Massive MIMO make this technology unique compared to MIMO technology. They are channel hardening and favourable propagation.

To mathematical understand these concepts, consider the following noiseless signal model where base station has $M$ antennas in downlink where user-$k$ receives the following signal:

$$y\_{k} = \mathbf h\_{k}^H\mathbf{x}$$

where $ \mathbf h_{k} \in \mathbb{C}^{N\times 1}$ is the channel between the base station and user $k$ and $\mathbf{x}$ is the transmitted signal by base station to all users which is given as follows

$$\mathbf{x} = \sum_{i =1}^{K} \mathbf{w}_i q_i$$

where $\mathbf{w}_k$ is the precoder designated for user $k$ and $q_k$ is the message signal intended for user $k$. Then the overall received signal can be expressed as follows:

$$y\_{k} = \mathbf{h}\_{k}^H \mathbf{w}_k q\_k + \sum\_{i\neq k}^{K}  \mathbf{h}_{k}^H \mathbf{w}_k q_i$$

The first term is the signal intended for the user $k$ and second term is signal intended for other users but it acts as interfering signal to user $k$ and hence undesirable.

This is where the precoders $\mathbf{w}_i$ usefulness comes into picture. There are many commonly utlized precoders such as maximum ratio transmitter (MRT), zero forcing (ZF) and regularized zero forcing (RZF). Computationally less expensive is MRT which is technically given by $\mathbf{w}_i = \frac{\mathbf{h}_i}{N}$ (different literatures have different scaling factors infront of this term, but we will consider this version to get the essence of the concepts we are trying decipher). Then accordingly, one can write the received signal as follow:

$$y\_{k} = \frac{\Vert \mathbf{h}\_{k} \Vert^2}{N} q\_k + \sum\_{i =1, \neq k}^{K}  \frac{\mathbf{h}_{k}^H \mathbf{h}_i}{N} q_i$$