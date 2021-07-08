매주 수요일(+금요일) 16:00 장승수, 이장희, 정재형 +신성균박사님(심사) 네명이서 딥러닝 세미나발표   
발표시간은 인당 10 ~ 15분이며 모든 발표가 끝나면 질문이나 논문리뷰를 10~15분하여 총 세미나시간은 1시간이 됨   

#
# 주간 계획

## 1주차(`21.7.5) : FasterRCNN + 1Stage_Detector Milestones(RCNN-SPPNet-FastRCNN-FasterRCNN)
- 무엇을했는지(말벌집 돌리는 과정, 오류해결 어떻게했는지를 중점적으로) 3page
- FasterRCNN 모델 구조 및 이론(RCNN -> Fast_RCNN -> Faster_RCNN순으로 설명하면될듯) 1~2page
- Data Foramt 정리 : .XML, .CSV, .JSON(1page정도로 요약)
- 민재형, 승수형 NAS 발표자료 참고

## 1주차 FeedBack(1) 발표(`21.7.7) : FasterRCNN
- FasterRCNN, RPN에서 loss계산과정, Anchor_Box 생성 및 IoU를 통한 NMS과정 좀더 상세히 정리
- Backbone change : Resnet101 -> Resnet50 // 실패

## 1주차 FeedBack(2) 발표(`21.7.9) : FasterRCNN
- Backbone change : Resnet101 -> Resnet50 
  좀더 가벼운 Resnet50을 통해 학습시간을 단축시켜 HyperParameter 변화에 따른 학습과정 개선과정 확인
- Training_Loss의 수렴과정 보이기, +mAP개선
- Loss(Cross_entropy, Smooth_L1)의 실제 코드를 통한 계산과정 분석

## 2주차(`21.7.14) : 1Stage-Detector 
- 1Stage-Detector (Yolo_V(n), SSD, EfficientDet) 모델 구조 및 이론정리

## 2주차-2(`21.7.16) : 1Stage-Detector
- 1Stage-Detector : EfficientDet으로 CustomData 실습
- 위 과정에서 Backbone 교체하면서 실습, 결과내오기

## 3주차(`19.7.22) : Segmentation_DeepLab-V3
- 미정

## 4주차(`19.7.29) : Data Augmentation + Loss Function 정리
- 미정
