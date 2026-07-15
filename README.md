Structure
GMM-EM-Algorithm-Week1/
│
├── README.md                          # Project documentation
├── Week1_Report.pdf                   # Detailed project report
├── synthetic_data.csv                 # Generated dataset
├── gmm_em_algorithm.R                 # Complete R implementation
│
└── Output/                            # Output directory
    ├── dataset.png                    # Raw data visualization
    ├── final_clusters.png             # Clustered data with centers
    ├── log_likelihood.png             # Log-likelihood convergence plot
    └── true_vs_estimated.png          # True vs estimated comparison

# Vectorized Expectation-Maximization (EM) Algorithm for Gaussian Mixture Models from Scratch

## Project Title
**Vectorized Expectation-Maximization (EM) Algorithm for Gaussian Mixture Models from Scratch**

## Project Objective
This project implements the Expectation-Maximization (EM) algorithm for Gaussian Mixture Models (GMM) entirely from scratch without using any clustering libraries. The implementation includes:

- **Data Generation**: Creating synthetic 2D Gaussian clusters with specified parameters
- **EM Algorithm Implementation**: Computing multivariate normal density matrices, dynamic posterior probabilities, and updating mixture parameters
- **Mathematical Verification**: Ensuring likelihood convergence constraints are satisfied
- **Visualization**: Displaying dataset, final clusters, and log-likelihood convergence

The goal is to demonstrate the theoretical foundation of the EM algorithm and its application in density estimation and soft clustering.

## Software Used
- **R** (version 4.0 or higher)
- **Base R packages**: No external libraries required
- **Graphics**: Base R plotting functions

## Steps to Run the Program

### Prerequisites
1. Install R on your system (https://www.r-project.org/)
2. Ensure you have write permissions to create directories and files

### Running the Program

#### Method 1: Run the Complete Script
```bash
Rscript gmm_em_algorithm.R
Method 2: Run in R Console
Open R or RStudio

Set the working directory:
setwd("C:/GMM-EM-Algorithm-Week1/")

========================================
PART 1: Generating Synthetic Dataset
========================================
Dataset saved to synthetic_data.csv
First 6 rows:
         [,1]     [,2]
[1,] 1.439524 2.104532
[2,] 1.769823 3.107379
[3,] 3.558708 3.565713
[4,] 2.070508 2.734273
[5,] 2.129288 2.240518
[6,] 3.715065 3.818537

========================================
PART 2: Initializing Parameters (Improved)
========================================
Initial pi: 0.5 0.5 
Initial mu:
           [,1]      [,2]
[1,] 7.84501300 10.051951
[2,] 0.03338284  1.461824

========================================
PART 7: Running EM Algorithm
========================================

Iteration       Log-Likelihood          Change
----------------------------------------
1                -671.1794              --
2                -671.054                0.1254909 
3                -671.054                9.977384e-08 

Convergence achieved at iteration 3 

========================================
PART 8: Final Cluster Assignment
========================================
Cluster distribution:
clusters
  1   2 
100 100 

========================================
RESULTS SUMMARY
========================================

TRUE PARAMETERS:
Cluster 1 - Mean: 2 3 
Cluster 1 - Sigma:
     [,1] [,2]
[1,]  1.0  0.5
[2,]  0.5  1.0
Cluster 2 - Mean: 7 8 
Cluster 2 - Sigma:
     [,1] [,2]
[1,]  1.0 -0.3
[2,] -0.3  1.0

ESTIMATED PARAMETERS:
Mixing coefficients: 0.4999942 0.5000058 
Cluster 1 - Mean: 7.120481 7.929323 
Cluster 1 - Sigma:
           [,1]       [,2]
[1,]  0.8932370 -0.3098089
[2,] -0.3098089  1.0775962
Cluster 2 - Mean: 2.090449 2.952106 
Cluster 2 - Sigma:
          [,1]      [,2]
[1,] 0.8250503 0.3751107
[2,] 0.3751107 0.8631585

Clustering Accuracy: 100 %

========================================
EM ALGORITHM COMPLETED SUCCESSFULLY
========================================

Output files generated:
  - synthetic_data.csv
  - Output/dataset.png
  - Output/final_clusters.png
  - Output/log_likelihood.png
  - Output/true_vs_estimated.png

Summary Statistics:
  - Total points: 200 
  - Number of clusters: 2 
  - Iterations until convergence: 3 
  - Final Log-Likelihood: -671.054 
  - Accuracy: 100 %
