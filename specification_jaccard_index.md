# Specification: Jaccard index

## Overview

In this task you will implement one of the most common methods for comparing immune system datasets – Jaccard index. The specification or problem statement is broken down into two parts:

- The **Scientific background** section provides a high-level scientific overview and motivation for coding Jaccard index.  
- The **Technical specification** section provides a detailed API and testing approach to the function to be coded. **We expect the solution which is based on this document**.

Enjoy and let us know if you have any questions!
hr+r@immunomind.io.

## 🧬 Scientific specification

### Data overview

We work with the immune system data. Immune system has different types of cells, and in this task we focus on developing an analysis method for one specific type of cell called **T-cells**.

T-cells are cells that actively seek viruses in the blood of an organism and initiate the immune response. If you find equal or similar T-cells in different patients, this may indicate a similar underlying immune process or similar infection of the hosts.

In this task, each file except the **metadata file** is an immune system dataset corresponding to a specific patient: one file = one sample, one sample = one patient. Each dataset is called an **immune repertoire** or **clonotype table**.

**Clonotype** is a name given to T-cells and is a row in the clonotype table. We compare T-cells by their DNA or Protein sequences. DNA sequences of clonotypes are stored in the **CDR3.nt column**, and Protein sequences of clonotypes are stored in the **CDR.aa column**.

The pool of immune repertoires of patients has a corresponding file **metadata.txt** with meta-information about the patients, such as age, condition, history of diseases, specific gene profile, etc.

The analysis is done on immune repertoires and occasionally uses the metadata to group and sample patients.

### Method Overview

- **What?** Jaccard index is a common way to compare two immune repertoires and evaluate their similarity using a number of shared clonotype sequences. For instance, a Jaccard index of 10% means that 10% of the clonotype sequences from two immune repertoires are present in both immune repertoires.
- **Why?** Similar diseases impact immune repertoires in the same way. A large percentage of shared clonotypes indicates that there are similar immune processes, thus making it valuable for uncovering the hidden similarities between different conditions.
- **Background**
    - One of the first articles to use Jaccard index to track changes in immune repertoires: [https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4221123/](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4221123/)

## ⚙️ Technical specification

- **API**
    - Function name
        - `immuno_jaccard`
    - Arguments
        - `.first`, `.second` - an input data, first and second immune repertoires to compare. They have one of the following type and may be of different types:
            - `data.frame` - a base R `data.frame`with an immune repertoire table.
            - `data.table` - a `data.table::data.table` with an immune repertoire. Especially useful for large datasets as `data.table` provides accelerated computations.
        - `.col` - a string, specifying which immune repertoire column to use for finding equal sequences. Either `nt` for the `CDR3.nt` column or `aa` for the `CDR3.aa` column. Default: `nt`.
        - `.verbose` - a logical, indicating whether or not output additional information. Default: `FALSE`.
    - Output
        - Output the Jaccard index for the input pair of immune repertoires.
        - Output NA in case of errors, issues with the data or wrong `.col` argument.
        - If `.verbose` is `TRUE`, then print the update messages in the console. Update messages should notify users about finalization of preprocessing or analysis steps.
        - If `.verbose` is `FALSE`, then don't print any messages.
- **Test plan / Edge cases**
    - <ToDo for you: write two-three edge cases, how to handle them and write small tests to test for them>
    - Check the Background section for the testing framework. We provided basic test in [test_hello_world.R](./test_hello_world.R).
- **Background**
    - Tidyverse provides a dplyr-based interface to data.tables: [https://github.com/tidyverse/dtplyr](https://github.com/tidyverse/dtplyr)
    - An awesome library to test your code: [https://testthat.r-lib.org/](https://testthat.r-lib.org/)
    - Additional info on biology and analysis methods is on our tools' website: [https://immunarch.com/](https://immunarch.com/)
