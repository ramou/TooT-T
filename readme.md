# TooT-T
This tool predicts transporter proteins.
 
Input: proteins sequences in Fasta format
Output: the predicted class,1=transporter, 0=non-transporter

The method used in this tool is described in:

<a id="1">[1]</a> 
Alballa, Munira, and Gregory Butler. "TooT-T: discrimination of transport proteins from non-transport proteins." BMC bioinformatics 21 (2020): 1-10

However, it was trained with updated dataset retrieved from the Swiss-Port database as follows:
Protein sequences that belong to the transporter class were retrieved using the following search query:
This query searches for proteins that have the GO:0005215 transporter activity GO MF annotation. 

This GO MF was chosen here because it is directly related to the actual function of the protein rather than the general process in which it is involved.

Protein sequences that do not belong to the transporter class but are located in the
membrane were retrieved as non-transporters using the following search query:
The initial set was then filtered to attain the best-quality dataset by adhering to the following criteria:

- `Step 1:` Protein sequences that have evidence ?inferred from homology? for the existence of a protein were removed.
- `Step 2:` Protein sequences that are annotated with multiple functions (e.g., transporters and enzymes) were removed.
- `Step 3:` Protein sequences that have no GO MF annotation or annotation based only on computational evidence (IEA) were eliminated.
- `Step 4:` Protein sequences with more than 60\% pairwise sequence identity were removed via the CD-HIT  program to avoid any homology bias.


## FOLDERS
There are a number of folders that support the running of TooT-T and its outputs.

### Working Directory
When run, the tool will create a `work` directory, common among all the TooT Suite. TooT-SC will create a directory named `TooT-T` which will hold intermediate files created during the running of these tools.
The top-level working directory contains the homology details needed to extract the features. Details of the `psi Blast hits` for each sequence are found here.

The `TooT-T` directory will also contain a `Compostions` folder which contains the extracted `psi_composition` features of the test set

The working directory can be quite large, so you may want to use `-work` to specify a better location for it if you're short on space, and be sure to clean it out from time to time.

### db
Contains the database to be used when performing psiBLAST as well as TCDB for ATH predictions.

By default, if you unzip the contents of [this](https://tootsuite.encs.concordia.ca/databases/TooT-T-db.tar.gz) into a `db` folder adjacent to the source folder, it should be in the default location (or specify it manually).


### src
The scripts needed to use the tool.

## HOW TO USE
 - This tool requires that `BLAST` be pre-installed
 - This tool requires that M-View be pre-installed (link https://desmid.github.io/mview/)
 - Usage: `src/TooT_T.R -query=<input> [-out=<outdir>] [-db=<path to db>] [-work=<Workdir>] [-TooTR=<TooTTdir>]`
  - `<input>` is your sequence input file in fasta format
  - `<out>` is the output directory where you want the predicted 	results, formatted as csv
  - `<db> is the directory where the database (for psi-compositions) is stored in addition to TCDB for ATH predictions`
  - `<Workdir>` is the directory where intermediate files will be stored after each run
  - `<TooTTdir>` is the directory where the base TooT-T files are located
 - `psi-compositions` features of each sequence in the test set are found under the working directory `Compositions/`

