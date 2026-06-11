# PhD-Thesis
## Bioinformatic Analyses of Bacterioferritins

### HMM and MSA Analysis Tools

A collection of Python scripts designed to process Hidden Markov Model (HMM) outputs, calculate downstream profile metrics, and compute column-wise mean Shannon entropy from Multiple Sequence Alignments (MSA). 

> **Note for Users:** This repository is structured as a **template-based pipeline**. You will need to manually open these scripts and edit specific variables to match your data.

---

## Repository Architecture

```text
├── HMMprocessingFunctions.ipynb    # Parses and filters raw HMMER/HMM output files
├── HMMstats-FtnBfrAB.ipynb         # Computes downstream scores/metrics from the processed HMM data
└── Entropy.ipynb                   # Computes column-wise Shannon entropy from an MSA file
```

### HMMprocessingFunctions

This script comprises three functions which process the .tblout tabular output from HMMER3 and converts it to dataframes to clean, filter, and extract significance metrics from the HMM profile hits. 

1) ```process_tblout_data``` Filters the dataset for your specified target profiles and generates a dataframe showing the number of unique species matching each profile. Takes an input of ```target_names = []``` which is a list of your profile HMMs. The output dataframe is used as input for the following two functions.
2) ```most_significant_profile``` Deduplicates your data by retaining only the single best hit for each unique sequence based on the lowest full-sequence E-value.
3) ```significant_profile_count``` Quantifies the overall abundance of your HMM profiles by calculating the absolute count and percentage breakdown of every unique profile across the entire dataset.


### HMMstats-FtnBfrAB

This script comprises five functions to process the data from the raw HMMER3 profiles (.hmm) and parses out both the state transition probabilities (Match, Insert, Delete) and amino acid match emissions. It then standardises profiles of varying lengths and computes a custom pairwise distance matrix to determine structural and sequence-level similarity between profiles.

1) ```parse_hmm_transitions``` Extracts state transition features from a HMMER3 profile and converts them into normalised probabilities. Takes the file path to the ```.hmm``` as input.
2) ```compute_transition_stats``` Calculates the mean transition probabilities across an entire HMM profile. Takes the file path to the ```.hmm``` as input.
3) ```parse_hmm_emissions_corrected``` Extracts match-state emission scores for the 20 amino acids and handles non-permissible states (*) as zero probability. Takes the file path to the ```.hmm``` as input.
4) ```align_profiles``` Aligns multiple HMM profiles to the length of the shortest profile. Takes a dictionary of dataframes as input where each DataFrame contains HMM emission probabilities indexed by position ```dfs_dict = {profile_name: pandas.DataFrame}```
5) ```compute_combined_distance``` Calculates the overall distance between two HMM profiles by combining sequence-level differences (emission probabilities) and profile architecture differences (transition probabilities). Takes the aligned emission arrays and transition matricies for the two profiles to be compared as input.


### Entropy

This script comprises two functions which read a MSA and outputs mean Shannon entropy scores, normalised between 0 and 1. 

1) ```column_entropy``` Calculates the Shannon entropy for each column in a MSA. Takes a MSA as input, loaded using ```AlignIO.read()``` from ```Bio```.
2) ```conservation``` Converts entropy values into a normalised conservation score between 0 and 1. Takes the array of entropy values calculated from ```column_entropy``` as input.


### Citation

```bibtex
@phdthesis{Imogen_Garner_thesis_2026,
  author      = {Imogen Garner},
  title       = {Ironing out the Ferritin Family Tree: Bioinformatic Analyses and Single Particle Cryo-EM Structural Determination of Bacterioferritins},
  school      = {[Newcastle University]},
  year        = {2026},
  note        = {GitHub Repository: [https://github.com/](https://github.com/)[glitterbox]/PhD-Thesis}
}




