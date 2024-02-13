# Generating Docker Image
Accel-sim Environment setting.

아래 환경의 이미지를 생성할 수 있다 (dockerfile 참조).
- Ubuntu-18.04
- CUDA 11.3.0
- python 3.8
- PyTorch 1.12.1

이외에도 사용 목적에 맞게 변용 가능.

# Build container
```
docker build -t [이미지] [컨테이너 위치]
docker build -t accel-sim/ubuntu-18.04_3.8_11.3.0_1.12.1 .
```

# Run container
```
docker run -[컨테이너 실행 옵션] --name=[컨테이너 이름] --gpus all --restart=[재시작 옵션] -v [로컬 마운트 경로]:[컨테이너 마운트 경로] [이미지 이름] /bin/bash
docker run -it --name=jykim --gpus all --restart=unless-stopped -v /home/jykim/share:/EEE4610/share accel-sim/ubuntu-18.04_3.8_11.3.0_1.12.1 /bin/bash
```
컨테이너 환경과 로컬 환경을 mount할 수 있다 (파일 공유).
옵션에 따라 다양한 설정 가능.

# Attach to container
```
docker attach [컨테이너이름]
```

# Container exit
```
ctrl + d : 종료
ctrl + p + q: 중단없이 나가기
```
