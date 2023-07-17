# sublime的设置

## 安装PackageControl

点击上方工具栏 Tools - Install Package Control

下载CppFastOlympicCoding

## 下载fira-code
前往github将需要的zip包下载下来，然后右键open就行

## 不能使用install package 的解决办法

原因是macOS的版本太高导致没有旧版的SSL了

而sublime需要依赖openSSL1或者2

参考`https://github.com/wbond/package_control/issues/1612`

```bash

brew install openssl@1.1 && ln -sf $(set -- `brew --cellar openssl@1.1`/1.1.1? && echo "$1")/lib/libcrypto.dylib /usr/local/lib/

```

即可