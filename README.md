# Physical Meaning of Style Transfer: Physics-Informed Style Transfer for CFD simulations.

We propose a potential physical meaning of the use
of the Gram Matrix for style transfer which extends beyond
the notion of texture, shape, and color in images to the relationships between feature vectors in simulations of physical
systems. We incorporate domain knowledge of the use of
CNNs in science applications with a focus on computational
fluid dynamics in the lagrangian regime and suggest that the
learned feature-vector Gram matrix may have physical significance in other domain applications. We propose future
areas of study for style transfer extending beyond the realm
of images and art into the relationship between learned feature vectors for physically-relevent data.


## Style Transfer: An Overview

![image](st_ex.png)

In style transfer, the machine learns a link between texture and color. For example, one texture often uses a particular color. Style is a correlation between shapes/color distributions, etc. One way to look at style is to consider it the correlation between kernels. The similarity between two kernels can be calculated using a dot product. (The gram matrix is effectively a "similarity matrix", showing the correlation between kernels.)

Convolutional feature maps are generally a good representation of input image’s features. They capture spatial
information of an image without containing the style information given that a feature map is used as it is. Starting from the network’s input layer, the first few layer
activations represent low-level features like textures, colors,
and edges. Proceeding through the network, latter layers
represent higher-level features like shapes, and recognizable
large scale feature artifacts like animals, faces, or objects.
We use the VGG19 network architecture, a pre-trained image classification network and extract intermediate layers to
define the representation of content and style from particle
data.

## Dataset 

The dataset was obtained through publicly available, pre-
run Lagrangian SPH fluid simulations. For each simula-
tion, the fluid block is set with different initial conditions
like shape, position, velocity, and fluid viscosity. The re-
sults of each simulation are stored as a .npy array file with
4 dimensions inside a folder with the respective simulation
ID, available for public download here: https://inductiva.ai/blog/article/fluid-cube-dataset

## Gram Matrix Calculation 

 The Gram matrix for a particular layer can be calculated as:

$$ G^l_{cd} = \frac{\sum_{ij} F^l_{ijc} (x) F^l_{ijd}}{IJ}$$

The Gram matrix is calculated by taking the outer product of
the feature vector with itself at each location and averaging
that outer product over all locations. the mean square error of the image’s output rela-
tive to each target can be used in gradient descent. Partially
fixed weights at the later convolutional layers in the Content
image preserve the content of the image while the weighted
sum of the losses is used to change the Gram Matrix results
for low-level features.


![image](gram.png)

Source: https://www.youtube.com/watch?v=Elxnzxk-AUk

## Future Work

There are many opportunities to expand this work, which
is simply opening the door to the possibility of a physical intuition of Style Transfer for simulation data. Fine-grained
SPH simulations were used such that the particles have only
undergone a few seconds of real-time motion, thus the starting point of the particles is sufficient metric along the x-
axis, preserving some spatial relevance. For longer simulations, this method could pose problems due to the parti-
cles undergoing long-range motion and a better pre-trained
model would be needed to capture the large-scale spatial
features of the data when applying Style Transfer to extract
small-order feature vectors. 

