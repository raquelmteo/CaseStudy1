Case Study I
The project will be carried out in teams of 5 or 6 students.

Each team must appoint a team leader.

The team leader will be responsible for defining the project activities and assigning team members to each task within Microsoft Planner.

The project has a duration of 3 weeks, structured into three distinct sprints:

Sprint 1: Pre-processing

Sprint 2: Modeling

Sprint 3: Optimization and Explainability

The final grade for the project will be calculated based on the following weights for each sprint:

Sprint 1: 40% - Submission date: 22/09/2026 23:59

Sprint 2: 30% - Submission date: 29/09/2026 23:59

Sprint 3: 30% - Submission date: 6/10/2026 23:59

At the end of each week, all teams are required to present the activities they have completed and the results obtained during that sprint.

The notebook corresponding to each sprint must be submitted on Moodle.

 Problem Definition
Have you ever been charged for something you did not subscribe to? How hard could it be to get my invoice right?

One of the most important processes for telecommunications operators is service provisioning to a customer. This is the process responsible to provide you with the services you contracted and to charge you for them.

A simple 4 Play subscription - Internet, TV, mobile phone and fixed line - involves configuring multiple systems: 

CRM- Customer Relationship Management - the master system that keeps the information about the offers that the customer subscribed to; 
TV platform - defines the channels that the customer can watch;
Internet platform - defines the internet speed;
Billing system - responsible for billing the services and the usage that the customer makes of them. 
It is a complex process as there are hundreds of options, thousands of possible combinations and millions of customers. It is subject to errors, both human and automatic. For this reason, operators have different "audit" processes that try to ensure that all intervening systems are consistent with each other.

In this competition, we challenge you to predict the right bill for a customer given the services he contracted. The goal is to build a model that receives the configuration of the CRM system and predicts the correct configuration of the Billing system.

As mentioned, CRM is normally the master of the information of the services that the customer has subscribed to, so it will be possible to infer which configuration to expect in the Billing system. Note, however, that the configurations between these two systems may not be one to one, in many cases there are many to one configurations, that is, two different CRM configurations may point to the same Billing configuration. 

Characteristics of the problem
The dataset contains several provisioning errors, i.e. in the dataset it may happen that for a CRM configuration there are different configurations in Billing;
The dimension of the output 731 is very large;
Different CRM configurations can correspond to only one Billing configuration;
The individual variables of the CRM configuration may not have a direct correspondence to the individual variables of the Billing configuration; 

Evaluation

Submissions are evaluated according to the Exact Matching Ratio (EMR): the percentage of samples that have all their labels classified correctly. 

𝐸𝑀𝑅=1𝑛∑𝑖=1𝑛𝐼(𝑌𝑖=𝑍𝑖)
Where (I) is the indicator function, (n) is the number of samples, (k) the size of the labelset, (Y_i \in \{0,1\}^k) represents a label and (Z_i \in \{0,1\}^k) represents a prediction.
Only samples where all labels are correct will be considered as correct. In order to have a perfect score of (EMR = 1) all the labels for all samples need to correct.


Dataset Description
The configurations in both systems have been pre-processed in order to obtain only binary variables. This way, each column corresponds to an option in the configuration of the respective system (CRM / BILLING), the value 0 indicates that the option is inactive and the value 1 indicates that it is active. The training dataset contains one line for each client and given the set of CRM system settings, the objective is to return the Billing system configuration. The training dataset contains errors in the configuration of CRM/BILLING, however when testing only pairs of CRM-BILLING configurations that we deem as correct will be used.

File descriptions
train.csv - the training set
test.csv - the test set
sampleSubmission.csv - a sample submission file in the correct format
Data fields
The training dataset is structured as follows: 1 column to identify the customer, 745 columns for the CRM configuration and 731 for the BILLING configuration.

MSISDN - customer's identifier, this field is encrypted;
Columns that start with 'CRM' (2nd – 746th (inclusive)) - these correspond to the input configuration (CRM);
Columns that start with 'BIL' (747th – 1477th (inclusive)) - these correspond to the output configuration (BILLING);
The test dataset is structured as follows: 1 column to identify the customer and 745 columns for the CRM configuration.