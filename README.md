# qt-window-opencv-install-guide

```
https://1d1cblog.tistory.com/448 참고 링크
설치시 문제가 생긴다면
CMakeLists.txt 파일 내부에
set(CMAKE_CXX_STANDARD 14)
추가하기
   ```
![스크린샷 2025-01-03 154508](https://github.com/user-attachments/assets/6f72651f-45ed-41eb-bef2-528323abce26)
![image](https://github.com/user-attachments/assets/b24f11df-98cc-44f4-b62e-08705b911ccf)

release 폴더에 생성된 exe 파일을 빈 폴더에 옮김.(소스 코드 없이 배포하기 위함.) →  qt mingw 터미널로 이동 → cd [폴더 위치] →  windeployqt [설치파일].exe
![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/28333e20-9d21-4491-a926-a6453cf4c229/ac54c4a2-c75c-4324-bb8e-c78d86ceba20/image.png)

```opencv 공식 사이트에서 원하는 버전 다운로드 받는다.
https://opencv.org/releases/
2) OpenCV 설치하기


  - 현재 버전은 opencv-4.5.3이므로 이 버전을 설치합니다. 원하는 경로에 압축을 우선 풉니다. 푸는 폴더에 opencv폴더가 만들어집니다. D:\에 압축을 풀고 시작해보았습니다.!

```
![img](https://user-images.githubusercontent.com/46109587/210205745-b00500f2-a2cd-4d7d-ab5d-ac5a9bcf7d74.png)


```
  - MinGW 환경변수를 등록해줍니다. 내 컴퓨터 아이콘에서 오른쪽 마우스를 눌러 고급설정 -> 시스템 환경변수 설정에서 Path에 아래 경로를 추가해줍니다. (본인이 설치한 Qt 경로 기준으로 하시면 됩니다.)
```

 ![img (1)](https://user-images.githubusercontent.com/46109587/210205816-16617d9b-18d6-4d59-9748-97361e0467f7.png)

```
  - opencv를 빌드하기 위해서 cmake 사이트로 가서 최신 파일(cmake-3.20.5-windows-x86_64)을 다운로드하여 설치합니다. (모든 사용자가 사용할 수 있게 PATH 경로 추가되도록 선택합니다.)

https://cmake.org/download/

```
 ![img (2)](https://user-images.githubusercontent.com/46109587/210205825-72e2e50e-cbee-4d17-be09-eaac22c2cc98.png)

```
  - C:\Program Files\CMake\bin 있는 cmake-gui를 실행합니다.

  Source code 부분에 opencv 경로를 넣고 Binaries에 결과물 라이브러리가 나오는 경로를 선택합니다. 그리고 configure를 누르면 generator for this project 선택하는 것이 나오는데 여기서 사용하는 것이 mingw 이므로 MinGW makefile를 선택합니다. (생성되는데 시간이 조금 걸립니다.)
```
 
![img (3)](https://user-images.githubusercontent.com/46109587/210205845-f1880186-2f32-4fcd-9b69-b7c05a9c489b.png)
![img (4)](https://user-images.githubusercontent.com/46109587/210205879-eb39b33b-ce4c-4c25-b4f0-913d9e929b7b.png)


```
  - 그러면 선택할 수 있는 옵션이 나오는데 여기서 우리가 필요한 것은 WITH_QT와 WITH_OPENGL를 선택해서 다시 Configure를 눌러서 진행을 합니다.
```

![img (5)](https://user-images.githubusercontent.com/46109587/210205968-6a9d86b8-6544-4e57-a0eb-5aa075b02c41.png)

 
```
  - Qt_DIR 경로를 잘못 입력하면 다음으로 넘어가지 않고 계속 에러 발생합니다. 그래서 구글링 해서 어떤 경로를 찾는지 확인해보았습니다.
```
 ![img (6)](https://user-images.githubusercontent.com/46109587/210205982-cb664e2d-ac00-47b2-9cbf-81752a5e8f3b.png)



 
```
  - C:\Qt\Qt5.12.11\5.12.11\mingw73_64\lib\cmake\Qt5  같이 경로를 입력하면 정상적으로 Configure이 된 것을 확인할 수 있습니다. 그리고 Generate를 눌러서 마무리합니다.
```
 ![img (7)](https://user-images.githubusercontent.com/46109587/210205992-a9cbfd8e-e5fa-4cc6-a5e1-87d4b1a5a7e7.png)



  
```
  - configure 한 경로로 release 폴더로 이동을 합니다. 그리고 실제로 소스를 컴파일러 환경에 맞게 컴파일시키기 위해 프로세서를 4개로 만들어 컴파일을 수행합니다. (시간이 조금 걸립니다.)

  mingw32-make  -j  4
```
 
![img (8)](https://user-images.githubusercontent.com/46109587/210206007-e2661201-acc6-4426-b1d8-fcbb85078a51.png)


 
```
  - 완료된 라이러리를 설치합니다.

  mingw32-make install

```
 ![img (9)](https://user-images.githubusercontent.com/46109587/210206021-f914bbd8-5d0a-4e13-b767-6712ac9bec7d.png)

```
- 마지막으로 라이브러리 경로를 윈도우 환경변수에 추가해줍니다. 

  내 컴퓨터 -> 속성-> 고급 시스템 설정 -> 환경변수-> Path에 추가

  D:\opencv\release\install\x64\mingw\bin
```
``` 
1) OpenCV 경로 설정해주기

  - ImageEditor.pro에 OpenCV 헤더 파일 경로와 사용할 라이브러리를 지정해줍니다. 컴파일한 경로나 라이브러리를 경로 등을 잘못 설정하면 에러가 발생하면서 컴파일이 안되므로 주의해서 경로를 입력해주어야 합니다.
INCLUDEPATH += C:\Users\Shoes\Documents\common\release\install\include

LIBS += -Lc:\Users\Shoes\Documents\common\release\install\x64\mingw\bin \
        -lopencv_core3416 \
        -lopencv_imgcodecs3416 \
        -lopencv_imgproc3416 \
        -lopencv_highgui3416        
```  
![img (10)](https://user-images.githubusercontent.com/46109587/210206092-92b94712-da36-49a3-abe6-25842c697f89.png)
 
```
2) mainwindow.cpp 소스 수정하기

  - OpenCV 사용할 수 있도록 해더 파일을 추가해줍니다.

#include "opencv2/opencv.hpp"  
```

Windows 10, C++, Qt 5, OpenCV 4.5.4 기준으로 설명하겠습니다.

 

먼저 http://qt.mirror.constant.com/archive/qt/5.9/5.9.3/에서 Qt Creator를 다운받습니다.

 
Index of /archive/qt/5.9/5.9.3/

 

qt.mirror.constant.com
다음으로 https://github.com/opencv/opencv/releases에서 opencv-4.5.4-vc14_vc15.exe를 다운받습니다.

 
Releases · opencv/opencv

Open Source Computer Vision Library. Contribute to opencv/opencv development by creating an account on GitHub.

github.com


CMake 설치 전 환경 변수를 설정합니다. 윈도우에서 시스템 환경 변수 편집을 검색하여 실행합니다. 아래 화면에서 환경 변수 클릭합니다.


Path를 더블 클릭하여 아래 화면을 띄운 후 C:\Qt\Qt5.9.3\Tools\mingw530_32\bin\ (mingw530_32\bin 경로)를 추가합니다.



다음으로 https://github.com/Kitware/CMake/releases/download/v3.22.0/cmake-3.22.0-windows-i386.msi에서 CMake를 설치합니다.


설치 후 CMake를 실행 후 source code에 설치한 opencv 폴더 안의 sources 폴더를 build the binaries에는 빌드된 결과물을 저장할 폴더를 지정 후 Configure를 클릭합니다.


다음 화면에서 아래와 같이 체크 후 Next를 클릭합니다. 

 

다음으로 Compilers에서 C에는 Qt/Qt5.9.3/Tools/mingw530_32/bin/gcc.exe C++에는 Qt/Qt5.9.3/Tools/mingw530_32/bin/g++.exe을 선택합니다.


마지막으로 Configurate를 클릭합니다.


한번의 과정이 끝나고 아래처럼 항목들이 생겼다면 BUILD_QT, BUILD_OPENGL을 체크, CMAKE_BUILD_TYPE에 Debug 후 다시 Configure를 해줍니다.



Configure이 끝났다면 마지막으로 Generate를 해줍니다.


build the binaries에 설정한 경로에 Makefile이 생긴지 확인합니다.


이제 Qt for Desktop (MinGW 5.3.0 32bit)를 실행 후 Makefile이 생성된 경로로 이동 mingw32-make를 실행합니다.


마지막으로 mingw32–make install를 실행합니다.


이제 설정한 경로 안 bin 폴더에 dll 파일이 생긴 것을 확인할 수 있습니다.


다음으로 환경 변수에 해당 라이브러리 파일들이 있는 경로도 추가해줍니다.


위 과정을 마치셨다면 Qt Creator를 실행 후 New Project > Qt Widgets Application 후 프로젝트를 생성합니다.




pro 파일을 아래와 같이 설정합니다.

#-------------------------------------------------
#
# Project created by QtCreator 2021-11-29T22:35:26
#
#-------------------------------------------------

QT       += core gui

greaterThan(QT_MAJOR_VERSION, 4): QT += widgets

TARGET = Start
TEMPLATE = app

# The following define makes your compiler emit warnings if you use
# any feature of Qt which has been marked as deprecated (the exact warnings
# depend on your compiler). Please consult the documentation of the
# deprecated API in order to know how to port your code away from it.
DEFINES += QT_DEPRECATED_WARNINGS

# You can also make your code fail to compile if you use deprecated APIs.
# In order to do so, uncomment the following line.
# You can also select to disable deprecated APIs only up to a certain version of Qt.
#DEFINES += QT_DISABLE_DEPRECATED_BEFORE=0x060000    # disables all the APIs deprecated before Qt 6.0.0


SOURCES += \
        main.cpp \
        imageload.cpp

HEADERS += \
        imageload.h

FORMS += \
        imageload.ui

INCLUDEPATH += C:\OpenCV4.5.4\opencv\Qt_Lib\install\include

LIBS += \
    C:\OpenCV4.5.4\opencv\Qt_Lib\bin\libopencv_core454d.dll \
    C:\OpenCV4.5.4\opencv\Qt_Lib\bin\libopencv_highgui454d.dll \
    C:\OpenCV4.5.4\opencv\Qt_Lib\bin\libopencv_imgproc454d.dll \
    C:\OpenCV4.5.4\opencv\Qt_Lib\bin\libopencv_imgcodecs454d.dll \
main.cpp는 건들지 않고 ui cpp 파일을 아래와 같이 수정합니다.

#include "imageload.h"
#include "ui_imageload.h"
#include <opencv2/opencv.hpp>
#include <QDir>
#include <QDebug>

ImageLoad::ImageLoad(QWidget *parent) :
    QMainWindow(parent),
    ui(new Ui::ImageLoad)
{
    ui->setupUi(this);

    connect(ui->btnShowImage, SIGNAL(clicked()), this, SLOT(Slot_pushShowImageButton()));
}

ImageLoad::~ImageLoad()
{
    delete ui;
}

void ImageLoad::ShowDebugMessage(QString sMsg)
{
    qDebug() << sMsg;
    ui->statusBar->showMessage(sMsg,3000);
}

void ImageLoad::Slot_pushShowImageButton()
{
    QString sImagePath = QApplication::applicationDirPath() + "/iu.jpg";
    qDebug() << sImagePath;

    QFile file(sImagePath);
    if ( !file.exists() ) {
        ShowDebugMessage("파일을 찾을 수 없습니다.");
    }

    cv::Mat image = cv::imread(sImagePath.toStdString(), cv::IMREAD_COLOR);

    if ( image.empty() ) {
        ShowDebugMessage("이미지 파일을 읽을 수 없습니다.");
    }

    cv::imshow("Image Test", image);
    cv::waitKey(0);
    cv::destroyAllWindows();
}
버튼을 누르면 아래와 설정한 이미지를 띄우게 됩니다.


