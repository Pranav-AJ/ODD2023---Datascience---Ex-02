# Ex02-Outlier
You are given bhp.csv which contains property prices in the city of banglore, India. You need to examine price_per_sqft column and do following,

## Algorithm

(1) Remove outliers using IQR

(2) After removing outliers in step 1, you get a new dataframe.

(3) use zscore of 3 to remove outliers. This is quite similar to IQR and you will get exact same result

(4) for the data set height_weight.csv find the following

(i) Using IQR detect weight outliers and print them

(ii) Using IQR, detect height outliers and print them

## Code and Output
```
import pandas as pd
import seaborn as sns
import numpy as np
from scipy import stats
```
```
age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
df=pd.DataFrame(age)
df
```
![image](https://github.com/Pranav-AJ/ODD2023---Datascience---Ex-02/assets/118904526/121bb183-4e6e-4849-85f1-fe9a05c30419)

```
q1=df.quantile(0.25)
q2=df.quantile(0.5)
q3=df.quantile(0.75)
iqr=q3-q1
iqr
```
![image](https://github.com/Pranav-AJ/ODD2023---Datascience---Ex-02/assets/118904526/40c3ed31-fce2-4b1f-ae46-f3ce4a962c8c)

```
low=q1-1.5*iqr
low
```
![image](https://github.com/Pranav-AJ/ODD2023---Datascience---Ex-02/assets/118904526/1313449e-fd92-4293-a058-e62778d144a4)

```
high=q3+1.5*iqr
high
```
![image](https://github.com/Pranav-AJ/ODD2023---Datascience---Ex-02/assets/118904526/84e1dfa4-af88-4013-b772-83b7e73b803e)

```
aq=df[((df>=low) & (df<=high))]
aq.dropna()
```
![image](https://github.com/Pranav-AJ/ODD2023---Datascience---Ex-02/assets/118904526/30a8aefc-acf1-470c-abbd-a7328e60b714)

sns.scatterplot(data=aq)

![image](https://github.com/Pranav-AJ/ODD2023---Datascience---Ex-02/assets/118904526/d8af704f-9810-428e-ae7c-a660ea83c2a8)

sns.boxplot(data=aq)

![image](https://github.com/Pranav-AJ/ODD2023---Datascience---Ex-02/assets/118904526/acecbdb1-9780-4c59-af54-cee21e7da37a)

```
df=pd.read_csv('heights.csv')
df
```
![image](https://github.com/Pranav-AJ/ODD2023---Datascience---Ex-02/assets/118904526/47db2bb3-5cad-4ca6-996c-8e775fa5ded7)

```
max=df['height'].quantile(0.75)
min=df['height'].quantile(0.25)
iqr=max-min
print(max,min)
print(iqr)
```
![image](https://github.com/Pranav-AJ/ODD2023---Datascience---Ex-02/assets/118904526/e77e6633-3945-4405-afda-0d1df20bad26)

```
qa=df[(df['height']>=min)& (df['height']<=max)]
qa
```
![image](https://github.com/Pranav-AJ/ODD2023---Datascience---Ex-02/assets/118904526/72a8d9cb-fa56-44d2-812f-52809917bac6)

```
low=min-1.5*iqr
high=max+1.5*iqr
print(low)
print(high)
```
![image](https://github.com/Pranav-AJ/ODD2023---Datascience---Ex-02/assets/118904526/64b15480-1a1f-46bf-82bb-ff5098f19bfd)

sns.boxplot(data=df)

![image](https://github.com/Pranav-AJ/ODD2023---Datascience---Ex-02/assets/118904526/c58e57ac-efe2-4a6b-85f6-cf580c296e6e)

sns.boxplot(data=qa)

![image](https://github.com/Pranav-AJ/ODD2023---Datascience---Ex-02/assets/118904526/009b24b9-847f-4bf5-bf35-15ff1ef79718)

**Z SCORE**
```
data={'weight':[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]}
#weight=[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]
df=pd.DataFrame(data)
df
```
![image](https://github.com/Pranav-AJ/ODD2023---Datascience---Ex-02/assets/118904526/5ed66b0c-363b-4c74-8d97-ace713a0609d)

```
z=np.abs(stats.zscore(df))
print(df[z['weight']>3])
```
![image](https://github.com/Pranav-AJ/ODD2023---Datascience---Ex-02/assets/118904526/76ac0638-f9d9-42c4-9540-46db35e44ea8)

```
out=[]
def d_o(val):
  ts=3
  m=np.mean(val)
  sd=np.std(val)
  for i in val:
    z=(i-m)/sd
    if np.abs(z)>ts:
      out.append(i)
  return out
op=d_o(weight)
op
```
![image](https://github.com/Pranav-AJ/ODD2023---Datascience---Ex-02/assets/118904526/89e8f0d5-16e9-41f6-8843-2621e49b68b4)
