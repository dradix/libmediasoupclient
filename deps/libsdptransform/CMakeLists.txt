cmake_minimum_required(VERSION 3.0)

project(sdptransform VERSION 1.2.9)

# For CMake >= 3.1.
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)


# For CMake < 3.1.
SET(CMAKE_LD_FLAGS  "${CMAKE_LD_FLAGS} -stdlib=libc++ 

-L${UE5_ROOT}/Engine/Source/ThirdParty/Unix/LibCxx/lib \
-static   -lc++abi -pthread -fuse-ld=lld  -nodefaultlibs\
 ")

 SET(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS}  -nostdinc++ \
-I${UE5_ROOT}/Engine/Source/ThirdParty/Unix/LibCxx/include/c++/v1 \
-static -pthread  \
 ")
subdirs(test readme-helper)

include_directories(${sdptransform_SOURCE_DIR}/include)

set(
	SOURCE_FILES
	src/grammar.cpp
	src/parser.cpp
	src/writer.cpp
)

set(
	HEADER_FILES
	include/sdptransform.hpp
	include/json.hpp
)

add_library(sdptransform STATIC ${SOURCE_FILES} ${HEADER_FILES})

install(TARGETS sdptransform DESTINATION lib)
install(FILES ${HEADER_FILES} DESTINATION include/sdptransform)
