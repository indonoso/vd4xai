---
permalink: /framework/
---
TODO: intro al modelo

# Roles
TODO: explain old roles + new roles

# Applying and extending the Nested Model for Visual XAI

<a href="https://www.cs.ubc.ca/~tmm/vadbook/">Munzner's nested model</a> provides a generic approach to analyzing and designing visualizations. It allows users to understand dependencies between visualization choices. In each of the levels, users must define certain aspects of the visualization. The levels are completed in order because what has been defined up to level $i$ is the input of level $i + 1$. This does not mean that they cannot be modified after being defined; it only means that the concepts defined at each level affect the following. A threat is a fact that can make the definition of a level not optimal. This framework defines threats and ways to validate that the threat does not affect the result. Validations can be applied during the definition of a level or after all levels have been applied, such as an exit validation.

## <span class="ds">Domain Situation</span>

This term encompasses "a group of target users, their domain of interest, their questions, and their data" (Munzner, 2014). The goal of this stage is to analyze the situation in which the visualization will be deployed. The outcome of this analysis is a set of questions that the users want to answer when using the data visualization. The following questions should be answered after finishing this stage:

1. Who are the users? What do they need?
2. What is the domain? Why do they need an AI model?
3. What are the data like? text, images, tabular data, graph or something else? What is the data semantics?
4. What are the users' questions about this data?

## XAI Task and explanation abstraction

The goal of this level is to identify the XAI task and the type of explanation. To achieve this goal the expert has to define the following XAI Space.

### AI model
We need to understand the output of the model that will be used to predict on the data. We asume this model has already been trained and it is ready for production.

### Data type
We determinate the type of data used by the AI model and the XAI method. For instance, text, images, tabular data, graph, among others.

### XAI tasks
We determinate the task that need  to be solved with the explanations. The possible tasks that we identify in this level are (Gunning, year):
1. Understand why does the given AI/ML model give its prediction.
2. Understand why the AI/ML model does not predict something else.
3. Understand when does the AI/ML model fail.
4. Understand when does the AI/ML model succeed.

## Selection of XAI Method

### Strategies used to generate explanations

We determinate the strategies to generate the explanations that solve the XAI tasks. The possible strategies to choose are:
1. Feature importance
2. Analogies (similarity-based examples, adversaries examples)
3. Counterfactual
4. Rules

### XAI method

We determine the computational method that applies the strategies to generate the explanations. The output of this method is to be used in the nested model to generate the visualization. If the model is a traditionally explainable model like a Decision Tree, and the AI expert use the model to generate the explanation, we can omit this dimension because we do not need to use another computational method such as LIME [63], SHAP [44] or attention mechanism [36] to generate the explanation. In other words, we can say that a traditionally explainable model could be considered, in this dimension, as the XAI method.

## Confirmation of visualization usefulness

## Data/Task abstraction

https://www.youtube.com/watch?v=tBWMOSrASkE&ab_channel=TamaraMunzner

## Visual encoding / Interaction Idiom

In this level it is decided how data is going to be represented in the visual space and how the user will interact with it.
