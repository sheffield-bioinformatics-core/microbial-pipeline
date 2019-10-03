FROM ubuntu:18.04
MAINTAINER Mark Dunning<m.j.dunning@sheffield.ac.uk>
RUN rm -rf /var/lib/apt/lists/*
ENV DEBIAN_FRONTEND=noninteractive 
RUN apt-get update  && apt-get install --fix-missing -y git wget unzip emboss bioperl ncbi-blast+ gzip libjson-perl libtext-csv-perl libfile-slurp-perl liblwp-protocol-https-perl libwww-perl liblzma-dev abyss subversion libdatetime-perl libxml-simple-perl libdigest-md5-perl git default-jre bioperl bowtie2 samtools bwa default-jre build-essential python3.6 python3.6-dev python-dev zlib1g-dev curl libbz2-dev emboss bioperl libjson-perl libtext-csv-perl libfile-slurp-perl liblwp-protocol-https-perl libwww-perl roary python3 python3-distutils libdatetime-perl libxml-simple-perl libdigest-md5-perl git default-jre bioperl mercurial
WORKDIR /opt
RUN wget http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.3.zip -P /opt
RUN unzip fastqc_v0.11.3.zip
RUN chmod 755 FastQC/fastqc
RUN ln -s /opt/FastQC/fastqc /usr/bin

## Cutadapt (required by trim galore)

RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
RUN pip install multiqc
RUN pip install cython
RUN pip install --user --upgrade cutadapt
RUN ln -s ~/.local/bin/cutadapt /usr/bin

## bcftools

RUN git clone git://github.com/samtools/htslib.git
RUN git clone git://github.com/samtools/bcftools.git
WORKDIR bcftools
RUN make 
RUN make install

## Trim Galore

WORKDIR /opt/
RUN curl -fsSL https://github.com/FelixKrueger/TrimGalore/archive/0.6.0.tar.gz -o trim_galore.tar.gz
RUN tar xvzf trim_galore.tar.gz
RUN ln -s /opt/TrimGalore-0.6.0/trim_galore /usr/bin

## bam2fastq
RUN git clone --recursive https://github.com/jts/bam2fastq
WORKDIR bam2fastq
RUN make
RUN ln -s /opt/bam2fastq/bam2fastq /usr/bin

## WeeSam
## FIXME
WORKDIR /opt
RUN git clone https://github.com/centre-for-virus-research/weeSAM.git
RUN pip install pysam
RUN ln -s /opt/weeSAM/weeSAM /usr/bin

## LoFreq

RUN wget -O lofreq-2.1.2.tgz https://sourceforge.net/projects/lofreq/files/lofreq_star-2.1.2_linux-x86-64.tgz/download
RUN tar zxvf lofreq-2.1.2.tgz
RUN mkdir /usr/bin/lofreq
RUN ln -s /opt/lofreq-2.1.2/bin/ /usr/bin

## Diversi tools
## FIXME
RUN git clone https://github.com/josephhughes/DiversiTools.git
RUN ln -s /opt/DiversiTools/bin/* /usr/bin

## ClustalW

RUN wget ftp://ftp.ebi.ac.uk/pub/software/clustalw2/2.1/clustalw-2.1-linux-x86_64-libcppstatic.tar.gz
RUN tar zxvf clustalw-2.1-linux-x86_64-libcppstatic.tar.gz
RUN ln -s /opt/clustalw-2.1-linux-x86_64-libcppstatic/clustalw2 /usr/bin

## RAxML
RUN wget http://ftp.debian.org/debian/pool/main/r/raxml/raxml_8.1.1.orig.tar.xz
RUN tar xf raxml_8.1.1.orig.tar.xz
WORKDIR standard-RAxML-8.1.1
RUN make -f Makefile.gcc
## FIXME
#RUN ln -s /opt/standard-RAxML-8.1.1/raxmlHPC /usr/bin

## Kraken
WORKDIR /opt
RUN git clone https://github.com/DerrickWood/kraken2.git
WORKDIR kraken2
RUN ./install_kraken2.sh /usr/bin/


## SPADES

WORKDIR /opt/
RUN wget http://cab.spbu.ru/files/release3.13.1/SPAdes-3.13.1-Linux.tar.gz
RUN tar zxvf SPAdes-3.13.1-Linux.tar.gz
RUN ln -s /opt/SPAdes-3.13.1-Linux/bin/* /usr/bin

## Mira

RUN wget -O mira_4.0.2.tar.bz2 https://sourceforge.net/projects/mira-assembler/files/MIRA/stable/mira_4.0.2_linux-gnu_x86_64_static.tar.bz2/download
RUN bzip2 -d mira_4.0.2.tar.bz2
RUN ln -s /opt/mira_4.0.2_linux-gnu_x86_64_static/bin/* /usr/bin

## QUAST

RUN wget -O quast-5.0.2.tar.gz https://sourceforge.net/projects/quast/files/quast-5.0.2.tar.gz/download
RUN tar zxvf quast-5.0.2.tar.gz 
WORKDIR quast-5.0.2/
RUN ./install.sh
RUN ln -s /opt/quast.py /usr/bin

## scaffold builder

WORKDIR /opt
RUN git clone https://github.com/metageni/Scaffold_builder.git
RUN ln -s /opt/Scaffold_builder/scaffold_builder.py /usr/bin/scaffold_builder.py


## mummer

RUN wget https://github.com/mummer4/mummer/releases/download/v3.9.4alpha/mummer-3.9.4alpha.tar.gz
RUN tar zxvf mummer-3.9.4alpha.tar.gz
WORKDIR mummer-3.9.4alpha
RUN ./configure --prefix=/opt/mummer
RUN make
RUN make install


## RATT

WORKDIR /opt
RUN svn co "https://svn.code.sf.net/p/ratt/code/" ratt-code
ENV RATT_HOME=/opt/ratt-code

## prokka

RUN git clone https://github.com/tseemann/prokka.git prokka
RUN ln -s /opt/prokka/bin/prokka /usr/bin

## Artemis

RUN wget -O artemis-18.0.2.tar.gz https://github.com/sanger-pathogens/Artemis/releases/download/v18.0.2/artemis-unix-release-18.0.2.tar.gz
RUN tar zxvf artemis-18.0.2.tar.gz

## MetAMOS
## FIXME
RUN git clone https://github.com/marbl/metAMOS.git

## Ribopicker

RUN wget -O ribopicker-0.4.3.tar.gz https://sourceforge.net/projects/ribopicker/files/standalone/ribopicker-standalone-0.4.3.tar.gz/download
RUN tar zxvf ribopicker-0.4.3.tar.gz
RUN ln -s /opt/ribopicker-standalone-0.4.3/ribopicker.pl /usr/bin

## GARM
## FIXME
RUN wget -O GARM_v0.7.5.tar.gz https://sourceforge.net/projects/garm-meta-assem/files/GARM_v0.7.5.tar.gz/download
RUN tar zxvf GARM_v0.7.5.tar.gz

## MetaPhlan
RUN hg clone https://bitbucket.org/nsegata/metaphlan

## Diamond
RUN wget http://github.com/bbuchfink/diamond/releases/download/v0.9.24/diamond-linux64.tar.gz
RUN tar xzf diamond-linux64.tar.gz
RUN ln -s /opt/diamond /usr/bin

## Krona Tools

RUN wget https://github.com/marbl/Krona/releases/download/v2.7.1/KronaTools-2.7.1.tar
RUN tar xvf KronaTools-2.7.1.tar
WORKDIR KronaTools-2.7.1
RUN ./install.pl

WORKDIR /opt


## Trimmomatic

RUN wget http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/Trimmomatic-0.36.zip
RUN unzip Trimmomatic-0.36.zip
ENV TRIMMOMATIC /opt/Trimmomatic-0.36/trimmomatic-0.36.jar

## Abricate

RUN git clone https://github.com/tseemann/abricate.git
RUN ln -s /opt/abricate/bin/abricate /usr/bin

## Snippy

RUN git clone https://github.com/tseemann/snippy.git
RUN ln -s /opt/snippy/bin/snippy /usr/bin

## Unicycler

RUN git clone https://github.com/rrwick/Unicycler.git
WORKDIR Unicycler
RUN apt-get install -y python3 python3-distutils
RUN python3 setup.py install
WORKDIR /opt

## breseq

RUN wget https://github.com/barricklab/breseq/releases/download/v0.33.2/breseq-0.33.2-Linux-x86_64.tar.gz
RUN tar zxvf breseq-0.33.2-Linux-x86_64.tar.gz
RUN ln -s ${pwd}/breseq-0.33.2-Linux-x86_64/bin/breseq /usr/bin
RUN ln -s ${pwd}/breseq-0.33.2-Linux-x86_64/bin/gdtools /usr/bin

## MOST


WORKDIR /opt
RUN wget https://github.com/samtools/samtools/archive/0.1.18.tar.gz
RUN tar zxvf 0.1.18.tar.gz
WORKDIR samtools-0.1.18
RUN make
RUN ln -s /opt/samtools-0.1.18/samtools /usr/bin/samtools-0.1.18


WORKDIR /opt
RUN git clone https://github.com/phe-bioinformatics/MOST.git
RUN pip install biopython
RUN pip install lxml

## Clean-up and zips and tar.gz

RUN rm /opt/*.tar.gz
RUN rm /opt/*.zip
RUN rm /opt/*.tar
RUN rm /opt/*.tgz
RUN rm /opt/*.xz

WORKDIR /home
