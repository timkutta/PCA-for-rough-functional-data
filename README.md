# FPCA
Code complementing the paper "Does PCA Work for Rough Functional Data?"

08.01.2026

Rcode in this folder contains the following files:

-README.txt:
this file

-files 0-6: 
these files should be run consecutively. They reproduce the main figures 
and plots in our data analysis for the temperature data (0-5; number 6 is
the adaption for the discharge data). In 1 it is necessary to replace 
the path to the data set at the beginning of the code. 

-files s1 and s2:
Files that run the code for our simulation study. EW stands for "Eigenwert"
and produces histograms for the eigenvalues. EV stands for "Eigenvectors" and
produces the histograms of angles. Recall that the critical threshold between
sub- and supercriticality (in the documents lambda1) is 1.3. For subcritical
values we set lambda=1.1 and for supercritical values lambda=2. Each code
produces two histogram plots. They are identical except for the vertical red line.
This is the theoretical prediction assuming sub- or supercriticality. The two
plots are given back to back for the convenience of the user, to avoid manual
adjutment of the theoretical red line.

-file s3:
Contains the simulation of onatski power curves.

-temperature_data 
Includes the tempertature dataset

-discharge_data
Includes the discharge dataset

