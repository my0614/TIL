# Depth Estimation
카메라나 영상 이미지에서 물체와의 떨어진 거리를 예측하는 것을 의미

## Depth Estimation 종류
Depth Estimation 대표적으로 2가지 종류로 나뉜다.
Mono Depth Estimation과 Stereo Depth Estimation.

### Mono Depth Estimation란?
한개의 RGB 영상을 통해서 깊이 추정하는 기술.
단일 이미지에서는 깊이를 추정하기 어려워 추가적인 센서나 보조가 필요.

### Stereo Depth Estimation란?
좌/우 카메라에서 찍은 두 장의 RGB 영상을 사용해서 Depth를 계산.
삼각측량(triangulation)원리를 이용해 두 영상의 시차를 계산하고, 이를 통해 Depth 얻음.

### RGB와 Depth 영상을 사용하여 시간 동기화
이때 각 센서의 프레임 캡처 시점이 조금씩 다를 수 있기 때문에
같은 순간의 장면을 정확히 비교하기 위해서는 시간 동기화 과정이 필요. </br>
-> ROS에서는 message_filters 패키지의 ApproximateTimeSynchronizer를 사용하여 RGB와 Depth 영상을 동기화
```
# 서로 다른 영상의 프레임 동기화
self.ts = message_filters.ApproximateTimeSynchronizer([self.rgb_sub, self.depth_sub], queue_size = 10, slop = 0.5)
self.ts.registerCallback(self.image_callback)
```