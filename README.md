# ECE-C147-Project
## EEG Classification Project
Contributors: Austin Liu, Brittney Trinh, Joseph Tseng

## Abstract:

This study explores the use of Convolutional Neural Networks (CNNs) and Long Short-Term Memory (LSTM) Neural Networks for the classification of time-series Electroencephalogram (EEG) data. The study compares the performance of pure CNNs against a hybrid architecture that combines CNNs with LSTMs. The dataset consists of EEG recordings, and the goal is to classify activities a subject was performing based on the EEG signals. The results indicate that the pure CNN model outperforms the hybrid CNN-LSTM model as well as the pure LSTM model in terms of classification accuracy.

## Introduction

In this study, we investigate the use of Convolutional Neural Networks (CNNs) and Long Short-Term Memory (LSTM) Neural Networks to classify EEG data. CNNs are well-suited for capturing spatial patterns in the EEG signals, while LSTMs are effective in modeling temporal dependencies. By combining these two architectures, we aim to optimize the classification accuracy for EEG signals while also comparing how they perform individually.

The study also examines the impact of data duration on classification accuracy, seeking to identify the minimum duration necessary for reliable classification performance. Furthermore, the study investigates the generalizability of training on data from a single subject to improve classification accuracy across multiple subjects.
Through these investigations, the study aims to provide insights into the optimal use of CNNs and LSTMs for EEG signal classification, while also addressing key questions regarding the generalization of training across subjects and the influence of data duration on classification accuracy.

## Results

Our CNN architecture consists of four 1D-convolution layers followed by one fully-connected layer that outputs the logits into a softmax loss. Each of our convolutional layers is followed by an ELU activation, a batch normalization layer, a max-pool layer with a kernel size of 3, and a dropout layer removing 30% of the neurons. Our convolutional layers contain 15, 25, 75, and 90 filters respectively, each with a kernel size of 5. Additionally, we found that adding L1-regularization to the weights of the fully-connected layer had a considerable effect on the performance of our model. Our results show that the pure CNN model that was trained and tested on all subjects performed better than both the pure LSTM model and the CNN-LSTM hybrid model, with an ability to correctly classify 71.3% of the test data.

Additionally, we trained the CNN model on data only from subject one and tested it on data among all subjects to gauge the generalizability of the data amongst subjects. This model did noticeably worse (accuracy=0.34) than the CNN that was trained on data from all subjects, with a test accuracy of 34%, indicating that the EEG data can drastically vary from subject to subject.

The LSTM architecture underperformed compared to the CNN architecture, and was only able to accurately classify 34.5% of the test data. This was unexpected due to the inherent temporal nature of the EEG data, and may signify that the data does not have strong temporal dependencies between time steps.

The CNN-LSTM hybrid model consisted of the four convolutional layers from our pure CNN model followed by an LSTM layer with a hidden size of 15. The LSTM layer outputs to a fully-connected layer that produces the logits for the softmax loss. Although the CNN-LSTM hybrid model was expected to outperform the pure CNN model due to its ability to capture temporal differences in the data, our results contradicted this, with our hybrid model having an accuracy of 53.7%.. We speculate that there may be weak temporal dependencies across time steps, causing the LSTM layer to underperform.

In our investigation of the impact of data duration on model performance, we trained five CNN models, each with different data durations ranging from 200 time steps to 1000 time steps. The results showed a clear upward trend in accuracy with respect to data duration. Additional analysis suggests that this is due to the fact that some activities don’t show clear patterns until time steps further into the trial. For instance, class 0 (cue onset left) and class 2 (cue onset foot) perform poorly on the model trained on the first 200 time steps, but perform well on the models trained on more time steps. This indicates a high variance in the data across trials for these classes in early time steps, but show patterns in further time steps.

## Discussion

One noticeable insight that helped the performance of the pure CNN was the importance of the preprocessing step. In the given template, there was an issue of data leakage caused by preprocessing the data before splitting it into training and validation sets. This causes the validation set to have somewhat of a grasp on the information produced in the training set, which negatively impacts the testing accuracy.
Furthermore, the pure LSTM also had a poor performance. This is likely due to the lack of data augmentation tactics. Further studies should also take note of the pure LSTM model’s limitations in its architecture and should look into Bidirectional LSTM models for more robust feature extractions and to improve the pure LSTM model’s contextual understanding.

## References
M. Fatourechi, A. Bashashati, R. K. Ward, G. E. Birch. EMG and EOG artifacts in brain computer interface systems: a survey. Clinical Neurophysiology 118, 480–494, 2007.

M. Naeem, C. Brunner, R. Leeb, B. Graimann, G. Pfurtscheller. Seperability of four-class motor imagery data using independent components analysis. Journal of Neural Engineering 3, 208–216, 2006.

C. Brunner, M. Naeem, R. Leeb, B. Graimann, G. Pfurtscheller. Spatial filtering and selection of optimized components in four class motor imagery data using independent components analysis. Pattern Recognition Letters 28, 957–964, 2007.

A. Schl¨ogl, C. Keinrath, D. Zimmermann, R. Scherer, R. Leeb, G. Pfurtscheller. A fully automated correction method of EOG artifacts in EEG recordings. Clinical Neurophysiology 118, 98–104, 2007. 

A. Schl¨ogl, J. Kronegg, J. E. Huggins, S. G. Mason. Evaluation criteria in BCI research. In: G. Dornhege, J. del R. Mill´an, T. Hinterberger, D. J. McFarland, K.-R. M¨uller (Eds.). Toward brain-computer interfacing, MIT Press, 327–342, 2007.
