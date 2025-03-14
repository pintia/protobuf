docker run -it --rm -v`pwd`:/protobuf ubuntu:20.04
cmake -DBUILD_SHARED_LIBS=OFF -DABSL_PROPAGATE_CXX_STD=ON -S . -B ./build
cmake -DBUILD_SHARED_LIBS=OFF CMAKE_EXE_LINKER_FLAGS=-static -S . -B ./build
cmake -DBUILD_SHARED_LIBS=OFF -DCMAKE_EXE_LINKER_FLAGS="-static" -DZLIB_LIBRARY=/usr/lib/x86_64-linux-gnu/libz.a -DABSL_PROPAGATE_CXX_STD=ON -S . -B ./build
cmake --build ./build --parallel 10

docker run -it --rm -v`pwd`:/protobuf alpine:3.18
apk add gcc g++ make cmake zlib-dev zlib-static pkgconfig linux-headers
cmake -DBUILD_SHARED_LIBS=OFF -DCMAKE_EXE_LINKER_FLAGS="-static" -DZLIB_LIBRARY=/lib/libz.a -DABSL_PROPAGATE_CXX_STD=ON -S . -B ./build
cmake --build ./build --parallel 10
