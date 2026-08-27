# logistics-and-supply-chain-analysis
Logistics Delivery Performance Analysis

Root-cause, profitability, and predictive-risk analysis of a global e-commerce fulfillment operation, built to identify why orders are delivered late, quantify the financial impact, and flag high-risk orders before dispatch.



Overview-
This project analyzes 172,765 orders (Jan 2015 – Jan 2018) from a global e-commerce platform to answer three questions:
How much of the business is affected by late delivery, and what does it cost?
What operational factors (shipping mode, region, order status, timing) actually drive delays?
Can we predict which orders are at risk of being late before they ship?




Headline result:- 54.71% of orders are delivered late, putting $2.1M in profit at risk. A Random Forest model trained on order-level features predicts late-delivery risk with 74% accuracy (78% precision on the late class), making it viable as a pre-dispatch alert system.




Key Findings-
Metric	Value
Total orders analyzed	172,765
Late delivery rate	54.71%
Total profit (profitable orders)	$7.5M
Profit at risk (delayed orders)	$2.1M
Predictive model accuracy (Random Forest)	74%
Precision on late orders	0.78
Recall on late orders	0.75




Biggest driver of delay:- shipping mode. First Class has a 100% delay rate, Second Class 79.8%, versus Standard Class at 39.8% — meaning shipping-mode assignment logic, not distance or region, is the dominant lever for fixing delivery performance.




Methodology-
Data Cleaning — removed cancelled orders, dropped redundant/PII columns, converted date fields to datetime.
Feature Engineering — derived Order Processing Time, Delay, Is_Delayed, and time-based features (order_month, order_day, order_hour), plus a Profitability Flag.
KPI Calculation — on-time/late delivery rate, total and at-risk profit, 90th-percentile delay.
Exploratory Analysis — profitability distribution, delay distribution, profit vs. delay days.
Bottleneck Detection — delay % by region, customer segment, shipping mode, order status, payment type, department.
Root Cause Analysis — deep-dive on the highest-delay region (Central Africa) to isolate top driver factors.
Time-Based Analysis — delay % by month, day of week, and hour of day to surface seasonal/capacity patterns.
Predictive Modeling — frequency-encoded categorical features, stratified train/test split, SMOTE oversampling for class imbalance, Random Forest classifier to predict Late_delivery_risk.




Tech Stack-
Python 3
pandas, numpy — data manipulation
matplotlib, seaborn — visualization
scikit-learn — Random Forest classification, train/test split, evaluation metrics
imbalanced-learn (SMOTE) — class imbalance handling
Setup
bash
pip install pandas numpy seaborn matplotlib scikit-learn imbalanced-learn jupyter
jupyter notebook logistics_analysis.ipynb




Strategic Recommendations-

Priority	                                        Recommendation

Critical              	Audit First Class & Second Class shipping capacity — both operate far outside their promised SLA
High                   	Deploy the predictive alert system in production to flag high-risk orders at confirmation
High	                  Resolve payment-processing bottlenecks (PAYMENT_REVIEW / PENDING_PAYMENT orders are disproportionately late)
Medium                	Build seasonal surge capacity plans for August, October, and December peaks
Medium	                Default eligible orders to Standard Class, which outperforms premium shipping modes
Medium                	Investigate high-delay departments (Outdoors, Golf) in Central Africa
Low	                    Review pricing/discounting tied to the 18.7% loss-making order share
Low	                    Retrain the predictive model quarterly with additional carrier and weather features





Author

Bhavishya pandita
