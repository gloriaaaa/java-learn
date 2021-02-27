# OpenMPI编译安装记录
- 下载解压安装包
```
tar -xjf openmpi-1.10.2.tar.bz2
cd openmpi-1.10.2
```
- 编译，注意添加多线程支持
```
./configure --prefix=/home/gloria/software/openmpi-1.10.2 --enable-mpi-thread-multiple 
make all install  
```
- 配置环境变量
```
sudo gedit ~/.bashrc
export PATH=/home/gloria/software/openmpi-1.10.2/bin:$PATH
export LD_LIBRARY_PATH=/home/gloria/software/openmpi-1.10.2/lib:$LD_LIBRARY_PATH
export LIBRARY_PATH=/home/gloria/software/openmpi-1.10.2/lib:$LIBRARY_PATH
export INCLUDE=/home/gloria/software/openmpi-1.10.2/include:$INCLUDE
export MANPATH=/home/gloria/software/openmpi-1.10.2/share/man:$MANPATH
```
每行路径末尾都有`:$PATH、:$INCLUDE、:$LIBRARY_PATH、:$LD_LIBRARY_PATH` 是因为在root目录下usr/local/安装了openMPI，在你普通用户下面也安装了openMPI。这样变量设置成优先检查搜索的目录是你普通用户下的openMPI 共享库路径 。如果root目录下没有openMPI则不需要末尾的定义
关闭保存之后`source ~/.bashrc`
- `mpiexec -V `查看版本

