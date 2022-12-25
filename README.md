# Setup unit testing

## Add munit submodule

git submodule add https://github.com/nemequ/munit.git external/munit

## Add a CMakeLists.txt file into the external dir.

```
add_library(munit STATIC
    munit/munit.c
)

target_include_directories(munit PUBLIC
    munit
)
```

## Add test

Copy https://github.com/nemequ/munit/blob/master/example.c and paste into test/test.c

# Add a CMAkeLists.txt file into the test subdir.

```
add_executable(test_app
    test.c
)

target_link_libraries(test_app
    munit
)

add_test(test test_app)
```

## Add an IF block into the root CMakeLists.txt to load the external and test directories

```
set(TARGET_GROUP production STRING "Group to build")

project(${PLAYDATE_GAME_NAME} C ASM)

if(TARGET_GROUP STREQUAL test)
    include(CTest)

    add_subdirectory(external)
    add_subdirectory(test)
else()
   # Do what was there before.
endif()
```

## Build test

```
cmake -DTARGET_GROUP=test .
```

## Build the test

```
make
```

# Run the test

```
./test/test_app
```

# Or, alltogether

```
cmake -DTARGET_GROUP=test . && make && ./test/test_app
```

# Build the normal app

```
cmake . && make
```

