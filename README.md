# Medicaid Spending 

This is a project that analyzes data from 2016-2020 and predicts Medicaid spending based on the data.  

## Dataset 

The data is collected from the [Center for Medicare and Medicaid Services](https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/NationalHealthExpendData/NHE-Fact-Sheet) website.

## Data Visualization and Analysis 

My analysis centered on a subset of the available data: 
<br>

**Brand Name**: The name of the drug filled. This includes both brand names (drugs that have a trademarked name) and generic names (drugs that do not have a trademarked name).
<br>

**Generic Name**: A term referring to the chemical ingredient of a drug rather than the trademarked brand name under which the drug is sold.
<br>

**Manufacturer Name**: Name of the manufacturer of the drug.
<br>

**Total Spending**: Aggregate drug spending for the Medicaid program during the specified benefit year.
<br>

**Total Dosage Units**: The sum of the dosage units of medication dispensed across the calendar year (e.g. number of tablets, grams, milliliters or other units). Unit refers to the drug unit in the lowest dispensable amount.
<br>

**Total Dosage Claims**: Number of prescription fills for each drug. Includes original prescriptions and refills.
<br>

**Total Spending Per Dosage Unit**: Medicaid drug spending divided by the number of dosage units, which is weighted by the proportion of total claims.
<br>

**Average Spending Per Claim**: Medicaid drug spending divided by the number of prescription fills.
<br>

The dataset contained 2552 brand names, 1665 generic names, and 501 different manufactuers. 

### Top brand names 

In February of 2016, the FDA approved Harvani, a new drug used to treat Hepatitis C. Priced at over $1,100 per capsule ($1,127.76 to be exact), the average spending per claim totaled to a whopping $27,502.56. In contrast, in 2016, the median average spending per medicare claim was $77.26, and the median dosage unit cost was $2.22. The novelty of the drug, along with an aggressive and costly advertising campaign and high prices drove up profits for the drug manufacturer, Gilead Sciences, the top earner of Medicaid spending in 2016. Interestingly enough, the drug dropped off the top ten list abruptly from 2018 onwards, which suggests a decreased interest in it.  

<br>
Vyvanse, which treats ADHD and binge-eating disorders, sat in the top five for all five years. Latuda, an antipsychotic used to treat schizoprenia, consistently ranked in the top ten sources of Medicaid spending and topped the list in 2019 and 2020 (see discussion in generic brands section). There were no other drugs that appeared in the top ten list all 5 years, but a two appeared 4 out of the 5 years: Lyrica, a nerve pain medication that can treat seizures and Humira Pen, an immunosuppressive drug used to treat arthritis that topped the list in 2017 and 2018. While Lyrica only costs $32 per unit, Humira Pen cost over $1,900 in 2016, and each claim averaged to about $4,500. The price increased over the years as well. 
<br> 

The following bar illustrates that a handful of health problems dominated medicare spending. Notably, brands that treat schizoprenia and lucid disorders sat in the top three in both 2019 and 2020. Over one quarter of the top ten brands treat lucid disorders. Almost one fifth of the spots were occupied by insulin sources. 

<img width="747" alt="Screen Shot 2022-11-17 at 4 45 09 PM" src="https://user-images.githubusercontent.com/74522146/202576150-dfe7046d-754b-4151-afe4-9927df7011a7.png">

The following quote from the [Kaiser Family Foundation](https://www.kff.org/medicaid/issue-brief/medicaids-role-in-financing-behavioral-health-services-for-low-income-individuals/) suggests a reason behind the dominance of antipsychotics in the list:
<br>
"As a major source of insurance coverage for low-income Americans, and as the only source of funding for some specialized behavioral health services, Medicaid plays a key role in covering and financing behavioral health care. In 2015, Medicaid covered 21% of adults with mental illness, 26% of adults with serious mental illness (SMI), and 17% of adults with SUD. In comparison, Medicaid covered 14% of the general adult population."

<br>
 <img width="634" alt="Screen Shot 2022-11-18 at 2 33 13 AM" src="https://user-images.githubusercontent.com/74522146/202657203-6404b3f8-d24b-44eb-8200-7b98ec2ebaca.png">


### Top generic brands

Two medications share the same generic brand if they share the same active ingredients. 

Insulin Glargine consistently held the top or second highest position across all five years. Adamlimumab (Humira Pen), used to treat arthritis and other autoimmune diseases, consistently sat in the top five. Other generic names that consistently sat in the top ten are Aripiprazole (Abilify) used to treat schizoprenia, Lisdexamfetamine (Vyvanse) used to treat ADHD and OCD, Paliperidone (Invega, Trenza, etc.) used to treat schizoprenia, and Lurasidone HCL, also used to treat schizoprenia and other lurid disorders. Lurasidone HCL sat in the top 3 list from 2018-2020. The data corroborates the fact that lurid disorders are a top source of Medicaid spending.

As we saw with the brand names, Ledipasvir (Harvani) topped the list in 2016 and sat in third place in 2017 but did not appear again in subsequent years. 2016 data is shown below. 


### Top manufacturers 

A small handful of companies dominated the top ten list for manufacturers. Gilead Sciences, Eli Lilly & Co. (specializing in diabetes and antipsychotics), and Novo Nordisk (known for diabetes medication) consistently sat in the top 5 spots while Genentech and Merck Sharp & D appeared in the top 10 all five years. All but six companies that appeared on the Top 10 list appeared multiple times. 

From 2016-2018, Gilead Sciences was the top earner of Medicaid money, earning twice as much as the second contender in 2016 and 2017 (see bar graph below for 2016 data). By 2020, Gilead had dropped to fifth place. Since they specialize in antiviral drugs and Hepatitis C medication was the top source of Medicaid spending for 2016, this makes sense.  

<img width="678" alt="Screen Shot 2022-11-17 at 4 23 54 PM" src="https://user-images.githubusercontent.com/74522146/202572941-3b4a06fc-2cb3-4b9f-bd8a-77cd5f15765d.png"> 

### Data Statistics 

The data is very skewed, exhibiting tail heavy behavior. This can be seen from the density distribution in the plot below. In order to mitigate the tail heavy behavior, we try a regression oversampling technique called [Synthetic Minority Over-Sampling Technique for Regression with Gaussian Noise](https://github.com/nickkunz/smogn). While the oversampling clearly shifted the distribution in the correct direction, we do not see any improvements in median absolute error when we use the altered data to train a decision tree and support vector machine. 

<img width="564" alt="Screen Shot 2022-11-18 at 1 42 41 AM" src="https://user-images.githubusercontent.com/74522146/202648151-4ad51b27-9924-4cf2-aeb2-ab2d6dd49379.png">

## Spending Prediction 

We use a wide variety of common models to predict Medicaid spending in 2020 based on brand, generic, and manufacturer name and the number of doses, claims, cost per dosage, etc. from 2019. The models were trained on data from 2016 - 2019. As a measure of accuracy, we choose median absolute error (MSE), which is more robust to skewed data than standard mean-based measures of accuracy. Overall, the decision tree classifier, which is more robust than the other models when the data is skewed, performed the best, with a MSE of around 100,000. While this is still not a great number, the median spending per entry was over 300,000, so the prediction on average estimated within 33% of the true value. Furthermore, the $R^2$ score came close to 90 percent, which suggests the model is a good fit for the test data. A summary of the results is shown below. 

| Model | MSE | R2 Score | 
| --- | --- | --- |
| Decision Tree | 97871 | 0.8714 |
| Decision Tree + Bagging | 98657 | 0.8888 |
| Voting | 324999 | 0.5479 |
| Nearest Neighbors | 350729 | 1 |
| Support Vector Machine | 615257 | -0.03750 |
| Stochastic Gradient Descent | 7465638 | 0.09195 |
| Linear Regression | 7585091 | 0.07849 |
| adaBoost | 8085436 | 0.7897 |
