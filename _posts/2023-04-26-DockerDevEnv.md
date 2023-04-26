---
title: Docker - 개발환경 셋팅
published: true
---
1. docker hub에서 node image pull
```cmd
docker pull node:18.16.0-alpine3.17
```
2. docker host에서 container port를 8000에서 8000으로 Floating router 하고, CLI 띄움
```cmd
docker run -it -p 8000:8000 --name node-18 node:18.16.0-alpine3.17 /bin/sh
```

3.app 폴더 만들고
<img width="478" alt="image" src="https://user-images.githubusercontent.com/88364980/234478298-0f934eb2-c686-4d59-9fac-94ff39212fe3.png">

4.app 폴더로 이동 후 vue project 생성
```cmd
npm init vue@latest
```
<img width="493" alt="image" src="https://user-images.githubusercontent.com/88364980/234478709-80c50572-132b-457c-86cf-0fb4ba2f5969.png">

5.프로젝트 폴더로 이동 후에 npm install
```cmd
npm install
```
<img width="524" alt="image" src="https://user-images.githubusercontent.com/88364980/234479058-b7d3b022-b41e-43aa-b476-a63970141d02.png">

6.vite는 기본 port가 5173으로 설정되어 있으니 packgage.json에서 port 변경
<img width="597" alt="image" src="https://user-images.githubusercontent.com/88364980/234479786-025e0f61-ed23-4841-9812-48eb4e7900ae.png">

7.front 실행
```cmd
npm run dev
```
<img width="951" alt="image" src="https://user-images.githubusercontent.com/88364980/234479933-678ab913-d3ce-4598-ba2b-cdb49c0e007e.png">



