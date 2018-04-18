#' genFakeData
#'
#' @param fake_data 
#' @param mu_mean 
#' @param mu_sigma 
#' @param gamma_mean 
#' @param gamma_sigma 
#' @param sigma_mean 
#' @param sigma_sigma 
#' @param sigma_a_sigma 
#' @useDynLib anRpackage .registration = TRUE 
#' @return
#' @export
#'
#' @examples
genFakeData <- function(fake_data,
                        mu_mean = 700,
                        mu_sigma = 75,
                        gamma_mean = 0.5,
                        gamma_sigma = 1,
                        sigma_mean = 16,
                        sigma_sigma = 11,
                        sigma_a_sigma =100){                                                             
  
  stan_list <- list(run_estimation = 0,
                    N = nrow(fake_data),
                    I = length(unique(fake_data$id)),
                    ii = fake_data$id,
                    pre_test = fake_data$pre_test,
                    raw_score = fake_data$raw_score,
                    mu_mean = mu_mean,
                    mu_sigma = mu_sigma,
                    gamma_mean = gamma_mean,
                    gamma_sigma = gamma_sigma,
                    sigma_mean = sigma_mean,
                    sigma_sigma = sigma_sigma,
                    sigma_a_sigma =sigma_a_sigma)
  
  fit <- sampling(stanmodels$parcc, data = stan_list)
  
  
  fake_data_matrix  <- fit %>% 
    as.data.frame %>% 
    select(contains("score_sim"))
  
  return(fake_data_matrix)
  
}