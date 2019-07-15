# Defects4J+M
This repository contains a dataset of computed metrics and test coverages for Defects4J projects.

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
them bug folders) each of which provides the extracted information about a corresponding bug. For
example, “Root Folder->Chart->1” folder contains the extracted information about the bug whose id is
“1” in “Chart” project. These ids are the same as ids in Defects4J. For example, users of Defects4J can
checkout to the mentioned buggy version with this command:

	defects4j checkout -p Chart -v 1b -w output_folder