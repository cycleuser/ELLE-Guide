Title: Elle Numerical Simulation Platform Installation Guide on Ubuntu 18.04
Date: 2019-5-2 10:57:29
Category: Software

The original installation guide on http://elle.ws/installation only works on Ubuntu 16.04, and does not work well on Ubuntu 18.04. So there come this guide.

## Install Dependicies

#### Open terminal and run:

```Bash
sudo apt install gfortran gcc mesa-common-dev libgl1-mesa-dev libglu1-mesa-dev libgtk2.0-0 zlibc zlib1g make build-essential xorg-dev libmotif-common libmotif-dev xutils-dev libgtk2.0-dev cvs xutils libx11-dev libxt-dev libxpm-dev x11proto-print-dev x11proto-xext-dev libxext-dev
```

Notice that the original version use `libmotif4`, which has been replaced by `libmotif-common` in Ubuntu 18.04.

#### Then run:

```Bash
sudo apt-get install  libgsl-dev libgsl23 libgslcblas0  libgsl-dbg
```

Notice that the original version use `libgsl2`, which has been replaced by `libgsl23 libgslcblas0  libgsl-dbg` in Ubuntu 18.04.

## wxWidgets 2.8.12

#### Download wxWidgets

Notice that only 2.8.12 works for elle！

Visit http://www.wxwidgets.org/downloads/ to download wxWidgets-2.8.12.zip

```Bash
wget https://github.com/wxWidgets/wxWidgets/releases/download/v2.8.12/wxWidgets-2.8.12.zip
```

#### Install wxWidgets

Here comes a trick! `wxgtk2.8 doesn't compile with the new gcc, needs -std=gnu++98`, so we need to add `export CFLAGS=-std=c99 CXXFLAGS=-std=c++98` in the terminal firstly and then configure it by running `./configure --prefix=/usr`.

##### ref: https://bugs.alpinelinux.org/issues/6361 and https://forums.wxwidgets.org/viewtopic.php?t=43118

Once the wxWidgets 2.8.12 downloaded, decompress the zip file, and cd into the directory in terminal then type:

```Bash
export CFLAGS=-std=c99 CXXFLAGS=-std=c++98
./configure --prefix=/usr
make
sudo make install
```

## Clone and Install ELLE

#### Clone the elle-git 

```Bash
cd /home/
git clone https://git.code.sf.net/p/elle/git elle-git
```

Then the `elle-git` folder which contains `elle` folder will be downloaded.
Here we put the `elle` folder to your `/home/` location. Of course you can change it into another location, but you will need to modify following commands to setting up the `PATH`.

Then cd into the `elle-git` folder, and copy the whole `elle` folder to `/home/` and become `/home/elle`:

```Bash
cd elle-git 
cp -R elle /home/
```

Now we have everything we need at `/home/elle` folder.

#### Install elle

```Bash
cd /home/elle
./install.sh wx
```

If no errors, the installation of `elle` succeeded!
Then set up the `PATH` by running following commands in terminal:

```Bash
export PATH=$PATH:/home/elle/elle/binwx
export LD_LIBRARY_PATH=/lib:/usr/lib:/usr/local/lib
ELLEPATH=/home/elle/elle/binwx
export PATH LD_LIBRARY_PATH ELLEPATH
```

The original installation guide use `/home/your_user/elle`, here we put it at `/home/elle` instead.
`your_user` here means the user location of your system.
For example, my user name is `fred`, then I can use `/home/fred/elle` instead of `/home/elle`, which requires me to copy the `elle` folder, which is contained in the cloned `elle-git` folder, to `/home/fred/elle` instead of `/home/elle`.

If you donnot get a clue about the path or folder, that is OK. Just follow my codes above and put it to `/home/elle`.

#### Test installed elle

```Bash
cd /home/elle/bin
./showelle
```

If the gui shows up, it works!

The `elle` files under `elle\examples` might work, but those under `elle-git\experiments` may give you a `Segmentation fault (core dumped)` error. I donnot know why because this `elle` is not written by me, and there seems not to be any detailed documents available on their [elle.ws](elle.ws) website. Go ask them for help please.



Title: 数值模拟平台软件 Elle 安装指南 Ubuntu 18.04
Date: 2019-5-2 10:57:29
Category: Software

在 http://elle.ws/installation 的原版安装指南只适用于 Ubuntu 16.04, 不适合 Ubuntu 18.04.

## 安装依赖包

#### 打开终端输入:

```Bash
sudo apt install gfortran gcc mesa-common-dev libgl1-mesa-dev libglu1-mesa-dev libgtk2.0-0 zlibc zlib1g make build-essential xorg-dev libmotif-common libmotif-dev xutils-dev libgtk2.0-dev cvs xutils libx11-dev libxt-dev libxpm-dev x11proto-print-dev x11proto-xext-dev libxext-dev
```

原版安装指南中使用的 `libmotif4` 仅用于 Ubuntu 16.04，现在在 Ubuntu 18.04 下要用 `libmotif-common` 替代.

#### 然后运行:

```Bash
sudo apt-get install  libgsl-dev libgsl23 libgslcblas0  libgsl-dbg
```

原版安装指南中使用的 `libgsl2` 仅用于 Ubuntu 16.04，现在在 Ubuntu 18.04 下要用  `libgsl23 libgslcblas0  libgsl-dbg` 替代.

## 安装wxWidgets 2.8.12

#### 下载 旧版本的 wxWidgets

只能用很古老的旧版本 2.8.12！

访问 http://www.wxwidgets.org/downloads/ 下载 wxWidgets-2.8.12.zip

```Bash
wget https://github.com/wxWidgets/wxWidgets/releases/download/v2.8.12/wxWidgets-2.8.12.zip
```

#### 安装 wxWidgets

这里一定要注意! `wxgtk2.8 根本不能兼容最新的标准, 需要使用上世纪的标准才行 -std=gnu++98`, 所以要先运行 `export CFLAGS=-std=c99 CXXFLAGS=-std=c++98`， 然后运行 `./configure --prefix=/usr`.

##### 上述信息参考: https://bugs.alpinelinux.org/issues/6361 and https://forums.wxwidgets.org/viewtopic.php?t=43118

下载完毕了解压缩，cd 命令进入到 wxWidgets-2.8.12 目录，然后依次运行下面的命令来安装:

```Bash
export CFLAGS=-std=c99 CXXFLAGS=-std=c++98
./configure --prefix=/usr
make
sudo make install
```

## 安装 ELLE

#### 先克隆 elle-git 

```Bash
cd /home/
git clone https://git.code.sf.net/p/elle/git elle-git
```

这里的`elle-git` 目录包含了一个 `elle` 目录，这个 `elle` 目录才是最关键的。
这里我把 `elle` 目录就放进 `/home/` 位置了，这样后面就不用折腾什么用户名了。原版指南里面是把这个文件夹放进个人目录，可是这样就要每次要求用户根据自己个人目录的不同来调整后面的命令，对一问三不知的小白来说不是闹呢么？

所以这里就 cd 进入 `elle-git` 目录, 然后复制整个 `elle` 目录到 `/home/`，于是就有了 `/home/elle`:

```Bash
cd elle-git 
cp -R elle /home/
```

要安装用的东西就都在 `/home/elle` 目录内了.

#### 终于开始安装了

```Bash
cd /home/elle
./install.sh wx
```

没报错的话就说明安装成功了。然后还要设置环境变量 `PATH`，在终端中运行下面的命令:

```Bash
export PATH=$PATH:/home/elle/elle/binwx
export LD_LIBRARY_PATH=/lib:/usr/lib:/usr/local/lib
ELLEPATH=/home/elle/elle/binwx
export PATH LD_LIBRARY_PATH ELLEPATH
```

官网文档说让你用 `/home/your_user/elle`,而这里我们直接就用了 `/home/elle` .
`your_user` 意思是你自己系统上面的家目录的用户名，比如我的用户名是 `fred`, 那么就要使用 `/home/fred/elle` 而不是 `/home/elle`, 这也就需要之前的步骤中把`elle` 目录复制到 `/home/fred/elle` 而不是 `/home/elle`。你自己要是搞得清楚用户目录和环境变量设置，完全可以随意设置。

你要是纯小白搞不懂什么家目录，就按照上文中的命令，使用 `/home/elle` 吧。

#### 测试安装好的 elle

```Bash
cd /home/elle/bin
./showelle
```

如果图形界面出现了，就是安装好了。
不过可能会出现很多问题，比如 `elle` 目录下的 `elle\examples` 中的一些 `elle`格式文件就可以运行，而 `elle-git\experiments` 下的打开可能就会出现 `Segmentation fault (core dumped)` 的报错。这你别问我，这软件也不是我开发的，官网也没发现详细的说明手册，自己想办法去吧。
