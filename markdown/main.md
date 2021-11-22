## Problem Statement

### Instance Segmentation Problem for Biological Images

* Instance segmentation in biological data object instances may be particularly densely
packed

* The appearance variation may be particularly low

* Excessive number of instances may be present


* Complex overlaps and occlusions

* The variability of sizes of individual instances may
be limited. 

We attempt to solve these peculiarities which show up when trying a traditional instance segmentation approach on biological images.

Note: Add main section slides here.


## Observations

* While complex overlaps and occlusions are present, the variability of scale is limited due to lack of perspective

* Learning good embeddings for instances with a conv network is challenging for biological data

* We can use sinusoidal guide functions as embeddings for biological images where scale variability is limited


## Implementation

* Training split into two stages:

    * Stage 1: Learn guide functions which can produce per instance embeddings
    * Stage 2: Train a convolutional network to take as input unsegmented image and produce per instance embeddings


* We use a sinusoidal guide functions
    * In many biomedical datasets, there is a certain (imperfect) regularity in the location of objects.
    * Such loosely-regular, semi-periodic structure calls for the use of harmonic functions as guides functions.


## Implementation

<img src='images/image1.png'>


## Stage 1

At train-time, we embed each pixel of the ground truth segmented image S<sup>I</sup> as the mean of predefined guide functions f over instance pixels it belongs to, resulting in embeddings e(S,	Ψ)

We train the guide functions by learning the parameter of the function (eg the frequency and phase)


## Choice of Guide Function

As discussed above, we choose harmonic functions as guide functions.

<img src='images/image2.png' height=20px>

Embeddings is defined by

<img src='images/image3.png' height=20px>


## Loss for stage 1

We use the hinge loss as our loss function.

We want to avoid collisions in the embedding space (different embeddings for different instances).

<img src='images/image4.png' height=20px>

Stochastic gradient descent is used to minimize the loss.


## Stage 2

We then train the neural network E to reproduce the ground truth embedding given the inputted unsegmented image I.

Guide functions f are inputted into intermediate representations of the network

* Network used is dependant on type of object we are instancing

* For worms we use U-Net, for people we use PSP net


## Loss for stage 2

Per pixel L<sub>1</sub> loss between Conv output and embedding output from stage 1

<img src='images/image5.png' height=20px>


## Guide functions as input to network

* The guide functions learned in stage 1 are inputted into the network

* If U-Net is used, we use concatenate the downsampled guide function with the original input


## Guide functions as input to network

<img src='images/image6.png'>


## Testing

During testing, we take the pretrained guide functions for a particular class, and input them into the trained network (also dependant on the class)

We have saved the trained guide functions (i.e their parameters) for people, plants and worms and use them during testing


## Results
### People (Good Results)

<img src='images/people/1.png'>


<img src='images/people/2.png'>


<img src='images/people/3.png'>


<img src='images/people/4.png'>


### Image of our team (Pretty good result!)

<img src='images/people/proce.png'>


### Plants (Good Results)

<img src='images/plant/1.png'>


<img src='images/plant/4.png'>


### Plants (Bad results)

<img src='images/plant/2.png'>


<img src='images/plant/3.png'>


### Worms (Good Results)

<img src='images/worms/1.png'>


<img src='images/worms/2.png'>


<img src='images/worms/3.png'>


### Worms (Bad Results)

<img src='images/worms/4.png'>


<img src='images/worms/5.png'>


<img src='images/worms/6.png'>


<img src='images/worms/7.png'>