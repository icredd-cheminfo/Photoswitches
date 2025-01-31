# Photoswitches

This repository contains the data and code for the manuscript 
"Towards data-driven design of visible-light photoswitches using structural features"
currently deposited in [ChemRxiv](https://doi.org/10.26434/chemrxiv-2024-4csd3).

## Photoswitch data

The "Photoswitches SI" folder contains the Excel file with the dataset used for all 
benchmarks and modeling in this manuscript (Photoswitch data.xls). 
The file itself contains a sheet describing the full dataset, including *SMILES* of structures, 
their properties (*lambda* for the absorption maximum and *t12* and *logt12* for the thermal half-life of
photoisomers), as well as solvents if they were reported in the initial source. The initial sources are 
indicated in the *subset* columns, and follow the subsets and corresponding references in the main text.

As a part of preprocessing, the full set is divided into trainig and test sets for each property.
These sets are also available in the file, in separate sheets. Otherwise, the sets can be reproduced 
by launching the code in the provided Jupyter notebook.

## Jupyter notebook to reproduce modeling results

The same folder contains a Jupyter notebook with the full code needed to reproduce the sets separation,
benchmark results, predictive modeling, chemical space investigation and model interpretation.

Please be aware that the notebook requires quite a few libraries to be installed, especially 
[Chython](https://github.com/chython/chython) for structure processing, 
[DOPtools](https://github.com/POSidorov/DOPtools) and RDkit for descriptor generation, and usual
libraries for machine learning (Numpy, pandas, scikit-learn, matplotlib, etc). 
The code has been tested with Python 3.10. Some versions of the libraries may be old compared to their 
current availabilities, so please pay attention that the results may be slightly different 
from what is reported in the manuscript.

The benchmark itself was launched using DOPtools on the local server, and the code for it is not provided.
To launch similar benchmarks, please refer to the DOPtools documentation and the corresponding 
[preprint](https://doi.org/10.26434/chemrxiv-2024-23v3c).

## Descriptor files

Descriptor files in svm format are provided for the training sets in the benchmark for both properties 
(**descriptors/lambda** and **descriptors/Htime** folders). They are separated by the type of descriptors.
The folder contain the svm files with the calculated descriptor (if several parameter setups were used 
to calculate descriptors, several files would be found) and the pickled version of the Fragmentor or
Fingerprinter object used to calculate them (these are DOPtools objects, please refer to the 
corresponding preprint). 

## Benchmark results

Benchmark results for each property are given in the **models** folder. Folders are separated by property, 
and then by descriptor type. Each lower level folder would contain three main things:

- **trials.all** file contains score and parameter setups for all optimization steps during benchmark.
The hyperparameters depend on the method used. The score for regression models is given as determination 
coefficient, R^2^.

- **trials.best** file is the subset of 50 best hyperparameter setups from the previous file.
The setups are sorted by the score, from highest to lowest.

- **trial.N** folder contains the predictions and statistical scores for the best hyperparameter setup. 
For the sake of the space in the repository, only the best setup is provided this way.

Model folders also have indications of the method that was used. If the folder name ends in "RFR", 
Random Forest was used; if XG - XGboost was used; if neither - Support Vector Machines regression was used.

## Model files

This folder contains folders with the scikit-learn pipeline objects for each of the best models, 
(.pkl objects), as well as the predictions on the external test made by these models (.csv or Excelt tables).

The code for restoring the models from these files is provided in the Jupyter notebook.

# Contributors

- Dr. Said Byadi, WPI-ICReDD, Hokkaido University
- Dr. Pavel Sidorov, WPI-ICReDD, Hokkaido University
  
Correspondence should be sent to Dr. Sidorov, please refer to the preprint for the contact information.
