---
title: "M5 Forecasting - Uncertainty"
author: "Ioannis Nasios"
date: "July 9, 2020"
output: html_document
---

kaggle name: Ouranos  

<br />  

You can visit [M5 Uncertainty competition](https://www.kaggle.com/c/m5-forecasting-uncertainty/) for more info about the competition or/and raw data.  
To learn more about my solution you can visit my [write-up](https://www.kaggle.com/c/m5-forecasting-uncertainty/discussion/166875).  

<br />
Our joint paper (with  my colleague Konstantinos Vogklis) is published by  
**[IJF](https://www.sciencedirect.com/science/article/pii/S0169207022000012).**  
Preprint can be found [here](https://www.researchgate.net/publication/358384908_Blending_gradient_boosted_trees_and_neural_networks_for_point_and_probabilistic_forecasting_of_hierarchical_time_series).  

<br />

#### **HARDWARE: (The following specs were used to create the original solution)**  
CPU: Intel(R) Xeon(R) CPU X5650  @ 2.67GHz with 24 cores  
GPU: GeForce GTX 1080 (server has 2 gpus but I only used 1)  
74 GB memory (used only a fraction)    

<br />
  
#### **OS/platforms:**   
Ubuntu 18.04.2 LTS  

<br />

#### **SOFTWARE (python packages are detailed separately in `requirements.txt`):**
Python 3.6.7  
CUDA 10.0.130  
cuddn 7.5.0  
nvidia drivers version 410.48  

<br />  
<br />  


#### **How to train your model**
cd M5_Uncertainty_3rd_place  
mkdir submissions  
mkdir processed_data  
mkdir lgbm_datasets  
mkdir models    

<br />

##### **Prepare data for lightGBM model**  
* python prepare_data.py  
Read training data from RAW_DATA_DIR (specified in SETTINGS.json)  
Run any preprocessing steps  
Save the processed data to PROCESSED_DATA_DIR (specified in SETTINGS.json)  

<br />

##### **Train models**  
* python train.py  
Read training data both from RAW_DATA_DIR and PROCESSED_DATA_DIR (specified in SETTINGS.json)  
Train and Save model weights to MODELS_DIR (specified in SETTINGS.json)  

<br />

##### **Make predictions - submission files **  
* python predict.py  
**Predictions for M5 Accuracy competition, used as starting point to M5 uncertainty competition.**  
Read test data both from RAW_DATA_DIR and PROCESSED_DATA_DIR (specified in SETTINGS.json)  
Load models from MODELS_DIR (specified in SETTINGS.json)  
Use models to make predictions on new samples  
Save predictions with filename 'lgbm3keras1.csv.gz' to SUBMISSION_DIR (specified in SETTINGS.json)  

* python predict_uncertainty.py lgbm3keras1.csv.gz  
**Predictions for M5 uncertainty competition.**  
lgbm3keras1.csv.gz is the output of predict.py, located in SUBMISSION_DIR (specified in SETTINGS.json). Placing another file inside submissions folder and calling predict_uncertainty.py on that file will generate a different submission file (same name).  
Read test data from RAW_DATA_DIR (specified in SETTINGS.json)  
Load models M5 accuracy submission file placed in SUBMISSION_DIR (specified in SETTINGS.json)  
Make predictions on new samples  
Save predictions to SUBMISSION_DIR (specified in SETTINGS.json)  


 

  
<br />  
<br />  


#### **How to make predictions on a new test set**
To make predictions on new data, replace raw files with new.   
Raw files:  
- sales_train_evaluation.csv  
- calendar.csv  
- sell_prices.csv  
sample_submission.csv is also needed.   
Second half (rowwise) of submission file correspond to new predictions.  

<br /> 


#### **Outputs - Submissions**
* **M5 Uncertainty final submission: submission_uncertainty.csv**
* M5 Accuracy submission, used as starting point of M5 Uncertainty: lgbm3keras1.csv.gz  

* M5 Accuracy keras1 submission: Keras_CatEmb_final3_et1941_ver-17last.csv.gz  
* M5 Accuracy keras2 submission: Keras_CatEmb_final3_et1941_ver-EN1EN2Emb1.csv.gz  
* M5 Accuracy keras3 submission: Keras_CatEmb_final3_et1941_ver-noEN1EN2.csv.gz  

* M5 Accuracy average 3 keras submission: Keras_CatEmb_final3_et1941_ver-avg3.csv.gz
* M5 Accuracy lightgbm submission: lgbm_final_VER4.csv.gz  

<br />


#### **Key assumptions made by your code.**  
lgbm_datasets folder must be empty when starting a training run


<br />


