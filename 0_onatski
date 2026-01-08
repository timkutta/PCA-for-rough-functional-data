# ============================================================
#  Onatski Eigenvalue-Ratio Criterion
# ============================================================
# Input:
#   lambdas : numeric vector of sample eigenvalues in decreasing order
#   K1      : maximum index to consider (integer >= 1)
#   q_alpha : (1 - alpha) quantile of the null statistic
#
# Output:
#   A list with:
#     R          : vector of eigenvalue ratios
#     Lambda_hat : max ratio statistic
#     K_hat      : estimated number of spikes
# ============================================================

onatski_ratio <- function(lambdas, K1, q_alpha) {
  
  stopifnot(is.numeric(lambdas), K1 >= 1, is.numeric(q_alpha))
  
  lambdas <- sort(lambdas, decreasing = TRUE)
  p <- length(lambdas)
  
  # Need K1+2 to construct K1 ratios
  if (p < K1 + 2) {
    stop("Need at least K1 + 2 eigenvalues.")
  }
  
  # Compute ratios vectorized
  R <- (lambdas[1:K1] - lambdas[2:(K1 + 1)]) /
       (lambdas[2:(K1 + 1)] - lambdas[3:(K1 + 2)])
  
  Lambda_hat <- max(R)
  K_hat <- if (Lambda_hat <= q_alpha) 0 else max(which(R > q_alpha))
  
  list(R = R, Lambda_hat = Lambda_hat, K_hat = K_hat)
}


# ============================================================
#  Simulate null distribution of Onatski ratio statistic
# ============================================================
# Input:
#   n      : sample size
#   p      : dimension
#   K1     : maximum index for ratios
#   alpha  : significance level (default 0.05)
#   nrep   : Monte Carlo replications
#
# Output:
#   Empirical (1 - alpha) quantile of Lambda_hat
# ============================================================

simulate_null_quantile <- function(n, p, K1, alpha = 0.05, nrep = 1000) {
  
  stopifnot(n > 0, p > 0, K1 >= 1, nrep >= 1)
  
  Lambda_vals <- numeric(nrep)
  
  for (r in seq_len(nrep)) {
    
    X <- matrix(rnorm(n * p), nrow = n)
    S <- crossprod(X) / n   # faster + cleaner
    
    lambdas <- sort(eigen(S, symmetric = TRUE, only.values = TRUE)$values,
                    decreasing = TRUE)
    
    # Ratios (vectorized as above)
    R <- (lambdas[1:K1] - lambdas[2:(K1 + 1)]) /
         (lambdas[2:(K1 + 1)] - lambdas[3:(K1 + 2)])
    
    Lambda_vals[r] <- max(R)
  }
  
  quantile(Lambda_vals, probs = 1 - alpha, names = FALSE)
}


# ============================================================
# Example usage
# ============================================================
set.seed(1)

K1 <- 3
q_alpha <- simulate_null_quantile(
  n     = 500,
  p     = 500,
  K1    = K1,
  alpha = 0.05,
  nrep  = 5000
)

print(q_alpha)
