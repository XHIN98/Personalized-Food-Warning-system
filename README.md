# 프로젝트 이름
Personalized food warning system(image classification)

# 프로젝트 소개
다양한 음식이미지를 분류기.

# 프로젝트 개요/동기
저희 프로젝트는 사용자가 입력한 정보(건강, 종교, 비건 등)을 분석하여 해당 사용자가 피해야할 음식 성분을 ai가 판단을 해서 경고알림을 주는 시스템입니다. 즉 질병이나 알레르기, 종교 등 사용자가 피해야할 음식을 파악을 하고 개인의 건강, 종교의 다양성, 식습관 등을 존중하고서 나이 구분 없이 세계 사람들의 삶의 질을 높이고 싶어 이 프로젝트를 개발 하였습니다. 

# 기술 스택
<p>
  <img src="https://img.shields.io/badge/python-3776AB?style=flat-square&logo=Python&logoColor=white"/>
   <img src="https://img.shields.io/badge/TensorFlow-FF6F00?style=flat-square&logo=TensorFlow&logoColor=white"/>
   <img src="https://img.shields.io/badge/Google Colab-F9AB00?style=flat-square&logo=Google Colab&logoColor=white"/>
  <img src="https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=Jupyter&logoColor=white"/>
</p>

# 데이터 수집 및 가공
1. 데이터 수집 및 가공은 전체적으로 구글을 통해서 이미지 데이터를 수집

2. 데이터 가공 절차
- 각 음식이미지를 세분화 시킴
- 이미지를 세분화 시키고 keras 모델을 이용하여 데이터를 로드함
- 데이타세트의 성능을 높일 수 있도록 버퍼링된 프리페치를 사용해서 I/o를 차단하지 않고 디스크에서 데이터를 생성할 수 있도록 했습니다.
 - Dataset.cache(): 이미지를 로드한 후 메모리에 유지하였습니다.(데이타세트의 병목상태 해결)
 - Dataset.prefetch(): 훈련하는 동안 데이터 전처리 및 모델 실행을 중첩시킴

# 모델링 및 학습 절차
1. 
 - 기본적으로 데이터 모델링을 할 때 keras의 Sequential 모델을 사용했습니다.
 - conv2d: (사이즈 3 x e의 16개의 필터) 이미지에서 특징이 추출되도록 하였스니다.
 - maxpooling2D: 이미지의 크기를 절반으로 줄입니다.
 - Flatten: 데이터를 1차원 배열의 형태로 변환하였습니다.
 - relu: 값 x가 주어질 때 max(x,0)을 반환하여 0이하의 값을 모두 제거해주는 장점이 있습니다.
 - dense: 입력과 출력을 연결해주는 레이어
 - dropout 과대적합을 방지하기 위해 사용하였습니다.

![image](https://user-images.githubusercontent.com/111558519/229436094-c2b93197-027e-4f74-8e3d-7e256faa8a26.png)

2. 설계한 모델을 compile 진행
![image](https://user-images.githubusercontent.com/111558519/229436293-847d555d-386c-4e58-924d-5cf5cfac7ce4.png)

설계한 모델을 compile 할 때
1. optimizer 함수
- adm을 사용하였습니다. 
* 사용한 이유 *
- 간단한 구현을 통해 효율적인 연산이 가능하기 때문입니다.
- 사실상 해당 프로젝트를 할 때 메모리 요구사항이 많아서 adm을 사용하였습니다.
2. 손실함수
- Sparse Categorical Crossentropy 사용하였습니다.
*사용한 이유*
저희 프로젝트는 이미지를 분류하였습니다. 데이터를 하나하나 전부다 세분화를 시켰기 때문에 분류해야할 클래스가 3개이상이 제공되어야한다고 판단이 되어 사용하였ㅅ브니다.
# 모델 테스트
![image](https://user-images.githubusercontent.com/111558519/229438476-329bcc83-27f8-4e9d-9018-cdeecf864c71.png)
![image](https://user-images.githubusercontent.com/111558519/229438492-38835f0c-7c84-43af-a2c7-d2bd21956ba0.png)

# 결과
![image](https://user-images.githubusercontent.com/111558519/229438513-3738019e-89b9-44de-a2c0-c3fcbe03026a.png)
![image](https://user-images.githubusercontent.com/111558519/229438523-1b356eae-ab22-473e-bde8-46c71f64b853.png)

# 배운 점 & 아쉬운 점
### **데이터 처리 속도**

**AUTOTUNE**

하드웨어 리소스 병렬로 매핑하기 때문에 작업시간을 줄일 수 있다. 

**Prefetch**

GPU에서 데이터 처리(작업)시간을 줄이기 위해 사용되는 파이프라인

### **모델링(Modeling)**

**Sequential model**

layer-by-layer으로 쌓아 올릴 수 있어 대부분의 문제를 해결할 수 있다.

**Sequential model을 사용하면서 깨달은 점**

1. 여러 소스의 입력을 받아오지 못한다.
2. 여러 곳에 사용될 수 있는 다중 출력을 만들지 못한다.
3. 하나의 입력과 하나의 출력이 있는 일반적인 레이어 스택에 적합함.

### 과대적합

1. **더 많은 훈련 데이터가 필요하다는 것을 알게 됨.**
2. **네트워크의 용량을 줄일 필요가 있다는 것을 알게 됨.**
3. 가중치의 규제를 추가해줘야함.
4. **드롭아웃을 추가해줘야한다.(과대적합을 방직하기 위해 dropout() 사용)**
