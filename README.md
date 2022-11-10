# cordDqChecker
`CordDqChecker` provides a set of Data Quality (DQ) tools and metrics for the special issue "Quality of Data in Health Research and
859 Health Care” in the “Methods of Information in Medicine" (MIM). Theses tools were used to conduct local as well as distributed data quality assessments and reporting in [`CORD-MI`](https://www.medizininformatik-initiative.de/de/CORD).

Acknowledgement: This work was done within the “Collaboration on Rare Diseases” of the Medical Informatics Initiative (CORD-MI) funded by the German Federal Ministry of Education and Research (BMBF), under grant number: 01ZZ1911R, FKZ-01ZZ1911R.
## Data Quality Metrics
- The following data quality indicators and parameters are configured by default data quality reports:
  | Dimension  | Indicator Name | 
  | ------------- | ------------- |
  | completeness  | item completeness rate, value completeness rate, subject completeness rate, case completeness rate, orphaCoding completeness rate  | 
  | plausibility  | orphaCoding plausibility rate, range plausibility rate | 
  | uniqueness | RD case unambiguity rate, RD case dissimilarity rate |
  | concordance |concordance with reference values| 
  
  |Parameter Name | Description |
  |-------------------------- | ------------|
  | inpatient cases |  number of inpatient cases per year |
  | inpatients |  number of inpatient per year |
  | RD cases | number of RD cases per year |
  | Orpha cases |  number of Orpha cases per year |
  | tracer cases |  number of tracer RD cases per year |
  | RD cases rel. frequency| relative frequency of inpatient RD cases per year per 100.000 cases|
  | Orpha cases rel. frequency| relative frequency of inpatient Orpha cases per year per 100.000 cases|
  | tracer cases rel. frequency| relative frequency of inpatient tracer RD cases per year per 100.000 cases|
  | missing mandatory data items |  number of missing data items per year |
  | missing mandatory data values| number of missing data values per year |
  | incomplete subjects |  number of incomplete inpatient records per year |
  | missing orphacodes |  number of missing Orphacodes per year |
  | outliers | number of detected outliers per year |
  | implausible links | number of implausible code links per year |
  | ambiguous RD cases | number of ambiguous RD cases per year |
  | duplicated RD cases |  number of duplicated RD cases per year |
  
- The data quality framework [`dqLib`](https://github.com/KaisTahar/dqLib) has been used as an R package for generating specific reports on data quality related issues and metrics.
- The following references are required to assess the quality of orphacoding and can be easily updated with new versions:
  - The standard Alpha-ID-SE terminology [1]
  - A reference for tracer diagnoses such as the list provided in [2].
  
	[1]   BfArM - Alpha-ID-SE [Internet]. [cited 2022 May 23]. Available from: https://www.bfarm.de/EN/Code-systems/Terminologies/Alpha-ID-SE/_node.html 
    
	[2]   List of Tracer Diagnoses Extracted from Alpha-ID-SE Terminology [Internet]. 2022 [cited 2022May 24]. Available from: https://doi.org/21.11101/0000-0007-F6DF-9 

## Distributed Execution
We applied our methodology for distributed data quality assessments on synthetic data stored in multiple FHIR servers (see [data curation](https://github.com/KaisTahar/cordDqChecker-MIM/tree/master/PHT/Data/Experiment)). `cordDqChecker` was successfully tested and validated using [Personal Health Train (PHT)](https://websites.fraunhofer.de/PersonalHealthTrain/). To create a  PHT image run the command ` sudo docker build -t dq-train .`. The FHIR data sets and tools used for data curation are stored in the folder `./PHT/Data/Experiment`. The aggregated results are stored in `./PHT/Data/Export`.

## Cross-site Reports
- Here are [examples](https://github.com/KaisTahar/cordDqChecker-MIM/tree/master/PHT/Data/Export) of cross-site reports on data quality generated using sythetic data.
- The used references are store in the folder ``` "./PHT/Data/refData" ```
  
## Local Execution
To analyse your data quality locally go to folder `./Local` and run `cordDqChecker.R` to genrate data quality reports.

- The script `cordDqChecker.R` reads data from FHIR server or from supported file formats such as CSV and Excel. The path varialbe specifies which dataset should be imported.
For Example you can define your path as following:
  - ```path="http://141.5.101.1:8080/fhir/" ```
  or
  - ``` path="./Data/medData/dqTestData.csv" ```
  or
  - ``` path="./Data/medData/dqTestData.xlsx" ```

- The default values of local variables are set as follows:
  - ``` reportYear=2020 ```
  - ``` max_FHIRbundles=50 ```
  - ``` INPATIENT_CASE_NO=997 ```
  - ```path="http://141.5.101.1:8080/fhir/``` 

Once the source data path and local variables are defined, start the script to check the quality of your data.
The genrated repots are saved in folder ``` "./Local/Data/Export" ```

## Local Reports
- In the folder  ``` "./Local/Data/Export" ``` you will finde some examples of data quality reports generated locally using sythetic data.
- The used references are stored in ``` "./Local/Data/refData" ```

## Note

- Before starting `cordDqChecker.R` you need to install required libraries using the script `installPackages.R` stored in ``` "./Local/R" ```

- To avoid local dependency issues go to folder `./Local` and just run the command `sudo docker-compose up` to get `cordDqChecker` running.
- The missing item rate will be calculated based on FHIR [implementation guidlines of the MII core data set](https://www.medizininformatik-initiative.de/en/basic-modules-mii-core-data-set). Hence, mandatory items of the basic modules Person, Case and Diagnosis are required.

- To cite `cordDqChecker`, please use the following **BibTeX** entry: 
  ```
  @software{Tahar_cordDqChecker,
  author = {Tahar, Kais},title = {{cordDqChecker}},
  url = {https://github.com/medizininformatik-initiative/cord-dq-checker},
  year = {2021}
  }

  ```
See also:  [`dqLib`](https://github.com/medizininformatik-initiative/dqLib)  [`CORD-MI`](https://www.medizininformatik-initiative.de/de/CORD)


