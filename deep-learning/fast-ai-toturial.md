# Table of Contents

[Jupyter lab](#juptyer-lab)

[Lesson 1](#lesson-1)

[Fetching stategy](#fetching-stategy)

# Jupyter lab

## Modes

Edit Mode:: Allows you to edit a cell's content.

Command Mode:: Allows you to edit the notebook as a whole and use keyboard shortcuts but not edit a cell's content.

ECS + Enter + Enter -> edit mode

To existed => ESC

## Shortcuts

Shift+Enter:: Run the code or markdown on a cell

# Lesson 1

## Deep learning vocabulary

| Term                 | Meaning                                                                                                                                    |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| **Label**            | The data that we're trying to predict, such as "dog" or "cat"                                                                              |
| **Architecture**     | The _template_ of the model that we're trying to fit; the actual mathematical function that we're passing the input data and parameters to |
| **Model**            | The combination of the architecture with a particular set of parameters                                                                    |
| **Parameters**       | The values in the model that change what task it can do, and are updated through model training                                            |
| **Fit**              | Update the parameters of the model such that the predictions of the model using the input data match the target labels                     |
| **Train**            | A synonym for _fit_                                                                                                                        |
| **Pretrained model** | A model that has already been trained, generally using a large dataset, and will be fine-tuned                                             |
| **Fine-tune**        | Update a pretrained model for a different task                                                                                             |
| **Epoch**            | One complete pass through the input data                                                                                                   |
| **Loss**             | A measure of how good the model is, chosen to drive training via SGD                                                                       |
| **Metric**           | A measurement of how good the model is, using the validation set, chosen for human consumption                                             |
| **Validation set**   | A set of data held out from training, used only for measuring how good the model is                                                        |
| **Training set**     | The data used for fitting the model; does not include any data from the validation set                                                     |
| **Overfitting**      | Training a model in such a way that it _remembers_ specific features of the input data, rather than generalizing well to unseen data       |
| **CNN**              | Convolutional neural network; a type of neural network that works particularly well for computer vision tasks                              |

=> 


Machine learning is a discipline where we define a program not by writing it entirely ourselves, but by learning from data. **Deep learning** is a specialty within **machine learning** that uses **neural networks** with multiple layers. **Image classification** is a representative example (also known as image recognition). We start with **labeled data**; that is, a set of images where we have assigned a **label** to each image indicating what it represents. Our goal is to produce a program, called a **model**, which, given a new image, will make an accurate prediction regarding what that new image represents.

Every **model** starts with a choice of **architecture**, a general template for how that kind of model works internally. The process of **training** (or **fitting**) the model is the process of finding a set of **parameter** values (or **weights**) that specialize that general architecture into a model that works well for our particular kind of data. In order to define how well a model does on a single prediction, we need to define a **loss function**, which determines how we score a prediction as good or bad.

To make the training process go faster, we might start with a **pretrained model**—a model that has already been trained on someone else's data. We can then adapt it to our data by training it a bit more on our data, a process called **fine-tuning**.

When we **train** a model, a key concern is to ensure that our model **generalizes**—that is, that it learns general lessons from our data which also apply to new items it will encounter, so that it can make good predictions on those items. The risk is that if we train our model badly, instead of learning general lessons it effectively memorizes what it has already seen, and then it will make poor predictions about new images. Such a failure is called **overfitting**. In order to avoid this, we always divide our data into two parts, the **training set** and the **validation set**. We train the model by showing it only the training set and then we evaluate how well the model is doing by seeing how well it performs on items from the validation set. In this way, we check if the lessons the model learns from the training set are lessons that generalize to the validation set. In order for a person to assess how well the model is doing on the validation set overall, we define a **metric**. During the training process, when the model has seen every item in the training set, we call that an **epoch**.

All these concepts apply to **machine learning** in general. That is, they apply to all sorts of schemes for defining a model by training it with data. What makes **deep learning** distinctive is a particular class of architectures: the architectures based on **neural networks**. In particular, tasks like **image classification** rely heavily on **convolutional neural networks**, which we will discuss shortly.
