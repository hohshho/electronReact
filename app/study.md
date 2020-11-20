# electronReact

# 주의할 점
 - Window, Linux, Mac OS 플랫폼과 x64, ia32, armv7 arm64 아키텍처를 지원
 - 의존 패키지가 네이티브 C++ 모듈이 들어간 패키지라면 그것들도 타겟 플랫폼/아키텍처를 지원하는지 여부를 따로 고려
 (ex : serialport Windows/Linux ia32/x64 용으로만 제공하고 있어서 armv7로는 바로 사용 불가)
 // 직접 타겟 환경에 따라 빌드해서 설정가능

# WebPack

# Why?

## WebPack과 같은 모듈 번들러는 여러개의 파일을 하나의 파일로 만들어 주기 때문에, 네트워크 병목현상을 최소화 시킬 수 있다.

# How to?

 - webpack.config.js 파일에서 설정 
 - Webpack4에서 Zero-configuration(설정파일이 없는 빌드)가 가능한 버전으로 업그레이드 // 더 알아보자

 1. Entry : 시작점, 여러개의 entry 가능

 2. Output : 생성한 번들을 저장할 위치 생성 (defalut : ./dist/main.js)

 3. Loader : Webpack이 이해할 수 있는 모듈로 변경해 주는 역할

 4. Plugins : 번들된 파일을 난독화 하거나, 압축하는데 사용

# Package.json

## dependencies -> npm install --only=prod[uction]

## devdependencies -> npm install --only=dev[elopment]

# Electron-Builder
 - pakage.json -> build 설정으로 빌드
 - app : 백엔드
 - build : create-react-app으로 빌드된 프론트엔드 결과물

Create-React-App으로 만들어진 앱은 기본적으로 JavaScript와 CSS 같은 에셋을 로드할 때 package.json의 homepage 값 혹은 정적으로 특정 경로를 참조하게 됩니다. 실제 앱이 실행될 때는 내부에 포함되어 있는 파일이 되므로 이것을 ./로 설정하여 로컬에서 정상적으로 불러오도록 만들어주어야 합니다.

# Node Module
 - cross-env: 실행하는 OS에 상관없이 환경 변수 지정
 - electron-is-dev: 현재 Electron.JS 앱이 개발 환경에서 실행하는지 파악
 - concurrently: 동시에 여러 프로세스를 실행 가능해짐
 - wait-on: 특정 시그널을 기다림
 - electron: Electron.JS

# script
## 실행
### 1)  "start-interface": "cross-env BROWSER=none npm run start"
 - Electron 앱을 지켜보게 될테니 먼저 브라우저없이 Webpack 개발 서버를 시작할 수 있도록 cross-env 패키지를 사용하여 BROWSER 환경 변수를 none으로 설정  
### 2) "start-electron": "electron ."
 - Electron앱만 시작 가능하게 설정  
### 3) "start-electron-after-interface": "wait-on http://localhost:3000 && npm run start-electron"
 - wait-on 패키지 활용해 Webpack 개발 서버 다음에 Electron앱이 실행하도록 설정
### 4) "dev": "concurrently -n interface,app 'npm:start-interface' 'npm:start-electron-after-interface'"
 - concurrently 패키지를 사용하여 동시에 시작되게 함.  

## 배포
### 5)  

# Entry Point
 - ReactJS 경우 src로 정해져 있음.
 - Electron-Builder의 프리셋에서 엔트리 포인트를 ./public/electron.js로 강제하고 있음.  
   -> ../app으로 설정해주면 된다.

# 참고 사이트

## 개념
 1) https://code0xff.tistory.com/177?category=804218
 2) https://www.fiveminutesdev.com/react%ec%99%80-electronjs%eb%a1%9c-%eb%8d%b0%ec%8a%a4%ed%81%ac%ed%86%b1-%ec%95%b1-%eb%a7%8c%eb%93%a4%ec%96%b4%eb%b3%b4%ea%b8%b0-1-%ed%94%84%eb%a1%9c%ec%a0%9d%ed%8a%b8-%ec%84%b8%ed%8c%85/
 3) https://typed.sh/react-jswa-electron-jsro-neitibeu-aeb-gaebalhag

## electron 배포
 1) https://knphouse.tistory.com/88

## 캐시 관련
 1) https://jrabbit.tistory.com/73?category=563144

## electron 보안
 1) https://www.electronjs.org/docs/tutorial/security

# custom titlebar
https://www.npmjs.com/package/custom-electron-titlebar