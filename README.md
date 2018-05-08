---
### 日志
1. 针对mtcnn的col-major模型添加了caffe2ncnn_mtcnn.cpp, 生成row-major模型
2. 添加void resize_image(ncnn::Mat& srcImage, ncnn::Mat& dstImage)，无arm优化
3. 前面都是用BGR图像做的，导致很多漏检，改过来了。
4. 3519编译：在CMakelist.txt的17行下面手动添加如下代码
```
set(CMAKE_C_COMPILER   arm-hisiv500-linux-gcc) 
set(CMAKE_CXX_COMPILER arm-hisiv500-linux-g++)
add_definitions(-D__ARM_NEON)
add_definitions("-O3 -mfloat-abi=softfp -mfpu=neon-vfpv4 -ffunction-sections") 
```
5. 在非手机的arm环境下，需要修改CMakeLists.txt才能把arm编译进去，如CMakeLists_arm.txt
6. 如果使用opencv2，需要将examples/CmakeLists.txt里的imgcodecs去掉，否则可能编译不过去
7. 在tx1下make时可能会出现"can't find -lopencv_dep_cudart"，重新cmake，"cmake -D CUDA_USE_STATIC_CUDA_RUNTIME=OFF .."
---
![image](https://github.com/ElegantGod/ncnn/blob/master/mtcnn/result.jpg)
# ncnn

[![License](https://img.shields.io/badge/license-BSD--3--Clause-blue.svg)](https://raw.githubusercontent.com/Tencent/ncnn/master/LICENSE.txt) 
[![Build Status](https://travis-ci.org/Tencent/ncnn.svg?branch=master)](https://travis-ci.org/Tencent/ncnn)


ncnn is a high-performance neural network inference computing framework optimized for mobile platforms. ncnn is deeply considerate about deployment and uses on mobile phones from the beginning of design. ncnn does not have third party dependencies, it is cross-platform, and runs faster than all known open source frameworks on mobile phone cpu. Developers can easily deploy deep learning algorithm models to the mobile platform by using efficient ncnn implementation, create intelligent APPs, and bring the artificial intelligence to your fingertips. ncnn is currently being used in many Tencent applications, such as QQ, Qzone, WeChat, Pitu and so on.

ncnn 是一个为手机端极致优化的高性能神经网络前向计算框架。ncnn 从设计之初深刻考虑手机端的部署和使用。无第三方依赖，跨平台，手机端 cpu 的速度快于目前所有已知的开源框架。基于 ncnn，开发者能够将深度学习算法轻松移植到手机端高效执行，开发出人工智能 APP，将 AI 带到你的指尖。ncnn 目前已在腾讯多款应用中使用，如 QQ，Qzone，微信，天天P图等。

---

### HowTo

[how to build ncnn library](https://github.com/Tencent/ncnn/wiki/how-to-build)

[how to use ncnn with alexnet](https://github.com/Tencent/ncnn/wiki/how-to-use-ncnn-with-alexnet)

[ncnn 组件使用指北 alexnet](https://github.com/Tencent/ncnn/wiki/ncnn-%E7%BB%84%E4%BB%B6%E4%BD%BF%E7%94%A8%E6%8C%87%E5%8C%97-alexnet)

[ncnn low-level operation api](https://github.com/Tencent/ncnn/wiki/low-level-operation-api)

[ncnn param and model file spec](https://github.com/Tencent/ncnn/wiki/param-and-model-file-structure)

[ncnn operation param weight table](https://github.com/Tencent/ncnn/wiki/operation-param-weight-table)

[how to implement custom layer step by step](https://github.com/Tencent/ncnn/wiki/how-to-implement-custom-layer-step-by-step)

---

### FAQ

[ncnn produce wrong result](https://github.com/Tencent/ncnn/wiki/FAQ-ncnn-produce-wrong-result)

---

### Features

* Supports convolution neural networks, supports multiple input and multi-branch structure, can calculate part of the branch
* No third-party library dependencies, does not rely on BLAS / NNPACK or any other computing framework
* Pure C ++ implementation, cross-platform, supports android, ios and so on
* ARM NEON assembly level of careful optimization, calculation speed is extremely high
* Sophisticated memory management and data structure design, very low memory footprint
* Supports multi-core parallel computing acceleration, ARM big.LITTLE cpu scheduling optimization
* The overall library size is less than 500K, and can be easily reduced to less than 300K
* Extensible model design, supports 8bit quantization and half-precision floating point storage, can import caffe/pytorch/mxnet/onnx models
* Support direct memory zero copy reference load network model
* Can be registered with custom layer implementation and extended
* Well, it is strong, not afraid of being stuffed with 卷   QvQ

### 功能概述

* 支持卷积神经网络，支持多输入和多分支结构，可计算部分分支
* 无任何第三方库依赖，不依赖 BLAS/NNPACK 等计算框架
* 纯 C++ 实现，跨平台，支持 android ios 等
* ARM NEON 汇编级良心优化，计算速度极快
* 精细的内存管理和数据结构设计，内存占用极低
* 支持多核并行计算加速，ARM big.LITTLE cpu 调度优化
* 整体库体积小于 500K，并可轻松精简到小于 300K
* 可扩展的模型设计，支持 8bit 量化和半精度浮点存储，可导入 caffe/pytorch/mxnet/onnx 模型
* 支持直接内存零拷贝引用加载网络模型
* 可注册自定义层实现并扩展
* 恩，很强就是了，不怕被塞卷 QvQ

---

### Example project

https://github.com/Tencent/ncnn/tree/master/examples/squeezencnn

### 技术交流QQ群：637093648  答案：卷卷卷卷卷

---

### License

BSD 3 Clause

