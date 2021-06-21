# Final Assignment:

This is the final and qualifying assignment for Phase I of EVA 2019 programme.   
Need to achieve beyond validation accuracy of 45% on the TinyImagenet dataset under the following constraints:
1. Only Google Colab to be used for limited amount of computational resource
2. No dropout for regularization
3. No 1x1 to increase number of channels
4. No dense layer
5. Total number of epochs should be less than 500

Similar approach from peer group published on [asXiv](https://arxiv.org/abs/1904.10429?utm_source=feedburner&utm_medium=feed&utm_campaign=Feed%253A+arxiv%252FQSXk+%2528ExcitingAds%2521+cs+updates+on+arXiv.org%2529).

**What I tried:**
* Tried with Resnet50 and also included skip connections in it. However the result was not going beyond validation score of 36.
* Switched from Resnet50 to Densenet. Introduced bottleneck approach with increamented number of channels at the start of each block. Added another layer of convolution at the end of concatation to make the receptive field size of 64
* Tried concatenating outputs from activations, batch normalization and convolution layers respectively. However the third approach resulted in better score.
* Trained the model first on low resolution (32 x32) and then on high resolution (64x64) -- Both without augmentation until I saw a good validation accuracy (53%)
* Tried with CLR trangular and trangular2, however could not get good result. Hence droped CLR and proceeded with ReduceLROnPlateu
* Tried with Keras augmentation only and then with both keras and imgaug augmentations. However in the both cases, I could not achieve better score.
* Then I continued only with imgaug augmentations. And this time, I did the training in three sets, with each set taking updated list of class_weights and last set with heavier aumentations.
* Subsequently, I tried a number of things including Adam-W and other augmentations to increase the validation accuracy further, however no luck.


**What I achived:**
* With training on low resolution images achieved validation accuracy of 33% (In 25 Epochs)
* Took the best weights and with further training on high resolution images, achieved validation accuracy of 53% (In additional 21 Epcohs)
* With augmentations and class_weights, achieved validation score of **62.4%** in (Effectively in additional 37 Epochs collectively from 3 sets)

**Note**
* Architecture changed from Resnet50 to **Densenet**
* **No Dropout** being used
* **No Dense** layer being used
* 1x1 **never** used to **increase** number of channels
* Number of augmentations used: **6**
* Number of model parameters **~ 7.3mn**
* **Effective number of epochs** to reach validation score of 62.4: **83**

