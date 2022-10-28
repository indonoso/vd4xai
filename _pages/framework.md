---
permalink: /framework/
---
Munzner’s framework is built for information visualization, but we argue that XAI applications are complex enough to require additional definitions to create a compelling visualization. Therefore, through this extension of the nested model, we address the analysis and validation of visualizations to XAI applications.

# Roles
## Adding User Roles

Originally, the nested model considered two roles: **end-user** and **visualization designer**. We
added two additional roles: **AI expert** and **Domain expert**. Notice
that in some cases, the same person can take several roles, as in the
case that the domain expert is also the end-user of an XAI application.
For generalization, we will consider them as different subjects in our
proposed framework.

The objective of an XAI visualization is to help interpret a particular
prediction made by the AI method to a given input case. Since AI and XAI
methods can have several layers of complexity, it is necessary to
include the role of AI experts in defining tasks, interacting with the
AI/ML model, and subsequent validations. In particular, the AI expert
knows to validate the correct use of the AI/ML model, extract the data
from the XAI method and validate that the XAI method can be applied to
the AI model. For instance, if the AI model is a decision tree, the AI
expert knows that attention mechanism [@AttentionMechanism] is not a
valid XAI method. Or, if the model is a transformer
[@TransformerAttention] and we use an attention mechanism to explain the
classification of a document, the AI expert knows from which layer we
should extract the attention values.

Moreover, the AI model will, in many cases, solve a task in a specific
domain, such as biology, finance, and law. Previous work has shown that
expert knowledge is important when deploying systems. For instance, Rojo
et al [@ROJO2021106183] designed a visualization that allowed domain
experts to select a model according to expert knowledge. This system
increased trust and understandability of the model. The issue is that
the knowledge related to these domains is not necessarily familiar to a
visualization designer, AI expert, or end user. There is a need to
include domain experts to make practical decisions based on alternative
designs produced by the visualization designer and the AI expert. For
example, explaining a medical x-ray classification to a patient involves
medical knowledge, and the end-user, i.e., the patient, does not
necessarily know about medicine. For this reason, a domain expert user
such as a medical doctor can justify and validate design decisions that
effectively communicate the information to the end user.

The interaction between these new roles, the visualization designer and
the end-user, is key to choose the most effective visual and
interactive encoding. Thus, we propose the moment when the new roles
have to interact in the different levels of the nested models:

1.  **Domain situation**[DS]{.ds} Since, at
    this level, the whole problem and data are presented, it is
    necessary to involve the two new roles. This way, the AI expert can
    understand the XAI problem to be addressed, and the domain expert
    can provide more information about the application domain and its
    data.

2.  [Data/task abstractionDTA]{.dta} At
    this stage, the visualization designer can make the choices on its
    own.

3.  **Visual Encoding / Interaction
    Idiom**[VEII]{style="background-color: green"} In the third level,
    the visualization designer makes decisions around the visualization
    design. Therefore, we propose that both new roles participate in
    validating the design decisions. The AI expert validates that the
    data related to the XAI model or method is interpreted correctly.
    For instance, if data corresponds to the probability given by the
    AI/ML model to classify a document, the AI expert can validate that
    the visual encoding allows us to understand that this value is a
    probability. The domain expert can validate that the design focuses
    on the relevant data of the problem and is understandable in the
    specific domain. For example, suppose we are explaining the
    classification of x-ray images and want to focus on an organ. In
    that case, the domain expert can guide the most effective way to
    highlight an organ on the x-ray and ensure that the end user can
    understand it.

4.  **Algorithm**[A]{style="background-color: pink"} Finally, the last
    level is to build the visualization, and therefore, it is not
    necessary to involve the new roles to make this task.

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
