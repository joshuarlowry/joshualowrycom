---
title: CodeCademy Data Science Analysis U.S. Medical Insurance Costs
description: A small data science project on U.S. Medical Insurance Costs I completed for my Data Science coursework.
heroimage: hero.jpg
type: portfolio
---
In this Codecademy exercise I was asked to explore U.S. Medical Insurance Cost data using Python. The document below was generated from Google Colaboratory, based on Jupyter Notebook, and shows the process I followed to examine my hypothesis that smoking plays the biggest role in increasing insurance costs on average. 

Please note that I am unsure of the data provenance since this was an educational exercise using realistic data. 

<div class="cell markdown" id="gAb1_T3Dxg5O">

# U.S. Medical Insurance Costs

Given the available variables, my hypothesis is that smoking plays the
biggest role in increasing insurance costs on average.

</div>

<div class="cell markdown" id="fLJq-jvAxibA">

# Get the data

Use the csv reader to get the data, split it up by row into an array of
values per line. Also, store each column in its own variable.

</div>

<div class="cell code" id="qRDcj3gQx8wt">

``` python
import csv
insuranceData = []
age = []
sex = []
bmi = []
children = []
smoker = []
region = []
charges = []
with open('/content/drive/MyDrive/Codecademy/US Medical Insurance Costs/insurance.csv', newline='') as csvfile:
  reader = csv.DictReader(csvfile)
  for row in reader:
      insuranceData.append(row)
      #print(row)
      age.append(row['age'])
      sex.append(row['sex'])
      bmi.append(row['bmi'])
      children.append(row['children'])
      smoker.append(row['smoker'])
      region.append(row['region'])
      charges.append(float(row['charges']))
```

</div>

<div class="cell markdown" id="CzFKwxtnzqq0">

# Define analysis functions.

Averaging is a function I plan to use a lot. I know there are
optimizations that can be done on lists so I decided to keep it separate
even though it looks simple.

</div>

<div class="cell code" id="rlWgOqgrzfLB">

``` python
def averageOfList(lst):
  return sum(lst) / len(lst)
```

</div>

<div class="cell markdown" id="Sug2jss0zuzM">

# Perform Analysis

What is the average charge for smokers versus non-smokers?

</div>

<div class="cell code" id="pykAQV31z_Xu">

``` python
chargeVSmoke = list(zip(smoker,charges))
smokerChargeAverage = averageOfList([charge for smoke, charge in chargeVSmoke if smoke == 'yes'])
nonSmokerChargeAverage = averageOfList([charge for smoke, charge in chargeVSmoke if smoke == 'no'])

print('Smokers average charges: ${0:.2f}\nNon Smokers Average Charges ${1:.2f}'.format(smokerChargeAverage, nonSmokerChargeAverage))
```

</div>

<div class="cell markdown" id="W4Ku2l8l8qqd">

    Smokers average charges: $32050.23
    Non Smokers Average Charges $8434.27

Smokers pay a lot more for thier coverage. For smokers and non-smokers,
what is the gender makeup?

</div>

<div class="cell code" id="kNFpTrWU8rLC">

``` python
sexVSmoke = list(zip(sex,smoker))
smokerSex = [sex for sex, smoke in sexVSmoke if smoke == 'yes']
nonSmokerSex = [sex for sex, smoke in sexVSmoke if smoke == 'no']

smokerSexMalePercent = sum(1 for sex in smokerSex if sex == 'male') / len(smokerSex) * 100
smokerSexFemalePercent = sum(1 for sex in smokerSex if sex == 'female') / len(smokerSex) * 100

print('There are {:.2f}% Males and {:.2f}% Females who smoke in our dataset.'.format(smokerSexMalePercent, smokerSexFemalePercent))

nonSmokerSexMalePercent = sum(1 for sex in nonSmokerSex if sex == 'male') / len(nonSmokerSex) * 100
nonSmokerSexFemalePercent = sum(1 for sex in nonSmokerSex if sex == 'female') / len(nonSmokerSex) * 100

print('There are {:.2f}% Males and {:.2f}% Females who don\'t smoke in our dataset.'.format(nonSmokerSexMalePercent, nonSmokerSexFemalePercent))

```

</div>

<div class="cell markdown" id="wtD7yUHh_KkQ">

    There are 58.03% Males and 41.97% Females who smoke in our dataset.
    There are 48.59% Males and 51.41% Females who don't smoke in our dataset.

It seems like there are more male smokers than females and roughly equal
sexes for non-smokers. Do the Males and Females in the smoker/non-smoker
category pay similar amounts?

</div>

<div class="cell code" id="2eh3L-P-_Uc6">

``` python
sexVSmokeVCharge = list(zip(sex, smoker, charges))

smokerMaleChargeAvg = averageOfList([charge for sex, smoke, charge in sexVSmokeVCharge if smoke == 'yes' and sex == 'male'])
smokerFemaleChargeAvg = averageOfList([charge for sex, smoke, charge in sexVSmokeVCharge if smoke == 'yes' and sex == 'female'])

nonSmokerMaleChargeAvg = averageOfList([charge for sex, smoke, charge in sexVSmokeVCharge if smoke == 'no' and sex == 'male'])
nonSmokerFemaleChargeAvg = averageOfList([charge for sex, smoke, charge in sexVSmokeVCharge if smoke == 'no' and sex == 'female'])

print('Smoker males are charged ${:.2f}\nSmoker females are charged ${:.2f}\nNon-smoker males are charged ${:.2f}\nNon-smoker females are charged ${:.2f}'.format(smokerMaleChargeAvg, smokerFemaleChargeAvg, nonSmokerMaleChargeAvg, nonSmokerFemaleChargeAvg))

```

</div>

<div class="cell markdown" id="p3ClxABEBGC9">

    Smoker males are charged $33042.01
    Smoker females are charged $30679.00
    Non-smoker males are charged $8087.20
    Non-smoker females are charged $8762.30

Interestingly males pay more if they smoke than females, but females who
don't smoke pay more than males who don't smoke. Smokers still pay the
most on average.

-----

During my initial scan of data I did note that there are a few people
who pay significantly more who don't smoke.

A 60 year-old female with a bmi of 25.84, no children, non-smoker in the
northwest pays `$28923.13692`.

A 33 year-old male with a bmi of 22.705, no children, non-smoker, in the
northwest pays `$21984.47061`.

While these seem out of line with the norm they pay significantly less
still than smokers.

</div>
