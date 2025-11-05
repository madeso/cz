cmake_minimum_required(VERSION 3.31.1)
project(cz LANGUAGES CXX)

add_library(cz_settings INTERFACE)
add_library(cz::settings ALIAS cz_settings)
target_compile_options(cz_settings INTERFACE
    $<$<CXX_COMPILER_ID:MSVC>:/W4 /permissive->
    $<$<NOT:$<CXX_COMPILER_ID:MSVC>>:-Wall -Wextra -pedantic>
)
set_target_properties(cz_settings PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED ON
    CXX_EXTENSIONS OFF
)
add_subdirectory(compiler)

