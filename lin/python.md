# python language

## package 4 data science

pytorch, numpy, matplotlib，pandas，pyplot，math，scipy，tensorflow 

## python in vscode

通过虚拟环境可以实现各个py项目的隔离，首先：py -3 -m venv .venv在当前项目下创建一个虚拟环境，然后运行vs命令：Python:Select Interpreter选择刚刚的虚拟环境，这样，当前项目所有的安装包只会安装在当前的虚拟环境中，当执行python -m pip install matplotlib可能提示：Can not perform a '--user' install，则需要在$home/pip/pip.ini中配置：user = false，从而pip不在虚拟环境中进行全局安装。也可在该文件中配置：index-url = https://mirrors.aliyun.com/pypi/simple，指定pip默认的服务器地址。


## jupyter notebook

jupyter notebook

## conda

conda config --remove channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://repo.continuum.io/pkgs/free/ 
conda config --add channels https://repo.continuum.io/pkgs/main/ 
conda config --set show_channel_urls yes
conda config --set always_yes false

conda create -n notebook python=3.7 ipykernel
conda install nb_conda_kernels
conda install nb_conda
jupyter kernelspec list
jupyter kernelspec remove base

## resource

- [python document](https://docs.python.org/3/tutorial/index.html)
- [numpy](https://www.numpy.org.cn/)
- [jupyter](https://jupyter.org/documentation)
- [pydata book](https://github.com/wesm/pydata-book)
- [anaconda](https://docs.anaconda.com/anaconda/install/windows/)
- [nb conda kernels](https://github.com/Anaconda-Platform/nb_conda_kernels)
