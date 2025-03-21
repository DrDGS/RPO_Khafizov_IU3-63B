cmake_minimum_required(VERSION 3.22.1)


project("fclient")


add_library(
        fclient
        SHARED
        native-lib.cpp)

add_library(spdlog STATIC IMPORTED)
set_target_properties(spdlog PROPERTIES IMPORTED_LOCATION
        C:/Users/Timur/Desktop/RPO_LR/libs/spdlog/build/${ANDROID_ABI}/libspdlog.a)

add_library(mbedcrypto SHARED IMPORTED)
set_target_properties(mbedcrypto PROPERTIES IMPORTED_LOCATION
        ${CMAKE_CURRENT_SOURCE_DIR}/../nativeLibs/${ANDROID_ABI}/libmbedcrypto.so)

target_include_directories(fclient PUBLIC
        C:/Users/Timur/Desktop/RPO_LR/libs/spdlog/spdlog/include)

target_include_directories(fclient PUBLIC
        C:/Users/Timur/Desktop/RPO_LR/libs/mbedtls/mbedtls/include)

find_library(log-lib log)


target_link_libraries(
        fclient
        spdlog
        mbedcrypto
        ${log-lib})



