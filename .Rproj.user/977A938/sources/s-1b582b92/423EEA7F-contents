data {
  int<lower = 0, upper = 1> run_estimation;               // a switch to evaluate the likelihood
  int N ;                                                 // number of observations
  int I ;                                                 // number of students
  int<lower=1,upper=I> ii[N];                             // student id index
  vector<lower=650,upper=850>[N] pre_test ;               // pre-test
  vector<lower=650,upper=850>[N] raw_score ;              // raw_score
  real mu_mean ;                                          //
  real<lower=0> mu_sigma;                                 //
  real gamma_mean;                                        //
  real<lower=0> gamma_sigma;                              //
  real sigma_mean ;                                       //
  real<lower=0> sigma_sigma;                              //
  real<lower=0> sigma_a_sigma;                            //
}

transformed data {
  real theta = sigma_mean/((sigma_sigma*sigma_sigma)) ;
  real k = sigma_mean/theta ;
}

parameters {
  real mu;
  vector[I] a_std;              
  real<lower=0> sigma_a;
  real<lower=0> gamma;
  real<lower=0> sigma;
}

transformed parameters {
  vector[I] a =  mu + sigma_a * a_std;                    // Matt trick
}

model {
  // priors
  mu ~ normal(mu_mean, mu_sigma);
  a_std ~ normal(0,1);
  sigma_a ~ normal(0,sigma_a_sigma);
  gamma ~ normal(gamma_mean,gamma_sigma);
  sigma ~ gamma(k,theta);
  // likelihood, which we only evaluate conditionally
  if(run_estimation==1){
    raw_score ~ normal(a[ii] + gamma*pre_test, sigma);
  }
}

generated quantities {
  vector[N] score_sim;
  vector[N] eta;
  for (n in 1:N)  {
    eta[n] = a[ii[n]] + gamma*pre_test[n] ;
    score_sim[n] = normal_rng(eta[n], sigma);
  }
}
