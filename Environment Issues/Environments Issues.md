# Environmental Issues

```
./opt/cachelib/bin/cachebench: symbol lookup error: ./opt/cachelib/bin/cachebench: undefined symbol: _ZN6google21kLogSiteUninitializedE
/usr/bin/ld: CMakeFiles/BogoShim.dir/test/BogoShim.cpp.o: undefined reference to symbol '_ZN6google11InitVLOG3__EPPiS0_PKci'
```

CacheLib link library wrong: _ZN6google21kLogSiteUninitializedE, related to glog, change the version of glog





```
[ 94%] Linking CXX shared library libfolly.so
/usr/bin/ld: /usr/local/lib/libfmt.a(format.cc.o): relocation R_X86_64_PC32 against symbol `stderr@@GLIBC_2.2.5' can not be used when making a shared object; recompile with -fPIC
/usr/bin/ld: final link failed: Bad value
```

It wants to link a static lib to a shared lib.

Build libfmt as the shared lib (libfmt.so) rather than (libfmt.a) solves the problem.

Using command `cmake -DBUILD_SHARED_LIBS=ON ...`



```
error: command 'x86_64-apple-darwin13.4.0-clang++' failed with exit status 1 error ERROR: Failed building wheel for torch-sparse
```

This problem is encountered when installing torch_sparse in python. It means the g++ version is not correct on Mac.

Use command `export CXX=clang++` to set the correct g++. https://github.com/astropy/halotools/issues/813#issuecomment-333701045

This twitter contains the needed commands to install pytorch_geometric on MacOS. https://twitter.com/xbresson/status/1154686843130011649?s=21   Note: If it doesn't work, uninstall the according librarys and reinstall them.



### Python Version (Anaconda)

install anaconda

```shell
wget https://repo.anaconda.com/archive/Anaconda3-2020.07-Linux-x86_64.sh
bash Anaconda3-2020.07-Linux-x86_64.sh
```

create a python3.7 environment

```shell
conda create -n python37 python=3.7
```

inwstall a specific package

```shell
conda install -n python37 scipy
```

list all environments

```shell
conda env list
```

activate an environment

```shell
conda activate python37
```

deactivate an environment

```shell
conda deactivate
```



### 查看文件行数

```shell
wc -l <filename>
```



### YCSB generation

```shell
cd ~/Desktop/Heterogeneous_Memory/ERT/index-microbench
conda activate python27
YCSB/bin/ycsb load basic -P workload_spec/workloada -s > workloads/ycsb_txn_randint_workloada_50M
```



### Docker 使用

启动docker `docker start <ID/docker_name>`

查看已启动docker `docker ps -n 5`

停止docker `docker stop` / `docker kill`

重启docker `docker restart <ID/docker_name>`



### Haskell学习

不能用tab，必须用空格，对齐很严格

https://www.w3cschool.cn/hsriti/

```haskell
-- 注释是 --
-- 表示输入一个Block 类型和一个(Int, Int, Int)类型的tuple，输出一个GCStmt
-- 第一行声明transBlk函数，然后定义该函数，函数内部使用pattern matching
transBlk :: Block -> (Int, Int, Int) -> GCStmt
transBlk blk ctr =
  case blk of
  [] -> GCAssume GCTrue
  [x] -> transStmt x ctr
  (x:xs) -> GCSeq (transStmt x ctr) (transBlk xs ctr)
```



### Markdown

New page command

```markdown
<div style="page-break-after: always"></div>
```

