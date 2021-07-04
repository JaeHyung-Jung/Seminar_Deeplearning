# Object_Detection 용어정리

## IoU 
iou = intersection over Union
![image](https://user-images.githubusercontent.com/79160507/124384251-5081e180-dd0b-11eb-8697-8f6284cc2449.png)
두 Box의 교집합 영역 넓이 / 합집합 영역 넓이

일반적으로 IoU의 threshold를 0.5로 잡아 사용한다.

### NMS
NMS는 Non-Maximum-Supression으로
예측결과, 즉 박스가 겹쳐서 나왔을때 class가 같은 박스들중 가장 정확도가 높은 박스만을 남기는 방법이다.
이때에도 IoU를 기준으로 하나의 box만 남기게 된다.
 
## Anchor_Box
이미지에서 다양한 형태의 object를 detection하기위한 미리 정해진 크기와 비율을 가진 경계박스

## Loss
Loss란 손실율을 뜻하며, Deep_learning에서는 이 손실율이 정답과 예측값의 차이를 뜻한다.

이 Loss를 구해주는 loss function은 매우 많은 종류가있으며 Classification에 사용되는 Cross-entropy등이 대표적이며
Object_Detection에서는 ' '가 대표적이다.

## RPN
RPN은 Faster R-CNN에서 활용되었는데, Faster R-CNN의 목표는 selective search 없이 RPN을 학습하는 구조로 모델을 만드는 것이다. 
RPN은 feature map을 input으로, RP를 output으로 하는 네트워크라고 할 수 있고, selective search의 역할을 온전히 대체한다.

### RPN의 구조   
1. CNN을 통해 뽑아낸 feature map을 입력으로 받는다. 이 때, feature map의 크기를 H x W x C(세로 x 가로 x 채널수)로 잡는다.
2. feature map에 3x3 convolution을 256 channel (or 512 channel)만큼 수행한다. 이 때, padding을 1로 설정해주어 H x W가 보존되도록 진행하며, intermediate layer 수행 결과 H*W*256 (or 512) 크기의 두 번째 featur map을 얻는다.
3. 2번째 feature map을 입력으로하여 classification(cls layer)과 bounding box regression(reg layer) 예측 값을 계산한다.
+) 이 과정은 Fully Connected Layer가 아니라 1 x 1 컨볼루션을 이용하여 계산하는 Fully Convolution Network의 특징을 갖는다. 이는 입력 이미지의 크기에 상관없이 동작할 수 있도록 하기 위함이며 자세한 내용은 Fully Convolution Network을 참고하길 바란다.
4. Classification layer에서는 1 x 1 컨볼루션을 (2(Object인지 아닌지를 나타냄) x 9(앵커(Anchor) 개수)) 채널 수 만큼 수행하며, 그 결과로 H*W*18 크기의 feature map을 얻는다. H*W 상의 하나의 인덱스는 피쳐맵 상의 좌표를 의미하고, 그 아래 18개의 채널은 각각 해당 좌표를 Anchor로 삼아 k개의 앵커 박스들이 object인지 아닌지에 대한 예측 값을 담는다. 즉, 한번의 1x1 컨볼루션으로 H x W 개의 Anchor 좌표들에 대한 예측을 모두 수행할 수 있다. 이제 이 값들을 적절히 reshape 해준 다음 Softmax를 적용하여 해당 Anchor가 Object일 확률 값을 얻는다.
+) 여기서 앵커(Anchor)란, 각 슬라이딩 윈도우에서 bounding box의 후보로 사용되는 상자를 의미하며 이동불변성의 특징을 갖는다.
5. Bounding Box Regression 예측 값을 얻기 위한 1 x 1 컨볼루션을 (4 x 9) 채널 수 만큼 수행하며 regression이기 때문에 결과로 얻은 값을 그대로 사용한다.
6. Classification의 값과 Bounding Box Regression의 값들을 통해 RoI를 계산한다

#### Selective Search란
Selective Search는 RCNN에 쓰였으며 이미지에서 랜덤한 bounding box를 무수히 그려 이 box들을 merge해가며 찾는 방식입니다.
현재는 Region Proposal을 RPN이 대체하고있기 때문에 자세하기 학습하지않았고 어떤개념인가만 알아보았습니다.

## RoI Pooling // Roi란 Region Of Intereset로 RPN을 통해 나온 영역을 의미한다. 
하나의 이미지에 여러 물체가 있다면 CNN에서 출력된 feature map에 region proposal이 씌워진 영역은 사이즈가 각 물체마다 다르다. 
따라서 사이즈가 다른 각 영역을 정해진 규격의 grid에 맞춰 max pooling을 적용해 동일한 사이즈의 출력을 뱉어내는 과정이다.

## mAP

## ++
#### Region Proposal : object가 있을 만한 영역을 다수 추천

#### Bounding Box Regression : Object영역을 미세조정

#### Ground-truth : 녹색 bounding box로 실제 object영역이다. 참고로 빨간색은 예측된 영역이다.




# Faster_RCNN 구조

# RPN구조
![image](https://user-images.githubusercontent.com/79160507/124396527-1a615380-dd45-11eb-86b6-eb2338a7e74f.png)

1. CNN을 통해 뽑아낸 피쳐 맵을 입력으로 받습니다. 이 때, 피쳐맵의 크기를 H x W x C로 잡습니다. 각각 가로, 세로, 체널 수 입니다.

2. 피쳐맵에 3x3 컨볼루션을 256 혹은 512 체널만큼 수행합니다. 위 그림에서 intermediate layer에 해당합니다. 이 때, padding을 1로 설정해주어 H x W가 보존될 수 있도록 해줍니다. intermediate layer 수행 결과 H x W x 256 or H x W x 512 크기의 두 번째 피쳐 맵을 얻습니다.

3. 두 번째 피쳐맵을 입력 받아서 classification과 bounding box regression 예측 값을 계산해주어야 합니다. 이 때 주의해야할 점은 Fully Connected Layer가 아니라 1 x 1 컨볼루션을 이용하여 계산하는 Fully Convolution Network의 특징을 갖습니다. 이는 입력 이미지의 크기에 상관없이 동작할 수 있도록 하기 위함이며 자세한 내용은 Fully Convolution Network에 관한 포스팅을 참고해주십시오.

4. 먼저 Classification을 수행하기 위해서 1 x 1 컨볼루션을 (2(오브젝트 인지 아닌지 나타내는 지표 수) x 9(앵커 개수)) 체널 수 만큼 수행해주며, 그 결과로 H x W x 18 크기의 피쳐맵을 얻습니다. H x W 상의 하나의 인덱스는 피쳐맵 상의 좌표를 의미하고, 그 아래 18개의 체널은 각각 해당 좌표를 앵커로 삼아 k개의 앵커 박스들이 object인지 아닌지에 대한 예측 값을 담고 있습니다. 즉, 한번의 1x1 컨볼루션으로 H x W 개의 앵커 좌표들에 대한 예측을 모두 수행한 것입니다. 이제 이 값들을 적절히 reshape 해준 다음 Softmax를 적용하여 해당 앵커가 오브젝트일 확률 값을 얻습니다.

5. 두 번째로 Bounding Box Regression 예측 값을 얻기 위한 1 x 1 컨볼루션을 (4 x 9) 체널 수 만큼 수행합니다. 리그레션이기 때문에 결과로 얻은 값을 그대로 사용합니다.

6. 이제 앞서 얻은 값들로 RoI를 계산해야합니다. 먼저 Classification을 통해서 얻은 물체일 확률 값들을 정렬한 다음, 높은 순으로 K개의 앵커만 추려냅니다. 그 다음 K개의 앵커들에 각각 Bounding box regression을 적용해줍니다. 그 다음 Non-Maximum-Suppression을 적용하여 RoI을 구해줍니다.

이렇게 RPN을 이용해서 RoI를 추론해내는 구조를 알아보았습니다. 이렇게 찾은 RoI를 다시 첫 번째 피쳐맵에 project 한 다음 RoI Pooling을 적용하고, 이를 다시 클래시피케이션에 적용하면 물체의 종류도 알아낼 수 있겠죠? 이 부분은 Fast R-CNN 구조를 계승하므로 궁금하신 분들은 이전 포스팅[4]을 참고해주시기 바랍니다.

# Segmentation
## Instance, Semantic
![image](https://user-images.githubusercontent.com/79160507/124398904-310ea700-dd53-11eb-9363-64d4658108b9.png)   
Instance Segmentation은 모든 객체를 따로 분류하여 Segmentaion해준다.

![image](https://user-images.githubusercontent.com/79160507/124398908-32d86a80-dd53-11eb-9100-a64babdb35df.png)   
semantic Segmentation은 같은 class끼리의 객체를 묶어서 Segmentation해준다.


## Deeplap V3의 Atrous Convolution의 이점
이러한 Atrous Convolution을 활용함으로써 얻을 수 있는 이점은 기존 convolution과 동일한 양의 파라미터와 계산량을 유지하면서도, field of view(한 픽셀이 볼 수 있는 영역)를 크게 가져갈 수 있게 된다는 것이다.
