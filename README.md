# **Mobile Genetic Elements Coordinates Extractor (MoGECE)**

Mobile Genetic Elements Coordinates Extractor (MoGECE) is a program that extracts mobile genetic elements location for prokaryotic genomes from outputs created by MGE analysis software. MoGECE then generates files that can be used for viewing that location in genome visualization software.

---

## RELEASE

Version 1.0.1 - March 23, 2016.

Available from <https://github.com/danillo-alvarenga/mogece>.

---

## REQUIREMENTS

MoGECE runs on Python 3 and has been tested on Ubuntu 14.04 and 16.04. It should work on any modern GNU/Linux distro. No installation for this program is required. However, since it works on outputs from other software, it is necessary to have access to such software in order to be able to use this program adequately.

Supported MGE analysis outputs in this version include files generated by the programs Alien_Hunter, ISsaga, MinCED, OligoWords, OASIS, PhiSpy, SeqWord Gene Island Sniffer, and VirSorter. Currently supported visualization software include Artemis and GView.

MoGECE has been developed with the following program versions in mind:
- Alien_Hunter 1.7
- Artemis 16.0.0
- GView 1.7
- ISsaga 03/09/2016
- MinCED 0.2.0
- OligoWords 1.2
- OASIS 8/11/08
- PhiSpy 2.3
- SeqWord Gene Island Sniffer 1.0
- VirSorter 1.0.3

>**Note:** Older or newer versions of these programs as well as other operating systems might also work, but since they have not been tested this is not guaranteed.

---

## USAGE

`MoGECE.py [-h] [-v] -f File (-l | -i | -m | -o | -w | -p | -s | -r) [-a] [-g]`  

optional arguments:

`-h`, `--help` | show a help message and exit  
`-v`, `--version` | show version and exit  

`-f File`, `--file File` | prediction file  

`-l`, `--alienhunter` | using Alien_Hunter sco prediction file  
`-i`, `--issaga` | using ISsaga csv prediction file  
`-m`, `--minced` | using MinCED gff prediction file  
`-o`, `--oasis` | using OASIS gff prediction file  
`-w`, `--oligowords` | using OligoWords out prediction file  
`-p`, `--phispy` | using PhiSpy tbl prediction file  
`-s`, `--sniffer` | using SeqWordSniffer out prediction file  
`-r`, `--virsorter` | using VirSorter fasta prediction file  

`-a`, `--artemis` | generate an Artemis gff file  
`-g`, `--gview` | generate a GView csv file  

In order to run MoGECE, indicate the output file you wish to process, the program in which this output file was created, and the program(s) in which you want to visualize the results. Only one file may be processed at each run, but both visualization files may be created at once if you wish.

**Example**: `MoGECE -f Escherichia\_coli\_K12.sco -l -a -g`

>**Note:** MoGECE is accompanied by an `Analyses.tar.gz` file containing results for the MGE analyses of 21 publicly available bacterial and archeal genomes to be used as examples. The `AnalyzedGenomes.md` file included with this program lists the genomes analyzed for that dataset. If you are not interested in examples, you may download the MoGECE.py script separately.

---

## NECESSARY FILES

### Alien_Hunter
Alien_Hunter generates three files after analysis. One of these files is a **`.sco`** file, which indicates coordinates and scores for the predicted genomic islands. Use the sco file as input for MoGECE.

### ISsaga
For ISsaga analysis results, it is necessary to first download the xls table containing IS annotations. This table is available in the Annotation Report section and can be downloaded by clicking on `annotation` > `extract annotation` > `Excel annotation file`. Open this file in a spreadsheet editor such as LibreOffice Calc or Microsoft Excel and save it as a **`.csv`** file from the file menu. This csv file can then be used as an input for MoGECE. Keep in mind that MoGECE ignores elements tagged as probable false positives by ISsaga.

### MinCED
By default, MinCED outputs results in a tab-separated values table to the terminal. For MoGECE, create a **`.gff`** file instead by adding the parameter `-gff` (not `-gffFULL`) to its command and pointing a filename for writing.

### OASIS
OASIS analyses produce two files: a .fasta file containing both nucleotide and amino acid sequences, and a **`.gff`** file containing information about the predicted insertion sequences. Use the gff file as the MoGECE input.

### OligoWords
OligoWords writes a **`.out`** file for each genome analyzed containing all genomic island results to the output folder inside the software directories. Look for this file and take it for MoGECE processing. MoGECE takes scores from the calculated pattern skew (the *n0_4mer:PS* results).

### PhiSpy
After PhiSpy finishes analysis, the output directory will host a file named **`prophage.tbl`** pointing the predicted prophages. This is the file that should be fed to MoGECE.

### SeqWord Gene Island Sniffer
Similarly to OligoWords, Sniffer also creates a **`.out`** results file with coordinates and pattern skews that can be used with MoGECE.

### VirSorter
VirSorter writes a large number of files during analysis. The relevant coordinates for MoGECE can be found in the headers from fasta sequences written to the **`Predicted_viral_sequences`** directory. Instead of running MoGECE on each fasta separately, you may first concatenate the predicted prophage files into a single file.

---

## RESULTS

MoGECE will output either a feature table file for visualization in Artemis (a **`.ft`** file), a comma-separated values table for GView (a **`.csv`** file), or both according to the parameters you have chosen when running the program.

The files produced will be named according to the program output in which they were based, e.g. an Alien_Hunter output file used as input for MoGECE with the `-a` and `-g` parameters will be processed and two files will be created: `alienhunter.csv` and `alienhunter.ft`.

When using GView, make sure to add all the processed outputs containing the MGE you wish to visualize to the directory where your target GenBank genome file is stored along with the **`GViewStyleSheet.gss`** file included with this software so that GView can recognize them correctly. Select the gb and the gss files in the Open Files window.

For visualization in Artemis, select `file` > `read an entry` in the genome annotation viewer. Change file types to "all files" and add the feature table. You may concatenate different feature tables into a single file so that you can view all results at once.

MoGECE adds scores for files containing such information (Alien_Hunter, OligoWords, and SeqWords Gene Island Sniffer outputs). For software where this information is absent, it assumes 1 as the score for every MGE coordinate.

---

## ISSUES AND REQUESTS

If you experience any issues or would like to see support for an additional feature implemented in MoGECE, please file a  request in the GitHub issue tracker or email it to the developer. Please feel free to contact the developer with any further questions regarding this software. You can reach him at <mailto:danillo.alvarenga@gmail.com>.

---

## LICENSE

Copyright © 2016 Danillo Oliveira Alvarenga

This program is free software: you can redistribute it and/or modify it under the terms of the GNU Affero General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU Affero General Public License for more  details.

You should have received a copy of the GNU Affero General Public License along with this program. If not, see <https://www.gnu.org/licenses/agpl-3.0.html>.
