Where Does My CNN Make Its Mistakes?
Project Overview

This project builds a Convolutional Neural Network (CNN) to recognise handwritten digits from the MNIST dataset and investigates where the model makes mistakes. The main question is whether adding a deeper convolutional layer changes the types of errors made by the model.

The project compares an original CNN with a deeper version of the same network. Both models are evaluated using test accuracy and confusion matrices.

Dataset

The project uses the MNIST handwritten digit dataset. It contains 70,000 grayscale images of handwritten digits from 0 to 9. Each image has a resolution of 28 × 28 pixels.

The data was divided into:

56,000 training images

14,000 test images

The images were reshaped from 784 pixels into 28 × 28 × 1 images and the pixel values were scaled from the range 0–255 to the range 0–1.

First CNN Model

The first model was a small convolutional neural network with the following structure:

Input layer: 28 × 28 × 1

Conv2D: 32 filters, 3 × 3 kernel, ReLU activation

MaxPooling2D: 2 × 2

Dropout: 0.3

Flatten

Dense: 64 units, ReLU activation

Dense: 10 units, softmax activation

The model was compiled using the Adam optimiser and sparse categorical crossentropy loss. EarlyStopping was used to reduce unnecessary training and help control overfitting.

Evaluation of the First Model

The first CNN achieved a test accuracy of 98.64%.

The confusion matrix showed that the most common mistake was predicting 9 instead of 4, which happened 24 times. The second most common confusion was predicting 8 instead of 2, which happened 10 times.

These errors may occur because some handwritten versions of these digits have visually similar shapes.

Model Modification

To investigate whether a deeper network would change the mistakes, a second CNN was created.

Only one change was made: before the Flatten layer, a second convolutional and pooling block was added:

Conv2D: 64 filters, 3 × 3 kernel, ReLU activation

MaxPooling2D: 2 × 2

All other important training settings were kept the same so that the comparison between the two models was fair.

Results
Model	Test Accuracy
Original CNN	98.64%
Deeper CNN	98.92%

The deeper model achieved a slightly higher test accuracy.

The two main confusion pairs were also reduced:

Confusion Pair	Original CNN	Deeper CNN
4 → 9	24	13
2 → 8	10	7

The number of errors where a true 4 was predicted as 9 decreased from 24 to 13. The number of errors where a true 2 was predicted as 8 decreased from 10 to 7.

Error Analysis

The results show that accuracy alone does not tell the whole story. The confusion matrices provide more detailed information about which digits are difficult for the model to distinguish.

The deeper network slightly improved the overall accuracy and reduced both of the main confusion pairs identified in the first model. The reduction was particularly noticeable for the 4 → 9 confusion.

Ethical Considerations

A handwritten digit recognition system may not perform equally well for everyone because handwriting styles can vary across age, country, education, and personal habits. If some handwriting styles are under-represented in the training data, the model may make more mistakes on those styles.

A confident but incorrect prediction could have serious consequences in real-world applications such as reading account numbers, postcodes, or other important information. Therefore, the model should be carefully tested on diverse handwriting before being used in a real reading pipeline.

Reflection

One of the most useful parts of the project was analysing the confusion matrix rather than relying only on accuracy. The first model already performed very well, but the confusion matrix showed specific digit pairs that were more difficult to recognise.

The deeper model was also useful because it allowed me to investigate whether learning more detailed visual features could change these mistakes. The improvement in overall accuracy was small, but the reduction in the main confusion pairs showed that the model's errors changed in a meaningful way.

One limitation is that the project used a single train/test split and focused on the MNIST dataset. Further work could test the models on other handwritten digit datasets or on more diverse handwriting styles to investigate how well the results generalise.

Conclusion

The CNN performed very well on the MNIST test set, achieving 98.64% accuracy in the original model. Its most common errors involved confusing 4 with 9 and 2 with 8.

Adding a second convolutional and pooling block increased the test accuracy to 98.92% and reduced both of the main confusion pairs. This suggests that the deeper model learned additional features that helped distinguish some visually similar handwritten digits. The project demonstrates why examining specific model errors is important alongside overall accuracy.
