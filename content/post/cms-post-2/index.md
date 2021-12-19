---
title: MATLAB LDPC Example
subtitle: LDPC with MATLAB just made simple
date: 2021-12-19T14:44:28.684Z
draft: false
featured: false
categories:
  - Technical
projects:
  - Math
image:
  filename: featured
  focal_point: Smart
  preview_only: false
---
Starting from MATLAB R2021b version, comm.LDPCEncoder system object used for LDPC coding is not recommended. The recommended function is ldpcEncode(), which takes in two arguments: the first argument is a vector or a matrix. The second argument is the configuration object, which depends on the parity check matrix in use.


For all those who just want to use the function with a specific code rate, I have created a helper function called generateConfigLDPC(rate, codeword length, standard), which inputs the rate and outputs the configuration object, which can be directly given to ldpcEncode() function. This avoids the hassle of getting searching/providing manually the parity check matrix and properly creating configuration objects.


As of now, the rates supported by the function created are as per IEEE 802.11 standard, which supports: 1/2, 2/3, 3/4, and 5/6. Similarly, currently supported codeword block lengths: 648, 1296, and 1944. The default codeword length is 648 unless otherwise specified, and the "standard" argument can be left empty as currently, only the WLAN standard is supported.
When I get some time in the future, I can include WiMAX and 5G NR standard parity matrices.

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



Download the files from: <https://se.mathworks.com/matlabcentral/fileexchange/103360-matlab-ldpc-config>