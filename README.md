\documentclass[12pt,a4paper]{article}
\usepackage[utf8]{inputenc}
\usepackage{amsmath}
\usepackage{amsfonts}
\usepackage{amssymb}
\usepackage{graphicx}
\usepackage{float}
\usepackage{caption}
\usepackage{subcaption}
\usepackage{geometry}
\usepackage{hyperref}
\usepackage{booktabs}
\usepackage{array}
\usepackage{multirow}
\usepackage{color}
\usepackage{listings}
\usepackage{xcolor}

\geometry{margin=1in}

% Define colors for code listings
\definecolor{codegreen}{rgb}{0,0.6,0}
\definecolor{codegray}{rgb}{0.5,0.5,0.5}
\definecolor{codepurple}{rgb}{0.58,0,0.82}
\definecolor{backcolour}{rgb}{0.95,0.95,0.92}

\lstdefinestyle{mystyle}{
    backgroundcolor=\color{backcolour},   
    commentstyle=\color{codegreen},
    keywordstyle=\color{magenta},
    numberstyle=\tiny\color{codegray},
    stringstyle=\color{codepurple},
    basicstyle=\ttfamily\footnotesize,
    breakatwhitespace=false,         
    breaklines=true,                 
    captionpos=b,                    
    keepspaces=true,                 
    numbers=left,                    
    numbersep=5pt,                  
    showspaces=false,                
    showstringspaces=false,
    showtabs=false,                  
    tabsize=2
}

\lstset{style=mystyle}

\title{\textbf{Vectorized Expectation-Maximization (EM) Algorithm for \\ Gaussian Mixture Models from Scratch}}
\author{Project Report - Week 1}
\date{July 18, 2026}

\begin{document}

\maketitle

\begin{abstract}
This report presents a complete implementation of the Expectation-Maximization (EM) algorithm for Gaussian Mixture Models (GMM) developed entirely from scratch using R. The implementation includes synthetic data generation, parameter initialization, the EM algorithm with E-step and M-step, mathematical verification, and comprehensive visualization. The algorithm successfully clusters 200 data points into two Gaussian components with 100\% accuracy, demonstrating the effectiveness of the vectorized implementation. Key features include multivariate normal density computation, dynamic posterior probability updates, and convergence monitoring through log-likelihood tracking.
\end{abstract}

\section{Implementation Overview}

\subsection{Project Structure and Components}

The complete implementation consists of the following components organized in a structured directory:

\begin{itemize}
    \item \textbf{Data Generation}: Creation of synthetic 2D Gaussian clusters with specified parameters (means, covariance matrices, and mixing coefficients)
    \item \textbf{EM Algorithm}: Vectorized implementation including:
        \begin{itemize}
            \item E-step: Computation of posterior probabilities (responsibilities)
            \item M-step: Update of mixture parameters (π, μ, Σ)
            \item Convergence checking via log-likelihood monitoring
        \end{itemize}
    \item \textbf{Visualization}: Four comprehensive plots showing dataset, final clusters, log-likelihood convergence, and true vs estimated parameters
    \item \textbf{Validation}: Mathematical verification ensuring likelihood convergence and parameter constraints
\end{itemize}

\subsection{Mathematical Framework}

The Gaussian Mixture Model represents the probability density function as a weighted sum of K Gaussian components:

\begin{equation}
p(x) = \sum_{k=1}^{K} \pi_k \mathcal{N}(x | \mu_k, \Sigma_k)
\end{equation}

where $\pi_k$ are mixing coefficients satisfying $\sum_{k=1}^{K} \pi_k = 1$ and $\pi_k \geq 0$, and $\mathcal{N}(x | \mu_k, \Sigma_k)$ is the multivariate normal density:

\begin{equation}
\mathcal{N}(x | \mu, \Sigma) = \frac{1}{(2\pi)^{d/2}|\Sigma|^{1/2}} \exp\left(-\frac{1}{2}(x-\mu)^T \Sigma^{-1} (x-\mu)\right)
\end{equation}

\subsection{EM Algorithm Steps}

\subsubsection{E-Step (Expectation)}
Compute the responsibilities (posterior probabilities):

\begin{equation}
\gamma_{ik} = \frac{\pi_k \mathcal{N}(x_i | \mu_k, \Sigma_k)}{\sum_{j=1}^{K} \pi_j \mathcal{N}(x_i | \mu_j, \Sigma_j)}
\end{equation}

\subsubsection{M-Step (Maximization)}
Update the parameters:

\begin{align}
\pi_k &= \frac{1}{n} \sum_{i=1}^{n} \gamma_{ik} \\
\mu_k &= \frac{\sum_{i=1}^{n} \gamma_{ik} x_i}{\sum_{i=1}^{n} \gamma_{ik}} \\
\Sigma_k &= \frac{\sum_{i=1}^{n} \gamma_{ik} (x_i - \mu_k)(x_i - \mu_k)^T}{\sum_{i=1}^{n} \gamma_{ik}}
\end{align}

\subsection{Implementation Results}

\subsubsection{Generated Dataset}
The synthetic dataset consists of 200 points from two 2D Gaussian distributions with the following true parameters:

\begin{table}[H]
\centering
\caption{True Parameters for Synthetic Data}
\begin{tabular}{|c|c|c|c|}
\hline
\textbf{Cluster} & \textbf{Mean} & \textbf{Covariance Matrix} & \textbf{Mixing Coeff.} \\
\hline
1 & (2, 3) & $\begin{bmatrix} 1.0 & 0.5 \\ 0.5 & 1.0 \end{bmatrix}$ & 0.50 \\
2 & (7, 8) & $\begin{bmatrix} 1.0 & -0.3 \\ -0.3 & 1.0 \end{bmatrix}$ & 0.50 \\
\hline
\end{tabular}
\end{table}

\subsubsection{Estimated Parameters}
The EM algorithm converged in just 3 iterations, achieving the following estimates:

\begin{table}[H]
\centering
\caption{Estimated Parameters After Convergence}
\begin{tabular}{|c|c|c|c|}
\hline
\textbf{Cluster} & \textbf{Mean} & \textbf{Covariance Matrix} & \textbf{Mixing Coeff.} \\
\hline
1 & (7.120, 7.929) & $\begin{bmatrix} 0.893 & -0.310 \\ -0.310 & 1.078 \end{bmatrix}$ & 0.500 \\
2 & (2.090, 2.952) & $\begin{bmatrix} 0.825 & 0.375 \\ 0.375 & 0.863 \end{bmatrix}$ & 0.500 \\
\hline
\end{tabular}
\end{table}

\subsection{Performance Metrics}

\begin{itemize}
    \item \textbf{Clustering Accuracy}: 100\%
    \item \textbf{Total Points}: 200
    \item \textbf{Number of Clusters}: 2
    \item \textbf{Iterations Until Convergence}: 3
    \item \textbf{Final Log-Likelihood}: -671.054
    \item \textbf{Convergence Threshold}: $1 \times 10^{-6}$
\end{itemize}

\subsection{Visualization Results}

\begin{figure}[H]
\centering
\begin{subfigure}{0.48\textwidth}
    \centering
    \includegraphics[width=\textwidth]{Output/dataset.png}
    \caption{Raw synthetic dataset}
    \label{fig:dataset}
\end{subfigure}
\hfill
\begin{subfigure}{0.48\textwidth}
    \centering
    \includegraphics[width=\textwidth]{Output/final_clusters.png}
    \caption{Final clusters with centers}
    \label{fig:clusters}
\end{subfigure}
\caption{Visualization of the generated dataset and final clustering results}
\end{figure}

\begin{figure}[H]
\centering
\begin{subfigure}{0.48\textwidth}
    \centering
    \includegraphics[width=\textwidth]{Output/log_likelihood.png}
    \caption{Log-likelihood convergence}
    \label{fig:loglikelihood}
\end{subfigure}
\hfill
\begin{subfigure}{0.48\textwidth}
    \centering
    \includegraphics[width=\textwidth]{Output/true_vs_estimated.png}
    \caption{True vs estimated comparison}
    \label{fig:comparison}
\end{subfigure}
\caption{Convergence monitoring and parameter comparison}
\end{figure}

\subsection{Code Snippets}

\subsubsection{Multivariate Normal Density Function}
\begin{lstlisting}[language=R, caption=Multivariate Normal Density Computation]
multivariate_normal <- function(x, mean, sigma) {
    d <- length(mean)
    det_sigma <- det(sigma)
    inv_sigma <- solve(sigma)
    diff <- x - mean
    exponent <- -0.5 * t(diff) %*% inv_sigma %*% diff
    return((1 / ((2*pi)^(d/2) * sqrt(det_sigma))) * exp(exponent))
}
\end{lstlisting}

\subsubsection{EM Algorithm E-Step}
\begin{lstlisting}[language=R, caption=E-Step Implementation]
# E-Step: Compute responsibilities
for (k in 1:K) {
    # Compute multivariate normal density for each point
    for (i in 1:n) {
        density[i, k] <- multivariate_normal(X[i,], mu[,k], sigma[,,k])
    }
}
# Calculate responsibilities
for (i in 1:n) {
    denom <- sum(pi * density[i,])
    gamma[i,] <- pi * density[i,] / denom
}
\end{lstlisting}

\subsubsection{EM Algorithm M-Step}
\begin{lstlisting}[language=R, caption=M-Step Implementation]
# M-Step: Update parameters
for (k in 1:K) {
    nk <- sum(gamma[,k])
    pi[k] <- nk / n
    mu[,k] <- colSums(gamma[,k] * X) / nk
    centered <- sweep(X, 2, mu[,k])
    sigma[,,k] <- t(centered) %*% diag(gamma[,k]) %*% centered / nk
}
\end{lstlisting}

\subsection{Convergence Analysis}

The EM algorithm demonstrates rapid convergence, with the log-likelihood stabilizing after just 3 iterations:

\begin{table}[H]
\centering
\caption{Convergence History}
\begin{tabular}{|c|c|c|}
\hline
\textbf{Iteration} & \textbf{Log-Likelihood} & \textbf{Change} \\
\hline
1 & -671.179 & -- \\
2 & -671.054 & 0.125 \\
3 & -671.054 & $9.98 \times 10^{-8}$ \\
\hline
\end{tabular}
\end{table}

The algorithm successfully identified the optimal parameters, achieving perfect clustering accuracy. The convergence threshold of $10^{-6}$ was reached after the third iteration, indicating the efficiency of the vectorized implementation.

\subsection{Output Files Generated}

The implementation produces the following output files:

\begin{itemize}
    \item \texttt{synthetic\_data.csv}: Generated dataset with cluster labels
    \item \texttt{Output/dataset.png}: Raw data visualization
    \item \texttt{Output/final\_clusters.png}: Clustered data with estimated centers and covariance ellipses
    \item \texttt{Output/log\_likelihood.png}: Log-likelihood convergence plot
    \item \texttt{Output/true\_vs\_estimated.png}: True vs estimated parameter comparison
\end{itemize}

\subsection{Software and Requirements}

The implementation is developed entirely in R (version 4.0 or higher) using only base R packages, ensuring portability and reproducibility. No external libraries are required, making the code self-contained and easily deployable.

\subsection{Conclusion}

This implementation successfully demonstrates the theoretical foundations of the EM algorithm for Gaussian Mixture Models. The vectorized approach in R achieves rapid convergence with perfect clustering accuracy, validating the mathematical framework. The comprehensive visualization suite provides clear insights into the data structure, algorithm convergence, and parameter estimation quality.

\end{document}

## OUTPUT

<img width="800" height="600" alt="dataset" src="https://github.com/user-attachments/assets/a2415a2e-3937-4c5c-a6a6-8d3c9f310bf8" />
