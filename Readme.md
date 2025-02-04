# Feature Identification in RSD using Deep Learning and Neural Network

<p text-align="left">
    <a href="https://github.com/akhil-s-kumar/NRSC-Project-Feature-Identification-in-Remote-Sensing-Data-Using-Neural-Network-Model/issues" alt="Issues">
        <img src="https://img.shields.io/github/issues/akhil-s-kumar/NRSC-Project-Feature-Identification-in-Remote-Sensing-Data-Using-Neural-Network-Model" /></a>
    <a href="https://github.com/akhil-s-kumar/NRSC-Project-Feature-Identification-in-Remote-Sensing-Data-Using-Neural-Network-Model/pulls" alt="Pull Requests">
        <img src="https://img.shields.io/github/issues-pr/akhil-s-kumar/NRSC-Project-Feature-Identification-in-Remote-Sensing-Data-Using-Neural-Network-Model" /></a>
    <a href="https://github.com/akhil-s-kumar/NRSC-Project-Feature-Identification-in-Remote-Sensing-Data-Using-Neural-Network-Model/network/members" alt="Forks">
        <img src="https://img.shields.io/github/forks/akhil-s-kumar/NRSC-Project-Feature-Identification-in-Remote-Sensing-Data-Using-Neural-Network-Model" /></a>
    <a href="https://github.com/akhil-s-kumar/NRSC-Project-Feature-Identification-in-Remote-Sensing-Data-Using-Neural-Network-Model/stargazers" alt="Stars">
        <img src="https://img.shields.io/github/stars/akhil-s-kumar/NRSC-Project-Feature-Identification-in-Remote-Sensing-Data-Using-Neural-Network-Model" /></a>
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/akhil-s-kumar/NRSC-Project-Feature-Identification-in-Remote-Sensing-Data-Using-Neural-Network-Model/main/assets/ISRO_Logo.png" alt="ISRO Logo">
</p>

This project is done as part of my Internship at NRSC (ISRO). In this Readme file I will walk you through the complete details of my project in an easiest way as possible.

## :question: What is ML Vs DL

Basically, **Artificial Intelligence** is a broad category of Computer Science that uses machine intelligence to predict the expected output as human does. Now, coming to **Machine Learning**, It is a subset of Artificial Intelligence that uses data and algorithm to perdict an output, and last **Deep Learning**, is a subset of Machine Learning which is more complicated than of Machine Learning to extract certain features using certain layers called **Neural Network** to predict an expected output.

## :question: What is Semantic Segmentation?

Let's understand this concept with the help of an example. Since, here we are using Remote Sensing Data we can take help with that example.

![Orginal-Image](https://github.com/akhil-s-kumar/NRSC-Project-Feature-Identification-in-Remote-Sensing-Data-Using-Neural-Network-Model/blob/main/data-set/Tile%201/images/landsat_img_01.jpg?raw=true)

What all things we can see in the above Image?

1. **Roads**
2. **Buildings**
3. **Land**
4. **Trees**
5. **Vehicles**

If we closely look into the image we can extract a lot more features from the image.

Now, you are just thinking where does this **Semantic Segmentation** comes in the picture right?

In traditional Machine Learning models, If we wanted to predict a single object from an image it's possible by training the model using multiple images of the object that we wanted to predict. Now, what if in the case if we wanted to predict multiple objects in a single image itself here comes Semantic Segmentation in the picture.

Here, we will use masks to identify different object in an image and compare it with original image to extract different features of different objects and train the model accoding to that.

![Ground-Truth-Mask](https://github.com/akhil-s-kumar/NRSC-Project-Feature-Identification-in-Remote-Sensing-Data-Using-Neural-Network-Model/blob/main/data-set/Tile%201/masks/landsat_img_01.png?raw=true)

I hope, the above image gave some idea :bulb: we use differen colors to represent different objects.

## :books: Dataset

Here, I used **Landsat 8** Images `20 meter` above the ground level for all my images. You can freely download these images from this repositry and it's free to use. I used my own location `Thiruvananthapuram` to extract features because it will be easy to verify with **Ground Truth Data** for me. You are free to experiment with your own data but, it takes more time to create mask for each images.

### HEX Colors I used to represent differnt objects in the image

1. **Road** - `#0DC2E6`
2. **Buildings** - `#044079C`
3. **Others** - `#9A24FB`

### Dataset file structure

```
📂data-set
 ┣ 📂Tile 1
 ┃ ┣ 📂images
 ┃ ┃  ┣ 📜landsat_img_01.jpg
 ┃ ┃  ┣ 📜landsat_img_02.jpg
 ┃ ┃  ┣ 📜landsat_img_03.jpg
 ┃ ┃  ┣ 📜landsat_img_04.jpg
 ┃ ┃  ┗ 📜landsat_img_05.jpg
 ┃ ┗ 📂masks
 ┃ ┃  ┣ 📜landsat_img_01.png
 ┃ ┃  ┣ 📜landsat_img_02.png
 ┃ ┃  ┣ 📜landsat_img_03.png
 ┃ ┃  ┣ 📜landsat_img_04.png
 ┃ ┃  ┗ 📜landsat_img_05.png
 ┣ 📂Tile 2
 ┃ ┣ 📂images
 ┃ ┃  ┣ 📜landsat_img_01.jpg
 ┃ ┃  ┣ 📜landsat_img_02.jpg
 ┃ ┃  ┣ 📜landsat_img_03.jpg
 ┃ ┃  ┣ 📜landsat_img_04.jpg
 ┃ ┃  ┗ 📜landsat_img_05.jpg
 ┃ ┗ 📂masks
 ┃ ┃  ┣ 📜landsat_img_01.png
 ┃ ┃  ┣ 📜landsat_img_02.png
 ┃ ┃  ┣ 📜landsat_img_03.png
 ┃ ┃  ┣ 📜landsat_img_04.png
 ┃ ┃  ┗ 📜landsat_img_05.png
 ┗ 📜classes.json
```

I have taken totally 10 images seperated in two folders as `Tile 1` & `Tile 2` for the experiment of this project, you can use as many as you want because more the no of data more precised will be the prediction.

## :rocket: Working with trainingModel.py

This file includes every code on how this model works from scratch.

### Necessary Packages

First I imported all necessary packages required for the Model. `cv2`, `os`, `numpy`, `matplotlib`, `Image`, `tensorflow`, `sklearn`, `patchify`, `segmentation_model`, `random`.

Don't worry I will explain why and where to use these modules.

### CodeBase Walkthrough

First things is loading the `data-set` from the root directory, for that puspose only we are using `os` module.

The next thing is reading each images and their respective masks. Python loads each file in a random way so, in order to make it in a ordered and structured manner we loop through each file in an pre-defined ordered manner. 

In orderd to get maximum features out of an image, we will make use of `patchify` library to split each images and their respective masks in a 256 x 256 (square) images and save it as a numpy array `image_dataset` and `mask_dataset` respectively.

Now, I used `random` function to plot a random image and its respective mask from `image_dataset` and `mask_dataset` to verify orginal image and it's ground truth mask image are same.

It's somewhat look like this!

![Screenshot-1](https://github.com/akhil-s-kumar/NRSC-Project-Feature-Identification-in-Remote-Sensing-Data-Using-Neural-Network-Model/blob/main/assets/Screenshot_1.jpg?raw=true)

Next, is to covert Hexadecimal colors to RGB channels.

1. **Road** - `#0DC2E6` - `13, 194, 230`
1. **Buildings** - `#044079C` - `68, 7, 156`
1. **Others** - `#9A24FB` - `154, 36, 251`

Now, we will convert every pixels into `0, 1 & 2` because we are having only 3 labels that is Roads, Buildings & Others. If more labels are there the number will increase. Then we will use `random` function to plot a random image.

![Screenshot-2](https://github.com/akhil-s-kumar/NRSC-Project-Feature-Identification-in-Remote-Sensing-Data-Using-Neural-Network-Model/blob/main/assets/Screenshot_2.jpg?raw=true)

The next step is to split the `data-set` into `X_train` `X_test` `y_train` `y_test` to train the model. Here we used `train_test_split` function from `sklearn` library to do so.

The last step is to train the model and validate using `X_test` & `y_test` here I done with only `10 Epochs` so, the predictions may not be that much accurate. If you can do with `100 Epochs` then the predictions will be more accurate.

Once, the training is done the next step is to save the model into `hdf5` format so, that you can use this model wherever you want.

I also included my trained model within this repository with the file name `nrsc_project-model.hdf5`.

Now, we will use a random image to test with the ground truth image to verify the predictions are same.

![Screenshot-3](https://github.com/akhil-s-kumar/NRSC-Project-Feature-Identification-in-Remote-Sensing-Data-Using-Neural-Network-Model/blob/main/assets/Screenshot_3.jpg?raw=true)

So, from the above image it's clear that prediction is almost accurate. Like I said earlier, if you can do it with `100 Epochs` then the predictions will be more precised.

Now, we can use `load_model` from `keras` to load `hdf5` file to predict with new images and no more needed to train the model again and again every time you wanted to test.

## :rocket: Working of Model.py

Once your trained model is ready that is `nrsc_project-model.hdf5` in our case, we any more not required `trainingModel.py`. Now every prediction happens on this file `Model.py` that is if you wanted to predict buildings, roads, water bodies or anything that you trained, you just need to have only this file.

### Necessary Packages

Here, I imported all necessary packages required for the prediction. `cv2`, `numpy`, `matplotlib`, `Image`, `sklearn`, `patchify`, `segmentation_model`.

### CodeBase Walkthrough

The first thing is loading the image that we wanted to predict. Here I loaded both original image and it's mask to verify with the predicted image if it is done correctly or not.

Then like we did during the training I splited the original images into 250 X 250 using `patcchify` library.

After that we looped through each splited image and predicted using `load_model` from `keras` and saved in a numpy array.

Since, we splited the original image into small pieces, now, we need to merge back as the original image for the predicted mask. For that we use `unpatchify` from `patchify` library.

If we plot the the predicted image it will somewhat look like this.

![Screenshot-4](https://github.com/akhil-s-kumar/NRSC-Project-Feature-Identification-in-Remote-Sensing-Data-Using-Neural-Network-Model/blob/main/assets/Screenshot_4.jpg?raw=true)

Now, the last part is to convert the labelled mask image back to RGB.

Once it is done we can plot and verify with original image and ground truth mask of original image.

![Screenshot-5](https://github.com/akhil-s-kumar/NRSC-Project-Feature-Identification-in-Remote-Sensing-Data-Using-Neural-Network-Model/blob/main/assets/Screenshot_5.jpg?raw=true)

If you can do it with `100 Epochs` then the predicted image will be exact like ground thruth image.

## :minidisc: Installation Instructions

You can either do it locally by installing necessary packages or use `Google Collab` because most of the packages used in this project is pre-installed.

Just add these two lines and run it before importing the modules.

```
!pip install patchify
!pip install segmentation-models
```

Also, upload `data-set` folder and `simple_multi_unet_model.py` in the root directory.

You can also try it with your own `data-set` images.

## :globe_with_meridians: References

1. https://medium.com/analytics-vidhya/introduction-to-semantic-image-segmentation-856cda5e5de8
2. https://www.youtube.com/c/DigitalSreeni
3. https://earthexplorer.usgs.gov/
4. https://towardsdatascience.com/u-net-for-semantic-segmentation-on-unbalanced-aerial-imagery-3474fa1d3e56