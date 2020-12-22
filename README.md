# Pre-processing and analysis of counfounding factors towards immunoprofiling of adenocarcinomas of the pancreatobiliary system

## About the data:
 
Data was obtained from Fernández Moro et. al (2016) and found [here](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0166067#sec005).
The raw dataset comprises 439 tumor samples and 38 immunohistochemical markers.Data contains immunohistochemical information from patients with adenocarcinoma arising in the pancreatobiliary system who underwent diagnostic core needle biopsy or surgical resection.
Tumors are classified based on their anatomical localization,in accordance to the he 7th edition of the American Joint Committee on Cancer (AJCC)–Union for International Cancer Control (UICC) tumor node metastasis (TNM) classification:

Anatomical tumor classes are: 

- ampullary carcinoma (n=24)
- ductal pancreatic adenocarcinoma (n=143)
- distal bile duct cancer (n=8)
- gallbladder cancer (n=38)
- perihilar cholangiocarcinoma (n=28)
- and intrahepatic cholangiocarcinoma (n=98)
 
Control samples are hepatocellular carcinoma (n=100) , a tumor type with a well-known immunohistochemical profile.

Each tumor sample was stained with a panel panel consisting of up to 38 antibodies, of which finally 26 were considered for the analysis, after pruning of missing data.
Each marker column contains a continuous numeric score (from 1 to 100) based on the percentage of stained tumor cells. 
The final 27 immunohischemical markers used were:  ck5, ck7, ck17, ck18, ck19, ck20, vim, muc1, muc2, muc5ac, muc6, berep4, ema, mcea, pcea, ca125, ca19.9,    
maspin, wt1cyt, cdx2, p53, p63, ki67, chra, cd56, cd10.  

Prunned and imputed data can be found in ![here](https://github.com/valengrillo/tfcb-homework08/blob/main/data/tidy/imputed_data.csv)

The type of probes taken for immonohistochemical profiling , i.e. needle biopsy (labeled as 'b') or surgical resection (labeled as 'r'), was found in another dataset named  'pcbil_clinicaldata.cvs'. 
A recommendation for easing future analysis with this data would be having the type of probe included in the same immunomarker scores dataset.
Also, samples names could be simplified with a numeric ID, instead naming them as a combination of clinical classification (for which a column exists- 'clinical_dagnosis') and a identifier number. 
I assummed the 'pad' column represented the samples names, and so I merged both datasets based on it.   

## Questions:

### 1) Do selected immunohistochemical markers are biased for the pancreatic and biliary tumors?

A Principal Component Analysis (PCA) was used because it allows me to organize my data into groups, or clusters, on the basis of how closely associated they are. Different tumors types are expected to have different immunohistochemical markers and percentages of stained tumor cells,
and thus, are expected to cluster separately. I performed a PCA to make sure the selected list of immunohistochemical markers is comprehensive enough to correctly separate broadly distinct anatomycal tumor types.
The resulting PCA plot shows an admixture of all pancreatic and biliary anatomical tumor types and clustering tendency for hepatocellular carcinoma (the control group). This indicates that the pannel of immunomarkers can correctly separate distinct anatomycal tumor types
(i.e. it is not biased for the adenocarcinomas of the pancreobiliary system). 

![image1](https://github.com/valengrillo/tfcb-homework08/blob/main/data/byanatomicalmarkers.png)


### 2)Does the type of sample probe influences the immunohistochemical profiles?

A PCA analysis was used for the same reason as question 1. If the type of probe influences the immonohistochemical readout, then two clusters corresponding to each probe were expected.
Instead, figure 2 shows an admixture of probe types throughout the entire plot, disregarding sample's probe type as a counfounding factor.

![image2](https://github.com/valengrillo/tfcb-homework08/blob/main/data/byprobe.png)

## Reproducibility:

Cleaning of raw data followed the same steps as Fernández Moro et. al (2016). First, they filtered out every column missing more than 40% of it values. Second, they filtered out every row missing more than 50% of its data. Finally
they imputed remaining missing values. Yet, my resulting prunned dataframe differed from Fernández Moro's in its dimensions. This is because they first analyzed the number of missing values both for column and rows, and then selected for columns and rows satisfying
the conditions. However this is redundant, because an increase in the proportion of missing values per row might be caused by a generalized incomplete data of a certain immunomarker.
Thus, I first analyzed and filtered out missing values by columns, and later analyzed and filtered out rows. Our resulting data frame kept the same markers  as Fernández Moro's, but had 417 tumor samples instead of 409.

 The quest 



