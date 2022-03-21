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


## Core-periphery structure [Jan 13, 2022]
In these experiments, I have find the core-periphery structure from average correlation matrices using Ramboch's algorithm. All the core-core connections are retained, but noisy core-periphery and periphery-periphery connections are removed using corresponding thresholds.

Best performance: \ 
Train accuracy / F1-score = 98.4/0.98 \
Validation accuracy / F1-score = 77.64/0.84 \
Test accuracy / F1-score = 69.44/0.77


## Fixed_single_threshold + Weight decay regularization [Jan 13, 2022]
In these experiemnts, I have used weight decay regularization on baseline single threshold model.

Best performance: \ 
Train accuracy / F1-score = 97.53 / 0.98 \
Validation accuracy / F1-score = 74.94/0.82 \
Test accuracy / F1-score = 67.76/0.76

## Graph attention network (Single head) [Jan 13, 2022]
In these experiments, I have used standard Graph attention network model with single head attention.

Best performance: \
Train accuracy / F1-score = 92.71 / 0.93 \
Validation accuracy / F1-score = 74.19 / 0.82 \
Test accuracy / F1-score = 69.29 / 0.78


## Graph attention network (timeseries feature) [Jan 24, 2022]
In these experiments, I have used standard Graph attention network model with single head attention. Instead of functional connectivity matrix as feature, we used parcelleted time series as feature.

Best performance: \
Train accuracy / F1-score = 89.71 / 0.91 \
Validation accuracy / F1-score = 65.67 / 0.75 \
Test accuracy / F1-score = 54.22 / 0.66


## Signed GCN [Jan 24, 2022]
In these experiments, I have used Signed GCN model. This model uses balance theory to aggrregate information of the positively linked neighbours and negatively linked neighbours seperately.

Best performance: \
Train accuracy / F1-score = 97.75 / 0.98 \
Validation accuracy / F1-score = 78.42 / 0.85 \
Test accuracy / F1-score = 71.88 / 0.79

## Graph attention network (Sparse graph) [Jan 27, 2022]
In previous experiments, we have used fully connected graph. Here, we retain edges with edge weights higher than thresholds.

Best performance: \
Train accuracy / F1-score = 79.16 / 0.85 \
Validation accuracy / F1-score = 72.06 / 0.81 \
Test accuracy / F1-score = 67.97/ 0.77

## Data augementation literature review [Feb 03, 2022]
We tried various deep graph network architectures and found that most of them are overfitting. We previosly experimented with SMOTE technique and marginally improved val/test performances. However, Overfitting issue is not resolved completely. Reviewed recent literature related to Data augmentation for brain connectivity features.

## Data augementation literature review [Feb 10, 2022]
Found BrainNetGAN[https://arxiv.org/abs/2103.08494] useful for brain connectivity data augmentation purpose. Understood the methodology involving Wassestein GAN (WGAN), WGAN with Gradient penalty (an improved version) and BrainNetCNN, a specific architecutre designed for adjaceny matrices.

## Vanilla GAN based approach [Feb 17, 2022]
We decided to first start with simple GAN based approach. Experimented with various architectures of Generator and Discriminator in systematic manner.

## WGAN for Data augmentation [Feb 24, 2022]
Similar to Vanilla GAN, Experimented with various architectures of Generator and Discriminator in systematic manner. I didn't find any equillibrium point.

## Results [March 03, 2022]
Tried few more architectures, I was not able to find equillibrium point. I visulize the data generated from the trained GANs. 
Samples generated using WGAN were not realistic, but samples generated using GANs were visually realistic.
Further, I tested 200 samples using pre trianed GCN model. Average accuracy: 61.84% 

## Implementation of BrainNetGAN [March 10, 2022 & March 17, 2022]
GAN and WGAN used fully connected architectures with huge number of trainable parameters. BrainNetCNN architecture shares the parameters across the nodes to limit the number of trinable parameters and alongwith preserves the graph type of structure across the layers. We will to leverage this special architecture for our purpose.
