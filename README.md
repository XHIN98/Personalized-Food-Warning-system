# 프로젝트 이름
Personalized food warning system(image classification)


# 프로젝트 소개
다양한 음식이미지를 분류해주는 모델 설계

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

# 데이터 모델링
- 기본적으로 데이터 모델링을 할 때 keras 모델을 사용하여 모델을 구성하였습니다.
# 모델 학습

# 모델 테스트

# 결과


# 구현 기능
# 기능 1
# 기능 2
# 기능 3
# 기능 4

# 배운 점 & 아쉬운 점

