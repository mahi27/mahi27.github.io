---
layout: post
title: Recognizing hand-written digits using ANN
author: sal
categories: [Neural networks]
featured: false
hidden: false
image: assets/images/post_2_meme.jpeg
---

<link href="https://afeld.github.io/emoji-css/emoji.css" rel="stylesheet">
<h2><span style="text-decoration: underline;"><strong>Introduction</strong></span></h2>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Hand-written digit recognition falls under the field of research, Optical Character Recognition(OCR). OCR is the mechanical or electronic conversion of images of typed, handwritten or printed text into machine-encoded text. It is a common method of digitising hard copies of books, invoices, bank statements etc so that they can be electronically edited, searched,and stored more compactly. More specifically, digitising hand-written text is called Intelligent Character Recognition(ICR), a sub-field of OCR.</p>
<p>In this post, we&rsquo;ll be looking at how we can use an artificial neural network to predict hand-written digits.</p>
<h2><span style="text-decoration: underline;"><strong>The Approach</strong></span></h2>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; This is one of my projects I did when I started learning about neural networks. This would make a perfect project for beginners who want to start with image processing/neural networks.The approach I would be discussing in this post would involve extracting features from the image and building an ANN.</p>
<p>Well, as we have discussed in my previous post, images are represented as a matrix of pixel values. How do we extract features from them?</p>
<p>There are several feature extraction techniques and what worked for one application might not work for another.In this case, Histogram of Oriented Gradients(HOG) is used to extract the features of digits.</p>
<h4><strong>Histogram of Oriented Gradients</strong></h4>
<p>Using HOG, a feature vector can be created which is a representation of "useful" information in the image.</p>
<p>What is "useful" information? Let's say our job is to detect coffee mug in images. An edge detector would be useful, not the color or text on the mug. The shape detected would be enough to differentiate it from other objects.</p>
</p> In HOG, the histograms of directions of gradients are used as features. Gradients give intensity change (both direction and magintude) at any point in the image. They are useful because their magnitude is larger at the edges. HOG captures the information about gradients by dividing the image into blocks and blocks are divided into cells. In these cells the gradients are computed per pixel by applying a horizontal and vertical gradient filter to the image. With each pixel having an orientation and magintude, a histogram for all the orientations in a cell is built with bins (-180 - 180 or 0 - 360) and the magnitude as the vote in the histogram. These histograms built for each cell are concatenated for each block to produce a feature vector.This feature vector is given as an input to the artifical neural net.</p>
<figure><img src="{{ site.baseurl }}/assets/images/hog_animation.gif" align = "middle"><figcaption style = "font-size:9px;"> Source:https://gurus.pyimagesearch.com/lesson-sample-histogram-of-oriented-gradients-and-car-logo-recognition/</figcaption></figure>
<h4><strong>Artificial Neural Network(ANN)</strong></h4>
<p>Artificial neural networks are the reason for majority of the advances in artificial intelligence. They are inspired from how humans receive and process information. Billions of cells called neurons in our brain process information in the form of electric signals. They receive the stimuli through dendrites of the neuron, process in the cell body and fire (sends a pulse down the nerve to other connected neurons through axon) if the result is greater than a set threshold.</p>
<figure><img src="{{ site.baseurl }}/assets/images/neuron.png" align = "middle"><figcaption style = "font-size:9px;"> Source:https://simple.wikipedia.org/wiki/Neuron</figcaption></figure>
<p>Artificial Neural Network(ANN) consists of layers of nodes which are analogous to neurons in brain. It has an input layer, hidden layer(s), and an output layer. The nodes are connected by lines which have weight that are analogous to synapses in brain. The input and the hidden layers also have a bias node with weight = 1 added to increase the flexibility of the model to fit the data.</p>
<figure><img src="{{ site.baseurl }}/assets/images/ann.PNG" align = "middle"></figure>
<p>Each layer receives inputs from the layer to its left, these inputs are multiplied by the weights of the connections and summed. These values at each node are given as input to the next layer, if the value is more than a certain threshold specified.This is called forward propagation.</p> 
<p>How does the neural net learn?<br> They learn by a feedback process called backpropagation. The output obtained from the forward pass is compared with the actual output. The difference between them is used to modify the weights to the output layer through the hidden layer(s) to input layer. This process is repeated over and over until the model has the desired accuracy.</p>
<figure><img src="{{ site.baseurl }}/assets/images/backprop.png" align = "middle"><figcaption style = "font-size:9px;"> Source:https://goo.gl/Cs5r3d</figcaption></figure>
<p>ANN is called a black box method as studying its structure won't give any understanding on the structure of the function being approximated. Watch <a href="https://www.youtube.com/watch?v=x_Eamf8MHwU" target="_blank">this</a> amazing video to understand more about back propagation.</p>
<h2><span style="text-decoration: underline;"><strong>Dataset</strong></span></h2>
<p>The <a href = "http://yann.lecun.com/exdb/mnist/" target="_blank">MNIST database</a> of hand-written digits is used for building the model. It has 60,000 images for training and 10,000 images for testing. You can also download hand-written images from kaggle's Digit Recognizer competition.</p>
<h2><span style="text-decoration: underline;"><strong>Feature Extraction and Training</strong></span></h2>
<p>I have inverted the images and centered the digits in the image using bounding box. These cropped out digit images were all resized to 28X28. Cell size of 7X7 is used to extract hog features. This feature vector is given as input to a simple feed-forward neural network with two hidden layers. After a 100 iterations, with a batch size of 32, the resulting accuracy was close to 99%. </p>
<h2><span style="text-decoration: underline;"><strong>Testing</strong></span></h2>
I have saved the model as a pkl file and tested 10,000 images using it. The accuracy was around 98.46%.
<h2><span style="text-decoration: underline;"><strong>Try it out!</strong></span></h2>
<p>I have created a simple application using Tkinter to demonstrate the capabilities of the model. The application has two buttons - 'Predict' and 'Clear'. Hold the mouse and drag it to write numbers. Click on predict to see the results which will be opened in another window. Click on clear to clear the area and draw another one.</p>
<img src="{{ site.baseurl }}/assets/images/app2_gif.gif" align="middle">
<p>Wanna try it out? Download the python script for the app <a href="https://github.com/mahi27/Digit-Recognizer" target="_blank"> here</a></p>
