 Written Reflection — Fashion Classifier CNN

For this project, I built a fashion classifier using TensorFlow.js and p5.js. The program can recognize clothing items from the Fashion-MNIST dataset and can also classify clothing images uploaded by the user. Through this project, I learned how convolutional neural networks work and how different parts of a machine learning system connect together.

The project was divided into five main parts: loading the dataset, building the model, training the model, classifying images, and preprocessing uploaded images. Each part had an important role in making the program work correctly.

 1. Loading the Dataset

For the dataset, I used GitHub to host the Fashion-MNIST files instead of using an S3 bucket. I uploaded the files online and used the raw GitHub links inside the `DATA_BASE` variable so the sketch could download them directly.

When the user presses ENTER, the program downloads the training and testing files. Since the files are compressed, they first need to be decompressed before they can be used.

The image values are then converted from numbers between 0 and 255 into numbers between 0 and 1. This helps the neural network train better because smaller and consistent values are easier for the model to process.

The labels are also converted into arrays so the model can compare all ten clothing categories correctly.

This step is important because the model cannot train properly if the data is not loaded and prepared correctly.

2. Building the CNN Model (`buildModel()`)

The `buildModel()` function creates the neural network.

The model is made of several layers that each do a different job. The convolutional layers scan the image and try to find patterns like edges, curves, and shapes. The pooling layers reduce the image size while keeping the important information.

The flatten layer changes the image data into one long list of numbers so it can be passed into the dense layers.

The dense layers are responsible for making the final prediction. The last layer gives probabilities for the ten clothing categories using the softmax activation function.

For example, the model might say:

- Sneaker: 90%
- Sandal: 5%
- Boot: 5%

This means the model is most confident that the image is a sneaker.

The model uses the Adam optimizer and categorical crossentropy loss. The optimizer helps the model learn during training, while the loss function measures how wrong the predictions are.

This part helped me understand how CNNs slowly turn simple pixels into meaningful features that the computer can recognize.

3. Training the Model (`trainModel()`)

The `trainModel()` function teaches the neural network how to recognize clothing items.

The model trains using thousands of images from the dataset. During training, the network repeatedly looks at images and adjusts itself to improve its predictions.

The model trains for 8 epochs, meaning it sees the whole dataset eight times.

The batch size is set to 128, which means the model processes 128 images at once before updating its weights.

Validation data is also used to test how well the model performs on images it has never seen before. This is important because a model can sometimes memorize the training data instead of actually learning patterns.

While the model trains, the current epoch and accuracy are shown on the screen so the user can follow the progress.

This part showed me that machine learning models improve little by little over time by learning from mistakes.

4. Classifying Images (`classifyImage()`)

The `classifyImage()` function is responsible for making predictions.

The image pixels are first normalized between 0 and 1 because the model expects the same format that was used during training.

The image is then converted into a tensor and passed into `model.predict()`.

The model returns probabilities for all ten categories, and the program chooses the category with the highest probability as the final prediction.

I also used `tf.tidy()` to clean unused tensors from memory. Without it, TensorFlow.js would keep using more memory and eventually crash the browser.

This function is basically the part where the computer “guesses” what clothing item it sees.

5. Preprocessing Uploaded Images (`processAndClassifyUpload()`)

The uploaded image preprocessing was one of the most important parts of the project because real photos are very different from the Fashion-MNIST images.

The Fashion-MNIST dataset uses:

* grayscale images
* small 28×28 images
* centered objects
* dark backgrounds

However, uploaded images are usually colored, large, and often have white backgrounds.

The preprocessing function changes uploaded images so they look similar to the training dataset.

First, the program checks the corners of the image to see if the background is light or dark.

Then the image is cropped into a square and resized to 28×28 pixels.

After that, the image is converted into grayscale.

If the background is white, the colors are inverted so the clothing item becomes light on a dark background, just like the Fashion-MNIST images.

The processed image is then shown on the preview screen and sent to the classifier.

This part taught me that even a good model can fail if the input image format is too different from the data used during training.

Conclusion

Overall, this project helped me better understand how machine learning and convolutional neural networks work.

I learned how data is loaded, how CNN layers extract features from images, how models are trained, and how predictions are made in real time.

One of the biggest things I learned is that preparing data correctly is just as important as building the neural network itself.

This project gave me practical experience with TensorFlow.js and helped me better understand how image classification systems work behind the scenes.
