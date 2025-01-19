cmake_minimum_required(VERSION 3.28)

project(max
    VERSION 0.1.0
    DESCRIPTION "Proyecto sencillo de C++ con un solo target"
    LANGUAGES CXX
)

add_executable(${PROJECT_NAME} main.cpp)

# Para C++23
set_target_properties(${PROJECT_NAME} PROPERTIES
    CXX_STANDARD 23
    CXX_STANDARD_REQUIRED ON
    CXX_EXTENSIONS OFF
    RUNTIME_OUTPUT_DIRECTORY_DEBUG   ${CMAKE_BINARY_DIR}/debug
    RUNTIME_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR}/release
)

# Librerías a enlazar (si las necesitas en MinGW/UCRT)
target_link_libraries(${PROJECT_NAME} PRIVATE -lstdc++ -lpthread)

# Opciones de compilación según compilador (avisos y warnings)
if (CMAKE_CXX_COMPILER_ID MATCHES "MSVC")
    target_compile_options(${PROJECT_NAME} PRIVATE /W3 /WX)
elseif (CMAKE_CXX_COMPILER_ID MATCHES "Clang|GNU")
    target_compile_options(${PROJECT_NAME} PRIVATE -Wall -Wextra -pedantic -Werror)
endif()

# Mensajes informativos
message("-- CMake Generator: ${CMAKE_GENERATOR}")
get_target_property(CFEATURES ${PROJECT_NAME} COMPILE_FEATURES)
message("-- Project compile features: ${CFEATURES}")
get_target_property(COPTIONS ${PROJECT_NAME} COMPILE_OPTIONS)
message("-- Target compile options: ${COPTIONS}")
