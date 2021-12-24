# Project-updates

## Fixed threshold with Softmax layer
In previous models, we were not using softmax layer after fully connected layer.
These models are evaluated at best_validation checkpoint + 20 epochs.

Best performance:\
Train accuracy = 88.75\
Validation accuracy = 81.82\
Test accuracy = 68.73


## Weighted Cross-entropy loss
In this approach, I have used whole dataset at a time instead of taking samples from Majority class (CN cohort) to balance the class.
Splitted whole data into train, validation and test group (ratio = 70 : 15 : 15 ), while maintaining Age and Gender distribution across the groups.
Picked 100 seeds, shuffled data randomly for each seed and repeated above point for each seed.
While training, Used Weighted cross entropy as loss function with weight = CN_count / AD_count.

Best performance:\
Train accuracy = 94.23\
Validation accuracy = 75.16\
Test accuracy = 63.47


## Cross-entropy loss validation
I monitored validation loss instead of validation accuracy in these simulations. I used the softmax layer and evaluated the model at the early stopping checkpoint. 

Best performance:\
Train accuracy = 91.60\
Validation accuracy = 77.38\
Test accuracy = 69.56


## Cross-entropy loss validation + Negative edge weights (Normalize = False)
In these simulations, Negative edges are retained, and aggregated features were not normalized by degree of nodes. Again CE loss was validated, used softmax layer, evaluated the model at the early stopping checkpoint.

Best performance:\
Train accuracy = 91.60\
Validation accuracy = 77.38\
Test accuracy = 69.56
