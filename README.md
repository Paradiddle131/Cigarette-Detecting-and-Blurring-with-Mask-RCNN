# Cigarette Detecting and Blurring Using Mask RCNN

This is an image segmentation project which detects and extracts the masks of cigarette instances in images using [Mask R-CNN](https://github.com/matterport/Mask_RCNN). The Mask R-CNN model generates bounding boxes and segmentation masks for each instance of an object in the image as the [paper](https://arxiv.org/abs/1703.06870) suggests. 

- [Data](#data)
  - [To access the unlabeled images](#to-access-the-unlabeled-images)
  - [To access the processed and labeled images](#to-access-the-processed-and-labeled-images)
  - [Data Preprocessing](#data-preprocessing)
- [Results](#results)

## Data
  
There are 731 unlabeled images of cigarettes scraped only from google images and 193 of them are labeled pixel-by-pixel. Further scraping will be done from stock websites.

Since the dataset is stored in my personal Google Drive account and the size of the dataset is larger than 100MB, I had to use a script  in [this reposityory](https://github.com/circulosmeos/gdown.pl) of the user [@circulosmeos](https://github.com/circulosmeos) which directly downloads big files from Google Drive sharing links.
  
### To access the unlabeled images:

<img src="https://user-images.githubusercontent.com/36932448/80632017-4b6a3800-8a5f-11ea-8cf4-56f4f553e89c.png"
     alt="image" 
     width=840; height=600/>

Download the `gdown.pl` script
```python 
wget -O gdown.pl "https://drive.google.com/uc?export=download&id=1gc-D4ydSBY7jqhlM-Oq2xca5oJx9217B"
```

Permit the user to run the script
```python 
chmod +x ./gdown.pl 
```
  
Download the data using the script
```python
./gdown.pl 'https://drive.google.com/file/d/1-6QvZMUB13r-bN1eoiF3qlEplS_4imiK/view?usp=sharing' 'data-cigar-731.zip'
```
  
Unzip it
```python
unzip ./data-cigar-731.zip -d /path/to/extract
```
  
### To access the processed and labeled images:

<img src="https://user-images.githubusercontent.com/36932448/80632126-70f74180-8a5f-11ea-8346-36b9aaae7c9a.png"
     alt="image" 
     width=840; height=600/>
   
```python
!./gdown.pl 'https://drive.google.com/file/d/1nHKQMUbhNBAyn307K5jEJmX2PBK7rlfz/view?usp=sharing' 'cigarette.zip'
```

## Data Preprocessing

Because the dimensions of the images must be 1024x1024 before using Mask-RCNN model;

- images smaller than the target size got expanded using `np.pad()` function of Numpy module
![image](https://user-images.githubusercontent.com/36932448/80629158-1c51c780-8a5b-11ea-8c7f-151f7b3f3d6d.png)

-  images larger than the tarhet size got resized using `resize()` function of OpenCV module
![image](https://user-images.githubusercontent.com/36932448/80629546-a8fc8580-8a5b-11ea-9ccc-c052ce1b1f6e.png)

## Training

You need to clone the [Mask-RCNN GitHub Repository](https://github.com/matterport/Mask_RCNN) and configure the config files/codes according to your workspace and data. Instructions are given in the repository.

## Results

Despite having a very shallow dataset, using transfer learning leads the model having some baseline results.

<img src="https://user-images.githubusercontent.com/36932448/80630481-f75e5400-8a5c-11ea-94de-46e12d848e2a.png"
     alt="image" 
     width=1080; height=540/>
<img src="https://user-images.githubusercontent.com/36932448/80630504-fcbb9e80-8a5c-11ea-90d2-56d6972df0a2.png"
     alt="image" 
     width=1080; height=540/>
     
Since the model has been trained with only ~200 images, it easily gives false results in some cases.
    
<img src="https://user-images.githubusercontent.com/36932448/80631012-ca5e7100-8a5d-11ea-9e75-c232a26a57d7.png"
     alt="image" 
     width=1080; height=540/>
