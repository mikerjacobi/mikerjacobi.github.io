---
layout: post
title: Using CMake and swig to Connect Python to C
---
This post documents my experience with calling my own C library from a Python web server.

Here’s a bit of background. The project I’m referring to, among other things, has an API, written in C, that hooks into MongoDB. Since it’s an API, I wanted to create a shared object so that I could implement various interfaces into it. The first interface I wrote was also in C, so linking to this library was no problem. Then, I wanted my to write the next interface in Python (a Python webserver). This required that I either create a separate API in Python or wrap my C API with Python
handlers. I opted for the latter. SWIG is a technology that does exactly this - autogenerate interfaces in different languages from c/c++ code. The main benefit of this approach is that my API code is maintained in one location, in one language. Any change I make to the API, in C, will generate the corresponding Python code at compile time. Honestly, being new to both cmake and SWIG, the biggest challenge to accomplish this task was incorporating SWIG commands into cmake.

The directory structure of this project is: {root}/API.c {root}/API.h {root}/swig-controller.i {root}/build/CMakeLists.txt

From {root}, I run cmake -C build and then make -C build to compile.

The rest of this post describes my CMakeLists.txt file such that it will compile my API into a shared object and tell SWIG to generate a Python wrapper. Lines preceded by # are comments describing the following line. Here is CMakeLists.txt:

```
cmake minimum required(VERSION 2.8)
project (mongoAPI)

#allow gdb to run on the shared object; required for debugging.
set(CMAKE BUILD TYPE Debug)

#this sets the output directory of anything cmake generates
SET(CMAKE LIBRARY OUTPUT_DIRECTORY {root})

#this sets the output directory of anything SWIG generates
set(CMAKE SWIG OUTDIR {root})

#gcc flags.  this is required for the Mongo driver to compile
set(CMAKE C FLAGS "-std=c99")

#point to the Mongo driver header files
include_directories("/projects/mjacobi/lib/mongo-c-driver-master/mongoc/include/") 

#this generate the actual .so file for mongofs
add_library(mongoAPI SHARED ../mongofsAPI.c) 

#this says where to put the generated .so relative to the directory "cmake" is executed from
set target properties(mongoAPI PROPERTIES LIBRARY OUTPUT DIRECTORY ${PROJECT BINARY DIR}/..) 

#this tells cmake to link my API to the Mongo object
target link libraries(mongoAPI /path/to/libmongoc.so) 

#SWIG stuff:
#load the cmake SWIG package
find package(SWIG REQUIRED)
include(${SWIG USE_FILE})

#load the package that SWIG uses to generate Python
find_package(PythonLibs)

#point to python headers
include directories(${PYTHON INCLUDE_DIRS})

#tell SWIG to create a new module, called mongopyAPI, 
#in Python and point to the SWIG interface file (the .i file)
swig add module(mongopyAPI python ../mongopyAPI.i)

#link the above module to the API (the shared object) we just created
swig link libraries(mongopyAPI mongoAPI)

#also link the above module to Python
swig link libraries(mongopyAPI ${PYTHON_LIBRARIES} )
```
And that’s it! This code will generate both a shared object that can be linked to in gcc and a python library that can be directly imported. Now I can communicate with my API in C and Python, and adding a new language is relatively straight forward.


