cmake_minimum_required(VERSION 2.6.4)
project (mbedtls-examples)

# Global Build Settings
set(ENABLE_TESTING OFF CACHE INTERNAL "")
include_directories(source cryptoauthlib/lib cryptoauthlib/third_party/mbedtls/include scripts)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -g3 -DMBEDTLS_CONFIG_FILE=\\\"mbedtls_config.h\\\" -fPIC")

# Configure cryptoauthlib
set(ATCA_STATIC_LIB ON CACHE INTERNAL "")
set(ATCA_MBEDTLS ON CACHE INTERNAL "")
set(ATCA_PKCS11 OFF CACHE INTERNAL "")
set(ATCA_HAL_KIT_HID ON CACHE INTERNAL "")

# Add cryptoauthlib
add_subdirectory(cryptoauthlib/lib)


# Add the example programs
add_executable(connect source/connect.c source/cert_chain.c)
target_link_libraries(connect cryptoauth mbedtls)

add_executable(configure source/configure.c)
target_link_libraries(configure cryptoauth mbedtls)

add_executable(provision source/provision.c source/cert_chain.c)
target_link_libraries(provision cryptoauth mbedtls)

add_executable(tests source/tests.c source/cert_chain.c)
target_link_libraries(tests cryptoauth mbedtls)
