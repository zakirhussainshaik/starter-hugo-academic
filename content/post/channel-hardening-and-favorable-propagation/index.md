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

To mathematical understand these concepts, consider the following noiseless signal model where base station has $M$ antennas in downlink where there are $2$users and user $1$ receives the following signal:

$$y\_{1} = \mathbf h\_{1}^H\mathbf{x}$$

where $ \mathbf h_{1} \in \mathbb{C}^{N\times 1}$ is the channel between the base station and user $1$ and $\mathbf{x}$ is the transmitted signal by base station to all users which is given as follows

$$\mathbf{x} = \mathbf{w}_1 q_1 + \mathbf{w}_2 q_2$$

where $\mathbf{w}_k$ is the precoder designated for user $k$ and $q_k$ is the message signal intended for user $k$. Then the overall received signal can be expressed as follows:

$$y\_{1} = \mathbf{h}\_{1}^H  \mathbf{w}_1 q\_1 +  \mathbf{h}\_{1}^H  \mathbf{w}_2 q_2$$

The first term is the signal intended for the user $k$, and the second term is the signal intended for user $2$, but it acts as an interfering signal to user $k$ and is hence undesirable.

This is where the precoders $\mathbf{w}_i$ usefulness comes into picture. There are many commonly utilised precoders such as maximum ratio transmitter (MRT), zero forcing (ZF) and regularized zero forcing (RZF). Computationally less expensive is MRT which is technically given by $\mathbf{w}_i = \frac{\mathbf{h}_i}{N}$ (different literatures have different scaling factors infront of this term, but we will consider this version to get the essence of the concepts we are trying decipher). Then accordingly, one can write the received signal as follow:

$$y\_{1} = \frac{\Vert \mathbf{h}\_{1} \Vert^2}{N} q\_1 +  \frac{\mathbf{h}\_{1}^H \mathbf{h}_2}{N} q_2$$

There is a very interesting observation in the above equation as $N \rightarrow \infty$, i.e., as the number of antennas at the base station grows higher and higher. Can you see ?

To see that, let's consider a Rayleigh fading channel model which is most commonly used to model wireless channels in literature. Moreover, assume that all the elements of the channel vector are i.i.d and have zero-mean with unit variance (for the sake of simplicity).

Then from the law of large number following holds

$$\frac{\Vert \mathbf{h}\_{1} \Vert^2}{N} \rightarrow \mathbb{E}(\vert h\_{11}\vert^2)  = 1$$

and 

$$\frac{\mathbf{h}\_{1}^H \mathbf{h}\_2}{N} \rightarrow \mathbb{E}(h\_{11}^{\*}h\_{21} )  = 0$$