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

temp = []

for i in range(len(smoking)):
   
    s = gender[i]
  
    if 'female' in s:
        temp.append('Female')
        
    elif 'male' in s:
        temp.append('Male')
    else:
        print s
        temp.append('N/A')
        

gender_hist = pd.Series(temp)
gender_hist.value_counts() 


change = {'n/a': 'N/A'}
alcohol_category = alcohol_category.replace(change)

alcohol_category.index = range(568)
alcohol_category.value_counts()

temp = []
for i in range(len(df2.index)-1):
    id2 = ID2.iloc[i]
    ref = ID.index(id2)
    
    temp.append(severity[ref])
    

severity_rev = pd.Series(temp)




df2 = df2.replace([0.0, 1.0], ['No', 'Yes'])

folic_acid = df2['Folic Acid']
high_bp = df2['High BP']
cvd=df2['CVD']
anxiety = df2['Anxiety ']
depression =df2['Depression ']
multivitamin = df2['Multivitamins']
vitamin_d = df2['Vitamin D']
ID2 = df2['ID number']



#a.to_clipboard()
#h=a.copy()
#a


a =pd.crosstab(folic_acid, severity_rev)
col =a.columns.tolist().index('N/A')
if 'N/A' in a.index.tolist():
    row =a.index.tolist().index('N/A')
data_chisquare = a.values
            
x = np.delete(data_chisquare,(col), axis=1)
#x = np.delete(x,(3), axis = 1)
            
g,p,dof, expctd = stats.chi2_contingency(x)



temp = []

for i in range(len(smoking)):
    
    s = other_medical[i]
    if pd.isnull(s):
        s = 'N/A'
    
  
    if __builtin__.any(x in s for x in non_available) and len(s)<35: 
        temp.append('N/A')
        
    elif __builtin__.any(x in s for x in negative) and len(s)<35:
        temp.append('No-problems')
        
    else:
        temp.append('Has other problems')
        

other_medical_hist = pd.Series(temp)
other_medical_hist.value_counts() 



temp = []

for i in range(len(smoking)):
    
    s = age
    temp.append(s[i][:2])

age_hist = pd.Series(temp)




temp = []

for i in range(len(smoking)):
    
    s = alcohol[i]
    if pd.isnull(s):
        s='n/a'
    
    if __builtin__.any(x in s for x in non_available) and len(s)<15: 
        temp.append('N/A')
    
    elif __builtin__.any(x in s for x in negative):
        temp.append('No-Alcohol')
    else:
        temp.append('Used alcohol')

alcohol_hist = pd.Series(temp)
alcohol_hist.value_counts() 


temp = []

for i in range(len(smoking)):
    
    s = drugs[i]
    if pd.isnull(s):
        s = 'N/A'
    
    if __builtin__.any(x in s for x in non_available) and len(s)<15: 
        temp.append('N/A')
    
    elif __builtin__.any(x in s for x in negative):
        temp.append('No-drugs')
    else:
        temp.append('Used drugs')

drugs_hist = pd.Series(temp)
drugs_hist.value_counts() 













