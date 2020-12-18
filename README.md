![WordPneumoniaDeaths](https://github.com/RCKettel/PhaseFour_ImageClassification/blob/main/References/Images/WorldPneumoniaDeaths%202015-2017.png)

# Pneumonia Diagnosis Project

## Directory

[Data](https://github.com/RCKettel/PhaseFour_ImageClassification/tree/main/Data)

[Notebooks](https://github.com/RCKettel/PhaseFour_ImageClassification/tree/main/Notebooks)

[References](https://github.com/RCKettel/PhaseFour_ImageClassification/tree/main/References)

[Reports](https://github.com/RCKettel/PhaseFour_ImageClassification/blob/main/Reports)

[src](https://github.com/RCKettel/PhaseFour_ImageClassification/tree/main/src)

## Business Understanding
For this project a Convolutional Neural Network deep learning model was created for a proof of concept that would predict if a patient had lungs infected with pneumonia. The best model displayed a high level of accuracy which would demostrate the least number of false negatives.

## Accessing the Data
The data was downloaded from Kaggle [here](https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia) in the form of a zip file.  Due to the number of images and the size of the dataset, the images were downloaded to a folder and the keras Image Data Generator and flow_from_directory methods were used to access it.  Once opened exploration will reveal a number of redundant or empty files that were later deleted which contained the same data or no data.  The approach used for this project was to take the train, val, and test files from their parent folder and access them directly using a Tensorflow ImageDataGenerator and flow_from_directory to expedite access. alternative methods to access the data were used as there was 1.15 GB of image data that could be processed on the local machine but would have caused issues when running the models in the Jupyter Notebook or attmempting to push work to a repository. 

## The Data
The data was pediatric X-ray images of lungs from 5863 patients. These images were split into three different sets: Train, Val, and Test; each containing subsets: Normal, and Pneumonia. This data took very little preperation as it was already split into training and validation sets.  The Val classes were small in comparison to the training data as a result it was necessary to triple the number of samples by moving some of the images from the Train data folders to the Val folder.  This was done physically using the file explorer or finder on the local machine.  Due to a nearly three to one imbalance of images in the Normal  to Pneumonia images sets, SMOTE resampling was used to better balance the data to prevent bias.  

## First Simple Model
The first simple model focused on accuracy and  was very basic being made up of an instantiating convolutional layer followed by a layer with maxpooling  and a final sigmoid layer.  the activator used for the model was relu as it does better in shallow networks.  The optimizer and the loss functions were the standard adam and binary crossentropy that are often used in models whose output layer activation is sigmoid.  The fit method contained non-standard class weights that were calculated when instantiating the flow_from_directory method and are based on the compared datapoints of the training and target data from the training dataset.  These were used to help balance the weights of the model to reduce variance.

![FSM](https://github.com/RCKettel/PhaseFour_ImageClassification/blob/main/References/Images/fsm.png)

## Evaluation of FSM
Though the results of the model as tested by the validation and test scores showed high accuracy ratings of .71 and .76 respectively the loss in both models was fairly high, above .5.  This was likely due to how the function checks against false negatives.  Since the data set was balanced by SMOTE, it was likely giving high penalizations to bad predictions causing a higher loss.  In addition, the disproportionate performace by the training data as compared to the validation and test data show evidence of an overfit model.  This problem is usually caused when a model is too complicated for the data it is working with.  In Convolutional Neural Networks this can be rectified by tuning the hyperparameters of the model.

![FSMConfusionMatirix](https://github.com/RCKettel/PhaseFour_ImageClassification/blob/main/References/Images/FSMconfusion.png)

## The Final Model
The final model also focused on accuracy and was made up of eight layers. The instantiating convolutional layerand two hidden convolutional layers, all followed by maxpooling layers, an added dropout layer, a flattening layer and a final dense sigmoid output layer. The activation of each convolutional layer, used a tan-h activation which through expreimentation turned out to yeild the best results.  The dropout rate for the model was a standard twenty percent and the optimizer was adam as in the previous model. Since the Convolutional Neural Network didn't have an instantiated kernel, bias regularization was tested on the model but consistently yeilded bad results often lowering the accuracy of the data.  For these reasons an L2 activity weight regularizer was used to penalize the outgoing activity of each layer since it may lower a sigmoids activity but it wont drop it entirely lowering its impact while keeping its computational input.  Early stopping was used as well to halt the progression of the models development before it began to degrade preventing loss.  Finally, a non-standard focal loss function was added to penalize the harder to classify image data and allow the model to put more priority on data that is easier to learn all of which helped minimize the number of incorrect predictions reducing loss, one of the major issues in the FSM.

![FinModel](https://github.com/RCKettel/PhaseFour_ImageClassification/blob/main/References/Images/FinModel.png)

## Evaluation of Final Model
This model shows much less evidence of being overfit. Though the accuracy of the training data at 1.0 is still unrealistic in comparison to the val data being at .89, the two correlate much better in the plot of thier results.  The loss is also much lower as the focal loss function lowered the number of bad predictions by making the model learn the data at a more even rate.  The final test scores showed the model was able to generalize to unseen data as it showed an accuracy of .80 and a loss of .126.

![FinConfusionMatrix](https://github.com/RCKettel/PhaseFour_ImageClassification/blob/main/References/Images/FinalMconfusion.png)



      
     
