# hairColoring
 
This repo is inspired by and uses some of the work done by thangrtan480 https://github.com/thangtran480/hair-segmentation. The main packages used are TensorFlow, Keras and OpenCV.

**Deep Learning model:**  
The architecture can be found at nets/Hairnet.py. It's a deep network that consists mainly of 2D convolution, depthwise 2D convolution, batch normalization and activation layers.   

**Dataset:**  
The model uses the CelebAMask-HQ free dataset which can be downloaded at: https://drive.google.com/file/d/1badu11NqxGf6qM3PTTooQDJvQbejgbTv/view. The dataset contains a handful of classes belonging to landmarks of the human face. Thanks to thangrtan480 and his data preprocessing script, I was able to separate only the images and masks belonging to the hair class to use for training. Then I split them into 23,440 training images and 5860 validation images.  
  
**Data Augmentation:**  
In order to help the model generalize well to different image settings, I used different augmentation techniques like changing the brightness, flipping, rotating and more. This helped the model avoid overfitting.  
  
**Masking and coloring the hair:**  
After getting the prediction output of the model, it can be used as a mask for the hair. By creating three copies of this mask, each one can be used as a channel of color on the bgr colored image. Each channel intensity is determined by the corresponding color intensity given as an input by the user. After that, cv2.addWeighted() function is used to superimpose both the image and the rgb mask with a specific weight for each.  

**Performance:**  
Since I used a larger dataset and more augmentation steps, the model I trained performed better after one epoch
![image](https://user-images.githubusercontent.com/43937873/137564927-d21c0a73-6aae-46f0-857b-0bf37e026327.png)  
compared to thangrtan480's model.  
![image](https://user-images.githubusercontent.com/43937873/137565021-83567445-e87e-4791-8a41-b71d2a05eaf9.png)



**Results:**  
<p align="center">
  <img src=/test/results/1.jpg alt="drawing" width="220" height="230"/>
  <img src=/test/results/2.jpg alt="drawing" width="220" height="230"/>
  <img src=/test/results/3.jpg alt="drawing" width="220" height="230"/>
</p>
  
Use this Colab notebook to try it out:
https://colab.research.google.com/drive/1yF195suicuwQ1Iy6_ri0qKz3WnMDLy18?usp=sharing
