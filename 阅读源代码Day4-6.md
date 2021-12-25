A [Tutorial](https://bitbucket.org/khanghoj/epipaleomix/wiki/Tutorial.md) to understand the structure of the pipeline

It aims at generating methylation levels and nucleosome occupancy profiles in genomic regions surrounding CTCF binding sites. 

Data source: [Rasmussen and colleagues (2010)](http://dx.doi.org/10.1038/nature08835)

1. Installing R-packages

Two R-packages are required to plot the output

```
conda install -c conda-forge r-ggplot2 
conda install -c r r-gridextra
```

2. Downloading Tutorial data

Downloading and unpacking the [tutorial data](https://www.dropbox.com/s/5kxsqhq1aktm1i9/tutorial_epipal.tar.gz?dl=0 ) (1.3 GB), from 

```
tar xvzf tutorial_epipal.tar.gz
cd tutorial_epipal/
```

The uncompressed directory contains:

- A **prefix** folder, providing the Hg19 human reference genome (*hs.build37.1.fa.gz*) and its corresponding indeces (*hs.build37.1.fa.{fai,gzi}*) and mappability files (*GENOME_51_50.40000-20000.mappability*) of assembly Hg19;
- A **data** folder, providing the BAM read alignment file (*TUTORIAL_CTCF.bam*) together with its index file *TUTORIAL_CTCF.bam.bai*;
- A **bedfile** folder, providing the genomic coordinates of the first kilobase flanking OCCUPIED CTCF binding sites (*CTCF.bed*) [Fu et al., 2008)](http://dx.doi.org/10.1371/journal.pgen.1000138);
- A **yaml-format makefile** (*example.yaml*), representing the main input file required by epiPALEOMIX and containing path to BAM and BED files as well as indicating which analyses should be conducted;
- A **plottingtools** folder, providing additional R-scripts to visualize the outputs of epiPALEOMIX;
- A executable bash script (*createplots.sh*), commanding all R-scripts provided in the **plottingtools** folder.

3. epiPALEOMIX makefiles

```
python run.py makefile simple > new_makefile.yaml
```

更改在new_makefile.yaml或者example.yaml文件中的必要信息

```
--FastaPath: ./tutorial_epipal/prefix/hs.build37.1.fa.gz
--MappabilityPath: ./tutorial_epipal/prefix/GENOME_51_50.40000-20000.mappability
Nameofbed: ./tutorial_epipal/bedfile/CTCF.bed 
BamPath: ./tutorial_epipal/data/TUTORIAL_CTCF.bam
```

重新设置线程数

```
python run.py --write-config-file --max-threads 2 
vi /Users/u1995087/.pypeline/epiPALEOMIX.ini
```

4. Running epiPALEOMIX

Move all files we need to the directory **epiPALEOMIX**, these files will be paralleled with the script **run.py** if you didn't change the path information during step3. To check if all executables and input/output files to the node graph are available using

```
python run.py dryrun example.yaml --list-output-file
```

There are two output files **OUT_example** and **TEMPORARYFILES_example** after a dryrun. if some inTo run epiPALEOMIX

```
python run.py run new_makefile.yaml
OR
python run.py run example.yaml
```

NOTE: Try to run it on server.







