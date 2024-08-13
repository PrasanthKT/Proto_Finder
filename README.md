## Protospacer_Finder
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

The CRISPR-Cas system represents one of the most significant breakthroughs in gene and genome editing over the past few decades. This system is guided by guide RNAs (gRNAs), which search for specific sequences known as Protospacer Adjacent Motifs (PAMs). These sequences enable gRNAs to locate and edit targets at precise locations within the genome. Each CRISPR-Cas system has its own unique PAM sequence to identify and edit target positions. For example, PAMs can be present either on the 3' end for Cas9 (NGG) or the 5' end for Cas12a (TTTV).

This project introduces a tool developed using Python that identifies protospacers for various CRISPR-Cas systems, essentially serving as a universal protospacer finder for all Cas Nucleases which have different PAMs. The primary objective of a CRISPR-Cas system is to accurately edit specific targets while minimizing off-target effects, which are critical in gene/genome editing. This tool can be used to locate protospacers for specific PAM sequences, at desired locations, and with defined protospacer lengths. Additionally, it can identify off-targets present in the genome, enhancing the precision of CRISPR-Cas gene editing.

The results from this tool can be used to design gRNAs (although this tool does not have features to rank gRNAs or predict their efficiency), it provides the number of off-targets present in the genome for each protospacer Sequence. These results can also be used to determine whether target regions are locate in intronic or exonic regions if you have the GTF/GFF format file of the genome.
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

##Packages/ Dependencies
1. Conda 24.7.1
2. Python 3.12.2
3. Biopython 1.84
4. BWA 0.7.18
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

##Usage
1. Clone the Repository/ Download all the .py files
2. Run the main.py file

Run: [Make sure you activate your conda environment that contains all the required pacakages/ dependencies]
```
python main.py 'fasta_file' 'pam_sequence' 'pam_location' 'protospacer_length' 'reference_genome' 'output_file'

```
1. fasta_file - Targer Gene Fasta file
2. pam_sequence - PAM Sequence of the Nuclease.
3. pam_location - Location of the PAM (either 3' or 5')
4. protospacer_length - Length of the Protospacer (ex: 20bp for Cas9 24bp for Cas12a)
5. reference_genome - Reference genome of the organism to find the off targets for each protospacer
6. output_file - Name of the Output file for the script to write.
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Example Run:
Run the intial script with very small gene and genome of Prochlorococcus. 

```
python main.py gene.fasta NGG 3prime 20 ref_genome.fasta Output.txt
```

Output:
```
  Protospacer         PAM Sequence    Matching Sequence       Off-Target Count
GTTCCCGTTACAATCCTTAC    AGG        GTTCCCGTTACAATCCTTACAGG 	1
ACAATCCTTACAGGATTCTT    AGG        ACAATCCTTACAGGATTCTTAGG 	1
CTTACAGGATTCTTAGGTTC    AGG        CTTACAGGATTCTTAGGTTCAGG 	1
AGAATTTTAAGCGAAGAACA    TGG        AGAATTTTAAGCGAAGAACATGG 	1
GCCGTTATTGAGAACGAATA    TGG        GCCGTTATTGAGAACGAATATGG 	1
GAGAACGAATATGGAGAAGT    TGG        GAGAACGAATATGGAGAAGTTGG 	1
GGAGAAGTTGGAATTGACCA    AGG        GGAGAAGTTGGAATTGACCAAGG 	1
AGTTGGAATTGACCAAGGAT    TGG        AGTTGGAATTGACCAAGGATTGG 	1
GAAGTATTTGAAATGTCTAA    TGG        GAAGTATTTGAAATGTCTAATGG 	1
TGCATTTGTTGTACTGTTCG    AGG        TGCATTTGTTGTACTGTTCGAGG 	1
GGAGATCTTATTAGAGTCCT    TGG        GGAGATCTTATTAGAGTCCTTGG 	1
TTGGTAATTTGATGAAAAGA    AGG        TTGGTAATTTGATGAAAAGAAGG 	1
TGGTAATTTGATGAAAAGAA    GGG        TGGTAATTTGATGAAAAGAAGGG 	1
TATGTTTTAGTTGAAACCAC    TGG        TATGTTTTAGTTGAAACCACTGG 	1
ACCACTGGATTAGCAGACCC    AGG        ACCACTGGATTAGCAGACCCAGG 	1
CGTTGCTCAAACATTTTTTA    TGG        CGTTGCTCAAACATTTTTTATGG 	1
AGTTCTGAATTTATACTTGA    TGG        AGTTCTGAATTTATACTTGATGG 	1
GCTCATATTGATCAACAACT    TGG        GCTCATATTGATCAACAACTTGG 	1
```
##Result 
The output of the script consists of all the protospacers for the target gene the PAM sequence of the protospacer, the Matching Sequence in the Genome Off Target Count. [The  first version of the script gives the matching sequnence, we see the same sequence beacuse it identifies the same sequence in the genome and off target count is 1. So The next version of the code can be developed in such a way that we can input the number of mismatches we can allow for the off-targets and also to specify at which positions the mismatches are allowed and the future versions where it can identify whether the targets are presrnt in the intronic regions/ exonic regions if we can provide a the GTF/GFF file of the organism]. 


