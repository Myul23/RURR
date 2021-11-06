> ## 배치 정규화

- Batch Normalization
- 입력을 정규화해도 node들의 분포는 정규화되지 않아서 모델의 학습을 어렵게 함.

-> 각 layer에서 정규화를 실시하자.

- 학습을 빠르게 (training speed up)
  - large learning rate도 사용 가능하게 / 전보다 편하게 optima를 찾도록
  - 사방으로 넓은 variance를 쓸 수 있으므로 더 정교하게 parameter update할 수 있음.
- 초기 가중치의 영향 줄이기, weight initialization 민감도 줄이기
- 모델의 일반화(regularization)

<br /><br /><br />

---

| 정규화 | normalization<br />or standardizatoin | 평균을, 0으로 분산을 1로                                                                                                                    |
| :----: | ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| 백색화 | whitening                             | PCA를 통해 얻은 주성분을 회전시키고 분산을 줄이면서 특성 축의 영향력을 제거하는 것.<br />- 따라서 평균을 0으로, 공분산을 단위행렬로 만든다. |

<br />

<img src="https://latex.codecogs.com/svg.latex?\mu_{Batch}=\frac{1}{m}\sum_{i=1}^{m}x_i" alt="\mu_{Batch}=\frac{1}{m}\sum_{i=1}^{m}x_i" />, <img src="https://latex.codecogs.com/svg.latex?\sigma_{Batch}^2=\frac{1}{m}\sum_{i=1}^m(x_i-\mu_{Batch})^2" alt="\sigma_{Batch}^2=\frac{1}{m}\sum_{i=1}^m(x_i-\mu_{Batch})^2" />

<img align="center" src="https://latex.codecogs.com/svg.latex?\widehat{x_i}=\frac{x_i-\mu_{Batch}}{\sqrt{\sigma_{Batch}^2+\epsilon}}" alt="\widehat{x_i}=\frac{x_i-\mu_{Batch}}{\sqrt{\sigma_{Batch}^2+\epsilon}}" /> , <img align="center" src="https://latex.codecogs.com/svg.latex?y_i=\gamma\widehat{x_i}+\beta\equiv_BN_{\gamma,\beta}(x_i)" alt="y_i=\gamma\widehat{x_i}+\beta\equiv_BN_{\gamma,\beta}(x_i)" />

<br />

- 단순히 표준정규분포로 정규화하면 활성화 함수의 영향력이 감소할 수 있으나, 정규화 이후에 선형 변환을 실시하면서 비선형성을 유지하게 함.
- 배치 정규화를 설명한 논문에선 해당 기법이 hidden layer's 공변량 증가(좀 더 다이나믹한 test 데이터 분포 변화)를 줄일 수 있다고 하였으나, 이후 이를 비교한 논문에 의하면 공변량 변화에 영향을 주지 못한다. 그러나 3가지 장점과 같이 성능 면에서 효과를 보이기 때문에 해당 장점을 근거로 사용한다.
