> ## Faster R-CNN

- R-CNN, Fast R-CNN, Faster R-CNN 발전 과정 간략 비교

---

- single: classification, classification + localization (single object detection)
- multiple: (universal) object detection, instance segmentation
- 연산량도 저 순서대로 많아지지 않을까.

|     n-staged     | description                                                                                           |
| :--------------: | ----------------------------------------------------------------------------------------------------- |
| 2-stage detector | - localization: 물체가 있을 법한 곳을 n개 찾기 + 때때로 crop<br />- classification: use deep learning |
| 1-stage detector | end-to-end. 초기 YOLO                                                                                 |

<br />

|    model     |       | description                                                                                                                                                      |
| :----------: | :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|    R-CNN     | 장점  | Selective search + Crop & Resize + CNN                                                                                                                           |
| (CVPR 2014)  | 단점  | end-to-end 형식이 아니다보니 global optimal을 찾기 어렵다.                                                                                                       |
|              |       | warping된 이미지를 일일이 CNN에 forward                                                                                                                          |
|  Fast R-CNN  | 장점  | Selective search + (ROI pooling + CNN)                                                                                                                           |
| (ICCV 2015)  | 단점  | end-to-end 형식에 가까워졌지만, SS가 CPU 단에서 실행되므로 여전히 느리다.                                                                                        |
|              || 
| Faster R-CNN | 장점  | (Convolutional + RPN + Fully-Connected)                                                                                                                          |
| (NIPS 2015)  | 단점  | classification 단계에서 각 label 확률을 계산하기 위한 값들이 나오는데,<br />이 벡터는 다른 region을 의미하므로, 한 번에 하지 않고 각각을 연산한다는 의미로 보임. |

<br />

### Region Proposal

- '여기엔 뭐가 있는 것 같은데?'를 n개 찾기
- Sliding window: 마치 다양한 크기의 anchor box filter 연산
- Selective Search
  - Hierachical Grouping: 인접한 영역끼리 천천히 합치기
