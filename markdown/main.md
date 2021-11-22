## Problem Statement

Instance Segmentation Problem for Biological Images

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


### Level 3 heading

* A bullet list.
* Use these sparingly.


Just some text

```bash
#!/bin/sh

# This is a code snippet.
# It comes with syntax highlighting.

NUM=5

for i in `seq $NUM`; do
  echo "hello world $i"
done
```
