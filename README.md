## Lung Cancer Detection

This project is based on the lung cancer detection competition [Data Science Bowl 2017](https://www.kaggle.com/c/data-science-bowl-2017/) on Kaggle.

Here I show how to use Tensorflow to build a 3D convolutional neutral network to detect cancer in lungs. However, the training 3D lung scan data provided is very limited (only ~1000 cases). Especially for a large model with millions of parameters like this, significant amount of data is needed to prevent overfitting and ensure successful training, and this is the biggest bottleneck here.

A more realistic approach would be using other datasets (such as [LUNA16](https://luna16.grand-challenge.org/)) which have lung nodule location information. We can then train a neural network on such dataset (most of them use U-Net), and use the result model on our dataset to find possible nodule locations to reduce the search space. In fact, [previous researches](https://thesai.org/Downloads/IJARAI/Volume4No4/Paper_6-Lung_Cancer_Detection_on_CT_Scan_Images_A_Review_on_the_Analysis_Techniques.pdf) almost all focus on detecting potential malignant pulmonary noudles instead of predicting cancer directly.

Here I only use the DSB2017 dataset itself, which does not contain any information other than whether the patients have lung cancers or not. So, the code is only a demonstration of how to perprocess such dataset and how to apply 3D CNN directly on it, and I wouldn't expect its performance to be much better then just random guessing due to the lack of data.

In fact, it seems that in the competition the models with the best results almost all utilize other datasets (especially the LUNA16 dataset), but the results are still not that good. The start-of-art nodule detection algorithm can help radiologists, especially for small nodules that are easy to be ignored by humans. However, the accuracy of such algorithm now is not good enough to be used alone, and building a cancer predicion model on the top of it would be unreliable.  Now the best loss we can achieve in DSB2017 is around 0.4, which has a large room to improve. Actually if one can predict cancer in every case with a probability only 2/3, he can get a loss around 0.4 (`-log(2/3) = 0.4055`), let alone the fact that current models are probably overfitted more or less, and would obtain worse results if the proportion of cancer cases change.

