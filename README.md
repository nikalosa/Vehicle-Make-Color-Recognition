# Vehicle-Make&Color-Recognition
Vehicle manufacturer and color recognition model. Pytorch

### Vehicle Make Recognition

For this problem I found out Stanford University's paper with their own train & test data. (http://cs231n.stanford.edu/reports/2015/pdfs/lediurfinal.pdf) 
As it's mentioned in paper too, for this task with little number of data and resources transfer learning is the best practice. Among plenty of pretrained models
I finally chose resnext101_32x8d which produced best results (Also tried: googlenet).
##### Fine-tuning resnext101 model
After resnext's backbone two custom layers are comming. (LINEAR(2048, 512), RELU(), BATCHNORM(512)) and (LINEAR(512, 49))
##### Loss Function
For loss function I used custom implemented FocalLoss, which is better with this kind of data. (Also tried: CategorialCrossEntrophy, NLLLoss)
##### Optimizer
Adam optimizer (Also tried: adagrad, SGD)
##### Hyperparameters
learning rate: during first part of the training it was set to 0.001 as default for adam optimizer which converged in 0.00005 - 0.0001 range. For second part of the training it was set to 0.00003 with weight decay 0.000000001. (Second part means that I loaded the first trained model and continued training with different hyperparammeters and shuffled data)

Dataset contains 196 classes of cars, with their make, model and year names. I changed labeling with just manufactures name, because our goal is to predict Make not the whole model. It's 8144 images for training and 8144 for testing. The model ended up with 78% training and 70% validation accuracy.


### Vehicle Color Recognition

For this task and data preprocessing I used sighthound demo api which gives possibility to send an image of a car through api and it will send it's color and bounding box back. With this api I made myauto's (https://www.myauto.ge/) data to be more accurate and useful for training. 
Transfer learning is outcome here too. With the same pretrained model. I thought vgg would be better because color extraction could be possible easier after not very deep NN. But in that case still resnext101 was the best one to use. 


##### Fine-tuning resnext101 model
After resnext's backbone two custom layers are comming. (LINEAR(2048, 512), RELU(), BATCHNORM(512)) and (LINEAR(512, 9))
##### Loss Function
I used the same FocalLoss here too, like in make recognition
##### Optimizer
Adam optimizer (Also tried: adagrad, SGD), same as well.
##### Hyperparameters
learning rate: 0.0001


### Testing

For testing make recognition, you need just to use "predict_make" function. (For instance: predict_make('path/to/the/car/img'))
For testing color recognition, you need just to use "predict_color" function. (For instance: predict_color('path/to/the/car/img'))
$$$ SOON IT'LL BE ABLE FROM TERMINAL"
