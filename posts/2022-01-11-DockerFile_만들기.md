---
layout: post
title: "DockerFile 만들기"
date: 2022-01-11
---

<p><b>DockerFile 만드는 이유&nbsp;</b><br />Docker image에 필요한 OS 정보부터 패키지 설치까지 다 넣어놓음 &gt; 이미지 빌드 후 사용에 훨씬 편리함.&nbsp;</p>
<p>&nbsp;</p>
<p>1. DockerFile 작성 ( ubuntu 설치에 git, vim, python 등 필요한 패키지 및 pyenv 설치까지 포함된 DockerFile )&nbsp;</p>
```FROM ubuntu:bionic
RUN apt-get update
RUN apt-get install -y git
RUN apt-get install vim -y
RUN apt-get install -y python3-pip

# pyenv package 
RUN apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
xz-utils tk-dev```
<p>&nbsp;</p>
<p>2. 위 도커 파일 만들고 도커파일 경로로 이동&nbsp;</p>
<p>$ docker build -t ubuntu:[tagname] .&nbsp;</p>
<p>&nbsp;</p>
<p>3. 2에서 만든 이미지 확인&nbsp;</p>
<p>$ docker images&nbsp;</p>
<p>&nbsp;</p>
<p>4. 도커 이미지 컨테이너에 올리기&nbsp;</p>
<p>$ docker run -it ubuntu:[태그명] bash&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>DockerFile 빌드 방법&nbsp;</p>
```docker build --rm -t [컨테이너로하고싶음이름] .```
<p>&nbsp;</p>