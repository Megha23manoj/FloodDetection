### Introduction
Our modern world faces a number of problems due to the drastic changes in the climatic conditions. Natural calamities like flood, earthquake and landslides are some among them. This work concentrates on flood as a natural calamity and suggests a system which detects the flood affected area and estimates the flood extent there from images.

### Solution Approach
The proposed method analyses the image in detail as it examines the major components in the scene like humans, vehicles, color and brown area. The figure below illustrates the components involved, starting from the module of preprocessing, after which largest brown area segmentation takes place. This is followed by the estimation of water depth with respect to human beings and then water depth estimation with respect to vehicles. This along with the average brown colour intensity and largest brown area is compared against the rule set generated. Finally, the extent of flood is  estimated by fuzzy based decision making.
![image](https://github.com/user-attachments/assets/1bc01973-ca1f-48af-9c6b-a62a0f3c5098)

#### Preprocessing:
The image goes through gamma correction and HSV Conversion. 

![image](https://github.com/user-attachments/assets/67ed7a60-c24c-431c-ba0c-d148831c1a45)
#### Largest Brown Area Segmentation:
The brown color area in the image which is assumed to be the region of water, has to be segmented out. This region has to be further taken for estimation of brown color intensity. 

![image](https://github.com/user-attachments/assets/f8988c42-2bc7-430b-99fc-80c27673d0d4)

![image](https://github.com/user-attachments/assets/b9277127-0260-4da9-b9db-99a989e3f145)

If the largest contour area is less than a specified threshold value, then the system directly prints no flood and exits. This is because water area is taken as the most significant parameter in estimating flood. If it is greater than the threshold value, then the average or mean of the segmented image pixels is taken as average brown colour intensity which is also fed to the fuzzy module for estimation of flood

![image](https://github.com/user-attachments/assets/c3b5b71e-7d9d-470d-8637-021c2d58bbe5)
#### Water Depth Estimation with respect to human
The faces present in the scene are detected by face detection by haar classifiers. Here, we use a pre trained classifier of detecting faces for ease. If face is detected we draw proportionate bounding boxes beneath the face assuming it to be the body. The human body is thus divided into three regions namely torso region, waist region and knee region which is high, medium and low levels respectively.

![image](https://github.com/user-attachments/assets/e7d51cf0-9ba2-494e-bee4-5c11790e7607)

The tallest human segmented out is divided into the below mentioned three levels. The brown color segmented image i.e water segmented image is trimmed out to these three regions. Each region is thresholded so that we can find the contours and sum of contours in each region.

![image](https://github.com/user-attachments/assets/bf248df7-b12d-40d3-ac8a-3b6c137c296b)
The region where the water area is the largest, is taken to be the level of water with respect to the human being taken. The water area corresponding to this region is taken as the water depth compared against human beings and is fed to the final fuzzy module. The system finds the maximum among the three areas.
#### Water Depth estimation with respect to vehicles
For semantic segmentation a new form of convolutional neural network that combines the strengths of Convolutional Neural Networks (CNNs) and Conditional Random Fields (CRFs)-based probabilistic graphical modelling
is used. A mean-field approximate inference for the dense CRF with Gaussian pairwise potentials as a Recurrent Neural Network (RNN) which can refine coarse outputs from a traditional CNN in the forward pass, while passing error differentials back to the CNN during training is formulated.

![image](https://github.com/user-attachments/assets/fffec990-0927-4059-9b9e-243b539a82da)
If it is less than the specified threshold value, there is no enough vehicle area in the image to carry out our estimation i.e; no vehicle detected and depth with respect to vehicle is set to zero. If it has larger area than the threshold, then we move on to water depth estimation with respect to vehicles. If the image has multiple vehicles, it will take the one with larger area since largest contour is considered here.

![image](https://github.com/user-attachments/assets/cc539b73-504a-48af-b02e-936ca4465a4b)
After the vehicle is segmented out from the image successfully, a bounding box is drawn along the contour of the vehicle detected and is divided into three equal parts.

![image](https://github.com/user-attachments/assets/18204bff-d3ff-4fca-b637-a8cb4834c959)

#### Fuzzy Module for estimating flood extent
Fuzzy based systems are used to deal with parameters which can take a range of values instead of binary values(0 and 1). A fuzzy control system links fuzzy variables using a set of rules. These rules are simply mappings that describe how one or more fuzzy variables relates to another. Decision making and output computation in such cases are dealt with much ease and efficiency with fuzzy logic. Fuzzy logic seems closer to the way our brains work

![image](https://github.com/user-attachments/assets/fbece65e-f16b-432a-b64b-1130529ba4ad)

After defining the rules, all of them (for low flood, medium flood and high flood) are aggregated together. It aggregates the fuzzy membership functions of all the three levels of flooding to be defuzzified. Defuzzification is the process of converting the degrees of membership of output linguistic variables into numerical value

![image](https://github.com/user-attachments/assets/fd3dd5d9-dcbf-4445-a2de-ae3987bab262)

### Results
The proposed method is tested on a variety of images ranging from flood scenes and non flood scenes. The results in all the cases have been analyzed. The images tested are classified into flood and non flood categories by the flood detection system. Flood scene images can be correctly classified into flood category and can be incorrectly classified into non flood category. Same can happen with non flood scene images where they can be correctly and incorrectly classified into non flood and flood categories respectively. The figure below represents some correctly and incorrectly classified images. Green bordered images show the correctly classified images and red bordered images show the incorrectly classified images by the system.

![image](https://github.com/user-attachments/assets/a85eb13f-340f-4631-909f-c5449ee2b0e4)

After compiling the results together and analyzing them, the performance of the system has to be evaluated in detail. This is to ensure the efficiency and compute the accuracy of the system. Accuracy rate is the fraction of correctly classified images to the total number of images which is computed as 83.125 in this work. On the other hand, error rate is the fraction of incorrectly classified images to the total number of images. The error rate for our work is estimated to a minimal value of 16.875 which adds to the value of the work.

### Conclusion
The extent of flood is estimated from crowd sourced random images with simple color based segmentation, depth analysis and fuzzy based decision making. This result obtained from images can prove useful for sending help to flood affected areas. The extent or degree of flood within the range of 0 to 100 is estimated from the image. We plan to extend our work considering more factors like two wheelers and better human body part segmentation for comparison relative to the water level to calculate the flood extent so that the accuracy is improved. The work can be of immense help in providing technical assistance for flood victim rescue programmes and working teams.
