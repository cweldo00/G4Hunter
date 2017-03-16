# G4Hunter
App related to G4Hunter published in [Bedrat et al NAR 2016][paper ref].  
Supplementary Data can be downloaded from [here](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC4770238/bin/supp_44_4_1746__index.html).  
The EF184640.1.fa corresponds to the human mitochondrial genome used in the publication.

The app requires the following packages:
* Biostrings
* GenomicRanges
* (S4Vectors)
* (shiny)

The file to download has to be a **single** fasta file that do not exceeds the size limit imposed by Shiny (default is 5Mb, see below how to change it).  
Letters in the sequence have to belong the the DNA alphabet (A,C,T,G,M,R,W,S,Y,K,V,H,D,B,N). Gaps (- or .) and hard masking (+) are also accepted.  
The first line of the fasta file (after the > sign) imposes the sequence name (seqname) in the output. This can be changed by checking the **Alternate Seqname** option and entering the chosen sequence name in the **New Seqname** option.

The _Threshold_ and _Window size_ fixe the parameters for the sequence search as described in the [publication][paper ref].  
Pleas check that the **Length of the Input Sequence** corresponds to the length of the DNA sequence you enter with your Fasta file.

The output table contains the sequence name (**seqnames**), the **start**, **end** and **width** of the _refined_ sequences, that meet the search criteria.  
The **strand** is **+** if the proposed G4 forming sequence is in the Input Sequence and this is set to **-** if the G4 forming sequence in on the reverse complementary strand.  
The **score** is the G4Hunter score of the _refined_ sequence and **max_score** is the highest score in absolute value in a window of the chosen **window size** for the sequence.  
**hl** and **k** are respectively the **Threshold** and **Window size** used for the search.  
The **sequence** correspond the the _refined_ sequence in the **Input file**.  
Please note that the procedure extracts sequences that have a G4Hunter score above the threshold in a window, fuses the overlapping sequences and then _refine_ theses sequences by removing bases at the extremities that are not G for sequences with a positive score (or C the negative ones). It also looks at the first neigbouring base and adds it to the sequence if it is a G for sequences with a positive score (C for sequences with a negative score).  
Please see the [pulbication][paper ref] and Figure S1B for more details


--------------------------------------------------------------------------
As this is a simple Shiny app, there is a limit to the size you can upload (5Mb).  
If necessary (but might not be good for the host), the size limit can be increased  to XX Mb by adding  
```{r}
options(shiny.maxRequestSize=XX*1024^2)
```
at the top of the server.R file  
_adapted [from stackoverflow](http://stackoverflow.com/questions/18037737/how-to-change-maximum-upload-size-exceeded-restriction-in-shiny-and-save-user)_  


[paper ref]:http://doi.org/10.1093/nar/gkw006
