---
title: Image Classification and Explanations with Saliency Maps
---

{% include figure image_path="/assets/images/saliency.jpg" alt="First LIME redesign" caption="The image used in the visualization was taken
from the [ChestX-ray8 dataset](https://doi.org/10.48550/arXiv.1705.02315)." id="saliency" %}


## Domain situation
A radiologist is using a new system powered by an AI model. This system was design to help radiologist find tumors in chest x-rays. She wants to understand what parts of the medical image area making the AI give certain predictions.

## XAI task & explanation abstraction

1. Data type: Image

2. AI model: A [Convolution Neural Network](https://ieeexplore.ieee.org/document/726791) in which input is an image, and the output is the class score. This CNN model was trained on the [ChestX-ray8 dataset](https://doi.org/10.48550/arXiv.1705.02315).

3. XAI task: Understand why the given AI/ML model gives its prediction.

## Selection of XAI method

1. Strategies used to generate explanations: Feature importance.
2. XAI Method: [Saliency Map](https://doi.org/10.48550/arXiv.1312.6034). The saliency map approximates the model output as a linear regression based on (i) the image it receives and (ii) weights calculated with the gradient that the model generated when classifying the image. Therefore, these weights are used to describe how each pixel contributes to the prediction result, which can be interpreted as the importance per pixel.

## Confirmation of visualization usefulness
The XAI method that was chosen can get the information to generate a useful visualization to help the radiologist in its task.

## Data/task abstraction

### Data Abstraction
**Vector field** where each cell contains (i) a color pixel and (ii) the
importance of that pixel in the prediction of the class. This importance
corresponds to a **quantitative** attribute with **sequential** order
whose minimum is 0.

### Task Abstraction

\(i\) **Summarize** pixel importance, (ii) **find** cluster and outlier
of pixels based of their importance, and (iii) **identify** features in
the image based on pixel importance

## Visual encoding/interation idiom

**Juxtapose** with two scalar field: (i) The first field **encodes** the
original image, e.i. the color of each pixel. (ii) The second field
**maps** the importance of the pixels with a sequential color scale.

# Redesign Saliency visualization with `VD4XAI`

An important study to consider in this case is presented by Dennis and Carte ([1998](https://doi.org/10.1287/isre.9.2.194)). They describe the adjacent visualizations as a form of presentation where the data is displayed directly upon the image by coloring the areas in different colors to indicate their data values. In short, superimpose the visualization with the image. They show that adjacent visualizations should help decision-makers to associate areas of a visualization image with its data, simplifying the complex relationship between them and leading to faster, more accurate decisions.

This paper justifies to re-design the visualization and simplifying its complexity. The new design would superimpose both scalar fields, interpolate the importance per pixel to generate areas of importance in the image, and encode these areas with a heatmap. A possible alternative is shown in Figure [1.B](#fig:image-case), which unifies both fields and uses a heatmap with a rainbow scale to encode the importance of the pixels.

However, we can iterate the visualization shown in Figure [1.B](#fig_image-case) and improve it if we seek to optimize its accessibility to different users. This visualization is not designed to be color-blind safe because the rainbow scale uses many colors like red, blue, yellow, and green that a color-blind cannot correctly differentiate. So, if the end-user is colorblind, we need to change the color scale. We suggest changing the rainbow scale to a sequential scale, such as in Figure [1.C](#fig_image-case). We use a single color and change the saturation to encode the importance. With a sequential scale, color-blind people will also see the visualization and correctly interpret the coding used.
