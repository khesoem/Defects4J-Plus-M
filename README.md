# Defects4J+M
This repository contains a dataset of computed metrics and test coverages for Defects4J projects.

## Citing Defects4J+M
If you are using this dataset for your research, we would be really glad if you cite our paper using the following bibtex:
```
@misc{1908.06502,
	Author = {Mostafa Mahdieh and Seyed-Hassan Mirian-Hosseinabadi and Khashayar Etemadi and Ali Nosrati and Sajad Jalali},
	Title = {Incorporating fault-proneness estimations into coverage-based test case prioritization methods},
	Year = {2019},
	Eprint = {arXiv:1908.06502},
}
```

## Data
The structure of the directories of this repository is as follows:

	Root Folder
	|
	|--- Chart
	    |--- 1
	        |--- Metrics.zip
	        |--- TestCoverage.zip
	|--- Closure
	|--- Land
	|--- Math
	|--- Time

There is a separate folder for each of the projects in the
initial published version of Defects4J. Each project folder includes a number of folders (let’s call
them *bug folders*) each of which provides the extracted information about a corresponding bug. For
example, “Root Folder->Chart->1” folder contains the extracted information about the bug whose id is
“1” in “Chart” project. These ids are the same as ids in Defects4J. For example, users of Defects4J can
checkout to the mentioned buggy version with this command:

	defects4j checkout -p Chart -v 1b -w output_folder

Each bug folder contains two files: “Metrics.zip” and “TestCoverage.zip” presenting the computed
metrics and test coverage of the corresponding buggy version, respectively.

### Computed Metrics
[SourceMeter](https://sourcemeter.com) is used to compute the values of various source code metrics. For each buggy
version of a project, the computed metric values could be found in the csv file inside “Metrics.zip” file in the
corresponding folder.

These metrics are calculated at class level. Each row of the file represents the
calculated metric values for a class and each column represents the calculated values of a specific
metric for different classes. The class name and the metric name abbreviation appear on the first cell
of row and column, respectively. The following table shows the list of types of metrics calculated for each class.
Further information about each metric could be found on the [documentation section of SourceMeter website](https://www.sourcemeter.com/resources/java/).

| Metric Type           | Number of Computed Metrics |
|-----------------------|----------------------------|
| Cohesion Metrics      | 1                          |
| Complexity Metrics    | 3                          |
| Coupling Metrics      | 5                          |
| Documentation Metrics | 8                          |
| Inheritance Metrics   | 5                          |
| Size Metrics          | 30                         |
| **Sum**               | **60**                     |

### Computed Test Coverages
The statement coverage is calculated at method level. For each
buggy version, the test coverage of each unit test on each program method is computed using [JaCoCo](https://www.jacoco.org).

Since a unit test usually covers only a few number of methods, the resulting matrix would be a
sparse matrix. Therefore, the result is stored as a file named “TestCoverage.zip” that includes a file
with HDF5 format in order to reduce the size of the dataset. There are many libraries for retrieving the
information inside a HDF5 file, such as [h5py](https://www.h5py.org/), which is a Python module.

Every “TestCoverage.h5” file contains five datasets. The following table explains each contained dataset.

| Dataset Name         | What *i*th Element Represents                               |
|----------------------|-------------------------------------------------------------|
| column               | index of the test name related to the *i*th coverage data   |
| columnTestNamesArray | ith test method name                                        |
| data                 | *i*th coverage data                                         |
| row                  | index of the method name related to the *i*th coverage data |
| rowMethodNamesArray  | *i*th program method name                                   |

In order to better understand the content of the “TestCoverage.h5” file, consider this example:
Suppose that the *i*th elements of ‘data’, ‘row’, and ‘column’ datasets are x, ind_r, and ind_c, respectively.
Also, let say the *ind_r*th element of ‘rowMethodNamesArray’ dataset is MName and *ind_c*th element of
‘columnTestNamesArray’ dataset is TName. This means that the coverage of TName test method over
MName program method is x.