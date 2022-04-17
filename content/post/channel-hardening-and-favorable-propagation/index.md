---
title: " Channel Hardening and Favorable Propagation"
subtitle: Technical jargons made simple
date: 2022-04-04T07:31:54.876Z
draft: false
featured: false
tags:
  - MIMO
  - Channel Hardening
  - Favorable Propagation
categories:
  - Technical
image:
  filename: featured
  focal_point: Smart
  preview_only: false
---
5G is around the corner and soon will be deployed worldwide. If one has been following the technical community closely, we may know that “Massive MIMO” is one of the key enabling technology in 5G. If someone is not aware what the acronym MIMO stands for, MIMO actually stands for multiple-input-multiple-output. Here, the multiple input corresponds to the multiple-transmit antennas that can send various signals by multiplexing, and multiple-output corresponds to multiple users to which the base station will be serving. The word “Massive” indicates that the base station has very large number of antennas, practically 64 antennas and more. For more information, refer to: https://ma-mimo.ellintech.se/2020/05/13/how-massive-are-the-current-massive-mimo-base-stations/

One may wonder what makes Massive MIMO so special than its pioneering technology MIMO, except that it has a massive number of antennas rather than four to eight antennas. One immediate benefit that one can easily guess is that with a very large number of antennas, the various gains and benefits Massive MIMO networks can provide over standard MIMO networks (4-8 antennas) will be significant. However, two key important features of Massive MIMO that make this technology unique compared to MIMO technology are channel hardening and favourable propagation.

To mathematical understand these concepts, consider the following noiseless signal model where base station has $N$ antennas in downlink where there are $2$ users and user $1$ receives the following signal:

$$y\_{1} = \mathbf h\_{1}^H\mathbf{x} + n$$

where $n$ is the noise which we will assume for sake of this tutorial zero i.e., $n=0$, $ \mathbf h_{1} \in \mathbb{C}^{N\times 1}$ is the channel between the base station and user $1$ and $\mathbf{x} \in \mathbb{C}^{N\times 1}$ is the transmitted signal by base station to all users which is given as follows

$$\mathbf{x} = \mathbf{w}_1 q_1 + \mathbf{w}_2 q_2$$

where $\mathbf{w}_k  \in \mathbb{C}^{N\times 1}$ is the precoder designated for user $k$ and $q_k$ is the message signal intended for user $k$.  Also the operator we used $(\cdot)^H$ is the Hermitian of the vector/matrix. Then the overall received signal can be expressed as follows:

$$y\_{1} = \mathbf{h}\_{1}^H  \mathbf{w}_1 q\_1 +  \mathbf{h}\_{1}^H  \mathbf{w}_2 q_2$$

The first term is the signal intended for the user $1$, and the second term is the signal intended for the user $2$, but it acts as an interfering signal to user $1$ and is hence undesirable. Similarly, one can write the signal received at user $2$ with the signal intended to user $1$ acting as an interfering signal. 

This is where the precoders $\mathbf{w}_i$ usefulness comes into the picture to boost the signal component and mitigate the interfering signals. There are many commonly utilised precoders such as maximum ratio transmitter (MRT), zero forcing (ZF) and regularized zero forcing (RZF). Computationally less expensive is MRT which is technically given by $\mathbf{w}_i = \frac{\mathbf{h}_i}{N}$ (different literatures have different scaling factors infront of this term, but we will consider $1/N$ scaling in this tutorial to get the essence of the concepts we are trying decipher). Then accordingly, one can write the received signal as follow:

$$y\_{1} = \frac{\Vert \mathbf{h}\_{1} \Vert^2}{N} q\_1 +  \frac{\mathbf{h}\_{1}^H \mathbf{h}_2}{N} q_2$$

There is a very interesting observation in the above equation as $N \rightarrow \infty$, i.e., as the number of antennas at the base station grows higher and higher. Can you see ?

To see that, let's consider a Rayleigh fading channel model which is most commonly used to model wireless channels in academic literature. Moreover, assume that all the elements of the channel vector are i.i.d (independent and identically distributed) and have zero-mean with unit variance (for the sake of simplicity).

Then from the law of large numbers following holds

$$\frac{\Vert \mathbf{h}\_{1} \Vert^2}{N} \rightarrow \mathbb{E}(\vert h\_{11}\vert^2)  = 1$$

and 

$$\frac{\mathbf{h}_{1}^H \mathbf{h}\_2}{N} \rightarrow \mathbb{E}(h\_{11}^{*}h_{21} )  = 0$$

where $h\_{11} corresponds to the first element of vector $\mathbf{h}\_{1}$ and similarly $h\_{21}$  corresponds to the first element of vector $\mathbf{h}\_{2}$. Here, the operator $(\cdot)^{*}$ is the conjugate of the argument.  

Thus, the implication on the received signal is as follows

$$y_{1} \rightarrow  q_1$$

what this essentially tells us is that the effective channel (inner product between the precoder and the channel vector) become constant (in the example above the constant is one) i.e., the randomness in the channel has disappeared which is what we call technically the channel hardening. Here, the term "harden" refers to the diminishing randomness of the effective channel and becoming more deterministic.

On other hand, the interference term has become zero, which is more of a favorable situation. Here, technically channels become orthogonal as $N \rightarrow \infty$ which we refer to as favorable propagation.

These concepts in simple words imply that Massive MIMO network with a simple precoder like MRT one can turn a Rayleigh fading channel to an effective AWGN channel and moreover effectively mitigates the interference by virtue of its properties presented above which do not normally occur with conventional MIMO (with 2-4) antennas hold.

Hope these concepts are clear to the readers with a basic technical background in wireless communications.

Now there are some questions for the readers to think about, why can't we deploy infinite antennas (practically let's say some 1000 antennas) and with very minimal processing like MRT get the optimally best performance? Are there any practical limitations?

We mentioned in the introduction that the practically deployed Massive MIMO system has 64 antennas (as of now).  Then, the question arises with just 64 antennas do the above properties hold?

The research community currently talking about distributed MIMO (there are many names: Cell-Free Massive MIMO, Cell-Free Networks, Network MIMO etc).  Do these properties hold for such networks?

Think over it, we shall answer these concepts in the next post and also do some simulations in MATLAB and check whether 64 antennas are good enough for the above properties to hold.