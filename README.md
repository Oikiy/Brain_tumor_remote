## Introduction
This notebook presents a comprehensive machine learning study focused on brain tumor detection using a two-tier ensemble approach. The study employs three specialized base models in the first layer that feed into a meta-model in the second layer for final classification.

## Methods
### Dataset
- The study utilized a dataset comprising 3,000 MRI images distributed across the four classification categories:
  - Glioma,
  - Meningioma,
  - No tumor,
  - and Pituitary. 
- Images were resized to 300×300 pixels
- Pixel values were normalized to [0,1]
- Data augmentation techniques (rotation, width/height shifts, zoom) were applied to enhance model robustness
- The dataset was split into training (70%), validation (15%), and test (15%) sets.

### Model Architecture
- The study implements a two-tier ensemble approach:

#### First Layer Models:
- ***Custom CNN***: A 7-layer convolutional neural network with max pooling and dropout layers
- ***VGG16***: A pre-trained model fine-tuned for brain tumor classification
- ***EfficientNetB0***: A pre-trained model also fine-tuned for the task

#### Second Layer (Meta-Model):
- A Random Forest classifier that takes predictions from the three base models as input features

## Training Process
- Each first-layer model was trained for 20 epochs with a batch size of 16
- Learning rate was set to 0.0001 with Adam optimizer
- Early stopping with patience=5 was implemented to prevent overfitting
- The meta-model was trained on the outputs of the first-layer models

## Results
***Individual Model Performance:***
- Custom CNN: 50.76% accuracy
- VGG16: 72.08% accuracy
- EfficientNetB0: 76.90% accuracy

***Ensemble Performance***
- Meta-Model (Random Forest): 74.87% accuracy.

