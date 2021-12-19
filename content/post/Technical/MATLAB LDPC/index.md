---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "MATLAB: LDPC encoder configuration object"
subtitle: ""
summary: ""
authors: []
tags: ["MATLAB","LDPC"]
categories: ["Technical"]
date: 2019-06-25T19:15:39+05:30
lastmod: 2019-06-26T19:15:39+05:30
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image: 
  caption: "Image credit: [**Space.com**](https://www.space.com/28552-interstellar-movie-black-holes-study.html)"
  focal_point: "Center"
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---
Starting MATLAB R2021b version, comm.LDPCEncoder system object used for LDPC coding is not recommended. The recommended function is ldpcEncode() which takes in two arguments: first argument is vector or a matrix and second argument is configuration object which depends on the parity check matrix in use. 

For all those who just want to use the function with specific code-rate, I have created a helper function called generateConfigLDPC(rate,codeword length, standard) which takes input the rate and outputs the configuration object which can be directly given to ldpcEncode() function. This avoids hassle of getting searching/providing manually the partiy check matrix and also properly creating configuration object.

As of now the rates supported by the function created are as per IEEE 802.11 standard which supports: 1/2, 2/3, 3/4, and 5/6. Similarly, currently supported codeword block lengths: 648, 1296 and 1944. Default codeword length is 648 unless otherwise specified. Standard argument can be left empty as currently only WLAN standard is supported.

When I get sometime in future, I can include WiMAX and 5G NR standard parity matrices.

syntax to use the function:  
E.g. 1: cfgLDPCEnc = generateConfigLDPC(3/4); % rate 3/4 and n = 648  
E.g. 2: cfgLDPCEnc = generateConfigLDPC(1/2,1944); % rate 1/2 and n = 1944  
By default WLAN is selected

Above two examples are equivalent to:  
E.g. 3: cfgLDPCEnc = generateConfigLDPC(3/4,648,'wlan'); % rate 3/4 and n = 648  
E.g. 4: cfgLDPCEnc = generateConfigLDPC(1/2,1944,'wlan'); % rate 1/2 and n = 1944

$$\gamma{n} = \frac{ \left | \left (\mathbf x\_{n} - \mathbf x\_{n-1} \right )^T \left \[\nabla F (\mathbf x\_{n}) - \nabla F (\mathbf x\_{n-1}) \right ] \right |} {\left |\nabla F(\mathbf{x}\_{n}) - \nabla F(\mathbf{x}\_{n-1}) \right |^2}$$