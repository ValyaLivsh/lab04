# Homework IV

```
$ mkdir lab04 && cd lab04
$ git clone https://github.com/ValyaLivsh/lab03.git
$ git remote remove origin
$ git remote add origin https://github.com/ValyaLivsh/lab04.git
```
Cоздание CMakeLists.txt
```
cmake_minimum_required(VERSION 3.10)
project(formatter)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(formatter STATIC formatter_lib/formatter.cpp)
include_directories(formatter_lib)

add_library(formatter_ex STATIC formatter_ex_lib/formatter_ex.cpp)
include_directories(formatter_ex_lib)

add_executable(hello_world hello_world_application/hello_world.cpp)
target_link_libraries(hello_world formatter formatter_ex)

add_library(solver_lib STATIC solver_lib/solver.cpp)
include_directories(solver_lib)

add_executable(solver solver_application/equation.cpp)
target_link_libraries(solver formatter formatter_ex solver_lib)
```
Создание файла build.yml
```
$ mkdir .github
$ mkdir .github/workflows
$ nano .github/workflows/build.yml
```
```
name: Build-with-CMake-on-Linux
on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: Configure CMake
        run: cmake -B_build
      - name: Build project
        run: cmake --build _build --config Release
```
```
$ git branch -M main
$ git add .
$ git commit -m "upd"
$ git push -u origin main
```
