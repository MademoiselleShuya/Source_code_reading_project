本节主要介绍[epiPALEOMIX使用](https://bitbucket.org/khanghoj/epipaleomix/wiki/Home)

1.epiPALEOMIX Installation

A. clone epiPALEOMIX from Github

```
git clone https://github.com/KHanghoj/epiPALEOMIX.git
```

B. Environment Setting

用编译器pycharm打开epiPALEOMIX，创建适合和环境command + , 具体操作如下

project epiPALEOMIX  --> python interpreter --> add ... --> Virtualenv Enviroment OR **Conda Enviroment** --> python 2.7 -->ok

C. Install pysam

*Pysam* is a python module that makes it easy to read and manipulate mapped short read sequence data stored in SAM/BAM files

```
conda install -c bioconda pysam
```

OR

```
pip install pysam
```

D. Install R 

```
conda install -c r r
```

E. Install Samtools(optional)

```
conda install -c bioconda samtools 
```

为了方便阅读源代码，我们没有将运行文件进行改名，暂时也没有设置环境变量

2.Setting default optional arguments

It is recommended to write a config file `--write-config-file` prior to running epiPALEOMIX to set default parameters such as temporary folder, number of threads used by default, and warning levels. For instance, for setting the maximum number of parallel threads to 20:

```
python run.py --write-config-file --max-threads 20
```

这里的python run.py相当于文件中epiPALEOMIX(设置环境变量以后)

3.How to run epiPALEOMIX

Check the overview of required steps to run epiPALEOMIX

```
python run.py -h   # Prints extensive optional arguments
```





