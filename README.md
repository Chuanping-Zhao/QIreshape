# QIreshape
This tool is specifically designed to merge qualitative and quantitative metabolomics data
exported from Progenesis QI software. 

# Purpose

QIreshape processes and merges datasets in CSV, XLSX, and TXT formats,prioritizing quantitative data when overlaps occur. The package filters data by qualitative score, handles duplicate entries, and augments the data with polarity information, making it ideal for Progenesis QI analysis workflows.

# How to Install
```R
install.packages("remotes")
remotes::install_github("Chuanping-Zhao/QIreshape")
```
# use
In the function QI_mergeQQ, the parameters "identical_path", "intensity_path", "score_value", and "polarity" respectively represent the pathway for the qualitative matrix, the pathway for the quantitative matrix, the qualitative score, and the mode of metabolite acquisition. These are all required parameters.
```R
rm(list = ls())
library(QIreshape)
#QI_mergeQQ:Merge quantitative and qualitative matrices
demo <- QI_mergeQQ(identical_path="test/pos_identification.csv",
           intensity_path="test/pos_measurement.csv",
           score_value=0,#qualitative score
           polarity="pos")
```
pos_identification.csv:

![image](https://github.com/Chuanping-Zhao/QIreshape/assets/134377196/6d12f4da-c6b6-4fc8-9efa-900d7e45b367)

pos_measurement.csv

![image](https://github.com/Chuanping-Zhao/QIreshape/assets/134377196/82e9eaa3-fafe-453c-93db-f5541325474f)


demo:

![image](https://github.com/Chuanping-Zhao/QIreshape/assets/134377196/68d79251-1141-4de6-b4c2-5b5670e6e52d)

QI_mergePos:Merge Positive and Negative Metabolomics Data
```R
pos_data <- read.csv("test/pos_result.csv")
neg_data<- read.csv("test/neg_result.csv")
all_Data <- QI_mergePos(posData =pos_data, negData=neg_data)
```
"pos_data" and "neg_data" are the combined data resulting from the function QI_mergeQQ, representing the summarization of qualitative and quantitative results under positive and negative ion modes respectively. QI_mergePos can merge the two matrices mentioned above. The merging rule is to select the metabolite with the highest score when there are multiple entries for the same metabolite under positive and negative ion modes. If there are still duplicate entries, the metabolite with the highest Fragmentation Score will be selected.



