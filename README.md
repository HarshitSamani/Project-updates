# Project-updates

## Fixed threshold with Softmax layer [Dec 24, 2021]
In previous models, we were not using softmax layer after fully connected layer.
These models are evaluated at best_validation checkpoint + 20 epochs.

Best performance:\
Train accuracy = 88.75\
Validation accuracy = 81.82\
Test accuracy = 68.73


## Weighted Cross-entropy loss [Dec 24, 2021]
In this approach, I have used whole dataset at a time instead of taking samples from Majority class (CN cohort) to balance the class.
Splitted whole data into train, validation and test group (ratio = 70 : 15 : 15 ), while maintaining Age and Gender distribution across the groups.
Picked 100 seeds, shuffled data randomly for each seed and repeated above point for each seed.
While training, Used Weighted cross entropy as loss function with weight = CN_count / AD_count.

Best performance:\
Train accuracy = 94.23\
Validation accuracy = 75.16\
Test accuracy = 63.47


## Cross-entropy loss validation [Dec 24, 2021]
I monitored validation loss instead of validation accuracy in these simulations. I used the softmax layer and evaluated the model at the early stopping checkpoint. 

Best performance:\
Train accuracy = 91.60\
Validation accuracy = 77.38\
Test accuracy = 69.56


## Cross-entropy loss validation + Negative edge weights (Normalize = False) [Dec 24, 2021]
In these simulations, Negative edges are retained, and aggregated features were not normalized by degree of nodes. Again CE loss was validated, used softmax layer, evaluated the model at the early stopping checkpoint.

Best performance:\
Train accuracy = 70.35\
Validation accuracy = 76.36\
Test accuracy = 62.72


## Validation with Weighted CE loss [Dec 24, 2021]
In this approach, I have used whole dataset at a time instead of taking samples from Majority class (CN cohort) to balance the class and also used weighted CE loss for validation.

Best performance: \
Train accuracy = 96.29\
Validation accuracy = 73.05\
Test accuracy = 66.25


## Community detection + CE loss validated [Dec 30, 2021]
In this approach, I have used CE loss for validation with community structure in graph.

Best performance: \
Train accuracy = 86.96\
Validation accuracy = 77.93\
Test accuracy = 68.81


## Trainable threshold + CE loss validated [Dec 30, 2021]
In this approach, I have used modified GCN with trainble threshold and used CE loss for validation.

Best performance: \
Train accuracy = 88.05\
Validation accuracy = 77.53\
Test accuracy = 68.15


## Fixed threshold + F1-score validated (w/o early-stopping) [Dec 30, 2021]
In this approach, I used F1-score for validation, and run the experiment for 200 epochs without using early-stopping for creating checkpoints.

Best performance: \
Train accuracy / F1-score = 90.28 / 0.91 \
Validation accuracy / F1-score = 77.94 / 0.77 \
Test accuracy / F1-score = 63.61 / 0.64


## Fixed threshold + F1-score validated + Minority class oversampled [Dec 30, 2021]
In these experiments, I have used baseline GCN model, Oversampled the minority class and validated F1-score.

Best performance: \
Train accuracy / F1-score = 98.43/0.98 \
Validation accuracy / F1-score = 76.41/0.83 \
Test accuracy / F1-score = 68.3/0.76


## Fixed_Communtiy + F1-score validated + Minority class oversampled [Jan 06, 2022]
In these experiments, I have used community structure based model, Oversampled the minority class and validated F1-score.

Best performance: \
Train accuracy / F1-score = 98.39/0.98 \
Validation accuracy / F1-score = 75.96/0.83 \
Test accuracy / F1-score = 69.11/0.78


## Fixed_single_threshold + SMOTE [Jan 06, 2022]
In these experiments, I have used baseline GCN model, Oversampled the minority class using SMOTE technique and validated F1-score.

Best performance: \
Train accuracy / F1-score = 96.49 / 0.98 \
Validation accuracy / F1-score = 75.48 /0.83 \
Test accuracy / F1-score = 67.74 / 0.76


## Core-periphery structure [Jan 12, 2022]
In these experiments, I have find the core-periphery structure from average correlation matrices using Ramboch's algorithm. All the core-core connections are retained, but noisy core-periphery and periphery-periphery connections are removed using corresponding thresholds.

Best performance: \ 
Train accuracy / F1-score = 98.4/0.98 \
Validation accuracy / F1-score = 77.64/0.84 \
Test accuracy / F1-score = 69.44/0.77


## Fixed_single_threshold + Weight decay regularization [Jan 12, 2022]
In these experiemnts, I have used weight decay regularization on baseline single threshold model.

Best performance: \ 
Train accuracy / F1-score = 97.53 / 0.98 \
Validation accuracy / F1-score = 74.94/0.82 \
Test accuracy / F1-score = 67.76/0.76

## Graph attention network (Single head) [Jan 12, 2022]
In these experiments, I have used standard Graph attention network model with single head attention.

Best performance: \
Train accuracy / F1-score = 92.71 / 0.93 \
Validation accuracy / F1-score = 74.19 / 0.82 \
Test accuracy / F1-score = 69.29 / 0.78
