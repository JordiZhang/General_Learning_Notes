Autoencoders are a direct extension from the neural network, used to learn efficient embeddings of input data. To do so, we setup a simple neural network as a regression task. The goal is to to reconstruct the input data. The neural network looks as follows:
![[autoencoder.png]]
The encoder converts the inputs into lower dimension representations, the code, and the decoder reconstructs the code back into the original input with as little error as possible. This compression of the hidden layers forces the autoencoder to capture the most important features of the input data. Note that autoencoders are usually symmetric as we want the encoder and decoder to be essentially the same but in the opposite direction.
# Variations and Applications
Autoencoders are very simple to understand so we won't go in depth on the different variations as a simple description suffices to understand them.
- Stacked Autoencoders: Autoencoders with more than one hidden layer
- Sparse Autoencoders: Autoencoders using the Kullback-Leibler divergence, similar to L1 regularization, it forces sparse weights.
- Denoising Autoencoders: Trained using Noisy inputs and clean outputs, thus model learns to clean the noise.
- Anomaly Detection: We can train autoencoders using normal data. Then if we encounter that some unseen data point results in a high reconstruction error, then this is an anomaly.

