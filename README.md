# <p align="center"> cordDqChecker-MIE2023 </p>
## <p align="center"> Data Quality Assessment on Rare Diseases Data – A set of Metrics and Tools for the 33rd Medical Informatics Europe Conference 2023 </p>

`cordDqChecker-MIE2023` This repository provides the code version and all instructions for conducting the study presented in the paper submitted for the 33rd Medical Informatics Europe (MIE) Conference 2023 (MIE2023). 

Acknowledgement: This work was done within the “Collaboration on Rare Diseases” of the Medical Informatics Initiative (CORD-MI) funded by the German Federal Ministry of Education and Research (BMBF), under grant number: FKZ-01ZZ1911R.

## 1. Local Execution
We would like to note that the developed tool supports HL7 FHIR as well as file formats such as CSV or Excel. To conduct local DQ assessments, please follow the following instructions. 
1. clone reposistory and checkout branch mie_2023
   - Run the git command: ``` git clone --branch mie_2023 https://github.com/KaisTahar/cordDqChecker ```

2. Go to the folder `./Local` and edit the file `config.yml` with your local variables
   - Set your custom variables (v1...v5)
     - Define your organization name (v1) and data input path (v2). This variable specifies which data set should be imported. When importing CSV or Excel data formats,   please define the headers as specified in the examples stored in `Local/Data/medData`. You can, for example, define your path as following:
	   - ```path="http://141.5.101.1:8080/fhir/" ```
	  or
	   - ``` path="./Data/medData/dqTestData.csv" ```
	  or
	   - ``` path="./Data/medData/dqTestData.xlsx" ```

     - Set proxy and access configuration (v3) if required 
     - Set the total number of inpatient case for 2020 (v4) as following:
  ``` inpatientCases_number: !expr list ( "2020"=997) ```
     - Set the corresponding code for filtering inpatient cases (v5) else default = NULL
   - Please change the variables v6 - v9 only if technical or legal restrictions otherwise prevent successful execution! In this context we would like to note that the CORD-MI list of tracer diagnoses version 1.0 (=v1) is used as a default reference for required diagnoses (see tracerPath v9). This [reference list](https://github.com/KaisTahar/cordDqChecker/tree/mie_2023/Local/Data/refData/CordTracerList_v1.csv) is stored in the folder for reference data `./Local/Data/refData` 

3. Once the source data path and local variables are defined, start the script using this command: ```Rscript cordDqChecker.R ``` to assess the quality of your data. You can also run this script using Rstudio or Dockerfile. To avoid local dependency issues just run the command ```sudo docker-compose up``` in the folder `./Local` to get the script running

4. The script generates two files per year analyzed – the first one is a CSV file that contains the calculated DQ metrics, while the second file is an Excel file that contains a report on DQ violations. To enable users to find the DQ violations and causes of these violations, this report provides sensitive information such as Patient Identifier (ID) or case ID – it is meant for internal use only. The generated reports are saved in the folder `./Local/Data/Export`.

## 2. Examples of Local Reports
Here are some [examples](https://github.com/KaisTahar/cordDqChecker/tree/mie_2023/Local/Data/Export) of data quality reports generated locally using sythetic data.	

## 3. Data Quality Metrics
- The data quality framework [`dqLib`](https://github.com/KaisTahar/dqLib) has been used as an R package for generating specific reports on DQ related issues and metrics. The code version used for this study is availabe in the folder `./Local/R`.
- The following DQ indicators and parameters are configured by default reports:
  | Dimension  | DQ Indicator | 
  | ------------- | ------------- |
  | completeness  | item completeness rate, value completeness rate, orphaCoding completeness rate  | 
  | plausibility  | orphaCoding plausibility rate, range plausibility rate | 
  | uniqueness | RD case unambiguity rate, RD case dissimilarity rate |

  
  |DQ Parameter | Description |
  |-------------------------- | ------------|
  | inpatient cases |  number of inpatient cases per year in a given hospital |
  | analyzed inpatient cases |  number of analyzed inpatient cases in a given study |
  | RD cases rel. frequency| relative frequency of inpatient RD cases per year per 100.000 cases|
  | Orpha cases rel. frequency| relative frequency of inpatient Orpha cases per year per 100.000 cases|
  | tracer cases rel. frequency| relative frequency of inpatient tracer RD cases per year per 100.000 cases|
 
  
- The following references are required to assess the quality of orphacoding and can be easily updated with new versions: (1) The standard Alpha-ID-SE terminology [1], and (2) the reference for tracer diagnoses provided in [2].
  
	[1]   BfArM - Alpha-ID-SE [Internet]. [cited 2022 May 23]. Available from: [BfArM](https://www.bfarm.de/EN/Code-systems/Terminologies/Alpha-ID-SE/_node.html) 
	
	[2]   Tahar K, Martin T, Mou Y, et al. Distributed Data Quality Assessment Across CORD-MI Consortia. [doi:10.3205/22gmds116](https://www.egms.de/static/en/meetings/gmds2022/22gmds116.shtml)


## 4. Note

-  You can also run `cordDqChecker` using Rstudio or Dockerfile. When using Rstudio, all required packages should be installed automatically using the script [`installPackages.R`](https://github.com/KaisTahar/cordDqChecker/tree/mie_2023/Local/R/installPackages.R). We would like to note that the `fhircrackr` package is only required to run local DQ assessments on FHIR data. To avoid local dependency issues go to folder `./Local` and just run the command `sudo docker-compose up` to get `cordDqChecker` running

- The missing item rate will be calculated based on FHIR [implementation guidlines of the MII core data set](https://www.medizininformatik-initiative.de/en/basic-modules-mii-core-data-set). Hence, mandatory items of the basic modules Person, Case and Diagnosis are required

- To cite `cordDqChecker-MIE2023`, please use the following **BibTeX** entry: 
  ```
  @software{Tahar_cordDqChecker-MIE2023,
  author = {Tahar, Kais},title = {{A set of Metrics and Tools for the 33rd Medical Informatics Europe Conference 2023}},
  url = {https://github.com/KaisTahar/cordDqChecker/tree/mie_2023},
  year = {2023}
  }

  ```
See also: [`CORD-MI`](https://www.medizininformatik-initiative.de/de/CORD)

