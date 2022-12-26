# Open-World-Recognition-In-Image-Classification

Continual learning, considering the computer vision
field, refers to the ability of a visual object classification
system to incrementally learn about new classes once acquired data on them.
One of the main problems of the incremental learning scenario is catastrophic forgetting, i.e. adapting a model to new data results in performance degradation on
previous tasks. 

<img width="884" alt="incrlearn" src="https://user-images.githubusercontent.com/70110839/209574625-e43cfcb3-17aa-4b6f-af48-25d1c08b3d09.png">

This repository presents an exploration and re-implementation in pytorch of different incremental learning techniques: 
- **fine-tuning**, consisting of training the same network in subsequent steps adding a
neuron for each new class to the output layer.
- **Learning without Forgetting (LwF)** as proposed in the iCaRL paper. This technique envisions, besides the classification loss, a distillation loss which ensures that the discriminative information learned previously is not lost.
- **iCaRL**. In this framework the network is a trainable feature extractor followed by a single classification layer. A new countermeasure to catastrophic forgetting is introduced: the storage of exemplars, i.e. images from the previously
encountered classes. For the testing phase iCaRL uses the nearest-mean-of-exemplars
(NME) classifier, a variation of the nearest-class-mean classifier. An image is assigned to the class whose prototype,
which is is the average feature vector of all exemplars for a
class, is nearest to the image feature representation.

![base incremenatal](https://user-images.githubusercontent.com/70110839/209574335-63e27e96-c231-4da4-b3fb-162cc06636d0.png)


After the comparison of these models, **ablations studies** are conducted over loss functions (both classification and distillation terms are varied) and classifiers (using KNN or SVC instead of NME). Furthermore, it is proposed a **modification of the
nearest-mean-of-exemplars** classifier aiming to code the **dispersion of a class** in its features space, exploiting a
second exemplar set.


Finally, the model is tested in an Open World scenario, in which it could encounter classes never seen before. To address this, the models are added the capability to reject samples, labeling them as unknown. 

An in-depth description of the work can be found in https://github.com/ScorcaF/Open-World-Recognition-In-Image-Classification/blob/94c2e807cd9dd9891bb1941eddacb20f21bde461/Calderaro_Giannuzzi_Scorca.pdf
