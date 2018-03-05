

```python
import pandas as pd
import os
```


```python
# load CSV
csvpath = os.path.join('raw_data','schools_complete.csv')
csvpath1 = os.path.join('raw_data','students_complete.csv')
schools_df = pd.read_csv(csvpath)
students_df = pd.read_csv(csvpath1)
```


```python
school_count = len(schools_df)
student_count = len(students_df)
total_budget = schools_df["budget"].sum()
avg_math = students_df["math_score"].mean()
avg_read = students_df["reading_score"].mean()
pass_math = students_df.loc[(students_df["math_score"]>65)]
pass_math_count = len(pass_math)
pass_read = students_df.loc[(students_df["reading_score"]>65)]
pass_read_count = len(pass_read)
math_percentage = (pass_math_count / student_count)*100
read_percentage = (pass_read_count/student_count)*100
overall_percentage = (math_percentage + read_percentage) / 2 
district_summary = pd.DataFrame({"Total Schools":[school_count],
                                "Total Students":[student_count],
                                 "Total Budget": [total_budget],
                                 "Average Math Score":[avg_math],
                                 "Average Reading Score":[avg_read],
                                 "% Passing Math": [math_percentage],
                                 "% Passing Reading": [read_percentage],
                                 "Overall Passing Rate": [overall_percentage]
                                }) 
district_summary
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
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>Overall Passing Rate</th>
      <th>Total Budget</th>
      <th>Total Schools</th>
      <th>Total Students</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>83.112076</td>
      <td>94.263467</td>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>88.687771</td>
      <td>24649428</td>
      <td>15</td>
      <td>39170</td>
    </tr>
  </tbody>
</table>
</div>




```python
schools_df = schools_df.rename(columns={"name":"school"})
merge_df = students_df.merge(schools_df, on = "school")
merge_df.head()
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
      <th>School ID</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
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
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
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
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
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
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
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
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
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
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
  </tbody>
</table>
</div>




```python
school_group = merge_df.set_index("school").groupby(["school"])
school_type = schools_df.set_index("school")["type"]
student_per_school = school_group['name'].count()
school_budget = schools_df.set_index("school")["budget"]
student_budget = school_budget / school_count
avg_math_school = school_group["math_score"].mean()
avg_read_school = school_group["reading_score"].mean()
math_pass = merge_df[merge_df["math_score"] >65].groupby("school")["name"].count() / student_per_school
read_pass = merge_df[merge_df["reading_score"] >65].groupby("school")["name"].count() / student_per_school
overall_pass = merge_df[(merge_df["reading_score"] >65) & (merge_df["math_score"] >65)].groupby("school")["name"].count() / student_per_school 

school_summary = pd.DataFrame({"School Type":school_type,
                               "Total Students":student_per_school,
                               "Total School Budget":school_budget,
                               "Average Math Score":avg_math_school,
                               "Average Reading Score": avg_read_school,
                               "% Passing Math":math_pass,
                               "& Passing Reading":read_pass,
                               "Overall Passing Rate":overall_pass                            
    })
school_summary
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
      <th>% Passing Math</th>
      <th>&amp; Passing Reading</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>Overall Passing Rate</th>
      <th>School Type</th>
      <th>Total School Budget</th>
      <th>Total Students</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>0.756029</td>
      <td>0.919011</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>0.694735</td>
      <td>District</td>
      <td>3124928</td>
      <td>4976</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>1.000000</td>
      <td>Charter</td>
      <td>1081356</td>
      <td>1858</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>0.748728</td>
      <td>0.918956</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>0.687691</td>
      <td>District</td>
      <td>1884411</td>
      <td>2949</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>0.761957</td>
      <td>0.907996</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>0.692954</td>
      <td>District</td>
      <td>1763916</td>
      <td>2739</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>1.000000</td>
      <td>Charter</td>
      <td>917500</td>
      <td>1468</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>0.754693</td>
      <td>0.914563</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>0.690615</td>
      <td>District</td>
      <td>3022020</td>
      <td>4635</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>1.000000</td>
      <td>Charter</td>
      <td>248087</td>
      <td>427</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>0.752828</td>
      <td>0.917724</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>0.691464</td>
      <td>District</td>
      <td>1910635</td>
      <td>2917</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>0.753833</td>
      <td>0.920605</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>0.693552</td>
      <td>District</td>
      <td>3094650</td>
      <td>4761</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>1.000000</td>
      <td>Charter</td>
      <td>585858</td>
      <td>962</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>0.755439</td>
      <td>0.915229</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>0.691173</td>
      <td>District</td>
      <td>2547363</td>
      <td>3999</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>1.000000</td>
      <td>Charter</td>
      <td>1056600</td>
      <td>1761</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>1.000000</td>
      <td>Charter</td>
      <td>1043130</td>
      <td>1635</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>1.000000</td>
      <td>Charter</td>
      <td>1319574</td>
      <td>2283</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>1.000000</td>
      <td>Charter</td>
      <td>1049400</td>
      <td>1800</td>
    </tr>
  </tbody>
</table>
</div>




```python
school_top_5 = school_summary.sort_values(by=["Overall Passing Rate","Average Math Score","Average Reading Score"], ascending = False)
top_5 = school_top_5.head(5)
top_5
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
      <th>% Passing Math</th>
      <th>&amp; Passing Reading</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>Overall Passing Rate</th>
      <th>School Type</th>
      <th>Total School Budget</th>
      <th>Total Students</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Pena High School</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>1.0</td>
      <td>Charter</td>
      <td>585858</td>
      <td>962</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>1.0</td>
      <td>Charter</td>
      <td>248087</td>
      <td>427</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>1.0</td>
      <td>Charter</td>
      <td>1049400</td>
      <td>1800</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>1.0</td>
      <td>Charter</td>
      <td>1043130</td>
      <td>1635</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>1.0</td>
      <td>Charter</td>
      <td>1056600</td>
      <td>1761</td>
    </tr>
  </tbody>
</table>
</div>




```python
school_bottom_5 = school_summary.sort_values(by=["Overall Passing Rate","Average Math Score","Average Reading Score"])
bottom_5 = school_bottom_5.head(5)
bottom_5
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
      <th>% Passing Math</th>
      <th>&amp; Passing Reading</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>Overall Passing Rate</th>
      <th>School Type</th>
      <th>Total School Budget</th>
      <th>Total Students</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Figueroa High School</th>
      <td>0.748728</td>
      <td>0.918956</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>0.687691</td>
      <td>District</td>
      <td>1884411</td>
      <td>2949</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>0.754693</td>
      <td>0.914563</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>0.690615</td>
      <td>District</td>
      <td>3022020</td>
      <td>4635</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>0.755439</td>
      <td>0.915229</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>0.691173</td>
      <td>District</td>
      <td>2547363</td>
      <td>3999</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>0.752828</td>
      <td>0.917724</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>0.691464</td>
      <td>District</td>
      <td>1910635</td>
      <td>2917</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>0.761957</td>
      <td>0.907996</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>0.692954</td>
      <td>District</td>
      <td>1763916</td>
      <td>2739</td>
    </tr>
  </tbody>
</table>
</div>




```python
ninth = students_df.loc[students_df["grade"] =="9th"].groupby("school")["math_score"].mean()
tenth = students_df.loc[students_df["grade"] =="10th"].groupby("school")["math_score"].mean()
eleventh = students_df.loc[students_df["grade"] =="11th"].groupby("school")["math_score"].mean()
twelve = students_df.loc[students_df["grade"] =="12th"].groupby("school")["math_score"].mean()

math_scores = pd.DataFrame({"9th":ninth,
                            "10th":tenth,
                            "11th":eleventh,
                            "12th":twelve
    
})
math_scores
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
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
      <th>9th</th>
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
      <td>76.996772</td>
      <td>77.515588</td>
      <td>76.492218</td>
      <td>77.083676</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.154506</td>
      <td>82.765560</td>
      <td>83.277487</td>
      <td>83.094697</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.539974</td>
      <td>76.884344</td>
      <td>77.151369</td>
      <td>76.403037</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.672316</td>
      <td>76.918058</td>
      <td>76.179963</td>
      <td>77.361345</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>84.229064</td>
      <td>83.842105</td>
      <td>83.356164</td>
      <td>82.044010</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>77.337408</td>
      <td>77.136029</td>
      <td>77.186567</td>
      <td>77.438495</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.429825</td>
      <td>85.000000</td>
      <td>82.855422</td>
      <td>83.787402</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>75.908735</td>
      <td>76.446602</td>
      <td>77.225641</td>
      <td>77.027251</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>76.691117</td>
      <td>77.491653</td>
      <td>76.863248</td>
      <td>77.187857</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.372000</td>
      <td>84.328125</td>
      <td>84.121547</td>
      <td>83.625455</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>76.612500</td>
      <td>76.395626</td>
      <td>77.690748</td>
      <td>76.859966</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>82.917411</td>
      <td>83.383495</td>
      <td>83.778976</td>
      <td>83.420755</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.087886</td>
      <td>83.498795</td>
      <td>83.497041</td>
      <td>83.590022</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.724422</td>
      <td>83.195326</td>
      <td>83.035794</td>
      <td>83.085578</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>84.010288</td>
      <td>83.836782</td>
      <td>83.644986</td>
      <td>83.264706</td>
    </tr>
  </tbody>
</table>
</div>




```python
ninth_read = students_df.loc[students_df["grade"] =="9th"].groupby("school")["reading_score"].mean()
tenth_read = students_df.loc[students_df["grade"] =="10th"].groupby("school")["reading_score"].mean()
eleventh_read = students_df.loc[students_df["grade"] =="11th"].groupby("school")["reading_score"].mean()
twelve_read = students_df.loc[students_df["grade"] =="12th"].groupby("school")["reading_score"].mean()

read_scores = pd.DataFrame({"9th":ninth,
                            "10th":tenth,
                            "11th":eleventh,
                            "12th":twelve
    
})
read_scores
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
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
      <th>9th</th>
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
      <td>76.996772</td>
      <td>77.515588</td>
      <td>76.492218</td>
      <td>77.083676</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.154506</td>
      <td>82.765560</td>
      <td>83.277487</td>
      <td>83.094697</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.539974</td>
      <td>76.884344</td>
      <td>77.151369</td>
      <td>76.403037</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.672316</td>
      <td>76.918058</td>
      <td>76.179963</td>
      <td>77.361345</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>84.229064</td>
      <td>83.842105</td>
      <td>83.356164</td>
      <td>82.044010</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>77.337408</td>
      <td>77.136029</td>
      <td>77.186567</td>
      <td>77.438495</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.429825</td>
      <td>85.000000</td>
      <td>82.855422</td>
      <td>83.787402</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>75.908735</td>
      <td>76.446602</td>
      <td>77.225641</td>
      <td>77.027251</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>76.691117</td>
      <td>77.491653</td>
      <td>76.863248</td>
      <td>77.187857</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.372000</td>
      <td>84.328125</td>
      <td>84.121547</td>
      <td>83.625455</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>76.612500</td>
      <td>76.395626</td>
      <td>77.690748</td>
      <td>76.859966</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>82.917411</td>
      <td>83.383495</td>
      <td>83.778976</td>
      <td>83.420755</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.087886</td>
      <td>83.498795</td>
      <td>83.497041</td>
      <td>83.590022</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.724422</td>
      <td>83.195326</td>
      <td>83.035794</td>
      <td>83.085578</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>84.010288</td>
      <td>83.836782</td>
      <td>83.644986</td>
      <td>83.264706</td>
    </tr>
  </tbody>
</table>
</div>




```python
bins = [0, 600, 625, 650, 999999]
group_name = ['< $600', "$601 - 625", "$625 - 650", "> $651"]
merge_df['spending_bins'] = pd.cut(merge_df['budget']/merge_df['size'], bins, labels = group_name)

by_spending = merge_df.groupby('spending_bins')

avg_math_spend = by_spending['math_score'].mean()
avg_read_spend = by_spending['reading_score'].mean()
pass_math_spend = merge_df[merge_df['math_score'] >= 65].groupby('spending_bins')['Student ID'].count()/by_spending['Student ID'].count()
pass_read_spend = merge_df[merge_df['reading_score'] >= 65].groupby('spending_bins')['Student ID'].count()/by_spending['Student ID'].count()
overall_spend = merge_df[(merge_df['reading_score'] >= 65) & (merge_df['math_score'] >= 65)].groupby('spending_bins')['Student ID'].count()/by_spending['Student ID'].count()
         
scores_by_spend = pd.DataFrame({
   "Average Math Score": avg_math_spend,
   "Average Reading Score": avg_read_spend,
   '% Passing Math': pass_math_spend,
   '% Passing Reading': pass_read_spend,
   "Overall Passing Rate": overall_spend
            
})
    
scores_by_spend
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
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>spending_bins</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt; $600</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>83.362283</td>
      <td>83.912412</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>$601 - 625</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>83.544856</td>
      <td>83.906996</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>$625 - 650</th>
      <td>0.795812</td>
      <td>0.948810</td>
      <td>77.469253</td>
      <td>81.162258</td>
      <td>0.756114</td>
    </tr>
    <tr>
      <th>&gt; $651</th>
      <td>0.777278</td>
      <td>0.945577</td>
      <td>77.034693</td>
      <td>81.030323</td>
      <td>0.734375</td>
    </tr>
  </tbody>
</table>
</div>




```python
merge_df
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
      <th>School ID</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>spending_bins</th>
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
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
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
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
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
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
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
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
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
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Bryan Miranda</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>94</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Sheena Carter</td>
      <td>F</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>82</td>
      <td>80</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>Nicole Baker</td>
      <td>F</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>96</td>
      <td>69</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Michael Roth</td>
      <td>M</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>95</td>
      <td>87</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>Matthew Greene</td>
      <td>M</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>96</td>
      <td>84</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>Andrew Alexander</td>
      <td>M</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>70</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>Daniel Cooper</td>
      <td>M</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>78</td>
      <td>77</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>Brittney Walker</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>64</td>
      <td>79</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>William Long</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>71</td>
      <td>79</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>Tammy Hebert</td>
      <td>F</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>85</td>
      <td>67</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>15</th>
      <td>15</td>
      <td>Dr. Jordan Carson</td>
      <td>M</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>88</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>16</th>
      <td>16</td>
      <td>Donald Zamora</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>88</td>
      <td>55</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>17</th>
      <td>17</td>
      <td>Kimberly Santiago</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>74</td>
      <td>75</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>18</th>
      <td>18</td>
      <td>Kevin Stevens</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>64</td>
      <td>69</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>19</th>
      <td>19</td>
      <td>Brandi Lyons</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>89</td>
      <td>80</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>20</th>
      <td>20</td>
      <td>Lisa Davis</td>
      <td>F</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>91</td>
      <td>89</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>21</th>
      <td>21</td>
      <td>Kristen Lopez</td>
      <td>F</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>77</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>22</th>
      <td>22</td>
      <td>Kimberly Stewart</td>
      <td>F</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>99</td>
      <td>84</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>23</th>
      <td>23</td>
      <td>Christopher Parker</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>81</td>
      <td>68</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>24</th>
      <td>24</td>
      <td>Chelsea Griffith</td>
      <td>F</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>85</td>
      <td>73</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>25</th>
      <td>25</td>
      <td>Cesar Morris</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>92</td>
      <td>70</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>26</th>
      <td>26</td>
      <td>Melanie Decker</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>63</td>
      <td>85</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>27</th>
      <td>27</td>
      <td>Tracey Oconnor</td>
      <td>F</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>80</td>
      <td>58</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>28</th>
      <td>28</td>
      <td>Kelly James</td>
      <td>F</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>73</td>
      <td>55</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>29</th>
      <td>29</td>
      <td>Nicole Brown</td>
      <td>F</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>88</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>&gt; $651</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>39140</th>
      <td>39140</td>
      <td>Cheyenne Hernandez</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>76</td>
      <td>99</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39141</th>
      <td>39141</td>
      <td>Jonathan Sullivan</td>
      <td>M</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>86</td>
      <td>93</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39142</th>
      <td>39142</td>
      <td>Deborah Higgins DDS</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>96</td>
      <td>83</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39143</th>
      <td>39143</td>
      <td>Steven Jackson</td>
      <td>M</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>71</td>
      <td>93</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39144</th>
      <td>39144</td>
      <td>Cristian Webster</td>
      <td>M</td>
      <td>12th</td>
      <td>Thomas High School</td>
      <td>77</td>
      <td>87</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39145</th>
      <td>39145</td>
      <td>Audrey Fry</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>94</td>
      <td>74</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39146</th>
      <td>39146</td>
      <td>Michael Carroll</td>
      <td>M</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>69</td>
      <td>95</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39147</th>
      <td>39147</td>
      <td>Raymond Hawkins</td>
      <td>M</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>88</td>
      <td>81</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39148</th>
      <td>39148</td>
      <td>Christopher Wilson</td>
      <td>M</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>89</td>
      <td>89</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39149</th>
      <td>39149</td>
      <td>Glenda Fletcher</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>82</td>
      <td>93</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39150</th>
      <td>39150</td>
      <td>Jennifer Hamilton</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>80</td>
      <td>75</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39151</th>
      <td>39151</td>
      <td>Shannon Williams</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>84</td>
      <td>73</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39152</th>
      <td>39152</td>
      <td>Lori Moore</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>98</td>
      <td>84</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39153</th>
      <td>39153</td>
      <td>William Hubbard</td>
      <td>M</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>80</td>
      <td>75</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39154</th>
      <td>39154</td>
      <td>Bradley Johnson</td>
      <td>M</td>
      <td>12th</td>
      <td>Thomas High School</td>
      <td>91</td>
      <td>71</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39155</th>
      <td>39155</td>
      <td>John Brooks</td>
      <td>M</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>92</td>
      <td>98</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39156</th>
      <td>39156</td>
      <td>Stephanie Contreras</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>79</td>
      <td>95</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39157</th>
      <td>39157</td>
      <td>Kristen Gonzalez</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>79</td>
      <td>94</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39158</th>
      <td>39158</td>
      <td>Kari Holloway</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>87</td>
      <td>90</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39159</th>
      <td>39159</td>
      <td>Kimberly Cabrera</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>85</td>
      <td>72</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39160</th>
      <td>39160</td>
      <td>Katie Weaver</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>89</td>
      <td>86</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39161</th>
      <td>39161</td>
      <td>April Reyes</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>70</td>
      <td>84</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39162</th>
      <td>39162</td>
      <td>Derek Weeks</td>
      <td>M</td>
      <td>12th</td>
      <td>Thomas High School</td>
      <td>94</td>
      <td>77</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39163</th>
      <td>39163</td>
      <td>John Reese</td>
      <td>M</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>90</td>
      <td>75</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39164</th>
      <td>39164</td>
      <td>Joseph Anthony</td>
      <td>M</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>97</td>
      <td>76</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39165</th>
      <td>39165</td>
      <td>Donna Howard</td>
      <td>F</td>
      <td>12th</td>
      <td>Thomas High School</td>
      <td>99</td>
      <td>90</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39166</th>
      <td>39166</td>
      <td>Dawn Bell</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>95</td>
      <td>70</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39167</th>
      <td>39167</td>
      <td>Rebecca Tanner</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>73</td>
      <td>84</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39168</th>
      <td>39168</td>
      <td>Desiree Kidd</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>99</td>
      <td>90</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
    <tr>
      <th>39169</th>
      <td>39169</td>
      <td>Carolyn Jackson</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>95</td>
      <td>75</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>$625 - 650</td>
    </tr>
  </tbody>
</table>
<p>39170 rows × 12 columns</p>
</div>




```python
bins = [0, 1000, 2000, 100000000]
group_name = ["Small (<1000)", "Medium (1000-2000)" , "Large (>2000)"]
merge_df['size_bins'] = pd.cut(merge_df['size'], bins, labels = group_name)

by_size = merge_df.groupby('size_bins')

avg_math_schoool_size = by_size['math_score'].mean()
avg_read_schoool_size = by_size['math_score'].mean()
pass_math_schoool_size = merge_df[merge_df['math_score'] >= 65].groupby('size_bins')['Student ID'].count()/by_size['Student ID'].count()
pass_read_schoool_size = merge_df[merge_df['reading_score'] >= 65].groupby('size_bins')['Student ID'].count()/by_size['Student ID'].count()
overall_schoool_size = merge_df[(merge_df['reading_score'] >= 65) & (merge_df['math_score'] >= 65)].groupby('size_bins')['Student ID'].count()/by_size['Student ID'].count()
        
scores_by_size = pd.DataFrame({
    "Average Math Score": avg_math_schoool_size,
    "Average Reading Score": avg_read_schoool_size,
    '% Passing Math': pass_math_schoool_size,
    '% Passing Reading': pass_read_schoool_size,
    "Overall Passing Rate": overall_schoool_size
})
scores_by_size
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
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>size_bins</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Small (&lt;1000)</th>
      <td>1.00000</td>
      <td>1.00000</td>
      <td>83.828654</td>
      <td>83.828654</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>Medium (1000-2000)</th>
      <td>1.00000</td>
      <td>1.00000</td>
      <td>83.372682</td>
      <td>83.372682</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>Large (&gt;2000)</th>
      <td>0.79555</td>
      <td>0.94911</td>
      <td>77.477597</td>
      <td>77.477597</td>
      <td>0.755904</td>
    </tr>
  </tbody>
</table>
</div>




```python
by_type = merge_df.groupby("type")

avg_math_type = by_type['math_score'].mean()
avg_read_type = by_type['math_score'].mean()
pass_math_type = merge_df[merge_df['math_score'] >= 65].groupby('type')['Student ID'].count()/by_type['Student ID'].count()
pass_read_type = merge_df[merge_df['reading_score'] >= 65].groupby('type')['Student ID'].count()/by_type['Student ID'].count()
overall_type = merge_df[(merge_df['reading_score'] >= 65) & (merge_df['math_score'] >= 65)].groupby('type')['Student ID'].count()/by_type['Student ID'].count()
        
scores_by_type = pd.DataFrame({
    "Average Math Score": avg_math_type,
    "Average Reading Score": avg_read_type,
    '% Passing Math': pass_math_type,
    '% Passing Reading': pass_read_type,
    "Overall Passing Rate": overall})
scores_by_type

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
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>$585 - 614</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>$615 - 644</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.745807</td>
    </tr>
    <tr>
      <th>&lt; $585</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>&gt; $644</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.691952</td>
    </tr>
    <tr>
      <th>Charter</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>83.406183</td>
      <td>83.406183</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>District</th>
      <td>0.778247</td>
      <td>0.944803</td>
      <td>76.987026</td>
      <td>76.987026</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>


