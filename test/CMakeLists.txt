add_executable(test_app
    test.c
)

target_link_libraries(test_app
    munit
)

add_test(test test_app)
