# **Problem Description**

Motor vehicles are the most common form of transportation in North America, eight out of ten commuters travel by car, truck, or van to work, either as a driver or passenger. While most travels in motor vehicles are safe, sometime owner negligence or lack of knowledge cause conditions that can endanger both the driver, passengers and fellow vehicles in the road, one such point of contention are tires that when word down and faulty can result in less vehicle control and grip for the driver and in worst cases an uncontrollable tire blowout that could end up in a crash.

# **Project Description**

In this project a convolutional neural network based on the ResNet architecture will be trained to correctly identify good and defective tires based on tire images, this model will leverage the advantages of transfer learning on a known model, allowing for a great accuracy model that can be finetuned to the task at hand and be used to do identify when preventive maintenance or exchange of the tires is required by drivers, or could be used as a quality control model in the tire factories.

# **Methodology**

## Data Loading

![A screenshot of a computer

Description automatically generated](Aspose.Words.68e0356d-aa9e-4e1f-bbc0-d2d151ba354e.001.png)The dataset of images was obtained from [Kaggle](https://www.kaggle.com/datasets/warcoder/tyre-quality-classification/data) and contains 1854 tire images in various formats and sizes, these images come pre labeled as either defective (1028 images) or good (828 images). 

![](https://github.com/wariormex/INFO-6147_FinalProject/blob/main/Images/Aspose.Words.68e0356d-aa9e-4e1f-bbc0-d2d151ba354e.002.png)

After downloading the dataset, a dataframe containing the file name, file path, class name and the encoded class     index (defective: 0, good: 1) was generated. The dataframe then goes through a conversion to a DataSet object from pytorch with no transform beign applied to the images for visualization purposes and it finally receives the [expected image transformations for the ResNet architecture](https://pytorch.org/hub/pytorch_vision_resnet/).

## Data Exploration

![image](https://github.com/wariormex/INFO-6147_FinalProject/assets/91165602/a3a650a1-2e91-4435-82f7-751d7de31b8b)

The images are transformed by converting to PIL image, resizing to 256, cropping the center of the image (224), converting to tensor, and applying the expected normalization for the ResNet network.

![image](https://github.com/wariormex/INFO-6147_FinalProject/assets/91165602/53d6845b-ba20-4e6d-913b-3ebaaf325f79)

## Model Selection and Hyperparameters

For comparison purposes the [ResNet34 and Resnet152](https://pytorch.org/hub/pytorch_vision_resnet/) pretrained networks will be finetuned by substituting the last layer of the network with a dense layer of size of 2 neurons (2 expected classes), this last layer will be trained from scratch and finetuned for the dataset, since no activation function was used on the last layer cross entropy loss was used as the loss function alongside Adam as the optimizer. Both models will use a batch size of 64, learning rate of 0.001 and run for 10 epochs. The dataset will be split into training, validation, and testing subsets with a split of (0.7,0.1,0.2) respectively.

## **Model Results**

### ResNet34

![image](https://github.com/wariormex/INFO-6147_FinalProject/assets/91165602/bb8701ac-7485-41b4-a3fb-fa4b0ff723d4)

![image](https://github.com/wariormex/INFO-6147_FinalProject/assets/91165602/3c78e65d-8a83-4c66-92c2-a0b6ae8dd000)

![](https://i.imgur.com/DrhedOf.png)

![image](https://github.com/wariormex/INFO-6147_FinalProject/assets/91165602/ee9fe828-b870-46c1-b97e-afca7bdc9b32)

![image](https://github.com/wariormex/INFO-6147_FinalProject/assets/91165602/350d0ae2-8ca8-4b57-bcdf-05258e3c961a)

The ResNet34 model achieved an 89.19% accuracy on its last validation epoch with a loss of 0.229. During testing this model achieved an overall accuracy of 91%, where f1 score achieved similar results between both classes, but the precision metric differed by 6 points (94% defective vs 88% good), suggesting that the class imbalance (defective > good) affected the model training.

### ResNet152

![image](https://github.com/wariormex/INFO-6147_FinalProject/assets/91165602/66ddc677-fb81-4fdf-8f81-ee7dcd2cb376)

![image](https://github.com/wariormex/INFO-6147_FinalProject/assets/91165602/568c1b3b-3124-4890-ae3c-0a9c7bfda84a)

![](https://i.imgur.com/Wnqly82.png)

![image](https://github.com/wariormex/INFO-6147_FinalProject/assets/91165602/fd83967b-bb3c-493a-bc0f-a3a88c210ffa)

![image](https://github.com/wariormex/INFO-6147_FinalProject/assets/91165602/d0ea6d67-3da9-4d6c-957d-91ea43ddd3b3)

The ResNet152 model achieved a 91.89% accuracy on its last validation epoch with a loss of 0.1939. During testing this model achieved an overall accuracy of 94%, where f1 score also achieved similar results between both classes, the precision metric difference between classes increased to 98% defective vs 89% good, suggesting that the imbalance class theory has some merit to it.

# **Conclusions**

The ResNet architecture and its pretrained weight had an excellent performance on the task at hand, from the two model achieved, we can conclude that a simpler version of the model would provide similar results to its more complex counterparts, more finetuning in these simpler versions could squeeze performance to the point of having the same results or better than the complex model while keeping the model small enough to be used in wide array of devices with different computational capabilities.

# **References**

Government of Canada, Statistics Canada. (2023, August 22). *The Daily — Commuting to work by car and public transit grows in 2023*. https://www150.statcan.gc.ca/n1/daily-quotidien/230822/dq230822b-eng.htm
