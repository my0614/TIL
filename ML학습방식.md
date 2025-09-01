# 머신러닝 학습 방법
머신러닝의 대표적인 학습 방식에 대해서 정리<br>
실무에서 많이 사용하는  머신러닝의 학습 방법 Pretraining, Transfer Learning ,Fine-tuning,3가지가 있다.

## Pretraining [사전학습]
- 대규모의 데이터셋이나 범용 데이터셋을 사용하여
학습하고 데이터셋에 대한 특징과 패턴을 학습하는 과정
- Pretrain 모델은 범용 데이터셋이 학습되어있어서
기본적인 특징과 패턴을 추출하는 할 수 있다. 

범용데이터셋 ex) ImageNet, COCO 등

## Transfer Learning [전이학습]
- 학습한 모델(weights)를 다른 학습 데이터셋에 활용하여 학습하는 방식
- 기존 학습 weights의 가중치, 파라미터를 그대로 가져와서 활용하는 방식

## Fine-tuning
- 전이학습 중에 한가지 방법이고, Pretraining 모델 weights를 가져와서 원하는 Task에 맞도록 수정해서 학습한다.
- Pretraining 모델의 Feature Extractor(특징 레이어)를 그대로 사용하여 학습하는 파라미터와 output channel만 수정하여 학습을 진행

**Feature Extractor 이란?**</br>
Input에서 Feature(특징)을 뽑아주는 모델의 앞단 레이어 부분

-> 이미지의 경계, 색상, 패턴 등에 대한 Feature 추출</br>
ex) CNN : Conv, Pooling