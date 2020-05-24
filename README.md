# Caffe

My distribution of Caffe on a CPU-ONLY mode Ubuntu machine.

This serves as an introduction to how to compile caffe.

Steps are as follows:

## 1. Install.

You could simply `sudo apt install caffe-cpu`.

Or you should install all the dependencies, and then download the source code in this file, and compile it your self.

## 2. Compile

Modify Makefile.config as I did, then:

'make all'

'make test'

'make runtest'

## 3. Modifications

1. data: 获取数据集
2. examples: 示例
3. include: 头文件
4. src: 源代码
5. scripts: 一些脚本，应该没得啥用
6. tools: 一些源代码



1. 安装依赖

   1. Ubuntu：如果有source.list，一键安装。否则，逐个安装

   2. ```
      sudo apt build-dep caffe-cpu        # dependencies for CPU-only version
      ```

      It requires a `deb-src` line in your `sources.list`.

   3. 逐个安装：

      ```
      sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler
      sudo apt-get install --no-install-recommends libboost-all-dev
      ```

      **BLAS**: install ATLAS by `sudo apt-get install libatlas-base-dev` or install OpenBLAS by `sudo apt-get install libopenblas-dev` or MKL for better CPU performance.

   4. hdf5 需要更改 include dir。否则找不到。

      ```
      INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include
      -LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib
      +LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/hdf5/serial
      ```
      ```
      diff --git a/Makefile.config.example b/Makefile.config.example
      index a873502..88828cc 100644
      --- a/Makefile.config.example
      +++ b/Makefile.config.example
      @@ -69,8 +69,8 @@ PYTHON_LIB := /usr/lib
       # WITH_PYTHON_LAYER := 1

       # Whatever else you find you need goes here.
      -INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include
      -LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib
      +INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial/
      +LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/hdf5/serial/

       # If Homebrew is installed at a non standard location (for example your home directory) and you use it for general dependencies
       # INCLUDE_DIRS += $(shell brew --prefix)/include
      ```
      

2. 编译。

   ```
   cp Makefile.config.example Makefile.config
   # Adjust Makefile.config (for example, if using Anaconda Python, or if cuDNN is desired)
   make all
   make test
   make runtest
   ```

3. 上述两步，在ubuntu当中，可以用 sudo apt install caffe-cpu 代替。不过在后续的示例处理中可能会遇到少许问题。