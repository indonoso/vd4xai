---
title: Text Classification with LIME
---

![Current lime](/assets/images/lime_orginal.jpg)

## Domain situation
A restaurant wants to understand whether the reviews it is getting from its clients are positive or negative. The number of reviews they receive daily is very high, so they decided to get help from an AI to classify these opinions.

## XAI task & explanation abstraction

1. Data type: Text
2. AI model: [DistilBERT](https://arxiv.org/abs/1910.01108) uncased fine-tuned on yelp reviews dataset. It returns the probability for positive and negative review.
3. XAI task: (i) Understand why the given AI/ML model gives a certain prediction & (ii) Understand why the AI/ML model does not predict something else


## Selection of XAI method
1. Strategies used to generate explanations: Feature importance
2. XAI Method: LIME. This method approximates the original ML classification method with a linear model to classify the document to be explained by sampling data instances around the neighborhood of the target document. With this linear surrogate model, LIME uses the learned coefficients weights to describe the importance of certain words when predicting the class of the target document.

## Confirmation of visualization usefulness

The person performing the tasks needs to quickly asses whether the predictions are correct. A visualization can help to do this task faster than simply looking at plain text.

## Data/task abstraction

### Data abstraction (What)

\(i\) The output probability of each class, which corresponds to a
**quantitative** attribute with continuous values between 0 and 1. (ii)
Words (features) with their corresponding weights, which can be positive
or negative values and correspond to a **quantitative** attribute with
**divergent** order. This word weight is interpreted as the importance
of the word for classifying the document as class 1 in case of being
positive or class 0 for negative weights.

### Task abstraction (Why)

\(i\) **Compare** the probabilities, (ii) **compare** the importance of
words for each answer, (iii) **summarize** the importance of all words,
and (iv) **identify** outliers or clusters of words based on their
importance.

## Visual encoding/interation idiom

**Juxtaposition** addresses three tasks: compare the output
probabilities, compare feature importance and summarize this importance
in the text with three charts, respectively. (i) For bar charts, bar
length is used to **encode** class probability. The color is used as a
categorical channel to **map** each possible class in the model: 0 or 1.
(ii) In the case of the center chart, the **bar length** is used to
**encode** the importance of the word for the model's output. The bars
are **ordered** with the highest absolute value at least and are
directed according to the sign of the weight: if they are positive, they
are bars to the right. In case of negative weights, the bars point to
the left. Also, use color to **map** the sign of the weight. (iii) For
the text chart, saturation on a bi-directional scale is used as the
background color to **encode** importance per word. Each word is
**arranged** in paragraph form to keep the original text structure.

# Redesign LIME Visualization with `VD4XAI`

## Option 1: Reduce cognitive load

This visualization (figure
[1](#fig_lime_vis)) allows us to compare and summarize the
importance of each feature. To accomplish the two tasks, they use
juxtaposition to construct one chart per task. However, this decision
increases the division of attention (Lobo et al, [2015](https://dl.acm.org/doi/10.1145/2702123.2702130)) for those looking
to perform both tasks simultaneously. In other words, users who use the
text to search for some words and then need to compare the importance of
those words see their cognitive load increased by requiring them to
intersperse their attention between one chart and the other.


![redesign_1](/assets/images/lime_redesign_1.jpg)

We can redesign this visualization with `VD4XAI`. If we want to allow
both visual tasks to be performed simultaneously without increasing
cognitive load, we alter the data/task abstraction level. Here we reduce
the number of tasks and delete the task (iv). After we alter the visual
encoding level. To do so, we can explore the design space proposed in
the literature, such as text clouds or neuronal attention in text
classification (see Felix et al [2017](https://ieeexplore.ieee.org/document/8017641/) and Valdivieso et al [2019](https://observablehq.com/@hernan4444/analyzing-the-design-space-for-visualizing-neural-attenti)). Figure
[2](#fig_redesign_1) shows a visual encoding that could be used to redesign the
visualization. In this proposal, an additional bar mark is added behind
each word, and the length of the bar encodes the importance of the word.
To distinguish positive and negative weights, the mark could be painted
in 2 colors according to the sign of the weight and ensure that they are
colorblind safe such as orange and blue.

### Option 2: Add interaction

In figure [1](#fig_lime_vis), the bar chart in the center has words ordered
by absolute weight. This produces two difficulties: first, the user is
not free to choose the position of each feature to compare in the bar
chart, and second, if the algorithm uses more features, the middle chart
will use more space. This implies that the design is not optimal for
very long text. To avoid this problem, we propose the end-user selects
the words she wishes to compare. Applying the framework will again be
necessary to iterate the decisions within the visual encoding level.

![redesign_2](/assets/images/lime_redesign_2.jpg)

In this case, we can propose building an interactive chart where the
user can select the words in the text, and only those words appear in
the bar chart (figure [3](#fig_redesign_2)). Additionally, the visualization designer
could explore the literature to find more alternatives which show more
features such as [TileBars](https://doi.org/10.1145/223904.223912), [Inkblots](https://doi.org/10.1145/1255175.1255178) or [TextArc](https://api.semanticscholar.org/CorpusID:59650683).
Nevertheless, the visualization designer has to verify if these
visualizations allow the end-user to perform the visual tasks that she
wants to do in the XAI task space.

### Option 3: Reduce XAI tasks

Finally, using the proposed framework, if we want to reduce the two XAI
tasks to one: *Understand why the given AI/ML model gives its
prediction*, it will be necessary to iterate the following levels: the
XAI method, the visual tasks, and the encodings used. In this case, LIME
can still solve this task, but it is only necessary to consider the
weights associated with the class with the highest probability.
Therefore, the original visualization can be redesigned as follows: (i)
The probability chart can be redesigned to just one text indicating the
probability of the most probable class. (ii) The middle bar chart should
only have bars for one side. (iii) The text chart should use a
sequential color scale. In short, only keep the information associated
with the most probable class.

![redesign_3](/assets/images/lime_redesign_3.jpg)
