# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
```
from google.colab import drive
drive.mount('/content/drive')
```
![image](https://github.com/user-attachments/assets/c0c28269-72cf-42bc-8ed2-45aff3794814)

```
import pandas as pd
#READ CSV FILE HERE
df = pd.read_csv("/content/drive/MyDrive/Data_Science/iris.csv")
```
```
#DISPLAY THE INFORMATION ABOUT CSV AND RUN THE BASIC DATA ANALYSIS FUNCTIONS
df.info()
```
![image](https://github.com/user-attachments/assets/25e55767-d185-435e-96d8-019574bc11d7)

```
#CHECK OUT NULL VALUES IN DATA SET USING FUNCTION
df.isnull()
```
![image](https://github.com/user-attachments/assets/b630094e-1fb9-4fae-9659-44d21741fcca)

```
#DISPLAY THE SUM ON NULL VALUES IN EACH ROWS
df.isnull().sum()
```
![image](https://github.com/user-attachments/assets/d2baa298-2f8f-4d24-8ce0-18d9b0cb73e2)

```
#FILL NULL VALUES WITH ffill or bfill METHOD
df.fillna(method = "ffill")
```
![image](https://github.com/user-attachments/assets/4f822880-e086-4901-86aa-0bc99e477c48)

```
#CALCULATE MEAN VALUE OF A COLUMN AND FILL IT WITH NULL VALUES
value = df['sepal_length'].mean()
df['sepal_length'].fillna(value ,inplace = True)
df
```
![image](https://github.com/user-attachments/assets/26482227-9df2-48d7-9e31-fedf2c87fde4)

```
#DROP NULL VALUES
df.dropna()
```
![image](https://github.com/user-attachments/assets/db198a7a-8b2d-4133-8174-765c1459bce6)


```
import pandas as pd
import seaborn as sns

```
```
age = [1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af = pd.DataFrame(age, columns=['Age'])
```

```
#USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
sns.boxplot(x=af['Age']).set(title='Boxplot of Age')
```
![image](https://github.com/user-attachments/assets/bdd617f4-76b2-44a7-84c0-ad9cf98b35b2)


```
#PERFORM IQR METHOD AND DETECT OUTLIER VALUES
import pandas as pd

def detect_outliers(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower_bound = Q1 - 1.2 * IQR
    upper_bound = Q3 + 1.2 * IQR

    print(f"Q1: {Q1}, Q3: {Q3}, IQR: {IQR}")
    print(f"Lower bound: {lower_bound}, Upper bound: {upper_bound}")
    outliers = df[(df[column] < lower_bound) | (df[column] > upper_bound)]
    return outliers

detect_outliers(af, 'Age')
```
![image](https://github.com/user-attachments/assets/39eabfdf-a055-4712-b108-00ee6f065f36)

```
#REMOVE OUTLIERS
import pandas as pd

def detect_outliers(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower_bound = Q1 - 1.2 * IQR
    upper_bound = Q3 + 1.2 * IQR

    print(f"Q1: {Q1}, Q3: {Q3}, IQR: {IQR}")
    print(f"Lower bound: {lower_bound}, Upper bound: {upper_bound}")
    outliers = df[(df[column] < lower_bound) | (df[column] > upper_bound)]
    return outliers

detect_outliers(df, 'Datas')
```
![image](https://github.com/user-attachments/assets/56277390-bea6-41a2-b914-9e8a106d403d)


```
#USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED
sns.boxplot(x=af_cleaned['Age']).set(title='Boxplot of Age After Removing Outliers')
```
![image](https://github.com/user-attachments/assets/8ec4b310-665c-4d66-8783-bf33c4b90898)

```
data=[1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,72,75,78,81,84,87,90,93,96,99,158]
df=pd.DataFrame(data,columns = ["Datas"])
```

```
#USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
sns.boxplot(x=df['Datas']).set(title='Boxplot of Age')
```
![image](https://github.com/user-attachments/assets/d8050326-0666-44dc-bdef-049652f71679)

```
#PERFORM Z SCORE METHOD AND DETECT OUTLIER VALUES
from scipy import stats
import pandas as pd

def detect_outliers_zscore(df, column):
    z_scores = stats.zscore(df[column])
    outliers = df[(z_scores < -3) | (z_scores > 3)]

    if outliers.empty:
        print(f"No outliers found in {column}.")
    else:
        print(f"Outliers in {column} using Z-Score:\n", outliers)

    return outliers

detect_outliers_zscore(df, 'Datas')

```
![image](https://github.com/user-attachments/assets/0cb59319-63ea-4a67-afe1-3233d620aebd)

```
#REMOVE OUTLIERS
def remove_outliers_zscore(df, column):
    z_scores = stats.zscore(df[column])
    df_cleaned = df[(z_scores > -3) & (z_scores < 3)]
    return df_cleaned

df_cleaned = remove_outliers_zscore(df, 'Datas')
```

```
#USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED
sns.boxplot(x=df_cleaned['Datas']).set(title='Boxplot of Cleaned Data')
```
![image](https://github.com/user-attachments/assets/ec2f1cf9-7ac5-474f-a3c9-d6d9cc17e893)



# Result
Thus, the Data Cleaning Process is executed Successfully.
