##Misc content

```
#Python Pandas Tutorial (Part 4): Filtering - Using Conditionals to Filter Rows and Columns
# filtering dataframes and series objects

#filter a series object (filter mask)
```
df['last'] == 'Doe'
```
#filter is python keyword
```
filt = (df['last'] == 'Doe')
df[filt]
df.loc[filt, 'email'] #get filter and columns
```

```
filt = (df['last'] =='John') & (df['first'] =='Doe') # and
filt = (df['last'] =='John') | (df['first'] =='Doe') # or
```

```
df.loc[filt, 'email'] #get filter and columns
df.loc[~filt, ['email', 'name'] #get opposite of filter (tilda) 
```

```
high_salary = (df['salary'] > 70000)
df.loc[high_salary, ['country', 'salary', 'language']]
```

#filter by in list
```
countries = ['Autralia', 'New Zealand', 'India', 'Taiwan']
filt = df['country'].isin(countries)
df.loc[filt, ['email', 'name', 'age']]
```

#string methods for conditional
```
filt = df['language'].str.contains('python', na=False) #for languages, if it contains python.
```
#note, can also use string methods to replace text, split values and all kinds of other useful things.
```
df.loc[filt, 'language'] # returns everything that only has python
```
#Another example
```filt2 = df['ACCOUNT NAME'].str.contains('Smith', na=False) # note, is case sensitive
df.loc[filt2, ['ACCOUNT NAME', 'AMOUNT']]
```


## L5
## V5 - updating rows Alter existing rows and columns
change columns - use list comprension.

eg upper:
```
df.columns = [x.upper() for x in df.columns]
```

remove spaces and replace with underscores
```
df.columns = df.columns.str.relace(' ', '_')
```
# change some columns only (use rename method and pass in dictionary)
```
df.rename(columns={'first_name': 'frist', 'last_name': 'last'}, inplace=True)
```

*update single value in a rows
```
df.loc[2] = ['mitch', 'smitch', '04040303020']
```

#selective update select columns first]
```
df.loc[2, ['last', 'first']] = ['Doe', 'jd@jd.com']
```

#change a single value
```
df.loc[2, ['last'] = 'smitch'
```

# can use at
```
df.at[2, ['last'] = 'smitch' #not sure why its there
```

# avoid mistake - change value with out loc or iloc - setting with copy warning (13:13s)
# don't ignore the warnings because they aren't perm setting the value!
#error
```
filt = (df['email'] == 'John@John.com')
df[filt]['last'] 'smith'
```

# resolve by
```
filt = (df['email'] == 'John@John.com')
df.loc[filt, 'last'] = 'Smith'
```

#update multiple rows of data
#update all rows to a lower case.
```
df['email'] = df['email'].str.lower()
```

# more advanced (4 methods)

#1 apply - call a function on values (on series)
#how long 
```
df['email'].apply(len)

def update(email):
	return email.upper()
	
df['email'].apply(update_email)

df['email'] = df['email'].apply(update_email)


df['email'] = df['email'].apply(lambda x: x.lower()) # lambda - can do with numbers
```
# use apply wtih dataframes (it runs on each row of the df)
```
df.apply(len) # applied to each series in the frame
df.apply(len, axis='columns') #rows are default
```

#get min value from each column 
```df.appy(pd.Series.min)
df.apply(lambda x: x.min())
```
#apply on each element for dataframe 
```
df.applymap(len) # get len for every element/cell of df.
df.applymap(str.lower) #convert all to lower
```

#map method (sub value wiht antoher value)
```
df['first'].map({'corey': 'chris', 'jane': 'mary'}) # has nans
df['first'].replace({'corey': 'chris', 'jane': 'mary'}) #replace
'''
