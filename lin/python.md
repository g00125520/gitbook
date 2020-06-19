# python language

## package 4 data science

numpy, matplotlib，pandas，pyplot，math，scipy，tensorflow 

## python in vscode

通过虚拟环境可以实现各个py项目的隔离，首先：py -3 -m venv .venv在当前项目下创建一个虚拟环境，然后运行vs命令：Python:Select Interpreter选择刚刚的虚拟环境，这样，当前项目所有的安装包只会安装在当前的虚拟环境中，当执行python -m pip install matplotlib可能提示：Can not perform a '--user' install，则需要在$home/pip/pip.ini中配置：user = false，从而pip不在虚拟环境中进行全局安装。也可在该文件中配置：index-url = https://mirrors.aliyun.com/pypi/simple，指定pip默认的服务器地址。

## resource

- [python document](https://docs.python.org/3/tutorial/index.html)
- [numpy](https://www.numpy.org.cn/)