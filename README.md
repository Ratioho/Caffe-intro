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