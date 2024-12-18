cmake_minimum_required(VERSION 3.2 FATAL_ERROR)
project(CKan)

# Ensure CUDA is not being enabled
# set(CMAKE_CUDA_COMPILER "" CACHE STRING "CUDA compiler" FORCE)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Specify the location of the libtorch directory
set(Torch_DIR "/home/thainq/Desktop/capstone/CPlusConvert/libtorch/share/cmake/Torch")

# Find the PyTorch package
find_package(Torch REQUIRED)

# Include the layers directory to locate headers
include_directories(${CMAKE_SOURCE_DIR}/include)
include_directories(${CMAKE_SOURCE_DIR}/layers)


# Add the executable
add_executable(CKan
        main.cpp
        src/layers/convolution.cpp
        include/layers/convolution.h
        src/layers/KAN_linear.cpp
        include/layers/KAN_linear.h
        src/layers/KAN_convolution.cpp
        include/layers/KAN_convolution.h
        src/architectures/conv_and_KAN.cpp
        include/architectures/conv_and_KAN.h
        src/architectures/KANconv_and_MLP.cpp
        include/architectures/KANconv_and_MLP.h
        src/architectures/KANconv_and_KAN.cpp
        include/architectures/KANconv_and_KAN.h
        src/architectures/convolution_cnn.cpp
        include/architectures/convolution_cnn.h
        test/calc_out_dims/calc_out_dims_test.cpp
        test/calc_out_dims/calc_out_dims_test.h
        test/add_padding/add_padding_test.cpp
        test/add_padding/add_padding_test.h
        test/layers/KAN_convolution_test.cpp
        test/layers/KAN_convolution_test.h
        test/architecture/conv_and_KAN/conv_and_KAN_test.cpp
        test/architecture/conv_and_KAN/conv_and_KAN_test.h
        test/architecture/convolution_cnn/convolution_cnn_test.cpp
        test/architecture/convolution_cnn/convolution_cnn_test.h
        test/architecture/KANconv_and_KAN/KANconv_and_KAN_test.cpp
        test/architecture/KANconv_and_KAN/KANconv_and_KAN_test.h
        test/architecture/KANconv_and_MLP/KANconv_and_MLP_test.cpp
        test/architecture/KANconv_and_MLP/KANconv_and_MLP_test.h
)

# Link the PyTorch library
target_link_libraries(CKan "${TORCH_LIBRARIES}")

# Set the C++ flags (using C++20)
set_property(TARGET CKan PROPERTY CXX_STANDARD 20)