add_library(munit STATIC
    munit/munit.c
)

target_include_directories(munit PUBLIC
    munit
)
