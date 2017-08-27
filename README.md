

```python
import pandas as pd
import numpy as np
import locale

locale.setlocale(locale.LC_ALL, 'en-US')

# declare path for student file
student_file = "Resources/PyCitySchools/students_complete.csv"

# declare path for school file
school_file = "Resources/PyCitySchools/schools_complete.csv"

#open files
student_pd = pd.read_csv(student_file)
school_pd = pd.read_csv(school_file)

school_pd.columns

# Rename columns for readability
renamed_school_pd = school_pd.rename(columns={
    "name": "School Name",
    "type": "School Type"
})

renamed_school_pd.head()

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>School Name</th>
      <th>School Type</th>
      <th>size</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
  </tbody>
</table>
</div>




```python
#renamed columns for merging

renamed_student_pd = student_pd.rename(columns={
    "name": "Student Name",
    "school" : "School Name"
})

renamed_student_pd.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>Student Name</th>
      <th>gender</th>
      <th>grade</th>
      <th>School Name</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>



# District Summary


```python
# get total schools
totalSchools = renamed_school_pd['School Name'].count()
df = pd.DataFrame([totalSchools], columns=['Total Schools'])
df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Schools</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>




```python
# get total students
totalStudents = renamed_student_pd['School Name'].count()
df["Total Students"] = locale.format("%d", totalStudents, grouping=True)
df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Schools</th>
      <th>Total Students</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39,170</td>
    </tr>
  </tbody>
</table>
</div>




```python
# total school budget
totalBudget = np.round(pd.to_numeric(renamed_school_pd['budget']).sum(), decimals=2)
# totalBudget
df["Total Budget"] = locale.currency(totalBudget, grouping=True)
# df
```


```python
# average math score
averageMathScore = renamed_student_pd["math_score"].mean()
df["Average Math Score"] = averageMathScore
df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Average Math Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39,170</td>
      <td>$24,649,428.00</td>
      <td>78.985371</td>
    </tr>
  </tbody>
</table>
</div>




```python
# average reading score
averageReadingScore = renamed_student_pd["reading_score"].mean()
df["Average Reading Score"] = averageReadingScore
df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39,170</td>
      <td>$24,649,428.00</td>
      <td>78.985371</td>
      <td>81.87784</td>
    </tr>
  </tbody>
</table>
</div>




```python
# get the number of students that scored 70 or more in Math
totalPassingMath = renamed_student_pd.loc[(renamed_student_pd["math_score"] >= 70)]["Student Name"].count()
percentPassingMath = (totalPassingMath / totalStudents) * 100
df["% Passing Math"] = percentPassingMath
df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39,170</td>
      <td>$24,649,428.00</td>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>74.980853</td>
    </tr>
  </tbody>
</table>
</div>




```python
# get the number of students that scored 70 or more in Reading
# totalPassingReading = renamed_student_pd.loc[(renamed_student_pd["reading_score"] >= 70)]["Student Name"].count()
totalPassingReading = renamed_student_pd[(renamed_student_pd["reading_score"] >= 70)]["Student Name"].count()
percentPassingReading = (totalPassingReading / totalStudents) * 100

df["% Passing Reading"] = percentPassingReading
df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39,170</td>
      <td>$24,649,428.00</td>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>74.980853</td>
      <td>85.805463</td>
    </tr>
  </tbody>
</table>
</div>




```python
# compute the average of the number of students that scored 70 or more in Math and those that scored 70 or more in Reading 
overallPassingRate = ((totalPassingMath + totalPassingReading) / 2) / totalStudents * 100

df["% Overall Passing Rate"] = overallPassingRate
df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39,170</td>
      <td>$24,649,428.00</td>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>74.980853</td>
      <td>85.805463</td>
      <td>80.393158</td>
    </tr>
  </tbody>
</table>
</div>



# School Summary


```python
merged_pd = renamed_school_pd.merge(renamed_student_pd, on='School Name', how='outer')
merged_pd.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>School Name</th>
      <th>School Type</th>
      <th>size</th>
      <th>budget</th>
      <th>Student ID</th>
      <th>Student Name</th>
      <th>gender</th>
      <th>grade</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
merged_pd.columns
```




    Index(['School ID', 'School Name', 'School Type', 'size', 'budget',
           'Student ID', 'Student Name', 'gender', 'grade', 'reading_score',
           'math_score'],
          dtype='object')




```python
# find total students, total budget, average math score, average reading score
# df = merged_pd.groupby(['School Name', 'School Type']).aggregate({'Student ID':'count','budget':'max', 'math_score': 'mean', 'reading_score': 'mean'})
df = merged_pd.groupby(['School Name']).aggregate({'School Type':'min','Student ID':'count','budget':'max', 'math_score': 'mean', 'reading_score': 'mean'})
df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Student ID</th>
      <th>budget</th>
      <th>math_score</th>
      <th>reading_score</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>77.048432</td>
      <td>81.033963</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>83.061895</td>
      <td>83.975780</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>76.711767</td>
      <td>81.158020</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>77.102592</td>
      <td>80.746258</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>83.351499</td>
      <td>83.816757</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Find the total # of students by School/District with math scores > 70 
TotalPassingMath = merged_pd[merged_pd['math_score'] >= 70].groupby(['School Name'])['math_score'].count()
df['Total Passing Math'] = TotalPassingMath
```


```python
# Find the total # of students by School/District with reading score > 70
TotalPassingReading = merged_pd[merged_pd['reading_score'] >= 70].groupby(['School Name'])['reading_score'].count()
df['Total Passing Reading'] = TotalPassingReading
```


```python
# calculate budget per student
df["Per Student Budget"] = df['budget']/df['Student ID']
df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Student ID</th>
      <th>budget</th>
      <th>math_score</th>
      <th>reading_score</th>
      <th>Total Passing Math</th>
      <th>Total Passing Reading</th>
      <th>Per Student Budget</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>3318</td>
      <td>4077</td>
      <td>628.0</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>1749</td>
      <td>1803</td>
      <td>582.0</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>1946</td>
      <td>2381</td>
      <td>639.0</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>1871</td>
      <td>2172</td>
      <td>644.0</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>1371</td>
      <td>1426</td>
      <td>625.0</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>3094</td>
      <td>3748</td>
      <td>652.0</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>395</td>
      <td>411</td>
      <td>581.0</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>1916</td>
      <td>2372</td>
      <td>655.0</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>3145</td>
      <td>3867</td>
      <td>650.0</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>910</td>
      <td>923</td>
      <td>609.0</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>2654</td>
      <td>3208</td>
      <td>637.0</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>1653</td>
      <td>1688</td>
      <td>600.0</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>1525</td>
      <td>1591</td>
      <td>638.0</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>2143</td>
      <td>2204</td>
      <td>578.0</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>1680</td>
      <td>1739</td>
      <td>583.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df["% Passing Math"] = df["Total Passing Math"]/df["Student ID"] * 100
```


```python
df["% Passing Reading"] = df["Total Passing Reading"]/df["Student ID"] * 100
```


```python
df["% Overall Passing Rate"] = ((df["Total Passing Math"] + df["Total Passing Reading"])/2)/df['Student ID'] * 100
```


```python
df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Student ID</th>
      <th>budget</th>
      <th>math_score</th>
      <th>reading_score</th>
      <th>Total Passing Math</th>
      <th>Total Passing Reading</th>
      <th>Per Student Budget</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>3318</td>
      <td>4077</td>
      <td>628.0</td>
      <td>66.680064</td>
      <td>81.933280</td>
      <td>74.306672</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>1749</td>
      <td>1803</td>
      <td>582.0</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>95.586652</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>1946</td>
      <td>2381</td>
      <td>639.0</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>73.363852</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>1871</td>
      <td>2172</td>
      <td>644.0</td>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>73.804308</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>1371</td>
      <td>1426</td>
      <td>625.0</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>95.265668</td>
    </tr>
  </tbody>
</table>
</div>




```python
# rename columns
df_renamed = df.rename(columns = {
    "budget":"Total School Budget",
    "Student ID": "Total Students",
    "math_score": "Average Math Score",
    "reading_score" : "Average Reading Score"
    
})
df_renamed.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>Total Passing Math</th>
      <th>Total Passing Reading</th>
      <th>Per Student Budget</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>3318</td>
      <td>4077</td>
      <td>628.0</td>
      <td>66.680064</td>
      <td>81.933280</td>
      <td>74.306672</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>1749</td>
      <td>1803</td>
      <td>582.0</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>95.586652</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>1946</td>
      <td>2381</td>
      <td>639.0</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>73.363852</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>1871</td>
      <td>2172</td>
      <td>644.0</td>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>73.804308</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>1371</td>
      <td>1426</td>
      <td>625.0</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>95.265668</td>
    </tr>
  </tbody>
</table>
</div>




```python
# select columns to show in report 
df_final = df_renamed[["School Type","Total Students","Total School Budget","Per Student Budget","Average Math Score","Average Reading Score","% Passing Math", "% Passing Reading","% Overall Passing Rate"]]
df_final
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>66.680064</td>
      <td>81.933280</td>
      <td>74.306672</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>95.586652</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>73.363852</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>73.804308</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>95.265668</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>66.752967</td>
      <td>80.862999</td>
      <td>73.807983</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>92.505855</td>
      <td>96.252927</td>
      <td>94.379391</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>65.683922</td>
      <td>81.316421</td>
      <td>73.500171</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>66.057551</td>
      <td>81.222432</td>
      <td>73.639992</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>94.594595</td>
      <td>95.945946</td>
      <td>95.270270</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>66.366592</td>
      <td>80.220055</td>
      <td>73.293323</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>93.867121</td>
      <td>95.854628</td>
      <td>94.860875</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>93.272171</td>
      <td>97.308869</td>
      <td>95.290520</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>93.867718</td>
      <td>96.539641</td>
      <td>95.203679</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>93.333333</td>
      <td>96.611111</td>
      <td>94.972222</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Final Report
df_final.style.format({"Total School Budget": "${:,.2f}", "Per Student Budget": "${:,.2f}"})
```




<style  type="text/css" >
</style>  
<table id="T_27024d2e_8b70_11e7_86ae_c821588b3f07" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >School Type</th> 
        <th class="col_heading level0 col1" >Total Students</th> 
        <th class="col_heading level0 col2" >Total School Budget</th> 
        <th class="col_heading level0 col3" >Per Student Budget</th> 
        <th class="col_heading level0 col4" >Average Math Score</th> 
        <th class="col_heading level0 col5" >Average Reading Score</th> 
        <th class="col_heading level0 col6" >% Passing Math</th> 
        <th class="col_heading level0 col7" >% Passing Reading</th> 
        <th class="col_heading level0 col8" >% Overall Passing Rate</th> 
    </tr>    <tr> 
        <th class="index_name level0" >School Name</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_27024d2e_8b70_11e7_86ae_c821588b3f07" class="row_heading level0 row0" >Bailey High School</th> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row0_col0" class="data row0 col0" >District</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row0_col1" class="data row0 col1" >4976</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row0_col2" class="data row0 col2" >$3,124,928.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row0_col3" class="data row0 col3" >$628.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row0_col4" class="data row0 col4" >77.0484</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row0_col5" class="data row0 col5" >81.034</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row0_col6" class="data row0 col6" >66.6801</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row0_col7" class="data row0 col7" >81.9333</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row0_col8" class="data row0 col8" >74.3067</td> 
    </tr>    <tr> 
        <th id="T_27024d2e_8b70_11e7_86ae_c821588b3f07" class="row_heading level0 row1" >Cabrera High School</th> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row1_col0" class="data row1 col0" >Charter</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row1_col1" class="data row1 col1" >1858</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row1_col2" class="data row1 col2" >$1,081,356.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row1_col3" class="data row1 col3" >$582.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row1_col4" class="data row1 col4" >83.0619</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row1_col5" class="data row1 col5" >83.9758</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row1_col6" class="data row1 col6" >94.1335</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row1_col7" class="data row1 col7" >97.0398</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row1_col8" class="data row1 col8" >95.5867</td> 
    </tr>    <tr> 
        <th id="T_27024d2e_8b70_11e7_86ae_c821588b3f07" class="row_heading level0 row2" >Figueroa High School</th> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row2_col0" class="data row2 col0" >District</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row2_col1" class="data row2 col1" >2949</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row2_col2" class="data row2 col2" >$1,884,411.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row2_col3" class="data row2 col3" >$639.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row2_col4" class="data row2 col4" >76.7118</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row2_col5" class="data row2 col5" >81.158</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row2_col6" class="data row2 col6" >65.9885</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row2_col7" class="data row2 col7" >80.7392</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row2_col8" class="data row2 col8" >73.3639</td> 
    </tr>    <tr> 
        <th id="T_27024d2e_8b70_11e7_86ae_c821588b3f07" class="row_heading level0 row3" >Ford High School</th> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row3_col0" class="data row3 col0" >District</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row3_col1" class="data row3 col1" >2739</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row3_col2" class="data row3 col2" >$1,763,916.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row3_col3" class="data row3 col3" >$644.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row3_col4" class="data row3 col4" >77.1026</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row3_col5" class="data row3 col5" >80.7463</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row3_col6" class="data row3 col6" >68.3096</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row3_col7" class="data row3 col7" >79.299</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row3_col8" class="data row3 col8" >73.8043</td> 
    </tr>    <tr> 
        <th id="T_27024d2e_8b70_11e7_86ae_c821588b3f07" class="row_heading level0 row4" >Griffin High School</th> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row4_col0" class="data row4 col0" >Charter</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row4_col1" class="data row4 col1" >1468</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row4_col2" class="data row4 col2" >$917,500.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row4_col3" class="data row4 col3" >$625.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row4_col4" class="data row4 col4" >83.3515</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row4_col5" class="data row4 col5" >83.8168</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row4_col6" class="data row4 col6" >93.3924</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row4_col7" class="data row4 col7" >97.139</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row4_col8" class="data row4 col8" >95.2657</td> 
    </tr>    <tr> 
        <th id="T_27024d2e_8b70_11e7_86ae_c821588b3f07" class="row_heading level0 row5" >Hernandez High School</th> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row5_col0" class="data row5 col0" >District</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row5_col1" class="data row5 col1" >4635</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row5_col2" class="data row5 col2" >$3,022,020.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row5_col3" class="data row5 col3" >$652.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row5_col4" class="data row5 col4" >77.2898</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row5_col5" class="data row5 col5" >80.9344</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row5_col6" class="data row5 col6" >66.753</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row5_col7" class="data row5 col7" >80.863</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row5_col8" class="data row5 col8" >73.808</td> 
    </tr>    <tr> 
        <th id="T_27024d2e_8b70_11e7_86ae_c821588b3f07" class="row_heading level0 row6" >Holden High School</th> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row6_col0" class="data row6 col0" >Charter</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row6_col1" class="data row6 col1" >427</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row6_col2" class="data row6 col2" >$248,087.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row6_col3" class="data row6 col3" >$581.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row6_col4" class="data row6 col4" >83.8033</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row6_col5" class="data row6 col5" >83.815</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row6_col6" class="data row6 col6" >92.5059</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row6_col7" class="data row6 col7" >96.2529</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row6_col8" class="data row6 col8" >94.3794</td> 
    </tr>    <tr> 
        <th id="T_27024d2e_8b70_11e7_86ae_c821588b3f07" class="row_heading level0 row7" >Huang High School</th> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row7_col0" class="data row7 col0" >District</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row7_col1" class="data row7 col1" >2917</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row7_col2" class="data row7 col2" >$1,910,635.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row7_col3" class="data row7 col3" >$655.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row7_col4" class="data row7 col4" >76.6294</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row7_col5" class="data row7 col5" >81.1827</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row7_col6" class="data row7 col6" >65.6839</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row7_col7" class="data row7 col7" >81.3164</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row7_col8" class="data row7 col8" >73.5002</td> 
    </tr>    <tr> 
        <th id="T_27024d2e_8b70_11e7_86ae_c821588b3f07" class="row_heading level0 row8" >Johnson High School</th> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row8_col0" class="data row8 col0" >District</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row8_col1" class="data row8 col1" >4761</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row8_col2" class="data row8 col2" >$3,094,650.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row8_col3" class="data row8 col3" >$650.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row8_col4" class="data row8 col4" >77.0725</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row8_col5" class="data row8 col5" >80.9664</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row8_col6" class="data row8 col6" >66.0576</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row8_col7" class="data row8 col7" >81.2224</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row8_col8" class="data row8 col8" >73.64</td> 
    </tr>    <tr> 
        <th id="T_27024d2e_8b70_11e7_86ae_c821588b3f07" class="row_heading level0 row9" >Pena High School</th> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row9_col0" class="data row9 col0" >Charter</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row9_col1" class="data row9 col1" >962</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row9_col2" class="data row9 col2" >$585,858.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row9_col3" class="data row9 col3" >$609.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row9_col4" class="data row9 col4" >83.8399</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row9_col5" class="data row9 col5" >84.0447</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row9_col6" class="data row9 col6" >94.5946</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row9_col7" class="data row9 col7" >95.9459</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row9_col8" class="data row9 col8" >95.2703</td> 
    </tr>    <tr> 
        <th id="T_27024d2e_8b70_11e7_86ae_c821588b3f07" class="row_heading level0 row10" >Rodriguez High School</th> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row10_col0" class="data row10 col0" >District</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row10_col1" class="data row10 col1" >3999</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row10_col2" class="data row10 col2" >$2,547,363.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row10_col3" class="data row10 col3" >$637.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row10_col4" class="data row10 col4" >76.8427</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row10_col5" class="data row10 col5" >80.7447</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row10_col6" class="data row10 col6" >66.3666</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row10_col7" class="data row10 col7" >80.2201</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row10_col8" class="data row10 col8" >73.2933</td> 
    </tr>    <tr> 
        <th id="T_27024d2e_8b70_11e7_86ae_c821588b3f07" class="row_heading level0 row11" >Shelton High School</th> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row11_col0" class="data row11 col0" >Charter</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row11_col1" class="data row11 col1" >1761</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row11_col2" class="data row11 col2" >$1,056,600.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row11_col3" class="data row11 col3" >$600.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row11_col4" class="data row11 col4" >83.3595</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row11_col5" class="data row11 col5" >83.7257</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row11_col6" class="data row11 col6" >93.8671</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row11_col7" class="data row11 col7" >95.8546</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row11_col8" class="data row11 col8" >94.8609</td> 
    </tr>    <tr> 
        <th id="T_27024d2e_8b70_11e7_86ae_c821588b3f07" class="row_heading level0 row12" >Thomas High School</th> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row12_col0" class="data row12 col0" >Charter</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row12_col1" class="data row12 col1" >1635</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row12_col2" class="data row12 col2" >$1,043,130.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row12_col3" class="data row12 col3" >$638.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row12_col4" class="data row12 col4" >83.4183</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row12_col5" class="data row12 col5" >83.8489</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row12_col6" class="data row12 col6" >93.2722</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row12_col7" class="data row12 col7" >97.3089</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row12_col8" class="data row12 col8" >95.2905</td> 
    </tr>    <tr> 
        <th id="T_27024d2e_8b70_11e7_86ae_c821588b3f07" class="row_heading level0 row13" >Wilson High School</th> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row13_col0" class="data row13 col0" >Charter</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row13_col1" class="data row13 col1" >2283</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row13_col2" class="data row13 col2" >$1,319,574.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row13_col3" class="data row13 col3" >$578.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row13_col4" class="data row13 col4" >83.2742</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row13_col5" class="data row13 col5" >83.9895</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row13_col6" class="data row13 col6" >93.8677</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row13_col7" class="data row13 col7" >96.5396</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row13_col8" class="data row13 col8" >95.2037</td> 
    </tr>    <tr> 
        <th id="T_27024d2e_8b70_11e7_86ae_c821588b3f07" class="row_heading level0 row14" >Wright High School</th> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row14_col0" class="data row14 col0" >Charter</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row14_col1" class="data row14 col1" >1800</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row14_col2" class="data row14 col2" >$1,049,400.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row14_col3" class="data row14 col3" >$583.00</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row14_col4" class="data row14 col4" >83.6822</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row14_col5" class="data row14 col5" >83.955</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row14_col6" class="data row14 col6" >93.3333</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row14_col7" class="data row14 col7" >96.6111</td> 
        <td id="T_27024d2e_8b70_11e7_86ae_c821588b3f07row14_col8" class="data row14 col8" >94.9722</td> 
    </tr></tbody> 
</table> 



# Top Performing School ( By Passing Rate)


```python
# Top 5 performing schools
df_sorted_top_final = df_final.sort_values('% Overall Passing Rate', ascending=False).head()
df_sorted_top_final
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>95.586652</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>93.272171</td>
      <td>97.308869</td>
      <td>95.290520</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>94.594595</td>
      <td>95.945946</td>
      <td>95.270270</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>95.265668</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>93.867718</td>
      <td>96.539641</td>
      <td>95.203679</td>
    </tr>
  </tbody>
</table>
</div>



## Bottom Performing Schools (By Passing Rate)


```python
# Bottom 5 performing schools
df_sorted_bottom_final = df_final.sort_values('% Overall Passing Rate', ascending=True).head()
df_sorted_bottom_final
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>66.366592</td>
      <td>80.220055</td>
      <td>73.293323</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>73.363852</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>65.683922</td>
      <td>81.316421</td>
      <td>73.500171</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>66.057551</td>
      <td>81.222432</td>
      <td>73.639992</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>73.804308</td>
    </tr>
  </tbody>
</table>
</div>



## Math Scores By Grade


```python
student_pd.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
student_sorted_pd = pd.DataFrame(student_pd)
level = pd.to_numeric(student_sorted_pd["grade"].str.split("th").str[0])
student_sorted_pd["level"] = level
student_sorted_pd.sort_values(["school","level","grade"], ascending=True, inplace=True)
student_sorted_pd.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>level</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>17871</th>
      <td>17871</td>
      <td>Blake Martin</td>
      <td>M</td>
      <td>9th</td>
      <td>Bailey High School</td>
      <td>75</td>
      <td>59</td>
      <td>9</td>
    </tr>
    <tr>
      <th>17874</th>
      <td>17874</td>
      <td>Frank Marsh</td>
      <td>M</td>
      <td>9th</td>
      <td>Bailey High School</td>
      <td>71</td>
      <td>89</td>
      <td>9</td>
    </tr>
    <tr>
      <th>17875</th>
      <td>17875</td>
      <td>Charles Goodman Jr.</td>
      <td>M</td>
      <td>9th</td>
      <td>Bailey High School</td>
      <td>90</td>
      <td>61</td>
      <td>9</td>
    </tr>
    <tr>
      <th>17880</th>
      <td>17880</td>
      <td>Aaron Moyer</td>
      <td>M</td>
      <td>9th</td>
      <td>Bailey High School</td>
      <td>81</td>
      <td>62</td>
      <td>9</td>
    </tr>
    <tr>
      <th>17882</th>
      <td>17882</td>
      <td>Michael Dean</td>
      <td>M</td>
      <td>9th</td>
      <td>Bailey High School</td>
      <td>99</td>
      <td>79</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
student_math_df = student_sorted_pd.groupby(['school','level']).aggregate({'math_score': 'mean'}).unstack(level=1)
# student_math_unstacked = student_math_df.unstack(level=1)
student_math_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="4" halign="left">math_score</th>
    </tr>
    <tr>
      <th>level</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>12</th>
    </tr>
    <tr>
      <th>school</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>77.083676</td>
      <td>76.996772</td>
      <td>77.515588</td>
      <td>76.492218</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.094697</td>
      <td>83.154506</td>
      <td>82.765560</td>
      <td>83.277487</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.403037</td>
      <td>76.539974</td>
      <td>76.884344</td>
      <td>77.151369</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.361345</td>
      <td>77.672316</td>
      <td>76.918058</td>
      <td>76.179963</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>82.044010</td>
      <td>84.229064</td>
      <td>83.842105</td>
      <td>83.356164</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>77.438495</td>
      <td>77.337408</td>
      <td>77.136029</td>
      <td>77.186567</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.787402</td>
      <td>83.429825</td>
      <td>85.000000</td>
      <td>82.855422</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>77.027251</td>
      <td>75.908735</td>
      <td>76.446602</td>
      <td>77.225641</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>77.187857</td>
      <td>76.691117</td>
      <td>77.491653</td>
      <td>76.863248</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.625455</td>
      <td>83.372000</td>
      <td>84.328125</td>
      <td>84.121547</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>76.859966</td>
      <td>76.612500</td>
      <td>76.395626</td>
      <td>77.690748</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>83.420755</td>
      <td>82.917411</td>
      <td>83.383495</td>
      <td>83.778976</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.590022</td>
      <td>83.087886</td>
      <td>83.498795</td>
      <td>83.497041</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.085578</td>
      <td>83.724422</td>
      <td>83.195326</td>
      <td>83.035794</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.264706</td>
      <td>84.010288</td>
      <td>83.836782</td>
      <td>83.644986</td>
    </tr>
  </tbody>
</table>
</div>




```python
student_math_df.columns.levels[1]
```




    Int64Index([9, 10, 11, 12], dtype='int64', name='level')




```python
# rename multi level column names Level 0 (math_score)
student_math_df.columns.set_levels(['Average Math Score'], level=0, inplace=True)
# rename multi level column names Level 1 (level) to an alphanumeric column name
student_math_df.columns.set_levels(['9th','10th','11th','12th'], level=1, inplace=True)

# rename rows index name
student_math_df.index.names = ['School Name']
# rename columns index name
student_math_df.columns.names = ['','']
student_math_df
# student_math_df.to_excel("output/AverageMathScore.xlsx", header=True)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="4" halign="left">Average Math Score</th>
    </tr>
    <tr>
      <th></th>
      <th>9th</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>77.083676</td>
      <td>76.996772</td>
      <td>77.515588</td>
      <td>76.492218</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.094697</td>
      <td>83.154506</td>
      <td>82.765560</td>
      <td>83.277487</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.403037</td>
      <td>76.539974</td>
      <td>76.884344</td>
      <td>77.151369</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.361345</td>
      <td>77.672316</td>
      <td>76.918058</td>
      <td>76.179963</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>82.044010</td>
      <td>84.229064</td>
      <td>83.842105</td>
      <td>83.356164</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>77.438495</td>
      <td>77.337408</td>
      <td>77.136029</td>
      <td>77.186567</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.787402</td>
      <td>83.429825</td>
      <td>85.000000</td>
      <td>82.855422</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>77.027251</td>
      <td>75.908735</td>
      <td>76.446602</td>
      <td>77.225641</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>77.187857</td>
      <td>76.691117</td>
      <td>77.491653</td>
      <td>76.863248</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.625455</td>
      <td>83.372000</td>
      <td>84.328125</td>
      <td>84.121547</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>76.859966</td>
      <td>76.612500</td>
      <td>76.395626</td>
      <td>77.690748</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>83.420755</td>
      <td>82.917411</td>
      <td>83.383495</td>
      <td>83.778976</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.590022</td>
      <td>83.087886</td>
      <td>83.498795</td>
      <td>83.497041</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.085578</td>
      <td>83.724422</td>
      <td>83.195326</td>
      <td>83.035794</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.264706</td>
      <td>84.010288</td>
      <td>83.836782</td>
      <td>83.644986</td>
    </tr>
  </tbody>
</table>
</div>



## Reading Scores by Grade


```python
student_reading_df = student_sorted_pd.groupby(['school','level']).aggregate({'reading_score': 'mean'}).unstack(level=1)
student_reading_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="4" halign="left">reading_score</th>
    </tr>
    <tr>
      <th>level</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>12</th>
    </tr>
    <tr>
      <th>school</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>81.303155</td>
      <td>80.907183</td>
      <td>80.945643</td>
      <td>80.912451</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.676136</td>
      <td>84.253219</td>
      <td>83.788382</td>
      <td>84.287958</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>81.198598</td>
      <td>81.408912</td>
      <td>80.640339</td>
      <td>81.384863</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>80.632653</td>
      <td>81.262712</td>
      <td>80.403642</td>
      <td>80.662338</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>83.369193</td>
      <td>83.706897</td>
      <td>84.288089</td>
      <td>84.013699</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>80.866860</td>
      <td>80.660147</td>
      <td>81.396140</td>
      <td>80.857143</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.677165</td>
      <td>83.324561</td>
      <td>83.815534</td>
      <td>84.698795</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>81.290284</td>
      <td>81.512386</td>
      <td>81.417476</td>
      <td>80.305983</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>81.260714</td>
      <td>80.773431</td>
      <td>80.616027</td>
      <td>81.227564</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.807273</td>
      <td>83.612000</td>
      <td>84.335938</td>
      <td>84.591160</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>80.993127</td>
      <td>80.629808</td>
      <td>80.864811</td>
      <td>80.376426</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>84.122642</td>
      <td>83.441964</td>
      <td>84.373786</td>
      <td>82.781671</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.728850</td>
      <td>84.254157</td>
      <td>83.585542</td>
      <td>83.831361</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.939778</td>
      <td>84.021452</td>
      <td>83.764608</td>
      <td>84.317673</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.833333</td>
      <td>83.812757</td>
      <td>84.156322</td>
      <td>84.073171</td>
    </tr>
  </tbody>
</table>
</div>




```python
# rename multi level column names Level 0 (math_score)
student_reading_df.columns.set_levels(['Average Reading Score'], level=0, inplace=True)
# rename multi level column names Level 1 (level) to an alphanumeric column name
student_reading_df.columns.set_levels(['9th','10th','11th','12th'], level=1, inplace=True)

# rename rows index name
student_reading_df.index.names = ['School Name']
# rename columns index name
student_reading_df.columns.names = ['','']
student_reading_df
# student_math_df.to_excel("output/AverageMathScore.xlsx", header=True)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="4" halign="left">Average Reading Score</th>
    </tr>
    <tr>
      <th></th>
      <th>9th</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>81.303155</td>
      <td>80.907183</td>
      <td>80.945643</td>
      <td>80.912451</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.676136</td>
      <td>84.253219</td>
      <td>83.788382</td>
      <td>84.287958</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>81.198598</td>
      <td>81.408912</td>
      <td>80.640339</td>
      <td>81.384863</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>80.632653</td>
      <td>81.262712</td>
      <td>80.403642</td>
      <td>80.662338</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>83.369193</td>
      <td>83.706897</td>
      <td>84.288089</td>
      <td>84.013699</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>80.866860</td>
      <td>80.660147</td>
      <td>81.396140</td>
      <td>80.857143</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.677165</td>
      <td>83.324561</td>
      <td>83.815534</td>
      <td>84.698795</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>81.290284</td>
      <td>81.512386</td>
      <td>81.417476</td>
      <td>80.305983</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>81.260714</td>
      <td>80.773431</td>
      <td>80.616027</td>
      <td>81.227564</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.807273</td>
      <td>83.612000</td>
      <td>84.335938</td>
      <td>84.591160</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>80.993127</td>
      <td>80.629808</td>
      <td>80.864811</td>
      <td>80.376426</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>84.122642</td>
      <td>83.441964</td>
      <td>84.373786</td>
      <td>82.781671</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.728850</td>
      <td>84.254157</td>
      <td>83.585542</td>
      <td>83.831361</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.939778</td>
      <td>84.021452</td>
      <td>83.764608</td>
      <td>84.317673</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.833333</td>
      <td>83.812757</td>
      <td>84.156322</td>
      <td>84.073171</td>
    </tr>
  </tbody>
</table>
</div>



## Scores by School Spending


```python
df_final
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>66.680064</td>
      <td>81.933280</td>
      <td>74.306672</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>95.586652</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>73.363852</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>73.804308</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>95.265668</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>66.752967</td>
      <td>80.862999</td>
      <td>73.807983</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>92.505855</td>
      <td>96.252927</td>
      <td>94.379391</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>65.683922</td>
      <td>81.316421</td>
      <td>73.500171</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>66.057551</td>
      <td>81.222432</td>
      <td>73.639992</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>94.594595</td>
      <td>95.945946</td>
      <td>95.270270</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>66.366592</td>
      <td>80.220055</td>
      <td>73.293323</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>93.867121</td>
      <td>95.854628</td>
      <td>94.860875</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>93.272171</td>
      <td>97.308869</td>
      <td>95.290520</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>93.867718</td>
      <td>96.539641</td>
      <td>95.203679</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>93.333333</td>
      <td>96.611111</td>
      <td>94.972222</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_final.index.get_level_values(0)
```




    Index(['Bailey High School', 'Cabrera High School', 'Figueroa High School',
           'Ford High School', 'Griffin High School', 'Hernandez High School',
           'Holden High School', 'Huang High School', 'Johnson High School',
           'Pena High School', 'Rodriguez High School', 'Shelton High School',
           'Thomas High School', 'Wilson High School', 'Wright High School'],
          dtype='object', name='School Name')




```python
df_final['Per Student Budget']
```




    School Name
    Bailey High School       628.0
    Cabrera High School      582.0
    Figueroa High School     639.0
    Ford High School         644.0
    Griffin High School      625.0
    Hernandez High School    652.0
    Holden High School       581.0
    Huang High School        655.0
    Johnson High School      650.0
    Pena High School         609.0
    Rodriguez High School    637.0
    Shelton High School      600.0
    Thomas High School       638.0
    Wilson High School       578.0
    Wright High School       583.0
    Name: Per Student Budget, dtype: float64




```python
df_final['Per Student Budget'].describe()
```




    count     15.000000
    mean     620.066667
    std       28.544368
    min      578.000000
    25%      591.500000
    50%      628.000000
    75%      641.500000
    max      655.000000
    Name: Per Student Budget, dtype: float64




```python
# use describe to find out 25%, 50%, 75%, max bins
firstvalue = df_final['Per Student Budget'].describe().loc["25%"]
secondvalue = df_final['Per Student Budget'].describe().loc["50%"]
thirdvalue = df_final['Per Student Budget'].describe().loc["75%"]
fourthvalue = df_final['Per Student Budget'].describe().loc["max"]

# create row names
firstbucket = " < " + locale.format("%d", (firstvalue), grouping=False)
secondbucket = locale.format("%d", (firstvalue), grouping=False) + " - " + locale.format("%d", (secondvalue), grouping=False)                             
thirdbucket = locale.format("%d", (secondvalue+1), grouping=False) + " - " + locale.format("%d", (thirdvalue), grouping=False)
fourthbucket = locale.format("%d", (thirdvalue+1), grouping=False) + " - " + locale.format("%d", (fourthvalue), grouping=False)

buckets = {firstbucket, secondbucket, thirdbucket,fourthbucket}
buckets

```




    {' < 591', '591 - 628', '629 - 641', '642 - 655'}




```python
# copy data frame
scoresBySpending_df = df_final.copy()
```


```python
# assign a bucket number to each of the school
scoresBySpending_df.loc[(scoresBySpending_df['Per Student Budget'] < firstvalue), 'Spending Ranges (per Student)'] = firstbucket
scoresBySpending_df.loc[(scoresBySpending_df['Per Student Budget'] >= firstvalue) & (scoresBySpending_df['Per Student Budget'] <= secondvalue), 'Spending Ranges (per Student)'] = secondbucket
scoresBySpending_df.loc[(scoresBySpending_df['Per Student Budget'] >= secondvalue+1) & (scoresBySpending_df['Per Student Budget'] <= thirdvalue), 'Spending Ranges (per Student)'] = thirdbucket
scoresBySpending_df.loc[(scoresBySpending_df['Per Student Budget'] > thirdvalue), 'Spending Ranges (per Student)'] = fourthbucket
```


```python
scoresBySpending_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
      <th>Spending Ranges (per Student)</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>66.680064</td>
      <td>81.933280</td>
      <td>74.306672</td>
      <td>591 - 628</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>95.586652</td>
      <td>&lt; 591</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>73.363852</td>
      <td>629 - 641</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>73.804308</td>
      <td>642 - 655</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>95.265668</td>
      <td>591 - 628</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Group schools by budget per student 
scoresBySpending_df.groupby('Spending Ranges (per Student)').aggregate({"Average Math Score":"median", "Average Reading Score":"median", "% Passing Math":"median","% Passing Reading":"median","% Overall Passing Rate":"median"})

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>Spending Ranges (per Student)</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt; 591</th>
      <td>83.478211</td>
      <td>83.965390</td>
      <td>93.600526</td>
      <td>96.575376</td>
      <td>95.087951</td>
    </tr>
    <tr>
      <th>591 - 628</th>
      <td>83.355477</td>
      <td>83.771241</td>
      <td>93.629746</td>
      <td>95.900287</td>
      <td>95.063271</td>
    </tr>
    <tr>
      <th>629 - 641</th>
      <td>76.842711</td>
      <td>81.158020</td>
      <td>66.366592</td>
      <td>80.739234</td>
      <td>73.363852</td>
    </tr>
    <tr>
      <th>642 - 655</th>
      <td>77.087528</td>
      <td>80.950403</td>
      <td>66.405259</td>
      <td>81.042716</td>
      <td>73.722150</td>
    </tr>
  </tbody>
</table>
</div>



## Scores by School Size


```python
# use describe to find out 25%, 50%, 75%, max bins
firstvalue = df_final['Total Students'].describe().loc["25%"]
secondvalue = df_final['Total Students'].describe().loc["50%"]
thirdvalue = df_final['Total Students'].describe().loc["75%"]
fourthvalue = df_final['Total Students'].describe().loc["max"]

# create row names
firstbucket = " < " + locale.format("%d", (firstvalue), grouping=False)
secondbucket = locale.format("%d", (firstvalue), grouping=False) + " - " + locale.format("%d", (secondvalue), grouping=False)                             
thirdbucket = locale.format("%d", (secondvalue+1), grouping=False) + " - " + locale.format("%d", (thirdvalue), grouping=False)
fourthbucket = locale.format("%d", (thirdvalue+1), grouping=False) + " - " + locale.format("%d", (fourthvalue), grouping=False)

buckets = {firstbucket, secondbucket, thirdbucket,fourthbucket}
buckets
```




    {' < 1698', '1698 - 2283', '2284 - 3474', '3475 - 4976'}




```python
# copy data frame
scoresBySize_df = df_final.copy()
```


```python
# assign a bucket number to each of the school
scoresBySize_df.loc[(scoresBySize_df['Total Students'] < firstvalue), 'School Size'] = firstbucket
scoresBySize_df.loc[(scoresBySize_df['Total Students'] >= firstvalue) & (scoresBySpending_df['Total Students'] <= secondvalue), 'School Size'] = secondbucket
scoresBySize_df.loc[(scoresBySize_df['Total Students'] >= secondvalue+1) & (scoresBySpending_df['Total Students'] <= thirdvalue), 'School Size'] = thirdbucket
scoresBySize_df.loc[(scoresBySize_df['Total Students'] > thirdvalue), 'School Size'] = fourthbucket
```


```python
scoresBySize_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
      <th>School Size</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>66.680064</td>
      <td>81.933280</td>
      <td>74.306672</td>
      <td>3475 - 4976</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>95.586652</td>
      <td>1698 - 2283</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>73.363852</td>
      <td>2284 - 3474</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>73.804308</td>
      <td>2284 - 3474</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>95.265668</td>
      <td>&lt; 1698</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Group schools by student population
scoresBySize_df.groupby('School Size').aggregate({"Average Math Score":"median", "Average Reading Score":"median", "% Passing Math":"median","% Passing Reading":"median","% Overall Passing Rate":"median"})

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Size</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt; 1698</th>
      <td>83.610814</td>
      <td>83.832844</td>
      <td>93.332271</td>
      <td>96.695946</td>
      <td>95.267969</td>
    </tr>
    <tr>
      <th>1698 - 2283</th>
      <td>83.316828</td>
      <td>83.965390</td>
      <td>93.867419</td>
      <td>96.575376</td>
      <td>95.087951</td>
    </tr>
    <tr>
      <th>2284 - 3474</th>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>73.500171</td>
    </tr>
    <tr>
      <th>3475 - 4976</th>
      <td>77.060448</td>
      <td>80.950403</td>
      <td>66.523328</td>
      <td>81.042716</td>
      <td>73.723987</td>
    </tr>
  </tbody>
</table>
</div>



## Scores by School Type


```python
# copy data frame
scoresByType_df = df_final.copy()
```


```python
# Group schools by student population
scoresByType_df.groupby('School Type').aggregate({"Average Math Score":"median", "Average Reading Score":"median", "% Passing Math":"median","% Passing Reading":"median","% Overall Passing Rate":"median"})

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Type</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Charter</th>
      <td>83.388902</td>
      <td>83.901965</td>
      <td>93.629746</td>
      <td>96.575376</td>
      <td>95.234673</td>
    </tr>
    <tr>
      <th>District</th>
      <td>77.048432</td>
      <td>80.966394</td>
      <td>66.366592</td>
      <td>80.862999</td>
      <td>73.639992</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
