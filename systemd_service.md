# systemd service란?

특정 프로그램이나 스크립트를 부팅 시 자동으로 실행되도록 
파일을 만들어서 관리

## service 생성
```
# systemd service 경로
cd /lib/systemd/system/

# 원하는 service 파일 생성
vim exam.service
```

## service 구조
### [Unit] 섹션
- 서비스 단위 자체를 설명하고, 다른 서비스나 시스템 상태와의 관계를 정의
```
Description=My App Service
After=network.target
Requires=docker.service
```
Description → 서비스 설명 </br>
After → 어떤 서비스/타겟 이후에 시작될지 지정 </br>
Requires → 반드시 필요한 서비스 지정 (없으면 시작 안됨) </br>

### [Service] 섹션
- 실제 서비스 실행 방법과 동작 방식 정의
```
[Service]
User=root
ExecStart=/usr/bin/my_app
ExecStop=/usr/bin/my_app_stop
Restart=always
```
User → 실행할 사용자 지정 </br>
ExecStart → 서비스 시작 시 실행할 명령어 </br>
ExecStop → 서비스 종료 시 실행할 명령어 </br>
Restart → 서비스 종료 시 재시작 정책 (always, on-failure 등)

### [Install] 섹션
- 서비스 설치 및 활성화 관련 설정 / 주로 부팅 시 자동 실행을 설정할 때 사용
```
[Install]
WantedBy=multi-user.target
```
WantedBy → 어느 타겟에서 서비스가 활성화될지 지정
multi-user.target → 일반 서버 모드에서 자동 시작

### Service 관련 command
```
# daemon reload
sudo systemctl daemon-reload
# 서비스 시작
sudo systemctl start exam.service
# 부팅 시 자동 시작
sudo systemctl enable exam.service
# 상태 확인
sudo systemctl status exam.service
```