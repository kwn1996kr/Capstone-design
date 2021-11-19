# Yolov5를 이용한 사과상태측정기 어플리케이션
상명대학교 캡스톤 디자인 <br />
- email address : kwn1996kr@naver.com <br />
<img src="https://user-images.githubusercontent.com/78460820/142620626-0122f36b-4a86-4a81-a331-8f1a88304f18.jpg" align="left" width="200" height="400"/>
<img src="https://user-images.githubusercontent.com/78460820/142620657-7a33d871-268a-4edd-aba8-19514e2c942a.jpg" align="center" width="200" height="400"/>

## Introduction
Yolov5와 Tensorflow Lite를 기반으로한사과 상태 측정 어플리케이션
1. Yolov5로 학습한 식재료 탐지 모델을 이용하여 실시간으로 사과 탐지
2. 현재까지 인식한 사과의 등급 및 상태를 보여줌
3. 병해충 클릭시 병해충 관련 링크 전송

## Development Environment
- Local
- Yolov5
- Tensorflow 1.15.2v
- Android Studio @3.5.3

## Food ingredients dataset
1. Class : 11
    - 탄저병, 그을음점무늬병, 검은별무늬병, 그을음병, 겹무늬썩음병, 사과, 색(상), 색(중), 색(하), 강한상처, 약한상처
    

2. Images : 1533
3. TRAIN/TEST SPLIT(100%) (기존의 데이터를 회전 반전으로 데이터 증강함)
    - Train : 1219(80%)
    - Valid : 157(10%)
    - Test : 157(10%)
    
![fsa](https://user-images.githubusercontent.com/78460820/142620555-fe57cbc5-a21f-4496-bc2c-5ab80d9bbf04.png)
    
Dataset download : https://app.roboflow.com/ds/GN9aUMJdR1?key=gcxVDmN2be

## Model Training
1. yolov5 설치
```bash
!git clone https://github.com/zldrobit/yolov5.git
```

2. requirements.txt 설치
```bash
%cd /content/yolov5/
pip install -r requirements.txt
```

3. Model 학습
```bash
python train.py --img 640 --batch 16 --epochs 100 --data ../data.yaml --cfg ./models/yolov5m.yaml --weights yolov5m.pt --name rotten_apple_v4
```

(요기부턴 안드로이드 연동)  
4. https://github.com/zldrobit/yolov5 이동
 models/tf.py 파일을 colab의 /content/models/ 디렉터리에 저장
 
5. 학습된 가중치 파일(.pt)를 .tflite로 변환


## Android 연동
1. yolov5 app 변경
yolov5의 app의 내용을 
https://github.com/kwn1996kr/Capstone-design.git 로 변경

2. assets에 Model Training에서 학습한 423-fp16.tflite 파일 저장
또는 
weight(.tflite) 
https://drive.google.com/file/d/1jcgIH6LM9JsDLLs1jfL3XtXecRb8qOQK/view?usp=sharing 저장

3. 실행 ^^
