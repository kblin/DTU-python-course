---
title: "Biopython"
teaching: 10
exercises: 10
questions:
- "How do I handle sequence files?"
objectives:
- "Use Biopython to parse and write sequence files"
- "Get to know other useful Biopython components"
keypoints:
- "Install and load Biopython"
- "Use Biopython to load sequence files"
- "Work with sequence records"
- "Convert formats"
- ""
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
records = SeqIO.parse('data/Streptomyces_coelicolor.gbk', 'genbank')
~~~
{: python}

## The filetype is important

You always need to tell `SeqIO.parse` what kind of filetype it is supposed to read.
It will not guess the type from the file extension.

~~~
records = SeqIO.parse('data/Streptomyces_coelicolor.gbk')
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-6-d92ec57b2f34> in <module>()
----> 1 records = SeqIO.parse('data/Streptomyces_coelicolor.gbk')

TypeError: parse() missing 1 required positional argument: 'format'
~~~
{: python}


## Exploring the record

Printing a record will give you some summary information on it.

~~~
for record in records:
    print(record)
~~~
{: python}


## `SeqIO.parse()` returns a generator function, not a list

If you run the previous loop again, you will not get any output.
This is because the return value of `SeqIO.parse()` is a so-called generator function.
In many ways a generator function works like a list, but it genrates the results on the fly.
This is beneficial for large input files where you don't want to keep the whole file in memory.

You have used generator functions before: `range()` is a generator function as well.

> ## Tip: If you need to iterate over your records multiple times, convert the generator to a list
> ```python
records = list(SeqIO.parse('data/Streptomyces_coelicolor.gbk', 'genbank'))
```
{: .callout}
