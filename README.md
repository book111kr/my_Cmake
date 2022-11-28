# my_Cmake
## CMake 란?
- __CMake__ 는 __빌드 파일을 생성해주는 프로그램__ 입니다. 다시 말해 CMake 를 통해서 프로젝트를 빌드를 하는 것이 아니라, CMake 를 통해서 빌드 파일을 생성하면 빌드 프로그램을 통해서 프로젝트를 빌드 하는 것입니다.

## CMake 개요
- CMake 를 사용하는 모든 프로젝트에는 반드시 __프로젝트 최상위 디렉토리에 CMakeLists.txt 파일이 있어야 합니다.__ 해당 파일에는 CMake 가 빌드 파일을 생성하는데 필요한 정보들이 들어 있습니다. 따라서 보통의 컴파일 과정은 다음과 같이 진행됩니다.
![19 2 1](https://user-images.githubusercontent.com/113752736/204235135-643c782d-a0cf-422f-ad43-7d92a3336815.png)

## CMakeLists.txt
    # CMake 프로그램의 최소 버전
    cmake_minimum_required(VERSION 3.11)

    # 프로젝트 정보
    project(
      ModooCode
      VERSION 0.1
      DESCRIPTION "project" 
      LANGUAGES CXX 
    )
- CMakeList.txt 를 생성하고 두 파일은 같은 경로에 있어야 한다.    
## 실행 파일 만들기
    #include <iostream>
    int main() {
      std::cout << "Hello, CMake" << std::endl;
      return 0;
    }
    
## 빌드 파일 생성
