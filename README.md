# Strelka2

Germline variant calling pipeline based on Strelka2 variant caller. Preprocessing and variant calling are handled by the pipeline.
## QuickStart

This by default will run the gatk haplotype caller on the data contained in the test folder in this repo.

```
nextflow run main.nf --test
```
## Input Parameters 

- #### Reference genome

 By default (if the user does not interveene) the hg19 version of the reference genome is used.
 
 Two standard version of the genome ( hg19 and GRCh38.p10 ) are prepared with all their compressed and indexed file in a lifebit s3 bucket.
 They can be selected by using one of the flags:
 
 ```
 --hg19
 --h38
 ```
 
  For testing purposes we provide the chr20 of the hg19 version of the genome, accessible by: 
 ```
 --hg19chr20
 ```
 
 Alternatively, a user can use an own reference genome version, by using the following parameters:

  ```
  --fasta "/path/to/myGenome.fa"                REQUIRED
  --fai   "/path/to/myGenome.fa.fai"            OPTIONAL
  --fastagz "/path/to/myGenome.fa.gz"           OPTIONAL
  --gzfai  "/path/to/myGenome.fa.gz.fai"        OPTIONAL
  --gzi  "/path/to/myGenome.fa"                 OPTIONAL
  ```
If the optional parameters are not passed, they will be automatically be produced for you and you will be able to find them in the "preprocessingOUTPUT" folder.

- #### Bam files  

```
--bam_folder "/path/to/folder/where/bam/files/are"            REQUIRED
```
In case only some specific files inside the BAM folder should be used as input, a file prefix can be defined by: 
```
--bam_file_prefix MYPREFIX
```


All the BAM files on which the variant calling should be performed should be all stored in the same folder. 

**! TIP** 
All the input files can be used in s3 buckets too and the s3://path/to/files/in/bucket can be used instead of a local path.

## Output

The output can be found the Result folder under: 
```
Results/calling_output.vcf
```


## References:

* **Strelka2**
  * [GitHub](https://github.com/Illumina/strelka)
  * [Publication](https://www.biorxiv.org/content/early/2017/09/25/192872)
  * DockerContainer: [lifebitai/strelka2](https://hub.docker.com/r/lifebitai/strelka2/)
