---
title: Recommendation Systems and Explanations with Attention Mechanism
---

{% include figure image_path="/assets/images/lol-items.png" alt="Visualization to explain the item recommendation with a Transformer for Team-aware Item Recommendation architecture" caption="Visualization to explain the item recommendation with a Transformer for Team-aware Item Recommendation architecture" id="fig_lol_items" %}

## Domain situation
The last case is about a visual explanation of recommendation systems.
The application goal is to recommend items in an online game called
League of Legends. More details can be found in the paper published by Villa et al [2020](https://doi.org/10.1145/3383313.3412211). The model uses a
Transformer neural architecture, modified for team-aware item
recommendation. The input data is the information from ten players: 5
characters for each game team (red and blue). Given that contextual
information, the model recommends up to six items to buy for each
character of the blue team inside the game. Figure
[1](#fig_lol_items) shows the visualization proposed by the
authors to explain the recommendation to users.

## XAI task & explanation abstraction

1. Data type: Array of tabular data.
2. AI model**: Transformer for Team-aware Item Recommendation architecture (TTIR).
3. XAI task: Understand why the given AI/ML model gives its
    prediction. In this case, the prediction will be the recommendation.

## Selection of XAI method

1. Strategies used to generate explanations: Feature importance.

2. XAI method: Attention mechanism


## Data/Task abstraction
### Data Abstraction

**Scalar field** where each cell contains the attention paid by the
model to the input data to generate the recommendation. The attention is
a **quantitative** attribute with **sequential** order value between 0
and 1. This value represents the importance of the input when the model
generates the recommendation.

### Task Abstraction

\(i\) **Summarize** the attention paid by the model. (ii) **Identify**
outliers or clusters.

## Visual Encodings

**2D matrix alignment** of area marks. The cell **encodes** the
attention value with a sequential colormap. Each column is input data,
while each row is the recommendation made to each player of the blue
team.

# Redesign the Visualization

{% include figure image_path="/assets/images/lol-items-alternative.png" alt="Visualization to explain the item recommendation with a Transformer for Team-aware Item Recommendation architecture" caption="First redesign" id="fig_lol_alternativve" %}

This visualization allows an exploration of the attention values used by
the model for the given recommendation. However, other visual tasks that
an end-user may want are (i) identifying extreme values and (ii)
comparing with high precision the attention values in different cells.
When using color to encode the attention values, we cannot perform both
visual tasks efficiently. Therefore, since we modify the Task
Abstraction of this visualization to allow these two new tasks, the
framework tells us that we must re-iterate the visual encoding level.

One design proposal is to change the color for a more efficient channel
to represent numerical data. As such, we suggest a chart like Figure
[2](#fig_lol_items_alternative) where the vertical position
channel is used to encode the attention values placed by each
recommendation on an input. The horizontal position separates each input
data, and the color channel maps each recommendation. These encodings
allow the end-user to compare with more precision and identify extremes
in each row and column.

Currently, some tasks in specific contexts are difficult to perform. A
likely case in this game is that the end-user has limited time to
analyze the visualization. In this scenario, tasks like seeing
information only for her character o searching for the character that
the model paid the most attention will be difficult to accomplish.

The current visualization requires searching for the row corresponding
to a specific character and then exploring the cells in that row to find
the character with the most attention. Since we propose to change the
visual tasks that the end-user will do, the framework tells us that we
must iterate the next stage, which is visual encodings. An alternative
to satisfy the task of finding the character with the most attention and
only displaying information about a specific character is shown in
Figure [3](#fig_lol_items_bar).


{% include figure image_path="/assets/images/lol-items-bar.png" alt="Visualization to explain the item recommendation with a Transformer for Team-aware Item Recommendation architecture" caption="Second redesign" id="fig_lol_alternativve" %}

In this interactive chart, the user selects a character, and the
visualization uses bar length to encode the attention values. Also, the
bar was ordered from highest to lowest. With this encoding, the end-user
selects the character to only view the information about that character.
Then, this user has to look up the first bar to identify the characters
with the most attention. Additionally, the end-user can effectively
compare the magnitude of that value with the other characters. These
encodings allow the end-user to perform the new visual task efficiently.
