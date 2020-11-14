

# Pneumonia Diagnosis Project

## Directory

[Data](https://github.com/RCKettel/PhaseFour_ImageClassification/tree/main/Data)

[Notebooks](https://github.com/RCKettel/PhaseFour_ImageClassification/tree/main/Notebooks)

[References](https://github.com/RCKettel/PhaseFour_ImageClassification/tree/main/References)

[Reports](https://github.com/RCKettel/PhaseFour_ImageClassification/blob/main/Reports)

[src](https://github.com/RCKettel/PhaseFour_ImageClassification/tree/main/src)

## Business Understanding
For this project a Convolutional Neural Network deep learning model was created for a proof of concept that would predict if a patient had lungs infected with pneumonia.  The best model showed a high level of accuracy which would show the least number of results that are that would predict the patient does not have pneumonia when they actually do.  Or in other words, are false negatives.

## Accessing the Data
Due to the number of images and the size of the dataset its recommended that it is downloaded to a folder and keras Image Data Generator and flow_from_directory methods are used to access it. The data can be downloaded from Keras [here](https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia).  The data will be downloaded as a .zip file and will require a program to access it.  Once opened exploration will reveal a number of redundant or empty files that contain much of the same data or no data at all such as MACOSX.  These files were deleted since they were considered unnessecessary.  The approach used for this project was to take the train, val, and test files from their parent folder and access them directly to expedite access and reduce the amount of code. 

## The Data
The data contains pediatric X-ray images of lungs from 5863 patients.  These images were split into three different sets: Train, Val, Test each containing subsets: Normal, and Pneumonia.  This data took very little preperation since the data was already split into training and validation sets.  Due to a nearly three to one imbalance of images with healthy lungs to images with pneumonia the normal lungs set was resampled with SMOTE to better balance the data.

## Evaluation of FSM
Though the results of the model as tested by the validation and test scores show high accuracy ratings of .71 and .76 respectively the loss in both models is fairly high, above .5. This is likely due to how the function checks against false negatives. Since the data set was balanced by SMOTE, it is likely giving high penalizations to bad predictions causing a higher loss. In addition to the high loss, the disproportionate performace by the training data as compared to the validation and test data show evidence of an overfit model. This problem is usually caused by a model that is too complicated for the data it is working with. In Convolutional Neural Networks this can be rectified by tuning the hyperparameters of the model.

## Evaluation of Final Model







      
     
