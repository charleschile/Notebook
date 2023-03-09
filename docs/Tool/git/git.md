# git 使用

### 一、git是什么

### 配置github的http端口
在vpn的配置`yaml`文件中，可以找到`mixed-port:7890`

所以需要在终端设置git的http端口:
```bash

git config --global http.proxy '127.0.0.1:7890'

git config --global https.proxy '127.0.0.1:7890'

```

在取消全局代理之后

需要将代理端口关闭:
```bash
git config --global --unset http.proxy

git config --global --unset https.proxy
```

### 配置github的ssh key

#### 配置github的用户设置

```bash
➜  ~ git config --global user.name charleschile
➜  ~ git config --global user.email charles.chi.le@outlook.com
```

#### 生成自己的ssh-key

```bash
➜  ~ ssh-keygen -t rsa -b 4096 -C charles.chi.le@outlook.com
```

注意输入好上面这条命令后，一直按回车，什么都不用输入

```bash
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/charleschile/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:

Your identification has been saved in /Users/charleschile/.ssh/id_rsa
Your public key has been saved in /Users/charleschile/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:MFuYaD/EEt+oNtc9nU+ssySqrMohTghqDg53F1uXVIs charles.chi.le@outlook.com
The key's randomart image is:
+---[RSA 4096]----+
|    .       .    |
|     = =   o .   |
|    + X o E .    |
|   . = * o o o   |
|.   + * S = o o  |
|+  . o = . . +   |
|*oo . o   . + .  |
|O+ o o   . o o   |
| +o...o..   .    |
+----[SHA256]-----+
```

拷贝~/.ssh/id_rsa.pub的输入到剪切板（即拷贝公钥内容）

```bash
➜  ~ cat /Users/charleschile/.ssh/id_rsa.pub
```

拷贝即可



#### 配置github的ssh key

打开https://github.com/settings/keys

New 一个ssh key

