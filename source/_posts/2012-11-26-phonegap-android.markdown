---
layout: post
title: "Phonegap-Android"
date: 2012-11-26 13:22
comments: true
categories: Phonegap Android
---

## 사용 환경

- 모델명    :     MacBook Pro
- 모델 식별자:	  MacBookPro8,1
- 메모리:	       4 GB
- Eclipse: v4.2.1

## 요구 환경

- Eclipse 3.4+

## Eclipse Classic 설치

### Eclipse 다운로드

이클립스 공식 사이트 [Eclipse Classic](http://www.eclipse.org/downloads/)에서 다운 받습니다.

{% img https://lh4.googleusercontent.com/-eEEddA1zCKw/UK9H_HFMlMI/AAAAAAAAADM/apX-8h1nAGE/%25252FUsers%25252Fhancho%25252FPictures%25252Feeclipse-down-classic.jpg 500 500 "Eclipse down" %}

### 압축 해제및 실행

다운 받은 파일은 .tar.gz 압축 파일 이므로 압축 해제후 Eclipse 아이콘을 클릭 합니다.

### Eclipse 실행

다음과 같은 페이지가 나오며 `ok`를 클릭 합니다.

{% img https://lh4.googleusercontent.com/-GlTWPfVPvs0/UK9I7Ea48yI/AAAAAAAAADU/Isd5LGHAKGo/%25252FUsers%25252Fhancho%25252FPictures%25252Feclipse-install-01.jpg 500 500 "Eclipse 설치" %}

## Android SDK 설치

### Android 다운로드
안드로이드 개발 공식 사이트인 [SDK](http://developer.android.com/sdk/index.html)에서 다운 받습니다.

{% img https://lh5.googleusercontent.com/-4Kryzuug_wA/UK9KTEltWAI/AAAAAAAAADc/Ci-vVNhUJC0/%25252FUsers%25252Fhancho%25252FPictures%25252Fphoone%25252Fphone-android-01.jpg 500 500 "SDK Down" %}

### Android SDK 환경 설정

#### 파일 열기

{% codeblock lang:bash %}
$ vi ~/.bash_profile
{% endcodeblock %}

#### .bash_profile 개인 SDK파일의 경로를 추가해 줍니다.
    
{% codeblock bash_profile %}
export PATH=${PATH}:/Development/android-sdk-macosx/platform-tools:/Development/android-sdk-macosx/tools
{% endcodeblock %}

#### 설정 확인

{% codeblock lang:bash %}
$ source ~/.bash_profile
$ echo $PATH
…./Users/han/Development/android-sdk-macosx/sdk/platform-tools:/Users/han/Development/android-sdk-macosx/tools….
{% endcodeblock %}
    
## Xcode Command Line Tools 설치

### Xcode 실행후 > Xcode Preferences 선택 합니다.

{% img https://lh6.googleusercontent.com/-9lGHtlIr6t0/UK3bfp3Kn9I/AAAAAAAAACc/7g0GBCw6L24/%25252FUsers%25252Fhancho%25252FPictures%25252Fxcode-line-tool-01.jpg 500 500 "Command line 설치" %}

### Downloads->Components-> Command Line Tools -> Install 클릭으로 설치 합니다.

{% img https://lh3.googleusercontent.com/-rAUx02VExcY/UK3br16WT8I/AAAAAAAAACk/1b5_-hdFebk/%25252FUsers%25252Fhancho%25252FPictures%25252Fxcode-line-tool-02.jpg 500 500 "Command Line Tolls 설치" %}

설치가 끝나면 Terminal.app (iTerm)에서 커맨드 라인으로 작업을 할수가 있습니다. 자세한 사항은
[Command-Line](http://docs.phonegap.com/en/2.2.0/guide_command-line_index.md.html#Command-Line%20Usage)에서 iOS 부분을 참고 하시면 됩니다.

## Apache Cordova 다운로드

다운로드된 파일은 .zip 파일이므로 압축을 풀어서 사용하시면 됩니다.

- Cordova는 [Cordova-Down](http://phonegap.com/download)에서 다운 받을수 있습니다.
- 다운 받은 폴더를 ~/CordovaLib-2.x.x 쓰기 편한 위치로 이동 시킵니다.

## 새로운 프로젝트 시작하기

### bin 폴더 열기

새로운 프로젝트를 생성하기 위해서는 ./create 파일을 실행 해야 합니다. create 파일은
lib/android/bin 폴더에 존재 합니다.

lib/ios/bin 폴더로 직접 이동 해서 사용할수 있습니다.
또는 ~/CordovalLib-2.2/lib/android/bin 폴더를 Terminal.app에 드래그 하면 bin 폴더로 바로 이동 할수 있습니다.

### create 실행하기

사용 방법

{% codeblock lang: bash %}
$ ./create <project_folder_path> <package_name> <project_name>
{% endcodeblock %}

#### create 사용

{% codeblock lang:bash %}
$ ./create <project_folder_path> pheonegap.start start
$ cd ~/project_folder_path
$ ls
AndroidManifest.xml	cordova   project.properties
ant.properties          gen	  res
assets	                libs	  src
bin	                local.properties
build.xml               proguard-project.txt
{% endcodeblock %}

## Eclipse 실행하기

### SDK 지정 하기

eclipse를 처음 실행 하게 되면 다음과 같이 SDK 폴더를 지정합니다.

{% img https://lh4.googleusercontent.com/-ot4Vk-4u5_Y/ULLcJlNDr9I/AAAAAAAAADs/5Vx_AyDGqRo/%25252FUsers%25252Fhancho%25252FPictures%25252Fphoone%25252FSDK-file-mv.jpg 700 700 "SDK 지정" %}

SDK 경로 수정은 `Command + ,` 사용해서 열수 있습니다.

### Android SDK 매니저 설치

Android SDK 매니저 버튼을 클릭하거나 `Window -> Android SDK Mannager`를 클릭 합니다.

{% img https://lh5.googleusercontent.com/-faBm7F2Gk0U/ULLhaJEOVKI/AAAAAAAAAD8/ei5iS_wI_C8/%25252FUsers%25252Fhancho%25252FPictures%25252FAndroid-sdk-man-01.jpg 100 100 "Android SDK Mannager" %}

### SDK 패키지 선택

모든 버전 보다는 현재 최신 버전과 Android 2.0대 까지만 있어도 충분 합니다.

{% img https://lh3.googleusercontent.com/-BpJep0rpajw/ULLidv8yTeI/AAAAAAAAAEE/fP0unxE902w/%25252FUsers%25252Fhancho%25252FPictures%25252Fphoone%25252FSDK-select.jpg 600 600 "패키지 선택" %}

### SDK 패키지 설치

체크된 패키지를 `Install`합니다.

{% img https://lh3.googleusercontent.com/-Lpn5YCOcQyM/ULLjgqCa5WI/AAAAAAAAAEM/PmE7fb1xD2E/%25252FUsers%25252Fhancho%25252FPictures%25252Fphoone%25252FSDK-install.jpg 500 500 "패키지 설치" %}

### Android ADK Plugin 설치

안드로이드 개발 공식문서 사이트인 [ADK Plugin](http://developer.android.com/sdk/installing/installing-adt.html)에서 다운 받고 설치 가이드를 확인 할수 있습니다.

### ADK 설치

#### Help -> insall new software를 클릭 합니다.

{% img https://lh4.googleusercontent.com/-QR5gGvGIngA/ULLoh0ZOI4I/AAAAAAAAAEc/tL9uY_4jPxE/%25252FUsers%25252Fhancho%25252FPictures%25252Fphoone%25252Fphonegap-eclipse-ADT-01.png 600 600 "install ADK" %}

#### 화면 오른쪽 위에 'add' 클릭

{% img https://lh6.googleusercontent.com/-0NJRgGDaZJM/ULLo4vEJUzI/AAAAAAAAAEk/824uJ-URvMo/%25252FUsers%25252Fhancho%25252FPictures%25252Fphoone%25252Fphonegap-eclipse-ADT-02.png 600 600 "클릭 Add" %}

#### Repository 추가

Location에서 문제가 발생하면 `https` -> `http` 사용하도록 합니다.

    Name: ADT Plugin
    Location: https://dl-ssl.google.com/android/eclipse/
    
{% img https://lh6.googleusercontent.com/-756En0wgbWg/ULLpdkrdeyI/AAAAAAAAAEs/tvSMuwiWP2o/%25252FUsers%25252Fhancho%25252FPictures%25252Fphoone%25252Fphonegap-eclipse-ADT-03.png 700 700 "Add Repository 설정" %}

##### Available Software

Developer Tools과 필요한 프로그램을 클릭 한뒤 `Next`를 클릭합니다.

{% img https://lh3.googleusercontent.com/-gregw6cQ3dg/ULLqQ4ptnsI/AAAAAAAAAE0/5Z_M_28kDto/%25252FUsers%25252Fhancho%25252FPictures%25252Fphoone%25252Fphonegap-eclipse-ADT-04.png 500 500 "Software 선택" %}

##### Install Details

인스톨 되는 정보를 확인후 `Next`를 클릭 합니다.

{% img https://lh4.googleusercontent.com/-52_7il-K0S8/ULLrXNkRVLI/AAAAAAAAAE8/qN-lTWrhHhM/%25252FUsers%25252Fhancho%25252FPictures%25252Fphoone%25252Fphonegap-eclipse-ADT-05.png 700 700 "Show Details" %}

##### Review Lienses

라이센스 확인후 `Finish`를 클릭 합니다.

{% img https://lh6.googleusercontent.com/-Yv_t0AQWpA0/ULLsKWQ2S-I/AAAAAAAAAFE/HwgarHXkDh0/%25252FUsers%25252Fhancho%25252FPictures%25252Fphoone%25252Fphonegap-eclipse-ADT-06.png 700 700 "Finish click" %}

##### Security Warning

경고 화면이 나오게 되면 `Ok`를 클릭 하도록 합니다.

{% img https://lh6.googleusercontent.com/-6yjCMs_WoVE/ULLsmN2bdCI/AAAAAAAAAFM/X7PlH385Prw/%25252FUsers%25252Fhancho%25252FPictures%25252Fphoone%25252Fphonegap-eclipse-ADT-07.png 500 500 "Security Warning" %}

##### Software Update

설치가 끝나면 `Yes`를 클릭하여 새로 eclipse를 시작 하도록 합니다.

{% img https://lh3.googleusercontent.com/-HzGam6KOJLE/ULLtUTbrgDI/AAAAAAAAAFU/bk2nSeaO2ns/%25252FUsers%25252Fhancho%25252FPictures%25252Fphoone%25252Fphonegap-eclipse-ADT-08.png 500 500 "Software Update" %}

### ADV(Android Virtual Device Manager)

 `ADV` 버튼을 클릭하거나 `Window -> Anroid Virtual Devie Manger`를 클릭 합니다.
 
 {% img https://lh6.googleusercontent.com/-nObeGIzAtuc/ULLw2ta5CII/AAAAAAAAAFk/SO4WnHg0130/%25252FUsers%25252Fhancho%25252FPictures%25252FADV.jpg 80 80 "ADV" %}
 
##### ADV New

오른쪽 상단에 'New' 버튼을 클릭 합니다.

{% img https://lh5.googleusercontent.com/-WgSKxxkSptI/ULLzFef9chI/AAAAAAAAAFs/YTf6Lq27rzA/%25252FUsers%25252Fhancho%25252FPictures%25252FADV-New.jpg 500 500 "ADV New" %}

##### ADV Create

ADV 이름과 Device를 선택후 `ok`를 누릅니다.

{% img https://lh3.googleusercontent.com/-aY9paQ9DKgY/ULLzyLaMHyI/AAAAAAAAAF0/Fc5g96lajm4/%25252FUsers%25252Fhancho%25252FPictures%25252FADV-name.jpg 500 500 "ADV Create" %}

### Eclipse 실행

1. Command line tools를 사용 하여 새로운 프로젝트를 만듭니다.
1. 다운 받은 eclipse폴더에서 eclipse를 실행 합니다.
1. eclipse에서 'File->New->Project'를 클릭 합니다.
1. New Project 창에서 'Android Project from Existing Code'선택후 'Next'를 클릭 합니다.
1. 우측 상단의 'Browse..' 클릭후 생성된 Cordova 프로젝트폴더를 엽니다.
1. Root Directory 정의후 'Run'실행 후 ADV를 선택 해주면 Android화면이생성
1. Phonegap Android는 컴파일 시간이 오래 걸리므로 기다려 주어야 합니다.

### Android Cordova 화면

완료된 Android 화면

{% img https://lh5.googleusercontent.com/-ESLlihvURZM/ULL2fVXdK9I/AAAAAAAAAGE/x_qo6Fslssw/%25252FUsers%25252Fhancho%25252FPictures%25252Fphone-Android.jpg 500 500 "안드로이드 Cordova" %}
