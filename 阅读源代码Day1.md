##### 第一步：查看readme文件

了解该pipeline的功能，以及基本信息

##### 第二步：阅读文献

了解代码的结构和原理

##### 第三步：查看源代码

可以在GitHub使用Octotree插件帮助阅读，或者将该项目直接克隆到本地再使用编译器查看

本次学习的材料为epiPALEOMIX，由Ludovic Orlando课题组于2014年发表在nature protocol上的一个开源项目，主要的编写语言为python以及小部分的R，该pipeline可以实现基于古代样品的高通量测序数据生成核小体和甲基化图的功能。

源代码链接：[GitHub - KHanghoj/epiPALEOMIX](https://github.com/KHanghoj/epiPALEOMIX)

参考文献：[Characterization of ancient and modern genomes by
SNP detection and phylogenomic and metagenomic
analysis using PALEOMIX](https://www.nature.com/articles/nprot.2014.063.pdf)

1. 查看readme文件

了解pycharm中几种查看readme文件的方式，以及修改该文件的方法

该文件主要介绍了该产品的功能、输入文件、以及作者信息和相关的参考文献

 epiPALEOMIX is used to **generate nucleosome and methylation maps** from high throughput sequencing data underlying **ancient samples**. It requires **BAM alignment files** against reference genomes as input, which can easily be generated using the PALEOMIX pipeline, previously released by our group (Schubert et al. 2014). epiPALEOMIX has been developed by **Kristian Hanghøj**in the research group of Dr. **Ludovic Orlando**, at the Centre for GeoGenetics, Natural History Museum of Denmark, University of Copenhagen, Denmark.

2. 文献阅读

文章的摘要部分介绍了该pipeline包含了哪些部分，以及能够用于哪方面的研究。

Starting with next-generation sequencing reads, paleoMIX carries out **adapter removal**, **mapping** against reference genomes, **pcr duplicate removal**, characterization of and compensation for **postmortem damage**, **snp calling** and maximum-likelihood **phylogenomic inference**, and it profiles **the metagenomic contents** of the samples. paleoMIX allows for a series of potential applications in paleogenomics, comparative genomics and metagenomics. 

文件的figure详细介绍了代码的结构，以及数据处理流程

![Screenshot 2021-12-18 at 20.42.23.png](/var/folders/5f/11d409g140lf_yxwc5zyfrl80000gq/T/TemporaryItems/NSIRD_screencaptureui_09PK5i/Screenshot%202021-12-18%20at%2020.42.23.png)

3. 查看源代码

在查看代码之前，想要创建相应的编程环境。在pycharm使用快捷键：command + ,逗号，选择所需要的编程环境，如果版本不一致，代码可能会出现大量的报错

使用快捷键 command + shift + - 减号，收缩代码，反之，加加号则是展开代码

注：写代码的一个原则是功能最小化，即一个函数实现一个功能，这样方便后期查看。冗长的代码阅读起来会让人感到十分吃力

homework：尝试自己先阅读代码，了解其结构。
