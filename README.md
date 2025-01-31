# Tensorflow-Classing---Eye-For-Blind

## I. Problem Statement
In this capstone project, you need to create a deep learning model which can explain the contents of an image in the form of speech through caption generation with an attention mechanism on Flickr8K dataset. This kind of model is a use-case for blind people so that they can understand any image with the help of speech. The caption generated through a CNN-RNN model will be converted to speech using a text to speech library.

This problem statement is an application of both deep learning and natural language processing. The features of an image will be extracted by a CNN-based encoder and this will be decoded by an RNN model.

The project is an extended application of Show, Attend and Tell: Neural Image Caption Generation with Visual Attention paper.

The dataset is taken from the Kaggle website and it consists of sentence-based image descriptions having a list of 8,000 images that are each paired with five different captions which provide clear descriptions of the salient entities and events of the image.

## II. Summary
The project commenced by acquiring and displaying both images and their corresponding captions. An exploratory data analysis (EDA) was executed to gain insights into the provided dataset. The data underwent a cleaning process, which encompassed the refinement of the caption files.

Additionally, data preprocessing was conducted, involving the following tasks:

Tokenizing the captions and creating embedded vectors.
Preprocessing the images.
Subsequently, the dataset was partitioned into training and testing subsets. The InceptionV3 model was utilized, recognized for achieving a remarkable accuracy of over 78.1% on the ImageNet dataset. In this project, however, the objective was not image classification but the extraction of feature vectors from the images. Therefore, the softmax layer of the model was removed. The output from this layer originally possessed dimensions of 8x8x2048, which was then reshaped to (64, 2048).

This feature vector served as input to the CNN Encoder, which comprised a single fully connected layer. In an abstract sense, the encoder's output, an initialized hidden state, and the start token were combined and forwarded to the decoder.

The decoder, implemented as a recurrent neural network (RNN, specifically GRU), employed an attention mechanism to predict the next word. This attention mechanism directed the decoder's focus to specific regions of the image, enhancing accuracy and mitigating noise. The decoder generated the predicted caption and the decoder's hidden state as outputs, which were looped back into the model to calculate loss using "SparseCategoricalCrossentropy." Teacher forcing was utilized to determine the next input to the decoder.

The decoder ceased prediction when the model predicted the end token. The model's word predictions were established by assessing word probabilities within the vocabulary. The chosen approach was greedy search, which determined word probabilities based on their frequency in the vocabulary. This method sampled words, computed their probabilities, and selected the word with the highest probability.

Finally, the "BLEU score" (Bilingual Evaluation Understudy) was adopted as the evaluation metric for comparing predicted and actual captions, gauging the disparity between them.
