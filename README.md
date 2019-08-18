# MOVIE-GERERE-PREDICTION
Objective
Classify a given malware into 9 different category.
Minimize multi-class error.
The model should not take more than a few minutes to return the results.
Data Overview
Source : https://www.kaggle.com/c/malware-classification/data For every malware, we have two files

.asm file (read more: https://www.reviversoft.com/file-extensions/asm) .bytes file (the raw data contains the hexadecimal representation of the file's binary content, without the PE header)
Total train dataset consist of 200GB data out of which 50Gb of data is .bytes files and 150GB of data is .asm files: Lots of Data for a single-box/computer.

There are total 10,868 .bytes files and 10,868 asm files total 21,736 files.

There are 9 types of malwares (9 classes) in our give data. Types of Malware:

Ramnit
Lollipop
Kelihos_ver3
Vundo
Simda
Tracur
Kelihos_ver1
Obfuscator.ACY
Gatak
Machine learning Problem.
This is clear that this is a multi-class classification problem as we have to classify a malware into 9 different category.

Performance metrics
Log-loss : We have used this metrics as this penalizes more if we make a prediction with more confidence and it actually is a wrong prediction.
Confusion Matrix : This will be used to see how many points are correctly classified vs the points which are incorreectly classified.
Approach
Data analysis.
We performed EDA and found out that Vundo(class 4), Simda(class 5) and Kelihos_ver1(class 7) are in minority.
Feature extraction.
We extracted unigram features from byte files and plotted TSNE plot to see whether points of same class are forming cluster or not.
We have used the following features in modelling . a. Unigram features from .byte files and top 1000 bigram features (based on idf values) of .byte files. b. Unigram features from .asm files. c. First 1000 pixels of image files of .asm files. We got this feature by converting .asm files to image files and then taking the first 1000 pixel values.
Modelling
We tried various models such as logistic regression , KNN, Random Forest and XGBoost. The best model that we got was XGBoost model which was trained on unigram of .byte files + bihgram of .byte files + unigram of .asm files and image features of .asm files. The best logloss that we got using these features and training XGboost model on this was 0.006.
