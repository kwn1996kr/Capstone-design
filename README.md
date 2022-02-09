<p align="center">
    <img src="https://user-images.githubusercontent.com/78460820/153244234-b615e79e-6f4e-4184-8645-da25088ac0c2.png" align="center" width="100" height="100"/>
</p>

# Yolov5를 이용한 사과상태측정기 어플리케이션
<!--상명대학교 캡스톤 디자인 <br />
- email address : kwn1996kr@naver.com <br />-->
The Apple condition detector detects the pests, cuts, bruises, and colors of apples and checks their grades in real time.</br>
You can use it if you want to know the grade of an apple or what pests you harvested are.
<p align="center">
    <img src="https://user-images.githubusercontent.com/78460820/153245339-45db95a6-d4af-41f1-b8e4-00d9cbf81516.png"  width="200" height="350"/>
</p>

## 🍎Introduction
Yolov5와 Tensorflow Lite를 기반으로한사과 상태 측정 어플리케이션
1. Yolov5로 학습한 식재료 탐지 모델을 이용하여 실시간으로 사과 탐지
2. 현재까지 인식한 사과의 등급 및 상태를 보여줌
3. 병해충 클릭시 병해충 관련 링크 전송

## 💻Development Environment
- Google colaboratory, local(GPU : 2070super 8GB, RAM : 16GB, CPU : 3700x)
- Yolov5
- Tensorflow 1.15.2v
- pytorch 1.10.0+cu111
- Android Studio @3.5.3

## 📀Food ingredients dataset
1. Class : 11
    - 탄저병, 그을음점무늬병, 검은별무늬병, 그을음병, 겹무늬썩음병, 사과, 색(상), 색(중), 색(하), 강한상처, 약한상처
    

2. Images : 1533
3. TRAIN/TEST SPLIT(100%) (기존의 데이터를 회전 반전으로 데이터 증강함)
    - Train : 1219(80%)
    - Valid : 157(10%)
    - Test : 157(10%)
    
![fsa](https://user-images.githubusercontent.com/78460820/142620555-fe57cbc5-a21f-4496-bc2c-5ab80d9bbf04.png)
    
Dataset download : https://app.roboflow.com/ds/GN9aUMJdR1?key=gcxVDmN2be

## 📀Apple Class example
 1. apple : It is a class to check if it is an apple(Using all kinds of apples)
<img src="https://user-images.githubusercontent.com/78460820/153246547-098ffe45-ce74-4d49-b12c-4b5cd0904d28.png"/>
 2. apple_A : An apple with superior color(Using only Fuji apples)
 <img src="https://user-images.githubusercontent.com/78460820/153247259-b3e9a5a8-cd50-4d48-99d8-2dd6c21054c9.png"/>
 3. apple_B : An apple with medium color(Using only Fuji apples)
 <img src="https://user-images.githubusercontent.com/78460820/153247343-97798a2a-3f9c-4fbf-af6f-d9fc8358f143.png"/>
 4. apple_C : An apple with bed color(Using only Fuji apples)
 <img src="https://user-images.githubusercontent.com/78460820/153247425-2b2f9b76-9677-4a0c-9071-e00d35fc9059.png"/>
 5. dmg_s : Apple with small cuts or weak bruises that can be sold as a prize(Using all kinds of apples)
 <img src="https://user-images.githubusercontent.com/78460820/153247611-9cc6bb87-7437-456f-8aba-4458981ddc63.png"/>
 6. dms_l : Apple with strong cuts or strong bruises that cannot be sold as a prize(Using all kinds of apples)
 <img src="https://user-images.githubusercontent.com/78460820/153247719-6f266de9-9c02-4db6-86bc-95bbf3389d0a.png"/>
 7. Scab
 <img src="https://user-images.githubusercontent.com/78460820/153247822-15ab530d-b75a-4607-8e74-cbd9c361f3cf.png"/>
 8. Anthracnose
 <img src="https://user-images.githubusercontent.com/78460820/153247914-5a86cad8-025e-4a85-a778-24d7542dd6ac.png"/>
 9. Sooty blotch
 <img src="https://user-images.githubusercontent.com/78460820/153247978-5773d2e5-2a6e-470b-bd78-c4ae63003d35.png"/>
 10. Fly speck
 <img src="https://user-images.githubusercontent.com/78460820/153248042-eb578f17-e360-46fb-a1f6-6248c542c18a.png"/>
 11. White rot
 <img src="https://user-images.githubusercontent.com/78460820/153248100-f7c4eae8-9b3d-4c51-9187-30cfb119fc2e.png"/>


## 📝Model Training
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


## 📱Android 연동
1. yolov5 app 변경
yolov5의 app의 내용을 
https://github.com/kwn1996kr/Capstone-design.git 로 변경

2. assets에 Model Training에서 학습한 423-fp16.tflite 파일 저장
또는 
weight(.tflite) 
https://drive.google.com/file/d/1jcgIH6LM9JsDLLs1jfL3XtXecRb8qOQK/view?usp=sharing 저장

3. 실행 ^^
