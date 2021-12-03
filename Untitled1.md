# Information Visualization We Selected  
  By selecting the GDP data of Hubei province from one year before the outbreak of COVID-19, which happened at the end of 2019, until now, our project aims to explore the impact of COVID-19 on the GDP of Hubei province  to search whether the epidemic has any negative effects on its GDP. And if true, how much did it go down, and how long this kind of downturn lasted. In addition, we looked at how long it would take for GDP to recover to the former standard, due to the opposite forces of the pandemic.
## Why we select it  
  Back to the Spring Festival at the beginning of 2020,which is the greatest traditional festival of China, the COVID-19 outbreak broke out suddenly in Wuhan and spread to the whole country and even many countries around the world. Hubei became the worst-hit area of the epidemic. In order to contain the spread of the epidemic and ensure the safety and health of the people, several cities in the province have been "closed down", taking emergency measures such as closing traffic channels, suspending public transport, delaying the resumption of work and production, and restricting the gathering and movement of people in communities. While effectively controlling the spread of the epidemic, these measures inevitably have a great impact on production, investment, export and service consumption, bringing economic losses to enterprises and increasing pressure on the economy of Hubei province.
Thus, in order to explore what happened to the GDP due to the impact, we select the data of Hubei province’s GDP from 2018 to 2021, to see whether the GDP was effected negatively and for what time it lasted.
## Its impact in the society
As we all know, GDP refers to the total value of all final products produced by all resident units in a country or region during a certain period, covering all sectors of the national economy. It is the overall reflection of the macro economy, including various industries of the national economy. Therefore, GDP is the most core and comprehensive statistical indicator to reflect the macro economy. It can reflect the national economic development, national income and consumption power changes in a certain period of time. 
GDP directly reflects the manufacturing level of a country or region, therefore, some people may think that GDP is only a macroeconomic indicator, far from daily life. In fact, GDP is closely related to each and every one of us. GDP reflects the results of economic growth. When GDP grows, it means that the output of production increases and enterprises expand their production scale, which helps to create job opportunities, increase people's income and increase tax revenue, which will be used to develop public services and ultimately benefit people's livelihood. 


# Detailed explanation of the information visualization
## The story behind the visualization
It is exactly two years since December 1, 2019. Two years ago today, Wuhan, the capital of China's Hubei province, reported its first case of pneumonia of unknown cause, followed by a spate of similar cases within a month. In early 2020, COVID-19 broke out in Wuhan, then spread across the country, and finally around the world, just before the Traditional Chinese New Year holiday. 
The Spring Festival was not as lively as usual, as most Chinese were stuck in their regions or cities due to the epidemic, unable to travel. A good friend of mine was exactly in Wuhan and I was told by him that street vendors were unable to come out for business normally, supermarkets were closed, and People's Daily necessities were delivered by the government.
I was pretty shocked and scared at the greatly negative effect of the epidemic. Thus I and my group members chose to search the GDP of that period to see what happened to it after all.
## The first impression of the graph  
![%E5%9B%BE%E7%89%87-4.png](attachment:%E5%9B%BE%E7%89%87-4.png)

![%E5%9B%BE%E7%89%87.png](attachment:%E5%9B%BE%E7%89%87.png)
In the visualization, we can see in a year, GDP is growing quarter by quarter.
Between 2018 to 2019, before COVID-19 happening, the GDP’s quarter-over-quarter value is increasing with a stable rate (approximately 7%),  in 2019 Q4 to Q1 2020, when the COVID-19 happened and struck this province, it’s GDP fell down rapidly. However, when the epidemic got controlled the GDP recovered rapidly.
## How to read it
### The visual patterns are used in the graph
1.	`Time` , using a quarter, usually three months of a year, which is the x axis’s value to be depicted.
2.	`Number of GDP`, using a unit of RMB yuan, in a year’s different season between 2018_1 to 2021_3, which uses bar chart to depict.
3.	`Year-on-year change`: year-on-year GDP growth in different quarters of the same year is depicted using line charts.

### Data types are represented in each visual patterns
Position in X-axis: Quarter of year(Datetime)  
Position in Y-axis in bar chart: The amount of the GDP(Ordinal)  
Position in Y-axis in plot chart: 
  1. increase or decrease of GDP(Categorical) 
  2. The amount of the rate of GDP year-over-year change rate(Ordinal)  

### Visual variables
1.	**`Time`**: 

Position: the closer time point is to the right side, the closer it is to the present.  
2.	**`Number of GDP`** 

Position: it is determined by time and displayed above time.  
Size: the higher the rectangle is, the higher the value is.  
3.	`Year-on-year change`  
Position: it is decided by time, it is on the top of it’s time, and more right side of the data is more close to the present. A higher (lower) position stands for a far more rapid change.  
Ontologies: Stands for change rate of the variable, 0-90°it is a positive change, and more close to 90° stands for a far more rapid change.  

### General relationships between data points (story) one can draw
### Summarize
![%E5%9B%BE%E7%89%87-2.png](attachment:%E5%9B%BE%E7%89%87-2.png)

# Replicate the information visualization
## Process
### Get axis data


```python
#Get axis data
GDP_2018 = [8188,17958,27634,39366]
GDP_2019 = [9110,19895,30509,45828]
GDP_2020 = [6379,17480,29779,43443]
GDP_2021 = [9872,22777,34731]
GPT_Total = np.array(GDP_2018 + GDP_2019 + GDP_2020 + GDP_2021)
Time=['Q1 2018','Q2 2018','Q3 2018','Q4 2018','Q1 2019','Q2 2019','Q3 2019','Q4 2019','Q1 2020','Q2 2020',
     'Q3 2020','Q4 2020','Q1 2021','Q2 2021','Q3 2021']
```

### Calculate the quarter-on-quarter growth rate by Excel


```python
# Calculate the quarter-on-quarter growth rate by Excel
Increase_Values = [11.24957869,11.24957869,10.78940672,10.40397187,11.24957869,10.78940672,10.40397187,16.41434162,-29.9745885,-12.13947702,-2.392703631,-5.203879436,54.75981095,30.30329207,16.6294038]
```

### Use matplotlib to draw the figure


```python
#Use matplotlib to draw the figure
fig, ax1 = plt.subplots(figsize=(13, 5))

plt.xticks(rotation=45)


ax1.bar(Time, GPT_Total, width=0.85,label="GDP",color='#37A2DA')
ax1.set_ylabel("GDP(Unit: 100 million yuan)")
plt.yticks(list(range(0,50001,5000)))


ax2 = ax1.twinx()
ax2.plot(Time, Increase_Values, color="orange", label="Increase")
ax2.set_ylabel("Increase(percent)")
plt.yticks(list(range(-50,51,10)))


plt.title("GDP of Hubei province in each quarter of each year")
fig.legend(loc="upper right", bbox_to_anchor=(1, 1), bbox_transform=ax1.transAxes)
plt.figure(figsize=(720,480))
plt.show()
```

# Propose changes that would improve the graph
## Pitfalls of the graph
### Unwanted biases issues
### Readability issues
## How to address the pitfalls
### Unwanted biases issues
### Readability issues

# Implement the changes
## Process

1. Gain data of different quarter’s in a year.


```python
#Gain data of different quarter’s in a year.
GDP1 = [8188,9110,6379,9872]
GDP2 = [17958,19895,17480,22777]
GDP3 = [27634,30509,29779,34731]
GDP4 = [39366,45828,43443,34731]
```

2. Convert the total GDP as of the quarter into the increment of GDP for the quarter


```python
# Convert the total GDP as of the quarter into the increment of GDP for the quarter
L1 = GDP1
L1
```


```python
L2 = []
for i in range(4):
    L2.append(GDP2[i] - GDP1[i])
L2
```


```python
L3 = []
for i in range(4):
    L3.append(GDP3[i] - GDP2[i])
L3
```


```python
L4 = []
for i in range(4):
    L4.append(GDP4[i] - GDP3[i])
L4
```


```python
L = []
for i in range(4):
    L.append(L1[i])
    L.append(L2[i])
    L.append(L3[i])
    L.append(L4[i])
L
```

3. Compute year to year GDP change ratio for graph 2


```python
# Compute year to year GDP change ratio for graph 2
r = []
for i in range(1,len(L) - 1):
    r.append((L[i]- L[i - 1])/L[i - 1])
r
```

4. Gain data of time data for x-axis


```python
r_lable = []
r_lable.append('2018_2')
y = 2019
for i in range(len(r) - 1):
    if i % 4 == 2:
        r_lable.append(str(y) + '_1')
        y = y + 1
    else:
        r_lable.append(' ')
r_lable
```

5. draw the figure


```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
fig = plt.figure('GDP statistics of Hubei Province for each quater',figsize=(18,18))
fig.tight_layout()
labels = year
x_lables = np.arange(len(year))
width = 0.5
ax1 = fig.add_subplot(311)
ax1.bar(x_lables, L1, width, label='the first quarter')
ax1.bar(x_lables, L2, width, bottom=L1, color = "green", label='the second quarter')
ax1.bar(x_lables, L3, width, bottom=GDP2,label='the third quarter')
ax1.bar(x_lables, L4, width, bottom=GDP3, color = "orange",label='the fourth quarter')
ax1.set_title('GDP statistics of Hubei Province')
ax1.set_ylabel('GDP(100 million yuan)')
ax1.set_xticks(x_lables)
ax1.set_xticklabels(year)
ax1.legend(bbox_to_anchor=(1, 0), loc=3, borderaxespad=0)
for i in range(4):
    ax1.annotate('{}'.format(GDP4[i]),
                    xy=(x_lables[i], GDP4[i]),
                    xytext=(0, 1),  # 3 points vertical offset
                    textcoords="offset points",
                    ha='center', va='bottom')
    ax1.annotate('{}'.format(L4[i]),
                    xy=(x_lables[i], GDP4[i]),
                    xytext=(0, -20),  # 3 points vertical offset
                    textcoords="offset points",
                    ha='center', va='bottom')
    ax1.annotate('{}'.format(L3[i]),
                    xy=(x_lables[i], GDP3[i]),
                    xytext=(0, -20),  # 3 points vertical offset
                    textcoords="offset points",
                    ha='center', va='bottom')
    ax1.annotate('{}'.format(L2[i]),
                    xy=(x_lables[i], GDP2[i]),
                    xytext=(0, -20),  # 3 points vertical offset
                    textcoords="offset points",
                    ha='center', va='bottom')
    ax1.annotate('{}'.format(L1[i]),
                    xy=(x_lables[i], GDP1[i]),
                    xytext=(0, -20),  # 3 points vertical offset
                    textcoords="offset points",
                    ha='center', va='bottom')
ax2 = fig.add_subplot(312)
x_lables = np.arange(len(r))
ax2.plot(x_lables, r, label="rate")
ax2.set_title('rate of improvement of GDP in Hubei Province')
ax2.set_ylabel('rate(<1)')
ax2.set_xticks(x_lables)
ax2.set_xticklabels(r_lable)
ax2.legend(bbox_to_anchor=(1, 0), loc=3, borderaxespad=0)
for i in range(len(r)):
    if r[i] > 0:
        ax2.annotate('{:.2f}'.format(r[i]),
                    xy=(x_lables[i], r[i]),
                    xytext=(0, 3),  # 3 points vertical offset
                    textcoords="offset points",
                    ha='center', va='bottom')
    else:
        ax2.annotate('{:.2f}'.format(r[i]),
                    xy=(x_lables[i], r[i]),
                    xytext=(0, -10),  # 3 points vertical offset
                    textcoords="offset points",
                    ha='center', va='bottom')
ax3 = fig.add_subplot(313)
x_lables = np.arange(len(r1_lable))
ax3.bar(x_lables, r1, width, label='rate of improvement')
ax3.set_title('rate of improvement of GDP in Hubei Province')
ax3.set_ylabel('rate(<1)')
ax3.set_xticks(x_lables)
ax3.set_xticklabels(r1_lable)
ax3.legend(bbox_to_anchor=(1, 0), loc=3, borderaxespad=0)
for i in range(len(r1)):
    if r[i] > 0:
        ax3.annotate('{:.2f}'.format(r1[i]),
                    xy=(x_lables[i], r1[i]),
                    xytext=(0, 3),  # 3 points vertical offset
                    textcoords="offset points",
                    ha='center', va='bottom')
    else:
        ax3.annotate('{:.2f}'.format(r1[i]),
                    xy=(x_lables[i], r1[i]),
                    xytext=(0, -10),  # 3 points vertical offset
                    textcoords="offset points",
                    ha='center', va='bottom')
fig.tight_layout()
plt.show()
```

## Compare the previous visualization project
### Unwanted biases issues
### Readability issues

# 导入进社交网站，分享（未做）
