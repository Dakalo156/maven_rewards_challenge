# Customer Segmantation
This is the analysis about Maven Rewards Challenge (Sept 2024).
The description of the challenge was: you’ll play the role of a Sr. Marketing Analyst at Maven Cafe. You've just run a test by sending different combinations of promotional offers to existing rewards members. Now that the 30-day period for the test has concluded, your task is to identify key customer segments and develop a data-driven strategy for future promotional messaging & targeting.

# Dataset
The dataset used in this analysis can be found of this link: https://mavenanalytics.io/challenges/maven-rewards-challenge/404c6060-60eb-400f-9bce-c3b9f97e9d5a

# Notebooks
This analysis is broken into 4 playbooks
* 00 - Is a simple exploratory analysis. Analysing data with minimal manipulations
* 01 - I used a principle of RFM (Recency, Frequency and Money) for segmenting customers using only the transactions they made
* 02 - I expanded RFM to include the offers the customers received, viewed and completed
* 03 - In 02 and 03 I only focussed on customers with full details. In this notebook 03, I focussed on the customers with missing details (this for me, represented the unknown class of customers)

# EDA
![image](https://github.com/user-attachments/assets/58d3e6a4-8c58-41cf-9001-2bb56391dc9b)

* The number of customers who joined the cafe increased as the years went by however this increase took a turn in 2018 when the number of new joiners started decreasing
* Most number of customers joined between 2017 July and 2018 February

![image](https://github.com/user-attachments/assets/ed0acde6-9add-4aaa-bd47-33888238cffa)
* Most number of customers who joined where about 10 at a particular date
* Lowest number of customers who joined is 1 and a max is 43

![image](https://github.com/user-attachments/assets/7ff95a7e-1665-4edf-ab84-313b7d60616a)
* Average Age is about 62 years old
* There are customers at max age of 118
* Most customers below 80 years old are males while those above 80 are females
* Customers classified as other are very few

![image](https://github.com/user-attachments/assets/33c346de-e436-407c-9f28-f516df4e3e1b)
* On average, Females and other customers are older compared to males

![image](https://github.com/user-attachments/assets/283fac84-9a37-42cd-9104-1b2861f8cfb2)
* As age increases, customer income increases
* Correlation is 0.31 between age and income

![image](https://github.com/user-attachments/assets/145ae55d-f37f-4f23-bc69-38e19d861c01)
* Average annual income is about $65 404.99 with a minimum of $30 000 and maximum of $120 000
* Most customers have low income (right tail distribution)
* More males have higher income below average income while female have more income above the average
* Customers classified as other gender, are have income across the whole spectrum of income

![image](https://github.com/user-attachments/assets/f45d7d7c-988c-486c-afa0-b2004ddae4d8)
* On avarage, females have higher income and males have lower income

![image](https://github.com/user-attachments/assets/d1cac919-b86c-4b33-adfc-0b1623ec4632)

![image](https://github.com/user-attachments/assets/7d359b21-c1f8-4d61-afe9-3d66248ec249)

* More customers are Males (57%) and other are the fewest customers (0.014%)

# Clustering - Customers with Full Details
KMeans clustering was used to segment customers into three segments.

## Model
![image](https://github.com/user-attachments/assets/058ed2af-cbdb-491e-9764-e9db656e27cf)

![image](https://github.com/user-attachments/assets/60f97342-276d-484e-9603-fec69973f93d)
* This step of PCA followed by clustering seems to indicate the best numbers of clusters much easier
* According to the above elbow method and silhouette score, a k = 3 is the best number of clusters

![image](https://github.com/user-attachments/assets/3dc01a66-e6b8-4d40-989a-cc399f903969)

![image](https://github.com/user-attachments/assets/0d05f20f-44f4-474a-a260-3948354c4518)

**Customer Clusters:**

* Cluster 0: Last bought long time ago, have lowest purchase frequency and spend low amount of money (Lost or churned customers)
* Cluster 1: Last bought more recently, have highest purchase frequency  and spend the highest amount (Loyal Customers -  keep coming and buying)
* Clsuter 3: Last bought recently, have low purcharse frequency and spent lowest amount of money (At risk customer - we might loose them)

## Customer Segments
![image](https://github.com/user-attachments/assets/148e6820-0849-40c7-8976-4748253a8060)

**For cluster 0 (Lost or Churned Customers):**

* Considering higher viewing of the offers received: ***discount_faf***, ***discount_229***, ***bogo_f19*** and ***bogo_4d5*** are the best options to send to this group
* ***discount_0b1***, ***bogo_9b9*** and ***discount_290*** have the highest completion to viewing ratio and they are also completed without being viewed. These are the same offers which are less viewed. Therefore these offers can be applied to customers without the need to send them to customers
* At a cut-off of 50% of completed to received offers, only ***bogo_0b1*** will not make it since it has a lower % ratio. Recommendation: don't focus on this offer.
* To get more than 60% conversion from receiving to completion focus on this offers: ***discount_faf***, ***discount_229*** and ***bogo_f19*** however to get the highest conversion focus on ***discount_faf***
* **Overall Recommendation**: For a higher return focus on this three offers in this group - ***discount_faf***, ***discount_229*** and ***bogo_f19***

![image](https://github.com/user-attachments/assets/3d813b18-1aaa-432b-9a7e-4e776241fa71)

**For cluster 1 (Loyal Customers):**

* Considering higher viewing of the offers received: ***discount_faf***, ***discount_229***, ***bogo_f19*** and ***bogo_4d5*** are the best options to send to this group
* ***discount_0b1***, ***bogo_9b9*** and ***discount_290*** have the highest completion to viewing ratio and they are also completed without being viewed. These are the same offers which are less viewed. Therefore these offers can be applied to customers without the need to send them to customers
* At a cut-off of 80% of completed to received offers, only ***bogo_4d5*** will not make it since it has a lower than 80% ratio.
* To get more than 80% conversion from receiving to completion focus on other offers besides ***bogo_4d5*** and ***informational offers*** however to get the highest conversions focus on ***discount_faf*** and ***discount_229***
* **Overall Recommendation**: Since these are loyal customers, sending all these offers will bring return or higher conversion.

![image](https://github.com/user-attachments/assets/f27f3385-4e8e-4ab2-a6ab-9aa57ac7c79a)

**For cluster 2 (At risk customers):**

* Considering higher viewing of the offers received: ***discount_faf***, ***discount_229***, ***bogo_f19***, ***bogo_4d5***, ***informational_5a8*** and ***bogo_ae2*** are the best options to send to this group
* ***discount_0b1***, ***bogo_9b9*** and ***discount_290*** have the highest completion to viewing ratio and no offers were completed without being viewed first. These are the same offers which are less viewed. Therefore these offers can be applied to customers without the need to send them to customers.
* All ratio for completed to received offers are below 50% however ***discount_faf*** and ***discount_229*** have highest % ratio.
* To get more than 40% conversion from receiving to completion focus on this offers: ***discount_faf*** and ***discount_229***
* **Overall Recommendation**: For a higher return focus on this two offers in this group - ***discount_faf*** and ***discount_229***. Since in this group, the return will be low, these offers in this group can be stopped or not sent.


## Conclusion

**Overall Offers:**

* In all clusters ***discount_faf*** and ***discount_229*** are the best two offers which will offer best outcomes. 
* In addition for higher viewing of the offers received ***bogo_f19***, ***bogo_4d5***. 
* Therefore the channels of sending offers should be all four: ***['web', 'email', 'mobile', 'social']***
* ***bogo_ob1*** has the highest dificulty and duration and lowest channels for sending offers. It's completion to receiving ratio is low however it's completion after viewing is high.
* Loyal customers will offer best return than other group of customers

# Clustering - Customers with missing details
KMeans clustering was used to segment customers into two segments.

## Model
![image](https://github.com/user-attachments/assets/7b48ecc1-8b24-4c95-a325-99a6e05d6377)

![image](https://github.com/user-attachments/assets/c224b9fa-b8fb-4790-a9aa-0fd71762068f)

* According to the above elbow method and silhouette score, a k = 2 is the best number of clusters

![image](https://github.com/user-attachments/assets/40419d1e-dd02-4aae-a4b8-84a0cef3eea5)

![image](https://github.com/user-attachments/assets/3a8c0eb2-6ea1-407a-969c-eaf70df29f3a)

**Customer Clusters:**
* Cluster 0: Customers who spent smallest amount of money and don't buy frequently and last bought some time ago (Lost Customers)
* Cluster 1: Customers who spent large amount of money and are very frequent in their purchases and last bought recently (Loyal Customers)

## Customer Segments
![image](https://github.com/user-attachments/assets/8ec10929-f4a4-436f-bb5e-f39bf9f497bb)

**For cluster 0 (Lost or Churned Customers):**

* Considering higher viewing of the offers received: ***discount_faf***, ***discount_229***, ***bogo_f19*** and ***bogo_4d5*** are the best options to send to this group
* ***discount_229***, ***bogo_9b9*** and ***discount_faf*** have the highest completion to viewing ratio. These are the same offers which are mostly viewed after being received as well.
* ***discount_229***, ***bogo_9b9*** and ***discount_faf*** have the best completion ratio after being received.
* **Overall Recommendation**: Do not focus on sending offers to this group as the conversion is very low. However, if offers must be sent, for a higher return focus on this three offers in this group - ***discount_faf***, ***discount_229*** and ***bogo_9b9***. 

![image](https://github.com/user-attachments/assets/36abe7a1-d302-4a35-9c41-628548c168e2)
**For cluster 1 (Loyal Customers):**

* Considering higher viewing of the offers received: ***discount_faf***, ***discount_229***, ***bogo_f19***, ***bogo_ae2***, ***informational_5a8*** and ***bogo_4d5*** are the best options to send to this group
* ***discount_229***, ***bogo_9b9*** and ***discount_faf*** have the highest completion to viewing ratio. These are the same offers which are mostly viewed after being received as well.
* ***discount_faf***, ***bogo_9b9*** and ***discount_229*** have the best completion ratio after being received.
* **Overall Recommendation**: Send offers ***discount_faf*** and ***discount_229*** to this group as the conversion is above 50%. 

## Conclusion
**Overall Offers:**

* In all clusters ***discount_faf*** and ***discount_229*** are the best two offers which will offer best outcomes. 
* In addition for higher viewing of the offers received ***discount_229***, ***bogo_9b9*** and ***discount_faf***. 
* Therefore the channels of sending offers should be all four: ***['web', 'email', 'mobile', 'social']***
* Loyal customers will offer best return than other group of customers
* This section of customers represent uncertainty where either leaving or including them can bring about loss or benefits. 
