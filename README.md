# ResearchIBD
import pandas as pd
import numpy as np
import __builtin__
from scipy import stats
import matplotlib.pyplot as plt

%matplotlib inline

df = pd.read_csv('/Users/ha-neuljung/Desktop/InternshipResearch/IBD Data/IBD_revised.csv')
#df = pd.read_csv('/Users/ha-neuljung/Desktop/InternshipResearch/IBD Data/IBD w distribution.csv')
#df2 = pd.read_csv('/Users/ha-neuljung/Desktop/InternshipResearch/IBD Data/IBD databse for analysis.csv')

df=df.fillna('n/a')

df

num_sample = df.shape[0]
cut_individual=[]
for i in range(num_sample):
    rw = df.iloc[i].value_counts()[non_available]
    rw=rw.fillna(0)
    
    
    if sum(rw) >11:
        cut_individual.append(i)
        
        
len(cut_individual)
df = df.drop(df.index[cut_individual])
df.shape


negative = ['no', 'none', 'no-', 'NO', 'none']
non_available = ['n/a', 'not applicable', 'n.a', 'nan', 'N/A']


ID = df['ID number '].tolist()
gender = df['Gender'].tolist()
age = df['Age'].tolist()
typesofibd = df['Type of IBD'].tolist()
smoking = df['Smoking '].tolist()
family = df['Family history '].tolist()
allergies = df['Allergies'].tolist()
extent = df['Extent of disease  - severity'].tolist()
symptom = df['Symptoms -Intestinal experiencing presently'].tolist()
symptom_extra = df['Symptoms - Extra-intestinal (arthritis, rash, uveitis etc.)'].tolist()
complication  = df['Complications (for example Colon cancer, Diverticulosis, C.diff infection)'].tolist()
psychology = df['Psychological disorders / therapy '].tolist()
BMI = df['BMI'].tolist()
weight = df['Weight'].tolist()
antibiotics = df['Anitbiotics used'].tolist()
drugs = df['Drug abuse '].tolist()
alcohol = df['Alcohol use '].tolist()
other_medical = df['other medical problems '].tolist()
#alcohol_category = df['Alcohol use_category']
num_flare_up = df['No. of flares in last 5 years ( Many/ few)'].tolist()


#folic_acid = df2['Folic Acid']
#high_bp = df2['High BP']
#cvd=df2['CVD']
#fish = df2['Fish Oil/Omega-3']

#ID2 = df2['ID number']


temp = []

for i in range(len(smoking)):
   
    s = num_flare_up[i]
    if pd.isnull(s):
        s = 'N/A'
    
  
    if __builtin__.any(x in s for x in non_available) and len(s)<15: 
        temp.append('N/A')
       
        
    elif __builtin__.any(x in s for x in negative) and len(s)<15:
        temp.append('No')
    elif s.isdigit() and np.float(s)==0:
        temp.append('No')
        
    elif 'many' in s or 'ongoing' in s or 'multiple' in s:
        temp.append('Many')
    else:
        temp.append('Few')
        #print s
        

num_flare_up_hist = pd.Series(temp)
num_flare_up_hist.value_counts() 

