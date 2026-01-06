cmake_minimum_required(VERSION 3.15)
project(src_unittest)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# FetchContent로 GoogleTest 자동 다운로드
include(FetchContent)
FetchContent_Declare(
    googletest
    GIT_REPOSITORY https://github.com/google/googletest.git
    GIT_TAG        v1.14.0
)
# Windows에서 gtest_force_shared_crt 설정
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

# 테스트 파일
set(TEST_FILES
    test_QuekkaMdb.cpp
    test_QuekkaConfig.cpp
    test_QuekkaProducer.cpp
    test_Epoll.cpp
)

add_executable(src_unittest test_main.cpp ${TEST_FILES})

target_include_directories(src_unittest PUBLIC
    ${CMAKE_SOURCE_DIR}/include
    ${CMAKE_SOURCE_DIR}/src
)

target_link_libraries(src_unittest
    gtest
    gtest_main
    pthread
    quekka_config
    quekka_common
    quekka_error
    quekka_pub
    quekka_internal
)
