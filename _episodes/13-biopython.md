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
- "Write new records with your own content"
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

## Records have a number of fixed and variable annotations

Every record has an `id`, a `name`, and a `description`, though they might be set to "unknown".
Additionally, the `annotations` attribute contains a dictionary of further annotations.

~~~
print(coelicolor.name)
print(coelicolor.id)
print(coelicolor.description)
print(coelicolor.annotations)
~~~
{: .python}
~~~
NC_003888
NC_003888.3
Streptomyces coelicolor A3(2) chromosome, complete genome.
{'sequence_version': 3, 'accessions': ['NC_003888'], 'data_file_division': 'CON', 'source': 'Streptomyces coelicolor A3(2)', 'references': [Reference(title='Comparative genomics of Streptomyces avermitilis, Streptomyces cattleya, Streptomyces maritimus and Kitasatospora aureofaciens using a Streptomyces coelicolor microarray system', ...), Reference(title='Complete genome sequence of the model actinomycete Streptomyces coelicolor A3(2)', ...), Reference(title='A set of ordered cosmids and a detailed genetic and physical map for the 8 Mb Streptomyces coelicolor A3(2) chromosome', ...), Reference(title='Direct Submission', ...), Reference(title='Direct Submission', ...)], 'keywords': ['RefSeq', 'complete genome'], 'organism': 'Streptomyces coelicolor A3(2)', 'gi': '32141095', 'date': '17-DEC-2014', 'taxonomy': ['Bacteria', 'Actinobacteria', 'Actinobacteridae', 'Actinomycetales', 'Streptomycineae', 'Streptomycetaceae', 'Streptomyces', 'Streptomyces albidoflavus group'], 'comment': 'REVIEWED REFSEQ: This record has been curated by NCBI staff. The\nreference sequence was derived from AL645882.\nOn Jun 22, 2003 this sequence version replaced gi:31340543.\nRefSeq Category: Reference Genome\n            MOD: Model Organism\n            UPR: UniProt Genome\nCOMPLETENESS: full length.'}
~~~
{: .output}

## Records can also contain features

Features are sequence features annotated in the record file, if present.

~~~
print(coelicolor.features[:10])
~~~
{: .python}
~~~
[SeqFeature(FeatureLocation(ExactPosition(0), ExactPosition(8667507), strand=1), type='source'), SeqFeature(FeatureLocation(ExactPosition(0), ExactPosition(21653), strand=1), type='misc_feature'), SeqFeature(FeatureLocation(ExactPosition(434), ExactPosition(440), strand=1), type='regulatory'), SeqFeature(FeatureLocation(ExactPosition(445), ExactPosition(1123), strand=1), type='gene'), SeqFeature(FeatureLocation(ExactPosition(445), ExactPosition(1123), strand=1), type='CDS'), SeqFeature(FeatureLocation(ExactPosition(1237), ExactPosition(1243), strand=1), type='regulatory'), SeqFeature(FeatureLocation(ExactPosition(1251), ExactPosition(3813), strand=1), type='gene'), SeqFeature(FeatureLocation(ExactPosition(1251), ExactPosition(3813), strand=1), type='CDS'), SeqFeature(FeatureLocation(ExactPosition(3868), ExactPosition(6220), strand=1), type='gene'), SeqFeature(FeatureLocation(ExactPosition(3868), ExactPosition(6220), strand=1), type='CDS')]
~~~
{: .output}


## Sequence features have multiple types

In theory, the allowed feature types are limited, in practice a lot of tools invent new types on the fly.

~~~
for feature in coelicolor.features[:10]:
    print(feature.type)
~~~
{: .python}
~~~
source
misc_feature
regulatory
gene
CDS
regulatory
gene
CDS
gene
CDS
~~~
{: .output}

## Often you will be interested in only a few feature types

You can use a loop statement to filter out uninteresting features.

~~~
for feature in coelicolor.features[:10]:
    if feature.type != 'CDS':
        continue
    print(feature.type)
~~~
{: .python}
~~~
CDS
CDS
CDS
~~~
{: .python}

## Features have qualifiers

~~~
for feature in coelicolor.features[:10]:
    if feature.type == 'CDS':
        break
print('Type:', feature.type)
print('Qualifiers:', feature.qualifiers)
~~~
{: .python}
~~~
Type: CDS
Qualifiers: {'locus_tag': ['SCO0001'], 'note': ['SCEND.02c, unknown, doubtful CDS, len: 225aa'], 'translation': ['MTGHHESTGPGTALSSDSTCRVTQYQTAGVNARLRLFALLERRACPRARRTTWWPGRSARWWSWTAWRRLLGVCCVRGRLGRRRDGGERGPGGHRGPGLATARRRSGGATELAVHCADVRQRERADLVRLEGFVRESVLPRAHPHTTARRRVLEVLGEAGSLCTARTVNSDEDYILCTLGVGHYDPDDQPPFKDGKPGWQRAGASIWNGSGAACIPHAAIEGPRK'], 'protein_id': ['NP_624362.1'], 'gene_synonym': ['SCEND.02c'], 'product': ['hypothetical protein'], 'codon_start': ['1'], 'db_xref': ['GI:21218583', 'GeneID:1095448'], 'transl_table': ['11']}
~~~
{: .output}

## Qualifiers are lists

Even if qualifiers only exist once per feature, Biopython always treats them as lists

~~~
print(type(feature.qualifiers['locus_tag']))
~~~
{: .python}
~~~
<class 'list'>
~~~
{: .output}

## Features can extract their DNA sequence from the records Seq

This is great if you need the DNA sequence of a specific gene.

~~~
for feature in tropica.features[:10]:
    if feature.type != 'CDS':
        continue
    protein_seq = feature.extract(tropica.seq)
    print('>' + feature.qualifiers['locus_tag'][0])
    print(protein_seq)
~~~
{: .python}
~~~
>STROP_RS00005
GTGACGGATACAACCGACCTCGCCGCGGTGTGGACGGCAACGACCGACGAGTTGGCCGACGAGATCGTCTCTGCCCAGCAGCGGGCCTATCTGCGACTGACCCGCCTCCGCGCCATCGTCGAGGACACCGCGCTCGTCTCCGTCCCGGACGCCTTCACCCGAGATGTCATCGAGTCCCGGCTCCGCCCGGCGATCACCGAGGCCCTCACCCGCCGGCTGGGGCGCCCCATCCAGGTGGCGGTCACGGTGCGAGCACCGGAAGACGCCCCCGGCCGCCCGGCCGGCACCATCTACCACAGCGCCCCGAGCCCGGAGACCGGCGCGTTGCCCGGCGACACCACCGACCGCGCCGCGGGAGGGGGCCCGGACGACGGCGTGGACCACAGGTTCCCGCTGATCCCCGGGCAGGCCCAACCGGAGCGCCGCACTGCGGCGCCCGCTGGTTCGTACGGCGAGCAGACGACGCCGATGTCCCGGGACAGCCAGGAGCCGTTGTTCAGCTCCGCCTTCGCCGGGCCGCCCCGAGGCGAGCGTCACGATGTTGACGAGCAGGCCCGGCTGGGCCCACCGGTGACCGAACGCCCGTTCGAGGCCCACTACCGAGCAGAGGGGGCGGACCAGCACGGGGGGCGGGCCCTGCCCCGGGAACTCGGCACCGACAGCGGGCCGGGGAGGGTGGACCACCGACCGGGTGGCCGCGAGGACCGTCGGCCACCGGCACCCGCCGACGGCGGCGGCAACCGGCTCAACCCGAAGTACATGTTCGAGACGTTCGTTATCGGTTCGTCGAACCGATTCGCCCACGCGGCTTCGGTGGCGGTCGCCGAGTCACCGGCGAAGGCGTACAACCCGCTGTTCATCTACGGCAGCTCAGGGCTGGGCAAGACGCACTTGCTGCACGCGATCGGCCACTACGCCACGACGCTCGGCAACGCCAACTCGGTCCGGTACGTCTCGACCGAGGAGTTCACCAACGACTTCATCAACTCGCTGCGCGACGACAAGACCAGCGCCTTCCAGCGCCGGTACCGGGACGTCGACATCCTCCTGATCGACGACATCCAGTTCCTGGAGAACCGGGAGCGGACGCAGGAGGAGTTCTTCCACACCTTCAACACACTGCACAACGCCAACAAGCAGATCGTGATCACCTCCGACCGGTCGCCGAAGCAGCTGGCGACTCTGGAGGACCGGCTGCGGACCCGGTTCGAATGGGGCCTACTCGCCGACATCCAGCCGCCAGACCTGGAGACCCGGATCGCGATCCTCCAGAAGAAAGCCGCCCAGGAACGGCTGTTCGCCCCGCCGGACGTACTGGAGTTCATTGCGTCCCGAGTGTCGAACTCCATCCGAGAACTTGAGGGTGCGCTGATCCGGGTCACCGCGTTCGCCAGCCTCACCCGGTCATCGGTGGAGTTGTCGCTGGCCGAGGAGGTGCTGCGGGACTTCATTCCGGACGGCACCGGGCCAGAGATCACCGCCGACCAGATCATGGTTGCCACCGCCGACTACTTCGGGGTGAGTCTGGAGGACCTGCGCGGGCACTCCCGCTCGCGGGTGCTCGTCAACGCCCGCCAGGTCGCCATGTACCTGTGCCGGGAGCTCACCGACCTGTCGCTGCCCCGAATCGGACAGGCGTTCGGGGGCCGCGACCACACCACGGTCATGCACGCCGACCGCAAGATCCGTCAGCAGATGGCCGAGCGCCGGTCGCTCTACAACCAGATCGCCGAGCTGACCAACCGGATCAAGCAGAACACCTGA
>STROP_RS00010
ATGAAGTTCCGAGTAGAGCGCGACGCGCTCGCCGAGGCCGTGGCCTGGACCGCGAAAAGCCTGCCGAACCGGCCGTCGGTGCCGGTGCTCGCCGGTGTGCTGCTGCGGGTCACCGACGGCAACCTGCAGGTCTCCGGCTTCGACTACGAGGTCTCCAGCCAGGTGACCGTCGAGGTGCAGGGGGACGCCGACGGCGCCACCCTGGTCTCCGGCCGGCTCCTCGCCGAGATCACCAAGGCGCTGCCGGCGAAACCGGTCGACATCGCGGCGGTCGGCGCTCATCTCGAACTCGTCTGCGGCAGCGCCCGCTTCACTCTGCCCACCATGCCGGTCGAGGACTACCCCACCCTCCCGGAGATGCCGGTCAGCGCTGGCACCATCGACGCCGCCGCGTTCGCCGCCGCCGTTGCCCAGGTAGCCGTGGCAGCCGGCCGGGACGAGACCCTGCCGATGATGACCGGCGTCCGGCTGGAGCTCTCCGGCGGCACGTTGGCCATGCTCGCCACCGATCGCTACCGCCTCGCCCTGCGCGAGATCGAGTGGAACCCGGAAGACCCGGAGATCAGCCTCAACGCGCTGGTACCGGCCCGCACGCTGCATGACACCGCCAAGGCCCTGGGGCCGCTCGGCGGTCAGGTAACCATGGCGCTCTCCCAGGGAGCGGCGGGTGAGGGCATGATCGGTTTTGTCGGCGGCCCCCGCCGCACCACCAGCCGACTGCTTGACGGCGCCAACTACCCGCCGGTGCGCTCCCTCTTCCCCGCCACCCAGAACGCGCAGGCCCAGGTCCCGGTCAGCGCGCTCATCGAGGTCGTCAAGCGGGTCGCGCTCGTCGCCGAACGCACCACTCCGGTGCTGCTGAGCTTCAGCGACGACGGACTGGTGGTCGAGGCCGGTGGCACCGAGGAGGCGCGCGCCAGCGAGGCGATGGAGGCCACCTTCAGCGGTGATCCGCTGACCATCGGCTTCAACCCCCAGTACCTGATCGACGGTCTCTCGAACATGGGGACCCAGTTCGCCGTTCTGTCGTTCGTCGACGCCTTCAAGCCGGCGGTGATTTCTCCCGTCGGCGAGGATGGCGAGGTCGTGCCCGGGTATCGCTACCTCATCATGCCGATCCGCGTTTCCCGCTGA
>STROP_RS00015
ATGCAGCTCGGCCTGGTAGGGCTCGGCCGCATGGGCGGCAACATGCGTGAGCGGCTGCGCGCCGCTGGGCATGAGGTGATCGGGTACGACAACCAGGCCGAGCTGAGCGACGTCGCGAGCCTGGCGGAGATGGCGAAGAAGCTGGACGCGCCCCGCGCAGTGTGGGTCATGGTCCCTGCCGCCGTCACCGACGAGACCATCACCAAGCTGGCGGAGGTGCTCGACACCGGCGACATCATCGTTGACGGCGGAAACTCGCGGTTCAGCGACGATGCCCCGCGCGCCGAGCGGCTGAACGAGCGCGGCATTGGGTACGTCGATGCCGGGGTTTCCGGGGGCGTTTGGGGCCGACAGAACGGGTACGCCCTCATGGTCGGCGGTGCCAAGGAACACGTTGACCGACTGATGCCGATCTTCGAGGCGCTCAAGCCGGCCGGAGAATTCGGCTTCGTGCACGCCGGGCCGGTCGGTGCCGGACACTACGCCAAGATGGTGCACAACGGCGTCGAGTACGGTCTCATGCACGCCTACGCCGAGGGCTACGAACTGCTCGCCAAGTCCGAGCTGGTCACCGATGTCCCCGGCGTCTTCAAGTCGTGGCGGGAGGGCACGGTCGTCCGCTCCTGGCTGCTCGACCTCCTCGACCGTGCTCTCGACGAGGACCCGAAGCTGGCCGAGCTGAGCCCCTACACGGAGGACACCGGCGAGGGTCGGTGGACCGTGGACGAGGCGGTCCGACTCGCTGTTCCGATGAACGTCATCGCCGCCGCGCTCTTCGCCCGTTTCGCCTCCCGCCAGGACGACTCGCCCGCGATGAAGGCCGTCGCCGCGCTGCGCCAGCAGTTCGGCGGGCACGCCGTTCGCAAGCGCTGA
>STROP_RS00020
GTGTACGTTCGCCGGCTGGAACTCGTCGACTTCCGCTCGTACGAGCGGGTCGGCGTGGACCTCGAACCAGGGGCGAACGTCCTGGTCGGTCCGAACGGGGTCGGCAAGACCAACCTGATCGAGGCGCTCGGCTACGTGGCGACCCTGGACTCCCACCGGGTCGCCACTGACGCCCCGCTGGTCCGGATGGGTGCCGCCGCGGGGATCATTCGCTGCGCCGTGGTGCATGAGGGCCGGGAGCTACTGGTCGAGTTGGAGATCGTTCCGGGGCGGGCCAACCGGGCCCGGCTCGGTCGGTCCCCGGCCCGGCGGGCCCGGGACGTCCTCGGTGCCCTGCGGCTGGTGCTCTTTGCCCCAGAGGACCTGGAACTGGTCCGGGGCGACCCGGCGCAGCGGCGCCGCTACCTCGACGATCTGCTGGTGCTCCGACAGCCCCGGTACGCCGGGGTGCGGACCGACTACGAGCGGGTGGTCCGGCAGCGGAACGCCCTGCTGCGCACCGCGTACCTGGCGCGCAAGACCGGTGGCACCCGCGGCGGCGACCTCTCCACGCTCGCGGTCTGGGACGACCACCTCGCGCGGCACGGCGCCGAGTTGCTCGCGGGTCGGCTCGACCTCGTCGCCGCGCTCGCCCCCCACGTCAACCGGGCGTACGACGCGGTGGCCGCGGGTGCGGGCGCCGCTGGCATCGCCTACCGGTCGTCGGTCGAGCTGGCCAGTTCGACCGCGGACCGGGCGGACCTGACCGCGGCGCTGAGCGACGCGCTCGCCGCCGGCCGCACAGCCGAGATCGAGCGGGGGACCACCCTGGTCGGCCCGCACCGGGACGAGCTCACCCTGACTCTGGGGCCACTGCCCGCGAAGGGGTACGCCAGCCACGGCGAGTCCTGGTCGTTCGCGCTGGCACTCCGGCTCGCCGGGTACGACCTGCTGCGCGCTGACGGGATCGAGCCGGTGTTGGTGCTGGATGACGTCTTCGCCGAACTGGACACCGGCCGGCGGGATCGCCTCGCCGAGTTGGTCGGTGACGCGAGCCAACTCCTGGTGACCTGCGCGGTGGAGGAGGATCTCCCCGCGCGTCTGCGCGGAGCGCGATTCGTTGTCCGCGAGGGAGAGGTACAGCGTGTCGGATGA
~~~
{: .output}


## File output

Biopython can also write SeqRecord objects into files again.

~~~
SeqIO.write([coelicolor], 'coe.gbk', 'genbank')
~~~
{: .python}

## Use this for sequence conversion

If you need to convert sequences from one file format to another, Biopython often is a quick way to do it.

~~~
records = SeqIO.parse('data/Streptomyces_coelicolor.gbk', 'genbank')
SeqIO.write(records, 'Streptomyces_coelicolor.embl'¸ 'embl')
~~~
{: .python}

> ## Load files
> Fill in the blanks to load two files
> ~~~
> from Bio import ____
> coelicolor = list(SeqIO.parse('data/Streptomyces_coelicolor.gbk', ____))[0]
> tropica = ____(_____('data/Salinispora_tropica_CNB_440.gbk', _____))[0]
> ~~~
> {: .python}
{: .challenge}
> ## File conversion
> Fill in the blanks to convert an EMBL format file to FASTA
> ~~~
> records = SeqIO.____('data/Streptomyces_coelicolor.embl', _____)
> SeqIO.____(records, 'Streptomyces_coelicolor.fa'¸ ____)
> ~~~
> {: .python}
{: .challenge}
