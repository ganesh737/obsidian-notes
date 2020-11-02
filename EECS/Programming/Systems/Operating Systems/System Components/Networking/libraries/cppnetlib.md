# cpp-netlib

## Setup

### Clone

```bash
git clone https://github.com/cpp-netlib/cpp-netlib
cd cpp-netlib
git submodule init
git submodule update
```

### Install Dependencies for Ubuntu 16

```bash
sudo apt-get install libboost-dev-all cmake 
```

### Build

```bash
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_C_COMPILER=gcc -DCMAKE_CXX_COMPILER=g++ ../cpp-netlib/

make -j $(nproc)
```

# Hashtags

#networking #cppnetlib