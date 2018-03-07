# ubuntu-caffe-build

Short notes to help with building/isntalling Caffe on Ubuntu 16.04 with Python 3.5

## install dependencies

	sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler
	sudo apt-get install --no-install-recommends libboost-all-dev
	sudo apt-get install libatlas-base-dev
	sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev
	sudo apt-get install python3-dev

## Makefile.config
 
In Makefile.config with Python 3 uncomment:

	CPU_ONLY := 1
	BLAS := atlas
	PYTHON_LIBRARIES := boost_python-py35 python3.5m
	PYTHON_INCLUDE := /usr/include/python3.5m \
                 /usr/local/lib/python3.5/dist-packages/numpy/core/include
	PYTHON_LIB := /usr/lib
	INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial/
	LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib

NOTE - useful tip for finding Python paths:

	python3
	> import sys
	> print '\n'.join(sys.path)

## Makefile 

In Caffe Makefile:

	LIBRARIES += glog gflags protobuf boost_system boost_filesystem m hdf5_serial_hl hdf5_serial

## Build

In caffe root dir: 

	make all
	make test
	make runtest

	make pycaffe
	make distribute


# library usage example

	testfile.py

	import sys
	sys.path.insert(0, '/home/<username>/caffe/python')
	import caffe
	caffe.set_mode_cpu()

	> python3 testfile.py
	or via command line interactive Python
