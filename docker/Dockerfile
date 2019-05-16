FROM ubuntu:18.04
MAINTAINER Mark Dunning<m.j.dunning@sheffield.ac.uk>
RUN rm -rf /var/lib/apt/lists/*
RUN apt-get update 
RUN apt-get install --fix-missing -y git wget unzip
WORKDIR /tmp
RUN wget http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.3.zip -P /tmp
RUN unzip fastqc_v0.11.3.zip
RUN chmod 755 FastQC/fastqc
RUN ln -s $(pwd)/FastQC/fastqc /usr/bin/fastqc
RUN apt-get install -y bowtie2 samtools bwa default-jre build-essential python3.6 python3.6-dev python-dev zlib1g-dev curl libbz2-dev

## Cutadapt (required by trim galore)

RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
RUN pip install multiqc
RUN pip install cython
RUN pip install --user --upgrade cutadapt

## bcftools

RUN apt-get install -y liblzma-dev
RUN git clone git://github.com/samtools/htslib.git
RUN git clone git://github.com/samtools/bcftools.git
WORKDIR bcftools
RUN make 
RUN make install

## Trim Galore

WORKDIR /tmp/
RUN curl -fsSL https://github.com/FelixKrueger/TrimGalore/archive/0.6.0.tar.gz -o trim_galore.tar.gz
RUN tar xvzf trim_galore.tar.gz
RUN ln -s ${pwd}/TrimGalore-0.6.0/trim_galore /usr/bin/trim_galore

## bam2fastq
RUN git clone --recursive https://github.com/jts/bam2fastq
WORKDIR bam2fastq
RUN make
RUN ln -s ${pwd}/bam2fastq/bam2fastq /usr/bin/bam2fastq

## WeeSam

WORKDIR /tmp
RUN git clone https://github.com/centre-for-virus-research/weeSAM.git

## LoFreq

RUN wget -O lofreq-2.1.2.tgz https://sourceforge.net/projects/lofreq/files/lofreq_star-2.1.2_linux-x86-64.tgz/download
RUN tar zxvf lofreq-2.1.2.tgz
RUN ln -s ${pwd}/lofreq-2.1.2/bin/* /usr/bin

## Diversi tools

RUN git clone https://github.com/josephhughes/DiversiTools.git
RUN ln -s ${pwd}/DiversiTools/bin/* /usr/bin

## ClustalW

RUN wget ftp://ftp.ebi.ac.uk/pub/software/clustalw2/2.1/clustalw-2.1-linux-x86_64-libcppstatic.tar.gz
RUN tar zxvf clustalw-2.1-linux-x86_64-libcppstatic.tar.gz
RUN ln -s ${pwd}/clustalw-2.1-linux-x86_64-libcppstatic/clustalw2 /usr/bin/clustalw2

## RAxML
RUN wget http://ftp.debian.org/debian/pool/main/r/raxml/raxml_8.1.1.orig.tar.xz
RUN tar xf raxml_8.1.1.orig.tar.xz
WORKDIR standard-RAxML-8.1.1
RUN make -f Makefile.gcc
RUN ln -s ${pwd}/raxmlHPC /usr/bin

## Kraken
WORKDIR /tmp
RUN git clone https://github.com/DerrickWood/kraken2.git
WORKDIR kraken2
RUN ./install_kraken2.sh /usr/bin/

## abyss

RUN apt-get install -y abyss

## SPADES

WORKDIR /tmp/
RUN wget http://cab.spbu.ru/files/release3.13.1/SPAdes-3.13.1-Linux.tar.gz
RUN tar zxvf SPAdes-3.13.1-Linux.tar.gz
RUN ln -s ${pwd}/SPAdes-3.13.1-Linux/bin/* /usr/bin

## Mira

RUN wget -O mira_4.0.2.tar.bz2 https://sourceforge.net/projects/mira-assembler/files/MIRA/stable/mira_4.0.2_linux-gnu_x86_64_static.tar.bz2/download
RUN bzip2 -d mira_4.0.2.tar.bz2
RUN tar xvf mira_4.0.2
RUN ln -s ${tmp}/mira_4.0.2_linux-gnu_x86_64_static/bin/* /usr/bin

## QUAST

RUN wget -O quast-5.0.2.tar.gz https://sourceforge.net/projects/quast/files/quast-5.0.2.tar.gz/download
RUN tar zxvf quast-5.0.2.tar.gz 
WORKDIR quast-5.0.2/
RUN ./install.sh
RUN ln -s ${pwd}/quast.py /usr/bin/quast.py

## scaffold builder

WORKDIR /tmp
RUN git clone https://github.com/metageni/Scaffold_builder.git
RUN ln -s ${pwd}/Scaffold_builder/scaffold_builder.py /usr/bin/scaffold_builder.py


## mummer

RUN wget https://github.com/mummer4/mummer/releases/download/v3.9.4alpha/mummer-3.9.4alpha.tar.gz
RUN tar zxvf mummer-3.9.4alpha.tar.gz
WORKDIR mummer-3.9.4alpha
RUN ./configure --prefix=/usr/bin
RUN make
RUN make install


## RATT

WORKDIR /tmp
RUN apt-get install -y subversion
RUN svn co "https://svn.code.sf.net/p/ratt/code/" ratt-code
ENV RATT_HOME=${pwd}/ratt-code

## prokka

RUN apt-get install -y libdatetime-perl libxml-simple-perl libdigest-md5-perl git default-jre bioperl
#RUN cpan Bio::Perl
RUN git clone https://github.com/tseemann/prokka.git prokka
RUN ln -s ${pwd}/prokka/bin/prokka /usr/bin

## Artemis

RUN wget -O artemis-18.0.2.tar.gz https://github.com/sanger-pathogens/Artemis/releases/download/v18.0.2/artemis-unix-release-18.0.2.tar.gz
RUN tar zxvf artemis-18.0.2.tar.gz

## MetAMOS
RUN git clone https://github.com/marbl/metAMOS.git

## Ribopicker

RUN wget -O ribopicker-0.4.3.tar.gz https://sourceforge.net/projects/ribopicker/files/standalone/ribopicker-standalone-0.4.3.tar.gz/download
RUN tar zxvf ribopicker-0.4.3.tar.gz
RUN ln -s ${tmp}/ribopicker-standalone-0.4.3/ribopicker.pl /usr/bin
## GARM
RUN wget -O GARM_v0.7.5.tar.gz https://sourceforge.net/projects/garm-meta-assem/files/GARM_v0.7.5.tar.gz/download
RUN tar zxvf GARM_v0.7.5.tar.gz

## MetaPhlan

## Diamond

## Krona Tools
