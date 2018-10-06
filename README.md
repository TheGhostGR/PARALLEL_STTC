## **INSTALLATION INSTRUCTIONS**

### `Linux`

In terminal, go to the preferred location (cd WHERE/YOU/WANT/TO/INSTALL), and run:

    git clone https://github.com/VagelisKalimeris/PARALLEL_STTC.git
    cd PARALLEL_STTC
    make

Make sure the directories:

    DATASETS
    ASTROCYTES
    RESULTS

   have been created. If any of them is missing, it must be created.  
   For example:  

    mkdir RESULTS

Every psm_avalenche, as well as astrocytes, input file should be converted from .mat to text, with the following commands in Matlab / Octave:

    load '<name>.mat'
    dlmwrite('<name>', <matrix>, 'newline', 'unix', 'delimiter', '')

   where \<name\> is the name of .mat file and \<matrix\> is the 1D astrocytes table or the 2D psm_avalenche table (frames * cells).  
   If psm_avalenche is 3D, the program does not support it, and it needs to be converted to 2D before analysis.  
   Every dataset should be placed inside DATASETS directory, and every Astrocytes file should be placed inside ASTROCYTES directory.  
   The program supports datasets without astrocytes' file.
   The names of the final input files (dataset + astrocytes) MUST have the same name and, preferred, no extension.  

The program must be executed with the following format:

    ./sttc <size_of_control_group> <size_of_Dt> <name_of_dataset>
    
For example, if control group has size of `500`, Dt is `3`, and dataset is `M696`, then execute:
    
    ./sttc 500 3 M696

   The resulting files will be accessible after program's completion inside RESULTS directory.  
   For every psm_avalenche input file is analyzed, the code produces 5 different output files (3 csv's and 2 txt's).  
   The first part of every output file is the same as the name of the corresponding input file: `M696_*`.  
   The second part of every output file lists the analysis parameters (control group, Dt): `M696_500-shifts_3-dt_*`.  
   The third part of every output file indicates its type.  
   There are five types as listed below:  

   1. motifs.csv: `M696_500-shifts_3-dt_motifs.csv`  
   Motif analysis.  

   2. neurons_info.txt: `M696_500-shifts_3-dt_neurons_info.txt`  
   The total number of significant pairs and triplets as well as some general information that was collected during the analysis.  

   3. neurons_spikes.txt: `M696_500-shifts_3-dt_neurons_spikes.txt`  
   The spikes found in each neuron.  

   4. pairs.csv (or tuplets.csv): `M696_500-shifts_3-dt_tuplets.csv`  
   All the significant pairs, along with their IDs, STTC value and their percentile (position among the control group).  

   5. triplets.csv: `M696_500-shifts_3-dt_triplets.csv`  
   All the significant triplets, along with their IDs, STTC value and their percentile (position among the control group).  

### `WINDOWS`

The instructions are the same as long as a terminal application, like `Cygwin`, has been installed, and added `git`, `make` and `gcc-g++` support.

## **Parameters that can be changed:**

#### After any change to the source code, save the changed file(s), and run the commands "make clean" and "make".

   Null distribution of the conditional STTC: If the conditional STTC of a given triplet (A->B)|C is greater than the significant threshold and the number of firing events of ‘reduced A’ is greater than 5, then this triplet is considered as significant.  
   To change the significant threshold, open the file `SRC/common.cpp` with a text editor and at line 75, enter the preferred value as a real number, not integer.  
   To change the value of second condition, open the file `SRC/cond_null_dist.cpp` with a text editor and at line 65, enter the preferred value as an integer number, not real.  

### For further information read STTC_conditional.pdf
