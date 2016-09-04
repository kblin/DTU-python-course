---
title: "Biopython"
teaching: 15
exercises: 15
questions:
- "How do I handle sequence files?"
objectives:
- "Use Biopython to parse and write sequence files"
- "Get to know other useful Biopython components"
keypoints:
- "FIXME"
---
## What is Biopython

Biopython is a collection of freely available Python tools for computational molecular biology.
It has parsers (helpers for reading) many common file formats used in bioinformatics tools and databases
like BLAST, ClustalW, FASTA, GenBank, PubMed ExPASy, SwissProt, and many more. Biopython provides
modules to connect to popular on-line services like NCBI's Blast, Entrez and PubMed or ExPASy's Swiss-Prot,
UniProt and Prosite.

## Installing Biopython in Jupyter

1. Click on the `Conda` tab
2. Type "biopython" into the search box
3. Select the checkbox for biopython
4. Hit the arrow button to install
5. Wait

## Loading the Biopython library

Open a new notebook for this.

~~~
import Bio
print(Bio.__version__)
~~~
{: python}


## Parse a GenBank file

~~~
from Bio import SeqIO
records = SeqIO.parse('NC_03888.gbk', 'genbank')
~~~
{: python}

## The filetype is important

You always need to tell `SeqIO.parse` what kind of filetype it is supposed to read.
It will not guess the type from the file extension.

~~~
records = SeqIO.parse('NC_03888.gbk')
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-6-d92ec57b2f34> in <module>()
----> 1 records = SeqIO.parse('NC_03888.gbk')

TypeError: parse() missing 1 required positional argument: 'format'
~~~
{: python}


## Exploring the record

~~~
for record in records:
    print(record)
~~~
{: python}
