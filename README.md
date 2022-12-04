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
    ```c
    #include <iostream>
    int main() {
      std::cout << "Hello, CMake" << std::endl;
      return 0;
    }
    ```
    
위 내용을 main.cc 에 저장한다.
## 빌드 파일 생성
    $ tree
    .
    ├── build
    ├── CMakeLists.txt
    └── main.cc
    
- CMake 에서 권장하는 방법은 빌드 파일은 작업하는 디렉토리와 다른 디렉토리에서 만드는 것입니다. 따라서 build 라는 폴더를 하나 만든다.


## build 안으로 들어가서 cmake .. 을 실행
    $ cmake ..
    -- The CXX compiler identification is GNU 9.3.0
    -- Detecting CXX compiler ABI info
    -- Detecting CXX compiler ABI info - done
    -- Check for working CXX compiler: /usr/bin/c++ - skipped
    -- Detecting CXX compile features
    -- Detecting CXX compile features - done
    -- Configuring done
    -- Generating done
    -- Build files have been written to: /build
 
- CMake 에서 여러가지 설정들을 체크한 뒤에 빌드 파일을 생성한 것을 볼 수 있습니다.

- CMake 를 실행 할 때에는 최상위 CMakeLists.txt 가 위치한 폴더의 경로를 입력해야 하는데, 바로 부모 디렉토리에 있으므로 .. 을 쓰는 것입니다. build 안에 여러가지 폴더와 파일들이 생성된 것을 볼 수 있다.

        $ tree
        .
        ├── build
        │   ├── CMakeCache.txt
        │   ├── CMakeFiles
        │   │   ├── 3.19.1
        │   │   │   ├── CMakeCXXCompiler.cmake
        │   │   │   ├── CMakeDetermineCompilerABI_CXX.bin
        │   │   │   ├── CMakeSystem.cmake
        │   │   │   └── CompilerIdCXX
        │   │   │       ├── a.out
        │   │   │       ├── CMakeCXXCompilerId.cpp
        │   │   │       └── tmp
        │   │   ├── cmake.check_cache
        │   │   ├── CMakeDirectoryInformation.cmake
        │   │   ├── CMakeOutput.log
        │   │   ├── CMakeTmp
        │   │   ├── Makefile2
        │   │   ├── Makefile.cmake
        │   │   ├── program.dir
        │   │   │   ├── build.make
        │   │   │   ├── cmake_clean.cmake
        │   │   │   ├── DependInfo.cmake
        │   │   │   ├── depend.make
        │   │   │   ├── flags.make
        │   │   │   ├── link.txt
        │   │   │   └── progress.make
        │   │   ├── progress.marks
        │   │   └── TargetDirectories.txt
        │   ├── cmake_install.cmake
        │   └── Makefile
        ├── CMakeLists.txt
        └── main.cc
    
- 여러가지 파일들이 생성된 것을 볼 수 있습니다. 특히 Makefile 도 만들어졌다.

## !주의 사항
> CMake는 실행시 많은 파일들을 생성하기때문에 디렉토리 정리가 안될 수 있다. 이미 있는 파일을 덮어 씌우기가 된다면 더욱 정리하기 어렵다. 그래서 __빌드 파일 용 디렉토리를 만든 다음에 해당 디렉토리에서 CMake를 실행해야한다.

## build 디렉토리로 들어가서 make 를 실행한다.
    $ make
    Scanning dependencies of target program
    [ 50%] Building CXX object CMakeFiles/program.dir/main.cc.o
    [100%] Linking CXX executable program
    [100%] Built target program

    $ ls
    CMakeCache.txt  CMakeFiles  cmake_install.cmake  Makefile  program
 
- program 이라는 이름의 실행 파일이 생성된 것을 볼 수 있다.

## 해당 파일을 실행한다.
> ### 실행결과
    Hello, CMake

## 생성할 실행 파일을 추가하는 명령 add_executable
> CMake 에서 실행 파일을 생성하기 위해서는 위와 같이 add_executable 을 사용하면 된다.
    
    add_executable(<실행 파일 이름> <소스1> <소스2> ... <소스들>)
- 맨 처음에 생성하고자 하는 실행 파일 이름을 적은 뒤에, 그 뒤로 해당 실행 파일을 만드는데 필요한 소스들을 쭈르륵 나열한다.

- foo.h
```c
int foo();
```
- foo.cc
```c
#include "foo.h"

int foo() { return 3; }
```

- main.cc
```c
#include <iostream>
    
#include "foo.h"
    
int main() {
    std::cout << "Foo : " << foo() << std::endl;
    return 0;
}
```

- 컴파일에 필요한 것이 소스 파일들인 main.cc 와 foo.cc 이므로, add_executable 을 다음과 같이 수정해주면 된다.
```c
add_executable (program main.cc foo.cc)
```
##  build 디렉토리에 들어가서 make 를 실행한다.
    $ make
    Scanning dependencies of target program
    [ 50%] Linking CXX executable program
    /usr/bin/ld: CMakeFiles/program.dir/main.cc.o: in function `main':
    main.cc:(.text+0x24): undefined reference to `foo()'
    collect2: error: ld returned 1 exit status
    make[2]: *** [CMakeFiles/program.dir/build.make:103: program] Error 1
    make[1]: *** [CMakeFiles/Makefile2:95: CMakeFiles/program.dir/all] Error 2
    make: *** [Makefile:103: all] Error 2

## !주의 사항
> 실행시 위와 같은 오류가 발생한다. CMakeLists.txt는 변경했으나 Makefile를 바꾼것이 아니기 때문에 cmake .. 을 통해서 Makefile을 다시 생성해야한다.

##  CMake 를 다시 실행해서 만든 새로운 Makefile 에서 컴파일
> 실행결과
```c
Foo : 3
```
