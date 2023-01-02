# qt-window-opencv-install-guide

```opencv 공식 사이트에서 원하는 버전 다운로드 받는다.
https://opencv.org/releases/
2) OpenCV 설치하기


  - 현재 버전은 opencv-4.5.3이므로 이 버전을 설치합니다. 원하는 경로에 압축을 우선 풉니다. 푸는 폴더에 opencv폴더가 만들어집니다. D:\에 압축을 풀고 시작해보았습니다.!


  ![img](https://user-images.githubusercontent.com/46109587/210205703-0e93c550-65a7-4401-b12e-1103410b4c7a.png)


  - MinGW 환경변수를 등록해줍니다. 내 컴퓨터 아이콘에서 오른쪽 마우스를 눌러 고급설정 -> 시스템 환경변수 설정에서 Path에 아래 경로를 추가해줍니다. (본인이 설치한 Qt 경로 기준으로 하시면 됩니다.)


 

  - opencv를 빌드하기 위해서 cmake 사이트로 가서 최신 파일(cmake-3.20.5-windows-x86_64)을 다운로드하여 설치합니다. (모든 사용자가 사용할 수 있게 PATH 경로 추가되도록 선택합니다.)

https://cmake.org/download/


 

  - C:\Program Files\CMake\bin 있는 cmake-gui를 실행합니다.

  Source code 부분에 opencv 경로를 넣고 Binaries에 결과물 라이브러리가 나오는 경로를 선택합니다. 그리고 configure를 누르면 generator for this project 선택하는 것이 나오는데 여기서 사용하는 것이 mingw 이므로 MinGW makefile를 선택합니다. (생성되는데 시간이 조금 걸립니다.)

 



  - 그러면 선택할 수 있는 옵션이 나오는데 여기서 우리가 필요한 것은 WITH_QT와 WITH_OPENGL를 선택해서 다시 Configure를 눌러서 진행을 합니다.

 


 

  - Qt_DIR 경로를 잘못 입력하면 다음으로 넘어가지 않고 계속 에러 발생합니다. 그래서 구글링 해서 어떤 경로를 찾는지 확인해보았습니다.

 


 

  - C:\Qt\Qt5.12.11\5.12.11\mingw73_64\lib\cmake\Qt5  같이 경로를 입력하면 정상적으로 Configure이 된 것을 확인할 수 있습니다. 그리고 Generate를 눌러서 마무리합니다.

 


  

  - configure 한 경로로 release 폴더로 이동을 합니다. 그리고 실제로 소스를 컴파일러 환경에 맞게 컴파일시키기 위해 프로세서를 4개로 만들어 컴파일을 수행합니다. (시간이 조금 걸립니다.)

  mingw32-make  -j  4

 


 

  - 완료된 라이버러리를 설치합니다.

  mingw32-make install


 

- 마지막으로 라이브러리 경로를 윈도우 환경변수에 추가해줍니다. 

  내 컴퓨터 -> 속성-> 고급 시스템 설정 -> 환경변수-> Path에 추가

  D:\opencv\release\install\x64\mingw\bin

 

INCLUDEPATH += C:\Users\Shoes\Documents\common\release\install\include

LIBS += -Lc:\Users\Shoes\Documents\common\release\install\x64\mingw\bin \
        -lopencv_core3416 \
        -lopencv_imgcodecs3416 \
        -lopencv_imgproc3416 \
        -lopencv_highgui3416
        
        
 

2) mainwindow.cpp 소스 수정하기

  - OpenCV 사용할 수 있도록 해더 파일을 추가해줍니다.

#include "opencv2/opencv.hpp"  
```
