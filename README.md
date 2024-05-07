

<h1 align="center"> <br>소깎사 </h1>
<h3 align="center"> 팀 소깎사 </h3>
<h5 align="center"> 조혜원 | 장태욱 | 옥창우 | 이승제 </h5>
<h5 align="center">
모두의 연구소 AIFFEL X 스마트사운드<br>
청진음을 이용한 Abnormal lung sound(crackles, wheezes) Object Detection<br>
  

</h5>
<br>

<div align="center">

</div>

---

## Description
<!--
<div align="center">
  

</div>
-->

- 진행기간: 24.02 ~ 04
- 개발 목적: 호흡음 데이터를 기반으로 정상음과 비정상음을 감별하여 호흡수와 비정상음 판별
- 개발 개요:
  
  호흡음은 공기의 흐름, 폐 내부의 조직 변화, 폐 내 분비물의 위치와 직접적인 관련이 있어 호흡기 건강 및 호흡기 질환의 중요 지표로 사용됩니다.<br>
  증상의 위험성으로는 이러한 호흡들이 폐질환과 관련이 있으며 삶의 질, 건강의 문제로 이어 질 수 있습니다.<br>
  저희 조는 이런 이상 호흡들의 조기진단과 실시간 모니터링, 효율적 치료를 목적으로 하고자 [ICBHI 2017 Challenge Respiratory Sound Database](https://bhichallenge.med.auth.gr/ICBHI_2017_Challenge)를 통해 객체 탐지를 분석하는 모델 구축을 진행하였습니다. 
- 과정: 전처리 > bbox 추출 > 모델링 > 결과 확인
- [ [발표자료 PDF](https://github.com/team-Sogaksa/Respiratory_CL/blob/main/%E1%84%89%E1%85%A9%E1%84%81%E1%85%A1%E1%86%A9%E1%84%89%E1%85%A1_%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8C%E1%85%A6%E1%86%A8%E1%84%90%E1%85%B3%20%E1%84%87%E1%85%A1%E1%86%AF%E1%84%91%E1%85%AD_%E1%84%8E%E1%85%AC%E1%84%8C%E1%85%A9%E1%86%BC.pdf) ]


## About Aiffelthon
**<평가 방식>** 

 
- 다양한 모델 적용 후,  데이터에 대한 결과 비교
- 과업 : 수포음(crackle)과 천명음(wheeze) 확인과 호흡 개수 확인.



## 1. Dataset 

- 데이터셋: [ICBHI 2017 Challenge Respiratory Sound Database](https://bhichallenge.med.auth.gr/ICBHI_2017_Challenge) 
- 10초에서 90초의 920개의 녹음 파일(126명의 환자) 수록
- 각각의 녹음 파일에 대한 주석이 포함됨
- 6898개의 호흡 주기를 포함해 총 5.5시간 분량의 녹음 기록
- 1864개에는 수포음(crackle), 886개에는 천명음(wheeze), 506개에는 수포음(crackle) 와 천명음(wheeze) 이 모두 포함되어 있음.
- 데이터에는 깨끗한 호흡음만을 포함한 녹음 파일과 실제 생활 조건을 반영해 소음이 포함된 녹음 파일이 있음. 
- 환자는 모든 연령대를 포함

<!--
- `wheeze` - High-pitched, **100 -2500Hz**의 주파수 대역과 **80msec 이상의 지속시간**
- `crackle` - High-pitched, crackle의 **지속시간**은 **20 ms보다 더 낮고** 주파수 대역은 **100와 200 Hz** 사이
-->
- `crackle`: 기포가 작은 공기 통로를 통과하면서 만들어내는 딱딱거리는 소리
- `wheeze`: 좁아진 통로를 공기가 지나가면서 내는 휘파람같은 소리
  ||normal lung sound|crackle|wheeze|
  |---|---|---|---|
  |frequency(Hz)|50-2500|100-200|100-2500|
  |duration||<20 ms|>80ms|

> reference: [Analysis of Respiratory Sounds: State of the Art](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2990233/)
> (소리의 특징은 특정 질환, 상황에 따라 충분히 달라짐)

## 2. 전처리
-  sampling(8000Hz)
- zero padding
- 5th Butterworth filter


## 3. 특징 추출
- mel feature extraction
- bbox 각각 혹은 1500hz로 일정하게 맞춤.


## 5. 모델링
- Faster RCNN
- Yolo v8

## 6. 결과 확인 
1) Task 1 : crackle wheeze object detection 

<p align="center"><img width="392" alt="" src=""></p>


2) Task 2 : breathing counts
<img width="527" alt="" src="">





 
## 7. 결 론

- 소리를 기반으로한 데이터 처리하는 프로젝트는 처음이였으므로 sound data에 대한 전반적인 이해와 다양한 pre-processing 방법을 시도해보는 것을 목표로 하였습니다.
- Yolo 모델과 faster RCNN SSD 모델을 비교 후 Yolo v8 을 가지고 다양한 데이터 셋에 대하여 실험을 진행하였습니다. 다양한 augmentation과 여러가지 데이터셋으로 평가를 시도해 보았습니다.
- 첫번째 과업인, 비정상음에 대한 object detection은 Yolo v8 model로 noise remove와 bbox를 1500hz 기준으로 만들고 image size가 1280x720에서 가장 좋은 점수를 얻었습니다.
- 호흡의 수는 bbox를 카운팅 하는 방식으로 얻을 수 있었습니다.
- 해커톤 발표를 통하여, transformer 모델을 이용해 점수를 더 높여야 실제로 쓰일 수 가 있는 성능 정도는 되겠다고 생각하여 향후 다양한 model building 과 함께 추가적인 test를 해볼 예정입니다.


## 8. References
- [Analysis of Respiratory Sounds: State of the Art](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2990233/)


<br>
<br>
<br>
