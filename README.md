#
## Machine Learning with Python Project

# How green is my city ?

## Identifying Plant surface on a city with satellite images.

![greenproject](https://user-images.githubusercontent.com/72912247/121811213-02297780-cc64-11eb-9476-6ceffd05d3a8.jpeg)
Photo by Paulo Simões Mendes on Unsplash

**Description**
This project is about identifying green areas in a given city , the user inputs a city name and it searches for it's GPS coordinates and gives back an appropriate corresponding usable satellite image without clouds from predefined and stored dataset of satellite images, it Selects only the area corresponding to the city limits thanks to cartography data (image superposition), computes and returns the green areas in the city and the ratio of nature from the total area thanks to a machine learning algorithm.


**Why this project ?**

Rapid and uncontrolled Urbanization along with economic and industrial development, have increased the rate of land-cover change ,while green areas offer innovative approaches to increase the quality of urban settings, enhance local resilience and promote sustainable lifestyles, and currently the importance of urban greenspaces in an urban ecosystem is being increasingly recognized . There is a need to examine the accuracy of different algorithms for land-cover mapping in order to identify the best classifier for further applications of these areas' observation and preservation.


**Project definition - Flow chart**
![flow](https://user-images.githubusercontent.com/72912247/121818590-65c59c00-cc88-11eb-8c6d-80f02a92b048.JPG)

**Datasets**

There are plenty of datasets :

Free Unlabeled datasets with satellite images used :

- Copernicus satellite images (Sentinel1 and 2) : 1 image every 5 or 6 days for 1 given earth location
- Landsat (US) :moderate spatial-resolution (30-meter) imagery that provides large areas of repeated data coverage at a scale that enables users to see detailed human-scale processes, such as urbanization, but not individual houses.

Cartography/map datasets:

- Open Street Maps
- IGN
- Corine land cover


**Project Steps:**

![steps](https://user-images.githubusercontent.com/72912247/121821154-79c4ca00-cc97-11eb-87d9-c45aab7ced9a.JPG)



## Step 1

![step1](https://user-images.githubusercontent.com/72912247/121911112-bd6b1280-cd2f-11eb-97d7-c30af0f82da2.JPG)

In this step, we pre-download satellite Sentinel2 images from [Copernicus Open Access Hub](https://scihub.copernicus.eu/dhus/#/home), we crop an area of interest and we use the reconstructed multispectral images for NN training and inference.


1.Create shapefile over area of interest, given GPS coodinates.

2.Visualise area of interest with geopandas and folium.

3.Download satellite file corresponding to footprint with Sentinel API.

4.Upsample 20m bands, mask satellite image and create multiband image for training or inference.


Links to notebooks :

[Create_shapefile_and_tiff_from_geo_coord.ipynb](https://github.com/how-green-is-my-city/how-green-is/blob/master/notebooks/Create_shapefile_and_tiff_from_geo_coord.ipynb)

[HG_NeuralNetwork_training_step1.ipynb](https://github.com/how-green-is-my-city/how-green-is/blob/master/notebooks/HG_NeuralNetwork_training_step1.ipynb)

[HG_inference_step1.ipynb](https://github.com/how-green-is-my-city/how-green-is/blob/master/notebooks/HG_inference_step1.ipynb)

[HG_inference_step1_bis.ipynb](https://github.com/how-green-is-my-city/how-green-is/blob/master/notebooks/HG_inference_step1_bis.ipynb)




## Step 2

**1.Using OSM to Create sat images and OSD shapes**

1.Receive any coordinate set or place name and get a coordinate set for data download. 

2.Change the area of interest interactively with folium 

3.Retrieve a geopadas dataframe with a set of polygons or multipolygons of green areas identified in the Open Street Map public database. 

4.Retrieve images of Sentinel2/Landsat8 satellites from Google Earth Engine  

5.Create a mask of 0 and 1 for green areas of the coordinate area identified above and of the dataframe created on 2 or any other geopandas dataframe with a list of polygons identifing green areas and save as a one band TIF file on google drive.

link to notebook : [Create_sat_images_and_green_areas_labels_(with_predict).ipynb](https://github.com/how-green-is-my-city/how-green-is/blob/master/notebooks/Create_sat_images_and_green_areas_labels_(with_predict).ipynb)

![io](https://user-images.githubusercontent.com/72912247/121821733-2a809880-cc9b-11eb-8fe2-20c48ef24d6a.JPG)



**2.Testing different ML and DL algorithms:**

**Pixel-Wise Classification Using Deep Neural Networks:**
A basic architecture of the NN 
![bands](https://user-images.githubusercontent.com/72912247/121820860-4a14c280-cc95-11eb-8648-6ab28852ba7d.jpeg)

Pixel-wise classification is a fundamental task in remote sensing that aims at assigning a semantic
class, e.g., vegetation, accurately to every individual pixel of an image.

Links to notebooks : 

[HG_NeuralNetwork_training_step2.ipynb](https://github.com/how-green-is-my-city/how-green-is/blob/master/notebooks/HG_NeuralNetwork_training_step2.ipynb)

[HG_inference_step2.ipynb](https://github.com/how-green-is-my-city/how-green-is/blob/master/notebooks/HG_inference_step2.ipynb)


**implementing UNet:**
a convolutional network model classically used for biomedical image segmentation with the Functional API
![unet](https://user-images.githubusercontent.com/72912247/121819354-da9ad500-cc8c-11eb-9bb8-3737330143e9.png)

The network consists of a contracting path and an expansive path, which gives it the u-shaped architecture. The contracting path is a typical convolutional network that consists of repeated application of convolutions, each followed by a rectified linear unit (ReLU) and a max pooling operation. During the contraction, the spatial information is reduced while feature information is increased. The expansive pathway combines the feature and spatial information through a sequence of up-convolutions and concatenations with high-resolution features from the contracting path 

Link to notebook :
[DeepLearning_Segmentation_(Model_training_notebook).ipynb](https://github.com/how-green-is-my-city/how-green-is/blob/master/notebooks/DeepLearning_Segmentation_(Model_training_notebook).ipynb)


**Pixel-Wise Classification using K-Nearest Neighbor Classifier (K-NNC) AND Support Vector Machine (SVM)**

k-Nearest neighbor classifier is one of the widely used classifiers in machine learning. The main objective of this method is that the data instances of the same class should be closer in the feature space.

The support vector machine (SVM) is a supervised learning method that generates input-output mapping functions from a set of labeled training data. The mapping function can be either a classification function, i.e., the category of the input data, or a regression function.

Link to notebook : [Pixel_Classification_in_Satellite_Imagery_KNN_SVM.ipynb](https://github.com/how-green-is-my-city/how-green-is/blob/master/notebooks/Pixel_Classification_in_Satellite_Imagery_KNN%2C_SVM%20(1).ipynb)


## Step 3 (Combination of algorithms and techniques)

**Demo-Link:**
***Demo of the UNet model***
Link to notebook :
[How_Green_Is_Demo.ipynb](https://github.com/how-green-is-my-city/how-green-is/blob/master/notebooks/How_Green_Is_Demo.ipynb)


## References

[Satellite imagery access and analysis in Python & Jupyter notebooks](https://towardsdatascience.com/satellite-imagery-access-and-analysis-in-python-jupyter-notebooks-387971ece84b)

[Neural Network for Satellite Data Classification Using Tensorflow in Python](https://towardsdatascience.com/neural-network-for-satellite-data-classification-using-tensorflow-in-python-a13bcf38f3e1)

https://towardsdatascience.com/land-cover-classification-in-satellite-imagery-using-python-ae39dbf2929

