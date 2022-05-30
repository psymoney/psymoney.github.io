---
title: 'AWS에 Jupyter Notebook 올리기'
categories: Coursera
tags: Algorithm
author_profile: true
published: true
---
## AWS에 Jupyter Notebook 올리기
### 부제: 동빈나님 강의를 따라갈 수 없어요!

해당 포스팅은 동빈나님의 강의인 "[도커(Docker) 활용 및 배포 자동화 실전 초급](https://www.youtube.com/watch?v=LoYpXoBJPMc)" 을 따라가던 중, 
EC2 인스턴스에 배포한 Jupyter Notebook에 접속이 원활하게 되지 않는 문제점을 해결하게 해준 대체 강의의 내용을 정리 및 요약한 내용이다.

내가 겪은 문제 상황은 다음과 같다.
1. EC2 인스턴스에서 Jupyter Notebook 서버의 구동은 정상적으로 작동한다.
2. 하지만, EC2 public IPv4를 통해 해당 Jupyter Notebook에 접속하면 접속이 되지 않는다.   

원인을 알 수가 없어 같은 주제를 다음 유튜브 영상을 보고 시도하여 해결하였다.   
[How to setup Jupyter notebook/lab for development on EC2 instance p1](https://www.youtube.com/watch?v=qYe5J5lBvn4&list=PLfkvr8CCU9yAD6mVM7RlVlQNJ8x9R6kGm&index=1)

해당 영상을 따라하기 위해 새로운 인스턴스를 생성하여 진행항 결과 Jupyter Notebook은 매우 잘 접속되었고, 이후 동빈나님의 Docker 실습 부분도 진행할 수 있었다.   
하지만, 동빈나님 강의를 보며 진행했던 인스턴스에도 해당 강의 내용을 동일하게 적용하였는데 여전히 Jupyter Notebook은 먹통인 상황이다. 원인 파악이 된다면 추후 수정하여 반영하겠다.


동빈나님의 영상과 해당 영상에서 공통적으로 다루는 부분은 제외하였다.

#### 1. 필요 라이브러리 설치
```shell
# apt-get 업데이트
$ sudo apt-get update

# 파이프라인 설치
$ sudo apt-get install python3-pip

# 파이썬 가상환경 라이브러리 설치
$ sudo apt-get install python3-venv
```
해당 강의에서는 파이썬 가상환경에서 실습을 진행한다.

#### 2. 파이썬 가상환경 설정
```shell
# 가상환경 패키지 설치
$ python3 -m venv pyenv

# 가상 환경 구동
$ source pyenv/bin/activate
```
가상환경 패키지를 설치하고,가상 환경을 구동한다.
#### 3. Jupyter lab 설치
```shell
# Jupyter lab 설치
$ pip3 install jupyterlab

# Jupyter Notebook 비밀번호 설정
$ jupyter notebook password
```
영상 제작자에 의하면 Jupyter lab에는 Jupyter notebook 및 관련 라이브러리가 포함되어 있다고 한다.   
동빈나님의 강의에서는 Jupyter notebook의 접속 비밀번호를 config.py 파일에 해시된 비밀번호로 설정하지만, 해당 강의에서는 커맨드를 통해 설정한다.

#### 4. Jupyter notebook 구동
```shell
$ jupyter notebook --ip 0.0.0.0 --no-browser --allow-root
```
여기까지 진행하고 해당 포트에 대한 EC2 인스턴스 방화벽을 해제한다면 Jupyter Notebook에 정상적으로 접속이 될 것이다.    
혹여나 동일한 어프로치를 적용해도 구동이 안되는 분들은 새로운 인스턴스에서 해당 영상을 정확히 따라해보는 것을 추천한다.

추가적으로 해당 강의에서는 ```nohup``` 명령어를 통해 Jupyter Notebook 서버를 백그라운드에서 구동시킨다.   
명령어는 Jupyter notebook 구동 명렁어 앞에 ```nohup``` 키워드를 추가해주면 된다.
