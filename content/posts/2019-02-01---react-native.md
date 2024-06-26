---
title: mac에서 react-native 설정
date: '2019-02-01T20:40'
template: 'post'
draft: false
slug: '/1/'
category: 'react-native'
tags:
  - 'react-native'
  - 'react'
  - 'IOS'
  - 'android'
  - 'expo'
description: 'Mac에서 react-native를 사용하기전에 설정방법들!'
---

###### Mac에서 xcode를 이용해서 IOS 실행하는 방법

`brew install watchman` 페이스북의 파일시스템 변환해주는 툴이다.

`npm install -g react-native-cli` 로 react-native 설치

appStore에서 xcode 설치

`react-native init AwesomeProject` react-native 실행 [폴더명]

폴더에 들어간 후에 `react-native run-ios` 실행하면 디바이스까지 뜬다.

---

##### Mac에서 android-studio를 이용해서 android 실행하는 방법

위에 과정을 먼저 실행해야한다.

###### android-studio를 설치

설치중에 설치유형을 선택하라는 메세지에서

'사용자 정의'설정으로

- `Android SDK`
- `Android SDK Platform`
- `Performance (Intel ® HAXM)`( [AMD는 여기를 참조하십시오](https://android-developers.googleblog.com/2018/07/android-emulator-amd-processor-hyper-v.html) )
- `Android Virtual Device`

다음을 누르면 확인페이지가 나오고 모두 설치하면된다.

###### Android SDK 설치

> SDK 관리자는 Android Studio '환경 설정'대화 상자의 **모양 및 동작** → **시스템 설정** → **Android SDK에서도 찾을 수** 있습니다. SDK 관리자에서 'SDK 플랫폼'탭을 선택한 다음 오른쪽 하단의 '패키지 세부 정보 표시'옆의 확인란을 선택하십시오. `Android 9 (Pie)`항목 을 찾아 확장 한 후 다음 항목이 선택되어 있는지 확인하십시오.
>
> - `Android SDK Platform 28`
> - `Intel x86 Atom_64 System Image` 또는 `Google APIs Intel x86 Atom System Image`
>
> 그런 다음 'SDK 도구'탭을 선택하고 '패키지 세부 정보 표시'옆의 확인란을 선택하십시오. 찾기 및 "Android SDK 빌드 - 도구"항목을 확장 한 다음 `28.0.3`선택되어 있는지 확인하십시오 .
>
> 마지막으로 "적용"을 클릭하여 Android SDK 및 관련 빌드 도구를 다운로드하고 설치하십시오.
>
> -출처 공식문서

```
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin
export PATH=$PATH:$ANDROID_HOME/platform-tools
```

.bash_profile 을 찾는다. 있으면 안에 위에 코드를 작성한다.

`echo .bash_profile` 을 이용해 파일이 있는지 어디에 있는지 찾는다.

`vim .bash_profile` 로 파일을 열고 안에 적어준다.

파일이 없다면 ~/ 에 만들어준다.

Java Development Kit https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

Open kit 8 [Mac OS X x64] 설치

`react-native init AwesomeProject`

AVD( 가상의 디바이스 )를 새로 만들어준다.

폴더에 들어가 `react-native run-android` 로 실행하면 된다.

---

###### expo를 이용해서 실행하는 방법

`npm install -g expo-cli` 실행하면 expo가 설치되고, 모바일에서 expo클라이언트를 받는다.

`expo init AwesomeProject` 를 이용해서 마찬가지로 폴더생성 후 폴더로 이동

`npm start` 를 하면 웹화면이 뜨는데 QR코드가 나온다.

QR코드로 확인하면 실제 핸드폰에서 확인가능

---
