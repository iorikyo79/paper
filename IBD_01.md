# Development of an artificial intelligence tool for detecting colorectal lesions in inflammatory bowel disease 
 
2023년 4월 Mayo Clinic에서 개발한 염증성 장질환(IBD) 환자의 대장 용종 및 병변을 검출하는 인공지능 모델인 IBD-CADe에 대한 연구.  

### 기여
IBD-CADe는 염증성 장질환 환자의 대장암 감시 검사에서 표적 조직검사를 늘리고 무작위 조직검사의 필요성을 줄임으로써 이형성증 검출을 도울 수 있음

![image](https://github.com/iorikyo79/paper/assets/11941673/35562983-3d49-4672-91b3-f8e9f89ce1d8)

#### 배경과 목적
염증성 장질환(IBD) 환자는 대장암 위험이 높습니다. 인공지능(AI)을 활용하면 의사가 암으로 발전할 수 있는 대장 용종을 보다 정확히 발견할 수 있어 IBD 환자의 대장암 발생률을 낮출 수 있습니다. 이에 저자들은 IBD 환자의 대장 병변을 검출하는 컴퓨터 보조 진단(CADe) 모델을 개발했습니다.
또한 기존 대장용종을 찾는 연구에서는 IBD 환자들은 배제되어 있었고 IBD환자의 경우 점막염증 때문에 용종 찾기가 더 어려웠습니다. 그래서 IBD 전용 인공지능 모델의 개발이 필요 했습니다.

### 방법 
- Step1. 
- IBD가 없는 환자의 대장 병변으로 학습된 기존 CADe 모델의 성능을 IBD 환자의 대장내시경 이미지로 먼저 평가
- Step2.
- 이후 저자들은 IBD 병변이 확인된 1,266장의 고화질 백색광 내시경(HDWLE) 이미지와 426장의 색소내시경 이미지로 CADe 모델을 재학습시켜 IBD-CADe 모델을 만들었습니다. 
- Step3. 
- 병변의 조직병리, 크기, 모양, 주변 염증 정도에 따라 이미지에 주석을 달았고, 모델의 재학습 전후 성능을 비교 평가했습니다. 
![image](https://github.com/iorikyo79/paper/assets/11941673/8dbb6a9d-c58a-4426-b87b-bec04b25c561)
- Figure 1Study flowchart for development of IBD-CADe. CADe, Computer-aided detection; HDWLE, high-definition white-light endoscopy; IBD, inflammatory bowel disease; WL, white light.

### 결과 
기존 CADe 모델의 IBD 병변 검출 민감도는 50%에 불과했으나, IBD 이미지로 재학습시킨 IBD-CADe 모델의 HDWLE 병변 검출 민감도는 95.1%로 크게 향상되었고, 특이도, 양성예측도, 정확도 모두 96% 이상으로 우수했습니다. 

색소내시경 영상에서의 성능은 이보다는 낮았습니다. 하위그룹 분석 결과, IBD-CADe는 5mm 이하 병변 93%, 6-10mm 병변 91%, 10mm 초과 병변 85%를 검출할 수 있었습니다. 모양별로는 융기형 병변에서 가장 잘 작동했고, 평편형은 잘 검출하지 못했습니다. 놓친 병변 대부분은 염증이 경미한 점막에 있었습니다. 

![image](https://github.com/iorikyo79/paper/assets/11941673/a967047e-b1c8-4ba5-8a01-1a819205e5f3)
![image](https://github.com/iorikyo79/paper/assets/11941673/0adfc657-251f-40aa-99bc-f70e979b5785)
- 위쪽 두 장의 사진(A)은 가성용종(pseudopolyp) 검출 예시, 모델 재학습 전(왼쪽)에는 검출하지 못했다가 재학습 후(오른쪽)에는 잘 찾아냄. 
- 아래쪽 두 장(B)은 톱니모양 상피 변화(serrated epithelial change), 재학습 전에 못 찾다가 재학습 후 경계 상자를 그려서 검출

### 결론 
이 연구는 IBD 환자의 대장 이형성증을 검출하는 AI 모델을 개발하는 첫 단계입니다. IBD-CADe는 IBD 환자에서 육안으로 식별 가능한 암 전구 병변의 검출을 향상시킬 수 있을 것으로 기대됩니다.

### 한계
염증이 심한 부위나 편평한 병변에 대한 검출률을 높이기 위해 더 많은 데이터로 추가 학습이 필요함. 데이터의 양이 부족함. 단순 검출에서 양성/악성 여부를 판단하는 모델로 개선이 필요.
