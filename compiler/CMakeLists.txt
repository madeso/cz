add_executable(cz_compiler
    src/main.cc
)
# add_library(cz::compiler ALIAS cz_compiler)

target_link_libraries(cz_compiler
    cz::settings
)
