# Emacs Configuration

This emacs configuration is based on [Purcell's emacs configuration](https://github.com/purcell/emacs.d).

## Table of contents
- [Install emacs configuration](#install-emacs-configuration)
- [Install rtags for cmake-ide](#install-rtags-for-cmake-ide)
  - [Install emacs >= 24.4](#install-emacs-24.4-or-higher)
  - [Preparation for rtags](#preparation-for-rtags)
  - [Compile and install](#compile-and-install)
  - [Usage](#usage)

#### More reading
- [Purcell's emacs](https://github.com/purcell/emacs.d): Most powerfull emacs configuration version.
- [Rtags](https://github.com/Andersbakken/rtags): client/server application for indexing C/C++ code.
- [Pandoc](http://pandoc.org/installing.html): Powerful document converter, it's used for markdown preview (shortcut: C-c C-c p).

## Install emacs configuration  
1. If you don't have purcell's configuration of emacs, please install it with the following command.  
```bash
    git clone https://github.com/purcell/emacs.d ~/.emacs.d  
```

2. Install my emacs configuration.
```bash
	git clone https://github.com/linweiyang/emacs.wylin  
	cd emacs.wylin  
	cp init-local.el ~/.emacs.d/lisp/init-local.el  
	cp -r wylin-emacs ~/.emacs.d/lisp/wylin-emacs  
```
    <font color=#ff0000>NOTE:</font> Recommend to use chinese elpa mirror in China.
    ```bash
    cp mirror/init-elpa.el ~/.emacs.d/lisp/lisp/init-elpa
    ```
3. For google cpplint.
```bash
	sudo apt-get install python-pip  
	sudo pip install cpplint
```

4. Change 'Caps' to 'Ctrl' (not swap), create ~/.Xmodmap file in Linux:
```xmodmap
   remove Lock = Caps_Lock
   keysym Caps_Lock = Control_L
   add control = Control_L
```	
	(In ubuntu 14 or 16, we need to add command "xmodmap ~/.Xmodmap" at the end of ~/.xinputc file.)  

## Install rtags for cmake-ide
<font color=#ff0000>NOTE:</font> If you don't want to use cmake-ide, just ignore this section.

[Rtags](https://github.com/Andersbakken/rtags) is a c/c++ client/server indexer for c/c++/objc[++] with integration for Emacs based on clang.

### Install emacs >= 24.4
Rtags package for emacs needs helm packge, but the helm package only supports emacs version >= 24.4. User need to install emacs 24.4 or higher version. Here are two methods for install high emacs version.

1. Provided packages for Ubuntu LTS 14.04 and 16.04. Stable versions (25.1 currently):
```bash
	sudo apt-add-repository -y ppa:adrozdoff/emacs
	sudo apt update
	sudo apt install emacs25
```
2. Or compile emacs by yourself (http://ubuntuhandbook.org/index.php/2014/10/emacs-24-4-released-install-in-ubuntu-14-04/).

### Preparation for rtags  
In Ubuntu
```bash
sudo apt-get install llvm clang libclang-dev openssl
```
In OSX or macOS
```bash
brew install llvm --with-libcxx --with-clang --without-assertions --with-rtti
```

<font color=#ff0000>NOTE:</font>  
    - LLVM/Clang >= 3.3  
    - GCC/Clang >= 4.7/3.2  
    - cmake >= 2.8  
    - emacs >= 24.4 is recommended  

### Compile and install
```bash
    git clone --recursive https://github.com/Andersbakken/rtags.git
    cd rtags
    mkdir build
    cd build
    cmake ..
    make
    sudo make install
```

### Usage
In a cmake project using the following command to compile the source code
```bash
    cmake -DCMAKE_EXPORT_COMPILE_COMMANDS=1 ..
```
In simple method, please add cmake-rtags to .bashrc using the following command:
```bash
    echo alias cmake-rtags=\'cmake -DCMAKE_EXPORT_COMPILE_COMMANDS=1\' >> ~/.bashrc
```
