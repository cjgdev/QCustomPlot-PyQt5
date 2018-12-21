# QCustomPlot2-PyQt5

- [Design goals](#design-goals)
- [Getting started](#getting-started)
- [Examples](#examples)
  - [Interactions](#interactions)
  - [Plots](#plots)
  - [QtQuick QML](#qtquick-qml)
  - [Scrollbars](#scrollbars)
  - [Text Document Integration](#text-document-integration)
- [Supported compilers](#supported-compilers)
- [License](#license)
- [Contact](#contact)
- [Thanks](#thanks)
- [Used third-party tools](#used-third-party-tools)
- [Projects using](#projects-using)
- [Notes](#notes)
- [Building](#building)

## Design goals

There are myriads of Python charting libraries out there, and each may even have its reason to exist. QCustomPlot2 for PyQt5 has the following goals:

- **Performance**. QCustomPlot is written in modern C++ with the excellent Qt library for superior performance over alternative libraries.

- **Flexibility**. QCustomPlot is one of the most customisable libraries available, with a wide range of supported graph types and full control over how the graph is rendered.


## Getting started

First install the package via our favourite package manager:

```sh
$ pip install QCustomPlot2
```

Now let's take a look at some code:

```python
from PyQt5.QtGui import QPen, QBrush, QColor
from QCustomPlot2 import *

customPlot = QCustomPlot()

graph0 = customPlot.addGraph()
graph0.setPen(QPen(Qt.blue))
graph0.setBrush(QBrush(QColor(0, 0, 255, 20)))

graph1 = customPlot.addGraph()
graph1.setPen(QPen(Qt.red))

x, y0, y1 = [], [], []
for i in range (251):
    x.append(i)
    y0.append(math.exp(-i/150.0)*math.cos(i/10.0)) # exponentially decaying cosine
    y1.append(math.exp(-i/150.0))                  # exponential envelope

graph0.setData(x, y0)
graph1.setData(x, y1)

customPlot.rescaleAxes()
customPlot.setInteractions(QCPInteractions(QCP.iRangeDrag | QCP.iRangeZoom | QCP.iSelectPlottable))
```

That's all!

Some important things:

* QCustomPlot is a QWidget type that can be used the same way as any other widget, added to layouts, etc. However, you can nest multiple graphs in a single QCustomPlot using layouts (see the Advanced Axes demo).


## Examples

Beside the examples below, you may want to check the [documentation](https://www.qcustomplot.com/index.php/support/documentation).


## Supported compilers

The following compilers are known to work:

- MSVC 140, 141
- GCC 4.8
- Clang 3.4

I would be happy to learn about other compilers/versions.

Please note:

The following compilers are currently used in continuous integration at [Travis](https://travis-ci.org/cjgdev/QCustomPlot2-PyQt5) and [AppVeyor](https://ci.appveyor.com/project/cjgdev/QCustomPlot2-PyQt5):

| Compiler        | Operating System             | Version String |
|-----------------|------------------------------|----------------|
| GCC 4.8.5       | CentOS 7                     | gcc version 4.8.5 20150623 (Red Hat 4.8.5-16) (GCC)  |
| Clang Xcode 10.0 | OSX 10.13.3                 | Apple LLVM version 10.0.0 (clang-1000.11.45.2) |


## License

<img align="right" src="http://opensource.org/trademarks/opensource/OSI-Approved-License-100x137.png">

This code is licensed under the [MIT License](http://opensource.org/licenses/MIT):

Copyright &copy; 2017-2018 Dmitry Voronin and [Christopher Gilbert](https://github.com/cjgdev/)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

* * *

This project contains the [QCustomPlot](https://gitlab.com/DerManu/QCustomPlot) library from Emanuel Eichhammer which is licensed under the [GPL Version 3 License](http://opensource.org/licenses/GPLv3). Copyright &copy; 2011-2018 [Emanuel Eichhammer](http://bjoern.hoehrmann.de/) <bjoern@hoehrmann.de>


## Contact

If you have questions regarding the library, I would like to invite you to [open an issue at GitHub](https://github.com/cjgdev/QCustomPlot2-PyQt5/issues/new). Please describe your request, problem, or question as detailed as possible, and also mention the version of the library you are using as well as the version of your compiler and operating system. Opening an issue at GitHub allows other users and contributors to this library to collaborate.


## Thanks

I deeply appreciate the help of the following people.

- [DerManu](https://gitlab.com/DerManu) is the official author and maintainer of the excellent QCustomPlot library.
- [dimv36](https://github.com/dimv36) is the original author of the Python bindings for QCustomPlot 1.0.0, upon which this project is based.
- [cowo78](https://github.com/cowo78) added support for the QCustomPlot 2.0.0 API.

Thanks a lot for helping out! Please [let me know](mailto:mail@nlohmann.me) if I forgot someone.


## Used third-party tools

This library is built, tested, documented, and whatnot using third-party tools and services. Thanks a lot!

- [**SIP**](https://www.riverbankcomputing.com/software/sip) to generate the Python bindings.


## Projects using

If you are using QCustomPlot2-PyQt5 in a project and would like to share with the community, please let me know, or even better, raise a pull request.


## Notes

None.


## Building

### Windows

Windows users may use [chocolatey](https://chocolatey.org/) and follow the instructions below for fetching the necessary packages needed to build the library, otherwise you will need to adapt the steps for your own environment.

```PowerShell
# Fetch the necessary development tools and libraries
choco install visualstudio2017buildtools python3 git jom pyqt5 qt-sdk

# Activate Qt 5.x tools and libraries
Push-Location
"C:\Qt\5.11.1\msvc2017_64\bin\qtenv2.bat"
Pop-Location

# Activate Visual Studio build tools for x64
"C:\Program Files (x86)\Microsoft Visual Studio\2017\Professional\VC\Auxiliary\Build\vcvarsall.bat" x64

# Clone the repository and submodules
git clone --recursive https://github.com/cjgdev/QCustomPlot2-PyQt5.git && cd QCustomPlot2-PyQt5

# Build
python setup.py build

# Zzz..

# Install
python setup.py install
```


### Linux

Apt users (Debian, Ubuntu, etc) may follow the instructions below, users of other distributions may adapt the steps below for your own package manager.

```sh
# Fetch the necessary development tools and libraries
$ apt-get install build-essential python3-pyqt5 pyqt5-dev-tools qttools5-dev-tools

# Clone the repository and submodules
$ git clone --recursive https://github.com/cjgdev/QCustomPlot2-PyQt5.git && cd QCustomPlot2-PyQt5

# Build
$ CFLAGS=-std=c++11 CXXFLAGS=-std=c++11 python setup.py build

# Zzz..

# Install
$ python setup.py install
```


### macOS

Users of macOS using [homebrew](https://brew.sh/) may follow the instructions below to fetch the required packages to build the library, or simply adapt to your own environment.

```sh
# First ensure Xcode is installed, as homebrew depends on it
$ xcode-select --install

# Fetch the necessary development tools and libraries
$ brew install qt --devel sip --without-python@2 pyqt --without-python@2

# Clone the repository and submodules
$ git clone --recursive https://github.com/cjgdev/QCustomPlot2-PyQt5.git && cd QCustomPlot2-PyQt5

# Build
$ CFLAGS='-std=c++11 -stdlib=libc++' CXXFLAGS='-std=c++11 -stdlib=libc++' python3 setup.py build

# Zzz..

# Install
$ python3 setup.py install
```


### Custom build options

If you need to override the paths for any reason, the way to do that is by modifying setup.cfg to match your environment. You will need to add a section as below, substituting everything between ``<<`` and ``>>`` with the correct paths.

```ini
[build_ext]
qmake = <<PATH_TO>>\qmake.exe
qt-include-dir = <<QT_INCLUDE_DIR>>\include
qt-library-dir = <<QT_LIBRARY_DIR>>\lib
make = <<PATH_TO>>\jom.exe
```
