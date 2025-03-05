# GDP-Inflatation-rate-relationship
import csv

# Question 1
def getLargestGDPIncrease(filename):
    with open(filename, newline = '') as csvfile:
        reader = csv.DictReader(csvfile)
        dict = {}
        for row in reader:
            for k in list(row.keys()):
                new_key = k.lstrip()
                row[new_key] = row.pop(k) 
            dict = calculateGDPDifference(row, dict)

    return max(dict, key=dict.get)

def calculateGDPDifference(row, dict):
    country = row['Country']
    year = row['Year']
    if (country not in dict):
        dict[country] = 0
    if (year == "2019"):
        dict[country] -= float(row['GDP (in billion USD)'])
    elif (year == "2025"):
        dict[country] += float(row['GDP (in billion USD)'])
    return dict

answer = getLargestGDPIncrease('/Users/moonjiung/Desktop/cse 8a code/Economic Indicators And Inflation.csv')
print(answer)

# Question 2

def getInflationUnemploymentCorrelation(filename):
    with open(filename, newline = '') as csvfile:
        reader = csv.DictReader(csvfile)
        prev_country = None
        prev_inflation = 0
        prev_unemployment = 0
        hasCorrelation = True
        for row in reader:
            for k in list(row.keys()):
                new_key = k.lstrip()
                row[new_key] = row.pop(k) 
            country = row['Country']
            inflation = float(row['Inflation Rate (%)'])
            unemployment = float(row['Unemployment Rate (%)'])
            if (prev_country == country) and not (inflation > prev_inflation and unemployment > prev_unemployment):
                hasCorrelation = False
                break
        
            prev_country = country
            prev_inflation = inflation
            prev_unemployment = unemployment
    return hasCorrelation

answer2 = getInflationUnemploymentCorrelation('/Users/moonjiung/Desktop/cse 8a code/Economic Indicators And Inflation.csv')
print(answer2)

# Question 3
def getCountryWithTheMostInflation(filename):
    with open(filename, newline = '') as csvfile:
        reader = csv.DictReader(csvfile)
        dict = {}
        for row in reader:
            for k in list(row.keys()):
                new_key = k.lstrip()
                row[new_key] = row.pop(k)
            country = row['Country']
            inflationRate = float(row['Inflation Rate (%)'])
            if (country not in dict):
                dict[country] = 0
            #Inflation is considered as high inflation if it is over than 5.0
            if (inflationRate) > 5.0:
                dict[country] += 1

    return max(dict, key=dict.get)

answer3 = getCountryWithTheMostInflation('/Users/moonjiung/Desktop/cse 8a code/Economic Indicators And Inflation.csv')
print(answer3)
