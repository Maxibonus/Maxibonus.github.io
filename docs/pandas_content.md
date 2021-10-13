##Misc content

#Python Pandas Tutorial (Part 4): Filtering - Using Conditionals to Filter Rows and Columns
# filtering dataframes and series objects

#filter a series object (filter mask)
df['last'] == 'Doe'

#filter is python keyword
filt = (df['last'] == 'Doe')
df[filt]
df.loc[filt, 'email'] #get filter and columns


filt = (df['last'] =='John') & (df['first'] =='Doe') # and
filt = (df['last'] =='John') | (df['first'] =='Doe') # or

df.loc[filt, 'email'] #get filter and columns
df.loc[~filt, ['email', 'name'] #get opposite of filter (tilda) 

high_salary = (df['salary'] > 70000)
df.loc[high_salary, ['country', 'salary', 'language']]


#filter by in list
countries = ['Autralia', 'New Zealand', 'India', 'Taiwan']
filt = df['country'].isin(countries)
df.loc[filt, ['email', 'name', 'age']]

#string methods for conditional
filt = df['language'].str.contains('python', na=False) #for languages, if it contains python.
#note, can also use string methods to replace text, split values and all kinds of other useful things.
df.loc[filt, 'language'] # returns everything that only has python

#Another example
filt2 = df['ACCOUNT NAME'].str.contains('Smith', na=False) # note, is case sensitive
df.loc[filt2, ['ACCOUNT NAME', 'AMOUNT']]
