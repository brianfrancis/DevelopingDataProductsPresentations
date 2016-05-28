qPCR Relative Quantification Calculator
========================================================
author: Brian Francis
date: 28-May-2016
transition: rotate


<small> 
Developing Data Products  
Coursera Data Science Specialization </small>



Motivation
========================================================

Quantification of gene expression in a transgenic animal 
can be determined via RT-qPCR (reverse transciption quantitative polymerase chain reaction) assays. The technique requires comparing the cycle threshold 
(Ct values) of the target gene to that of a reference gene (e.g., APOB).   Furthermore the unkown sample results are compared to a sample where the copies are known (a positive template control or PTC) to get the relative quantification.  

The prototype application created for this project assists in doing these calculations and in grouping the samples in a meaningful way (i.e., by genetic line). 



Challenges
========================================================

Instrument software frequently has minimal labeling of the attributes. In the case of the dataset considered here, that includes only the unique identification for samples which is a concatenation of the order # under which the samples are being processed and the 
sample number for each animal.  

However animals of different genetic lines may be tested using 
the same assays on the same PCR plate. Therefore the genetic 
line of the samples and which PTC values should be used to 
calculate the relative quantification are additional parameters 
needed to perform the calculations.  

Raw Data
========================================================

Below is some ouput from the raw instrument file

```
  Well Sample.Name Target.Name     CT
1    1 000001-2022      Assay1 28.986
2    1 000001-2022       rApoB 25.207
3    2 000001-2022      Assay1 28.797
4    2 000001-2022       rApoB 25.098
```

Additional information from the user that must be provided:

1. Which genetic line the samples in each Order are comprised of.
2. Which PTC values to use in caculating the relative quantification.


Calculating Relative Quantification
===

Relative quantification is represented by the Delta Delta of the CT.  The calcuation is as follows:

1.  We get take the difference of the two assays in each well on the plate. $DeltaCT_{well} = EndoCT_{well} - TargetCT_{well}$

2. For replicates of a single PTC we take the median. $DeltaCT_{ptcmedian} = Median(DeltaCT_{ptcwell})$

3. If more than one PTC is being used in the calcuation we take the average of the medians.  $DeltaCT_{ptcmean} = Mean(DeltaCT_{ptcmedian})$

4. Last we subtract the summarized delta PTC from the sample deltas.
$Delta Delta = DeltaCT_{well} - DeltaCT_{ptcmean})$

Conclusion
===

The application allows for simplified qPCR results analysis of transgenic aniamls through the following:

1.  Simplified sample labeling and linking of controls to samples.
2.  Auto-mated calculation of relative quantification.
3.  Visual display of the calculated results to make interpretation easier.
