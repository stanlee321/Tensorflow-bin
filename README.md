# Tensorflow-bin
Prebuilt binary with Tensorflow Lite enabled.  
And, The following problem was solved.  
1. `undefined symbol: _ZN6tflite12tensor_utils39NeonMatrixBatchVectorMultiplyAccumulateEPKaiiS2_PKfiPfi`  
2. `Bus Error`

RaspberryPi3 ... armv7l  
  
Bazel's pre-build binay is below.  
**https://github.com/PINTO0309/Bazel_bin.git**  

## Usage
**Example of Python 2.x series**
```
$ sudo apt-get install python-pip python3-pip
$ sudo pip2 uninstall tensorflow
$ git clone https://github.com/PINTO0309/Tensorflow-bin.git
$ cd Tensorflow-bin
$ sudo pip2 install tensorflow-1.11.0-cp27-cp27mu-linux_armv7l.whl

【Required】 Restart the terminal.
```

**Example of Python 3.x series**
```
$ sudo apt-get install python-pip python3-pip
$ sudo pip3 uninstall tensorflow
$ git clone https://github.com/PINTO0309/Tensorflow-bin.git
$ cd Tensorflow-bin
$ sudo pip3 install tensorflow-1.11.0-cp35-cp35m-linux_armv7l.whl

【Required】 Restart the terminal.
```

## Operation check
**Example of Python 2.x series**
```
$ python
>>> import tensorflow
>>> tensorflow.__version__
1.11.0
>>> exit()
```

**Example of Python 3.x series**
```
$ python3
>>> import tensorflow
>>> tensorflow.__version__
1.11.0
>>> exit()
```

## Build Parameter
**Python2.x**
```
$ cd tensorflow
$ ./configure

Please specify the location of python. [Default is /usr/bin/python]: 


Found possible Python library paths:
  /usr/local/lib/python2.7/dist-packages
  /usr/local/lib
  /home/pi/tensorflow/tensorflow/contrib/lite/tools/make/gen/rpi_armv7l/lib
  /usr/lib/python2.7/dist-packages
  /opt/movidius/caffe/python
Please input the desired Python library path to use.  Default is [/usr/local/lib/python2.7/dist-packages]

Do you wish to build TensorFlow with jemalloc as malloc support? [Y/n]: n
No jemalloc as malloc support will be enabled for TensorFlow.

Do you wish to build TensorFlow with Google Cloud Platform support? [Y/n]: n
No Google Cloud Platform support will be enabled for TensorFlow.

Do you wish to build TensorFlow with Hadoop File System support? [Y/n]: n
No Hadoop File System support will be enabled for TensorFlow.

Do you wish to build TensorFlow with Amazon AWS Platform support? [Y/n]: n
No Amazon AWS Platform support will be enabled for TensorFlow.

Do you wish to build TensorFlow with Apache Kafka Platform support? [Y/n]: n
No Apache Kafka Platform support will be enabled for TensorFlow.

Do you wish to build TensorFlow with XLA JIT support? [y/N]: n
No XLA JIT support will be enabled for TensorFlow.

Do you wish to build TensorFlow with GDR support? [y/N]: n
No GDR support will be enabled for TensorFlow.

Do you wish to build TensorFlow with VERBS support? [y/N]: n
No VERBS support will be enabled for TensorFlow.

Do you wish to build TensorFlow with nGraph support? [y/N]: n
No nGraph support will be enabled for TensorFlow.

Do you wish to build TensorFlow with OpenCL SYCL support? [y/N]: n
No OpenCL SYCL support will be enabled for TensorFlow.

Do you wish to build TensorFlow with CUDA support? [y/N]: n
No CUDA support will be enabled for TensorFlow.

Do you wish to download a fresh release of clang? (Experimental) [y/N]: n
Clang will not be downloaded.

Do you wish to build TensorFlow with MPI support? [y/N]: n
No MPI support will be enabled for TensorFlow.

Please specify optimization flags to use during compilation when bazel option "--config=opt" is specified [Default is -march=native]: 


Would you like to interactively configure ./WORKSPACE for Android builds? [y/N]: n
```
```
$ sudo bazel build --config opt --local_resources 1024.0,0.5,0.5 \
--copt=-mfpu=neon-vfpv4 \
--copt=-ftree-vectorize \
--copt=-funsafe-math-optimizations \
--copt=-ftree-loop-vectorize \
--copt=-fomit-frame-pointer \
--copt=-DRASPBERRY_PI \
--host_copt=-DRASPBERRY_PI \
//tensorflow/tools/pip_package:build_pip_package
```

**Python3.x**
```
$ sudo pip3 install keras_applications==1.0.4 --no-deps
$ sudo pip3 install keras_preprocessing==1.0.2 --no-deps
$ sudo pip3 install h5py==2.8.0

$ cd tensorflow
$ ./configure

Please specify the location of python. [Default is /usr/bin/python]: /usr/bin/python3


Found possible Python library paths:
  /usr/local/lib
  /usr/lib/python3/dist-packages
  /usr/local/lib/python3.5/dist-packages
  /opt/movidius/caffe/python
Please input the desired Python library path to use.  Default is [/usr/local/lib] /usr/local/lib/python3.5/dist-packages

Do you wish to build TensorFlow with jemalloc as malloc support? [Y/n]: n
No jemalloc as malloc support will be enabled for TensorFlow.

Do you wish to build TensorFlow with Google Cloud Platform support? [Y/n]: n
No Google Cloud Platform support will be enabled for TensorFlow.

Do you wish to build TensorFlow with Hadoop File System support? [Y/n]: n
No Hadoop File System support will be enabled for TensorFlow.

Do you wish to build TensorFlow with Amazon AWS Platform support? [Y/n]: n
No Amazon AWS Platform support will be enabled for TensorFlow.

Do you wish to build TensorFlow with Apache Kafka Platform support? [Y/n]: n
No Apache Kafka Platform support will be enabled for TensorFlow.

Do you wish to build TensorFlow with XLA JIT support? [y/N]: n
No XLA JIT support will be enabled for TensorFlow.

Do you wish to build TensorFlow with GDR support? [y/N]: n
No GDR support will be enabled for TensorFlow.

Do you wish to build TensorFlow with VERBS support? [y/N]: n
No VERBS support will be enabled for TensorFlow.

Do you wish to build TensorFlow with nGraph support? [y/N]: n
No nGraph support will be enabled for TensorFlow.

Do you wish to build TensorFlow with OpenCL SYCL support? [y/N]: n
No OpenCL SYCL support will be enabled for TensorFlow.

Do you wish to build TensorFlow with CUDA support? [y/N]: n
No CUDA support will be enabled for TensorFlow.

Do you wish to download a fresh release of clang? (Experimental) [y/N]: n
Clang will not be downloaded.

Do you wish to build TensorFlow with MPI support? [y/N]: n
No MPI support will be enabled for TensorFlow.

Please specify optimization flags to use during compilation when bazel option "--config=opt" is specified [Default is -march=native]: 


Would you like to interactively configure ./WORKSPACE for Android builds? [y/N]: n
Not configuring the WORKSPACE for Android builds.

Preconfigured Bazel build configs. You can use any of the below by adding "--config=<>" to your build command. See tools/bazel.rc for more details.
    --config=mkl            # Build with MKL support.
    --config=monolithic     # Config for mostly static monolithic build.
Configuration finished
```
```
$ sudo bazel build --config opt --local_resources 1024.0,0.5,0.5 \
--copt=-mfpu=neon-vfpv4 \
--copt=-ftree-vectorize \
--copt=-funsafe-math-optimizations \
--copt=-ftree-loop-vectorize \
--copt=-fomit-frame-pointer \
--copt=-DRASPBERRY_PI \
--host_copt=-DRASPBERRY_PI \
//tensorflow/tools/pip_package:build_pip_package
```
