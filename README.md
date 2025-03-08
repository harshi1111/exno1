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
#DROP NULL VALUES
df.dropna()
```
![image](https://github.com/user-attachments/assets/57487556-9d55-4946-98f6-282786099316)

```
#FILL NULL VALUES WITH CONSTANT VALUE "O"
df.fillna(0)
```
![image](https://github.com/user-attachments/assets/85873991-c861-4ba8-8425-32c2526565aa)

```
#CALCULATE MEAN VALUE OF A COLUMN AND FILL IT WITH NULL VALUES
value = df['sepal_length'].mean()
df['sepal_length'].fillna(value ,inplace = True)
df
```
![image](https://github.com/user-attachments/assets/afde12be-433c-4a84-9c61-aa4543247ed4)

```
#DROP NULL VALUES
df.dropna()
```
![image](https://github.com/user-attachments/assets/e6533ba5-c4c9-40db-a177-80129a1238ef)

```
import pandas as pd
import seaborn as sns
age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
af
```
![image](https://github.com/user-attachments/assets/7f935948-88b7-4f00-bfda-7a0283dff4fb)

```
#USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
sns.boxplot(x = df["sepal_length"])
```
![image](https://github.com/user-attachments/assets/7397ef48-a657-4d03-a55c-c1b106137b3c)

```
import pandas as pd

def detect_outliers(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower_bound = Q1 - 1.5 * IQR
    upper_bound = Q3 + 1.5 * IQR
    outliers = df[(df[column] < lower_bound) | (df[column] > upper_bound)]
    
    print(f"Outliers in {column}:\n", outliers)
    return outliers

# Example usage:
outliers_sepal = detect_outliers(df, 'sepal_length')
outliers_petal = detect_outliers(df, 'petal_length')
```
![image](https://github.com/user-attachments/assets/357e328c-70b7-4a79-a5a1-323406a7a0d2)

```
from scipy import stats #STATS METHOD IS USED TO IMPLEMENT Z SCORE METHOD
data=[1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,72,75,78,81,84,87,90,93,96,99,158]
df=pd.DataFrame(data,columns = ["Values"])
#USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
sns.boxplot(data)
```
![image](https://github.com/user-attachments/assets/960e8b06-6a3c-4f1d-b9ba-b275f56d17f2)

```
#PERFORM Z SCORE METHOD AND DETECT OUTLIER VALUES
df['Z-score'] = stats.zscore(df['Values'])
#REMOVE OUTLIERS
threshold = 3
df_cleaned = df[abs(df['Z-score']) <= threshold].drop(columns=['Z-score'])
print(df_cleaned)
```
![image](https://github.com/user-attachments/assets/be7eefda-66ce-44ed-8626-0a1d819887c6)

```
#USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED
sns.boxplot(x=df_cleaned["Values"])
```
![image](https://github.com/user-attachments/assets/71c2f73c-5339-4222-bd6d-b3cfe1694c69)


# Result
Thus, the Data Cleaning Process is executed Successfully.
