# Wildenhain-Data-Scraper

# DataScraper.py

For each compound library available on http://chemgrid.org/cgm/index.php, download all compounds vs mutant .csv data files and create chemogenomic matrix.

Module requirements:
- pandas (pip install pandas)
- beautifulsoup (pip install beautifulsoup4)
- requests (pip install requests)

How to run: *python DataScraper.py*

Outputs:
- Data-Files folder with sub-folders for each compound library containing compounds vs mutant .csv data files
- CGM folder with chemogenomic matrix .csv files for each compound library

Note: In CGM output file, y-axis are the compounds in the library & x-axis are the mutants treated against the compounds. Mutants labels are as follows: name of strain _ number of bioactive compounds _ number of toxic compounds. Numbers and name are taken from http://chemgrid.org/cgm/index.php

Note: Some library name clarifications
- Spectrum    = Microsource Spectrum 2003
- SPECMTS3    = Microsource Spectrum 2005
- Spectrum_ED = Microsource Spectrum 2008
- Bioactive = Yeast Bioactive I
- Cytotoxic = Yeast Bioactive II

# SMILESScraper.py

NOTE: Cannot run on Linux lab computer because of requests_html module requirement

Get the name and canonical SMILES of all compounds in given library.

Module requirements:
- pandas (pip install pandas)
- requests (pip install requests)
- requests_html (pip install requests_html) NOTE: Only supported by python3.6+
- beautifulsoup (pip install beautifulsoup4)

How to run: *python SMILESScraper.py library_cgm_file*
- library_cgm_file: path from current working directory to CGM file of library to process (eg. CGM\\Bioactive_CGM.csv)

Note: Need CGM output files from DataScraper.py to run

# CompoundStructure.py

For each compound in given library, convert SMILES string into 3D structure and output .pdb file.

Moduel requirements:
- OpenBabel (http://openbabel.org/wiki/Main_Page)
- pandas (pip install pandas)

How to run: *python CompoundStructure.py library_SMILES_file single_file*
- library_SMILES_file: path from current working directory to SMILES file of library to process (eg. Compound-SMILES\\Bioactive_SMILES.csv)
- single_file: "true" if want output to be single file containing all compounds info for each library

Note: Need SMILES output files from SMILESScraper.py

Note: if running with single_file = "true", need .txt file version of library_SMILES_file, where first column = SMILES, second column = compound ID, third column = compound name

# ConformerLogsParser.py

Parse log file generated by OMEGA conformational search and output .txt file containing info of all molecules with warnings, then collect .pdb files of all molecules with warnings into logs folder.

How to run: *python ConformerLogsParser.py*

Note: Filtered log .txt files will have "_Fails" suffix in file name

# UniqueCompoundStructure.py

For each unique compound defined in SuppTable_S2 of paper, get 3D structure .pdb file generated by CompoundStructure.py and copy into seperate folder, then create .csv file mapping compound ID to compound name.

Module requirements:
- pandas (pip install pandas)

How to run: *python UniqueCompoundStructure.py*

Note: Need .pdb files from CompoundStructure.py

Note: Need modified SuppTable_S2 file called UniqueCompounds.xlsx to work properly

Note: There are actually 4897 unique compounds + 892 compounds from Cytotoxic library (not added by script)

# CGMProcess.py

NOTE: task dropped.

Find genes overlapping between compound libraries. 
Initially designed to create 1 single CGM from different CGMs, but task dropped.

Module requirements:
- pandas (pip install pandas)

How to run: *python CGMProcess.py library1 library2 ...*
- library#: name of libraries to process