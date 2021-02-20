This code is the companion to "Impact of sex and pathophysiology on optimal drug choice in hypertensive rats: quantitative insights for precision medicine" by Sameed Ahmed, Jennifer C. Sullivan, and Anita T. Layton.

This file contains information about how to run the code.

-----------------------------------------------------------------------------

Data
male/female_AngII_data.xlsx
Raw data of time course response of mean arterial pressure (MAP) to chronic infusion of angiotensin (Ang) II for two weeks. Data is given for each rat. From Sullivan, 2010, Hypertension.

rat_male/female_AngII_data_bs_rep.mat
Bootstrap replicates of the time course response of MAP to Ang II infusion.

rat_male/female_ss_data_scenario_Normal.mat
Steady values of normotensive model variables.

rat_male/female_pars_scenario_Pri_Hyp_bs_rep1000.mat
Optimized parameter sets corresponding to each virtual individual in the virtual population.

rat_male/female_ss_data_scenario_Pri_Hyp_bs_rep1000.mat
Steady values of hypertensive model variables corresponding to each virtual individual in the virtual population.

rat_male/female_ss_data_scenario_Pri_Hyp_X.mat
Steady values of hypertensive model variables corresponding to each virtual individual in the virtual population before the drug dose, after the drug dose, and relative change. Also given are the mean and standard deviation of the response. These are given for the entire range of the drug dose. X indicates the drug class.

-----------------------------------------------------------------------------

get_pars.m
-Function that returns parameter vector required by bp_reg_mod.m.

bp_reg_mod.m
-Model equations file of the form f(t,x(t),x'(t);theta) = 0.
-Accepts inputs for perturbations (sodium loading, Ang II infusion, drug administration, etc.).

solve_ss_scenario.m
-Solves the steady state solution for different scenarios.

create_data_bs_rep.m
-Creates bootstrap replicates of the dataset of the time course response of MAP to Ang II infusion.

create_par_bs_rep.m
-Fits the subset of parameters corresponding to the pathophysiology of hypertension.
-The data fitted are three-fold. First, the constraints are satisfied for certain key physiological variables to be within range of measurements in the SHR. The other two datasets to be fit are perturbation experiments. One is dynamic response of MAP to Ang II infusion. The other is steady state MAP response to sodium loading.
-Calls upon solve_ss_hyp_fit.m.

solve_ss_hyp_fit.m
-Estimates the pathophysiological parameters by fitting to Ang II infusion data and sodium loading data, while satisfying the constraints of certain physiological variables being within range.
-Is called upon by create_par_bs_rep.m. 

create_vp.m
-Loads the bootstrap replicate parameter sets created for the virtual population. It then solves the corresponding steady state solution of the system for each parameter set and saves the result.

plot_vp_dist
-Loads the bootstrap replicate parameter sets and corresponding steady state variables for the virtual population. It then plots the distribution for each and saves the figures.

compute_err_hyp_fit.m
-Computes the error for the perturbation experiments for any user inputed virtual individual.
-The perturbation experiments are Ang II infusion and sodium loading.

run_sim_hyp_scen.m
-Simulates the dynamic blood pressure regulation model bp_reg_mod.m for various scenarios for a given virtual individual.
-Parameters and steady state data for the virtual population are calculated by create_par_bs_rep.m and create_vp.m, respectively.

run_sim_hyp_drugs.m
-Simulates the dynamic blood pressure regulation model bp_reg_mod.m for drug administration for a given virtual individual.
-Parameters and steady state data for the virtual population are calculated by create_par_bs_rep.m and create_vp.m, respectively.

solve_ss_drugs_dose_res.m
-Administers each drug for the entire inhibition range across the entire virtual population. 
-Saves the resulting steady state values of the model variables after drug administration.

plot_ss_drugs_post.m
-Performs post processing visualization on the result of administering a drug on the model for the entire inhibition range of the drug and the entire virtual population.
-Steady state data for the virtual population after drug administration are calculated by solve_ss_drugs_dose_res.m.

create_opt_drugs_class_dataset.m
-Creates the dataset on which to run the decision tree supervised learning classification algorithm that uses the pathophysiological profile as predictors for choosing the optimal drug class.
-The saved dataset can then be inputted into MATLAB's classification learner app.
-Parameters and steady state data for the virtual population are calculated by create_par_bs_rep.m and create_vp.m, respectively.

-----------------------------------------------------------------------------

man_figs_AngII.m
-Produces figure 1a from manuscript with appropriate formatting.

man_figs_Sodin.m
-Produces figure 1b from manuscript with appropriate formatting.

man_figs.m
-Produces figures 3, 4, 5 from manuscript with appropriate formatting.

