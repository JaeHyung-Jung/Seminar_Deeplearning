# Inpcetion-Resnet V2
## Paper Link : https://arxiv.org/abs/1602.07261
### Inception Architecture : https://hoya012.github.io/blog/deeplearning-classification-guidebook-2/

## Inception 돌리는 코드(간소화된것) : https://medium.com/the-owl/building-inception-resnet-v2-in-keras-from-scratch-a3546c4d93f0

https://norman3.github.io/papers/docs/google_inception.html

#### Pytorch Classification (1)   
https://deep-learning-study.tistory.com/537   
https://deep-learning-study.tistory.com/525   
   
#### Pytorch Classification (2)   
https://github.com/zhulf0804/Inceptionv4_and_Inception-ResNetv2.PyTorch   

#### TF-slim classification
Inception-ResNet V2 References :    
https://github.com/tensorflow/models/tree/master/research/slim ==> tensroflow is shit. Don't use this (reason of version dependencies)   
model : https://github.com/tensorflow/models/blob/master/research/slim/nets/inception_resnet_v2.py(shit because of same reason)   


# Human Dataset :

#### MP2 HumanData
Data Feature : Only 1person with specific pose.   
Data Size : (Data 12.9GB / Annot 12.5MB / 25K images)   
Link : http://human-pose.mpi-inf.mpg.de/#download   

#### INRIA PersonData 
Data Feature : Casual People & People with bike   
Data Size : (Data 700MB / Annot X / 772 images), (Data 193.5MB / Annot X / 210images : Bike people)   
Link : http://pascal.inrialpes.fr/data/human/   

#### PennFudanPed
Data Feature : Casual Pedestrians(most of images is two or more people)   
Data Size : (Data 53.2MB / Annot 170.6KB / 170 images)   
Link : https://www.cis.upenn.edu/~jshi/ped_html/    

#### CrowdHuman
Data Feature : Many pedestrian(train, val, test)   
Data Size : (Data 8.6GB / Annot(format : odgt, 80.0MB / 15K images)  
Data Size(val) : (Data 2.6GB / Annot(format : odgt, 23.3MB / 4.37K images)  
Data Size(Test) : (Data 3.3GB / Annot X / 5K images)  
Link : http://www.crowdhuman.org/download.html    
