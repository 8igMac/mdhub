Bioinformation
===

> Introduction to NGS and alignment problem tutorial by Ben Langmead, 
click [here](https://www.youtube.com/watch?v=hpb-mH-yjLc&index=1&list=\
PL2mpR0RYFQsBiCWVJSvVAO3OJ2t7DzoHA) to watch.

### Table of content
- [Next Generation Sequencing](#sequencing)
- [Alignment](#align)
    - [Exact match](#exact_match)
        - Online algorithm
            - [Naive Exact Match](#naive_exact_match)
            - [Boyer-Moore](#boyer_moore)
        - Offline algorithm: [Preprocess Reference Genome - Indexing](#preprocess)
            - [K-mer Index](#k-mer)
            - [Suffix Index](#suffix_index)
    - [Approximate matching](#approximate_match)
        - [Pigeonhole Principle](#pigeonhole)
        - [Use Dynamic Programming and Edit Distance](#dynamic_prog)
    - [ToDo](#todo)
- [Assembly](#assembly)
    - [Shortest Common Suffix](#short_common_superstring)
        - [Naive Solution](#scs_naive)
        - [Overlaps Graph Based - Greedy Solution](#scs_greedy)
    - [De Bruijn Graph Based - Eulerian Walk](#de_bruijn)


<a name="sequencing"></a>
# Next Generation Sequencing
**to-do**

<a name="align"></a>
#  Alignment and Alignment Algorithm
**to-do**
- repetitive genome cause ambiguity to alignment

<a name="exact_match"></a>
## Exact match

<a name="naive_exact_match"></a>
### Naive Exact Match

<a name="boyer_moore"></a>
### Boyer-Moore
- Improved version of naive exact match that learn from chracter compa
risons to skip pointless alignment
- start match read to reference from left-to-right. Do comparison from right-to-left.
- the **bad chracter rule**
- the **good suffix rule**
- take the max of the two rules is the amount we skip

<a name="preprocess"></a>
## Preprocess Reference Genome - Indexing
The work is amortized, i.e. the extra work is worth it.
It is a offline algorithm (the algorithm start working unpon
receiving entire input).

Genome are just like a book, we will make a table of content (the index)
for the book so that the query time will be reduced. So we can reduce
the alignment time by preprocessing the reference genome, i.e. indexing
the reference genome. Another way of thinking about indexing reference 
genome is to think of it as a grocery store, everytime you go to a grocery
store you know where to pick up the milk or the fruit because the items 
were groups into aisles.

<a name="k-mer"></a>
### K-mer Index
make a index consist of substring of length k, can use hash table or ordered index + binary search 
to implement.
Variation: 
1. build k-mer only on even index -> can save space, and binary search time, but pattern
needed to be match needs to match both odd and even query.
2. take subsequence instead to substring to build the index (increase the chance of index hit).

<a name="suffix_index"></a>
### Suffix Index
- **suffix tree**: concept of grouping (grossary store), take roughly **45GB** 
to build on a human genome.
- **suffix array**: take roughly **12GB** to build on a human genome.
- **fm-index**(base on BWT): most space efficient, take roughly **1.5GB** 
to build on a human genome. used in **bowtie family** (bowtie, bowtie2), 
and **bwa family** (bwa, bwa-sw, bwa-mem) reads alignment tool.

<a name="approximate_match"></a>
## Approximate matching
Why need approximate matching
- due to sequencing error
- due to individual difference (0.1% difference)


<a name="pigeonhole"></a>
### Pigeonhole Principle
use exact-match algorithm on approximate matching by divede the reads into n+1 substring, 
then at least one substring is going to exact match the reference string.

<a name="dynamic_prog"></a>
### Use Dynamic Programming and Edit Distance
- don't depend on exact-match algorithm
- solve global alignment and local alignment

#### Edit distance vs Hamming distance
**substitution**: i.e. mismatch  
**insertion**: extra base  
**deletion**: gaps  

- hamming distance: only allowe substitution
- edit distance: allow all three kinds of transformation (use deletion to allow difference length)
- **theorem: Two string X and Y with equal length, editDistance(X, Y) <= hammingDistance(X, Y)**
- **theroem: Two string X and Y with different length, editDistance(X, Y) >= | len(X)-len(Y) |**

#### Use Dynamic Programming to Solve Edit Distance
> This method is same as using dynamic programing to solve LCS(Longest Common Substring)

#### Use Dynamic Programming to Approximate match
- **Smith-Waterman** with panalty 1
- **time complexity is O(mn), so it is impractical to use, often combine with indexing
or pigeonhole principle.**

#### Global alignment
The task of aligning one string to another string (they maybe difference in length)
- human transition(A->G, C->T) to transversion(other) is 2:1, i.e. transition is more 
likely to happened than transversion, so **transversion penalty should be greater**.
- substituion rate is 0.001 and indel (insertion and deletion) rate is 0.00033, so **indel 
should have greater penalty than substitution.**
- **Penalty matrix**
- find **min score** in dynamic programming table

#### Local alignment
Find the most similar pair of **substring** from string X and Y.
- penalty matrix: give positive score if matched, other wise give negative score.
- find **max score** in dynamic programming table
- **Smith-Waterman** algorithm

<a name="todo"></a>
## ToDo
BWT+fm-index
- BWA
- Bowtie
- SOAP2

other
- BLAST


<a name="assembly"></a>
# Assembly
De Novo (Shutgun) assembly
- solve jiksol pazzle without reference picture (hints)
- origin construction of the Human Genome Project

**coverage**: numbers of layers of overlaps

**Fist law of assembly**: If a suffix of read A is similar to a prefix of read B
then A and B might overlap in the genome.
**Second law of assembly**: More coverage means more overlaps
**Third law of assembly**: Repeat make genome diffcult (impossible) to assembly. 
(In facts, half of the genome is repeatetive)


**Overlap graph**: a directed graph idicates the sequence of a groups of overlaps
reads, the number on the edge means the length of the overlaps (can have certain 
thredhold)

assembly problem is related to graph problem, **that is to find certain order of
the traversal of the overlaps graph.**

<a name="short_common_superstring"></a>
## Shortest Common Superstring
Find the shortest string that contains all the strings in a set given.
- It is a NP-Complete problem (don't have efficient algorithm)
- **Don't work on repeatetive genome.** Can't tell how many copy on the
genome.

<a name="scs_naive"></a>
### Naive Solution
```
for each permutation of all the permutation of the set of strings do
    skips the overlaps prefix and add the rest of the char to the output string
```
this algorithm will have a time complexity of T(n!) with n equals to the 
size of the set of strings

<a name="scs_greedy"></a>
### Overlap Graph Greedy Solution
- Starting from the overlaps graph, pick the maxinum edge and merge the node
- faster than naive solution
- solution not optimal    


<a name="de_bruijn"></a>
## De Bruijn Graph Based - Eulerian Walk
- try to solve repeatetive problem of shortest common superstring
- Directed multi graph
- Eulerian walk

1. build De Bruijn graph
2. Take a Eulerian walk to reconstruct

**problem: the reconstruction of repeatetive sequence may not be unique**, can't 
break the third law of assembly.

### De Bruijn Graph in Practice
Reason of big and messy De Bruijn graph
1. sequencing error
2. Extra inferable edge
3. Polyploidy (difference of the same copy of chromosone, one from father, another from mother)
4. Repeatetive DNA 

How to deal with this?
- chop the result genome, output the correct, unambiguous result first
- make reads longer to overcome repeatetive patern, but it is difficult to do, so there
goese **paired-end** reads which also give us more information (hints).







