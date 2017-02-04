<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#orgfe6a509">1. 介绍</a></li>
<li><a href="#org02a0f42">2. 软硬件环境</a></li>
<li><a href="#orga017fb4">3. 配置python开发环境(pyenv 和 anaconda)</a>
<ul>
<li><a href="#orgb990e8e">3.1. 安装pyenv</a></li>
<li><a href="#orgff0c4a6">3.2. 安装python(anaconda)</a></li>
<li><a href="#orga419365">3.3. pyenv 使用</a></li>
</ul>
</li>
<li><a href="#org919cec6">4. 安装tensorflow</a>
<ul>
<li><a href="#org5265bca">4.1. 安装pip</a></li>
<li><a href="#org2910d1c">4.2. 安装CUDA</a></li>
<li><a href="#orge37d98f">4.3. 安装tensorflow</a></li>
</ul>
</li>
<li><a href="#orga713f22">5. jupyter notebook 远程配置</a></li>
<li><a href="#orgc173f05">6. 参考</a></li>
<li><a href="#orgdf8837c">7. 联系</a></li>
</ul>
</div>
</div>


<a id="orgfe6a509"></a>

# 介绍

目前在学习优达学城的无人驾驶课程，在DeepLearning这一阶段的学习过程中，使用的了anaconda和tensorflow，在此过程中出现了一些问题。最终解决，现记录一下。


<a id="org02a0f42"></a>

# 软硬件环境

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<tbody>
<tr>
<td class="org-left">系统</td>
<td class="org-left">ubuntu 16.04 64bit</td>
</tr>


<tr>
<td class="org-left">shell</td>
<td class="org-left">zsh</td>
</tr>


<tr>
<td class="org-left">型号</td>
<td class="org-left">alw15</td>
</tr>


<tr>
<td class="org-left">内存</td>
<td class="org-left">16G</td>
</tr>


<tr>
<td class="org-left">独立显卡</td>
<td class="org-left">Nvdia Geforce 970m</td>
</tr>


<tr>
<td class="org-left">硬盘</td>
<td class="org-left">128G SSD +1TB HD</td>
</tr>
</tbody>
</table>


<a id="orga017fb4"></a>

# 配置python开发环境(pyenv 和 anaconda)

考虑到系统初始版本python为2.7.更改后可能使用其他软件会存在问题，如geeknote等，所以首先安装pyenv.


<a id="orgb990e8e"></a>

## 安装pyenv

执行 ： 

    url -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash

在~/.zshrc 中加入如下：

    export PATH="/home/shenmutong/.pyenv/bin:$PATH"
    eval "$(pyenv init -)"
    eval "$(pyenv virtualenv-init -)"

完成后执行source ~/.zshrc,使操作生效。


<a id="orgff0c4a6"></a>

## 安装python(anaconda)

    pyenv install --list  #列出pyenv可以安装的python 版本。

使用pyenv 安装python 版本，可以直接执行:

    pyenv install anaconda3-4.2.0

因为我是在中国，所以因为你懂得的原因过程异常痛苦，所以直接在 [anaconda下载地址](https://www.continuum.io/downloads) 下载python3.5 version的 anaconda4.2.0 for linux。
下载好的文件是'Anaconda3-4.2.0-Linux-x86<sub>64.sh</sub>。复制或移动该文件到~/.pyenv/cache/下，然后执行

    pyenv install anaconda3-4.2.0

pyenv在安装之前会在~/.pyenv/cache 查找是否存在安装包，若存在，则会直接进行安装。
另外，记得好像可以更换pyenv 的源，没有去确定，各位也可以试一下。


<a id="orga419365"></a>

## pyenv 使用

    pyenv rehash # 更新数据库
    #在安装 Python 或者其他带有可执行文件的模块之后，需要对数据库进行更新
    
    pyenv versions # 查看当前已安装的 python 版本
    pyenv global anaconda3-4.2.0 #设置全局的 python 版本
    pyenv local anaconda3-4.2.0 # 更改当前目录下python版本
    pyenv shell anaconda3-4.2.0 # 更改当前shell环境下 python 版本
    
    pyenv uninstall #卸载某个版本python
    pyenv update # 更新 pyenv 及其插件

更多使用可以参考<https://github.com/yyuu/pyenv>
至此python环境 安装完成。


<a id="org919cec6"></a>

# 安装tensorflow

注意：如果没有CUDA SDK 情况下直接安装tensorflow gpu 版本的话，在使用过程中使用import tensorflow 会出现一个比较奇怪的错误，
'Error importing tensorflow. Unless you are using bazel, you should not try to import tensorflow from its source directory '。
当时脑残的用了很久来解决这个问题，后来才发现是因为没有安装CUDASDK的原因。


<a id="org5265bca"></a>

## 安装pip

如果没有安装pip的话 ，使用该命令进行安装。

    sudo apt-get install python-pip python-dev


<a id="org2910d1c"></a>

## 安装CUDA

一下内容直接复制于  <https://www.tensorflow.org/get_started/os_setup#optional_install_cuda_gpus_on_linux>
Check NVIDIA Compute Capability of your GPU card

<https://developer.nvidia.com/cuda-gpus>

Download and install Cuda Toolkit

<https://developer.nvidia.com/cuda-downloads>

Install version 8.0 if using our binary releases.

Install the toolkit into e.g. /usr/local/cuda.

Download and install cuDNN

<https://developer.nvidia.com/cudnn>

Download cuDNN v5.1.

Uncompress and copy the cuDNN files into the toolkit directory. Assuming the toolkit is installed in /usr/local/cuda, run the following commands (edited to reflect the cuDNN version you downloaded):

    tar xvzf cudnn-8.0-linux-x64-v5.1-ga.tgz
    sudo cp -P cuda/include/cudnn.h /usr/local/cuda/include
    sud片～o cp -P cuda/lib64/libcudnn* /usr/local/cuda/lib64
    sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
    #Install other dependencies
    sudo apt-get install libcupti-dev


<a id="orge37d98f"></a>

## 安装tensorflow

在使用anaconda配置的 目录下，或切换当前shell到andconda 环境中。

    # Ubuntu/Linux 64-bit, CPU only, Python 3.5
    export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.12.1-cp35-cp35m-linux_x86_64.whl
    # Ubuntu/Linux 64-bit, GPU enabled, Python 3.5
    # Requires CUDA toolkit 8.0 and CuDNN v5. For other versions, see "Installing from sources" below.
    export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-0.12.1-cp35-cp35m-linux_x86_64.whl
    pip3 install --upgrade $TF_BINARY_URL

搞定


<a id="orga713f22"></a>

# jupyter notebook 远程配置

有时间再写。


<a id="orgc173f05"></a>

# 参考

<https://github.com/yyuu/pyenv>
<https://www.tensorflow.org/get_started/os_setup#optional_install_cuda_gpus_on_linux>


<a id="orgdf8837c"></a>

# 联系

如果大家有问题，欢迎讨论。我的邮箱是
shenmutong@hotmail.com

