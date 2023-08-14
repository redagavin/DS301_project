# DS301_project

In the pursuit of advancing image classification techniques, we explore LSTM with embeddings for image classification, aiming to test whether integrating positional and channel embeddings into Long Short-Term Memory (LSTM) networks could refine their capacity to process image data. By doing so, we hoped to provide an alternative or even complementary solution to traditional Convolutional Neural Networks (CNN) for RGB image classification. 

Drawing inspiration from the transformative “Attention is All You Need” article, we integrated concepts from transformer architectures into LSTMs, with a particular focus on embeddings. By merging these advanced computational concepts, we hypothesized the emergence of several potential benefits:

1. Spatial Context Recognition: The model would potentially recognize the spatial context of pixels, understanding how they relate to one another within an image.
2. Enhanced Channel Specificity: By dedicating specific embeddings to each RGB channel, the model would be better suited to discern the nuances of colors and their significance in image data.
3. Versatility over Pure CNNs: With these enhancements, LSTM could offer a fresh perspective on image classification tasks, possibly capturing patterns and features that might be overlooked by CNNs.

However, there were several challenges that we needed to handle. First of all, without rigorous testing, we risked over-estimating our model’s capabilities. Second, the adaptation of positional encoding to 2D image data was also a challenge, since it is a concept traditionally utilized for 1D sequences. Thirdly, ensuring the effective interplay of different embeddings was crucial. Each embedding had to bring something unique to the table, adding value and distinct information. (we made positional embedding to generate unique values in range [1, 2] and channel embedding to generate values of [2.0, 2.5, 3.0], since there were three channels)

Our approach was structured and multi-faceted:
1. Adaptive Embeddings:
    - Positional Embedding
    - Sinusoidal Embedding (Variant of Positional Embedding)
    - Channel Embedding
2. LSTM Augmentation: Embeddings were seamlessly integrated with LSTM layers, maintaining dimensional consistency and ensuring smooth data processing.

In specific:
1. Positional Embedding Layer:
    - This layer adds positional information to each element in the sequence.
    - We generate a tensor channel_embedding that linearly spaces values between 1.0 and 2.0 for the size of a single channel.
    - The combined tensor for all channels is then repeated for every position in the sequence, essentially assigning a unique value between 1.0 and 2.0 for every element in the input sequence.
2. Channel Embedding Layer: 
    - This layer augments the input sequence with channel information.
    - The channel embeddings, defined by constants like [2.0, 2.5, 3.0], are repeated and summed with the original sequence for each position.
    - By doing so, we might be informing the LSTM to treat certain channels as more important or distinct than others.

# Code Structure
All code is in the notebook file, LSTM_with_embeddings.ipynb. Inside the notebook, you will find data preprocessing section, training and evaluation functions, model implementation and experiments, and result presentation.

# How To Run the Code
Please upload the notebook to google colab and run it on google colab. No additional dependencies or datasets are needed.

# Results and Observation
Experimental Evaluation-Accuracy

![unnamed](https://github.com/redagavin/DS301_project/assets/39891180/564d1fa3-0f29-47c1-9fef-4a4873595295)

![unnamed (1)](https://github.com/redagavin/DS301_project/assets/39891180/fb286cfd-5d24-4cfe-8eb0-e3e8ed484003)

Experimental Evaluation-Macro F1 Score

![unnamed (2)](https://github.com/redagavin/DS301_project/assets/39891180/0d408dfa-d7f3-4150-8c2b-9c89785ecb65)

![unnamed (3)](https://github.com/redagavin/DS301_project/assets/39891180/eeff2704-9097-4e54-899a-152f464fd0f9)


Contrary to our hypothesis, all the embeddings we designed worsen or maintain the performance of LSTM on image classification, let along bridging the performance gap between CNN and LSTM on image classification. Instead of providing useful information, the embeddings might added noise that causes performance drop. Future works can focus on designing and testing parameterized ways to implement position and channel embedding for LSTM on image classification.


