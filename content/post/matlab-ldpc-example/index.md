---
title: MATLAB LDPC Example
subtitle: LDPC with MATLAB just made simple by custom encoder
date: 2021-12-19T18:28:33.368Z
draft: false
featured: false
tags:
  - MATLAB
  - LDPC
categories:
  - Technical
image:
  filename: featured
  focal_point: Smart
  preview_only: false
---
<!--StartFragment-->

LDPC code which stands for low-density-parity-check code is one of many error-correcting codes. LDPC codes are also known as **Gallager codes**, in honor of its developer [Robert G. Gallager](https://en.wikipedia.org/wiki/Robert_G._Gallager "Robert G. Gallager"). LDPC code is one of the new physical-layer channel coding schemes besides Polar codes that have been introduced in release-15 5G NR access technology standards by 3GPP. These two codes replaced convolution codes and Turbo codes which were part of 4G LTE.

However, this article is not a tutorial on LDPC code. But rather provides an example of how to implement LDPC encoding and decoding in MATLAB and also includes a helper function to assist with using MATLAB toolbox.

MATLAB currently has two versions of LDPC functions. One creates an LDPC object and the other is a direct function and they are comm.LDPCEncoder and ldpcEncode(). However, starting from MATLAB R2021b version, comm.LDPCEncoder system object used for LDPC coding is not recommended. The recommended function is ldpcEncode(), which takes in two-three arguments: the first argument can be a vector or a matrix. The second argument is the configuration object, which depends on the parity check matrix in use. For details on the third argument, refer to MATLAB documentation [here](https://se.mathworks.com/help/comm/ref/ldpcencode.html). We will focus on the usage of function ldpcEncode().

I have created a helper function called generateConfigLDPC(), which inputs the rate and outputs the configuration object, which can be directly given to the ldpcEncode() function. This avoids the hassle of getting searching/providing manually the parity check matrix and creating configuration objects.

The rates supported by the function created are as per IEEE 802.11 standard, which supports: 1/2, 2/3, 3/4, and 5/6. Similarly, currently supported codeword block lengths: 648, 1296, and 1944. The default codeword length is 648 unless otherwise specified, and the "standard" argument can be left empty as currently, only the WLAN standard is supported.

When I get some time in the future, I can include WiMAX and 5G NR standard parity matrices.

<!--EndFragment-->

Following syntaxes are supported:

```
% Example 1:
rate = 1/2;
[cfgLDPCEnc,decodercfg] = generateConfigLDPC(rate,'decoderAlgo','bp');

% Example 2:
rate = 1/2;
n = 1944;
[cfgLDPCEnc,decodercfg] = generateConfigLDPC(rate,n,'decoderAlgo','norm-min-sum');

% Example 3:
rate = 1/2;
n = 1944;
[cfgLDPCEnc,decodercfg] = generateConfigLDPC(rate,n,'decoderAlgo','norm-min-sum','standard','wlan');

% Example 4
rate = 3/4; % code rate
n = 1296; % Codeword length
decodAlgo = 'offset-min-sum'; % LDPC decoding algorithm
[cfgLDPCEnc,decodercfg] = generateConfigLDPC(rate,n,'decoderAlgo',decodAlgo,'standard','wlan');
```

For more details and to download the files: <https://se.mathworks.com/matlabcentral/fileexchange/103360-matlab-ldpc-config>