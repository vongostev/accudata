[![Language grade: Python](https://img.shields.io/lgtm/grade/python/g/vongostev/accudata.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/vongostev/accudata/context:python)
[![pypi](https://github.com/vongostev/accudata/actions/workflows/python-publish.yml/badge.svg)](https://github.com/vongostev/accudata/actions/workflows/python-publish.yml)

### Do you collect a heterogeneous data step by step?

Here you find a convinient solution of this problem.
class AccumulativeData provides a simple interface to store data step by step.
The data can be consisted of:
1. Numbers
2. Lists / arrays
3. Objects

You can store it as pickled object or Pandas Dataframe.

### Installation

The module can be installed from pip
```
pip install accudata
```

### For example

You have a social data collecting process. You must collect on every step heterogeneous data:
1. Name of a person
2. Age
3. Interests
4. Preferences by categories: food, pets, sport, politics

You can make a class:
```python
from accudata import AccumulativeData

class PeopleAccData(AccumulativeData):
	def __init__(self):
		lists = ['name', 'age', 'interests']
		dicts = {'pref': ['food', 'pets', 'sport', 'politics]}
		super().__init__(lists=lists, dicts=dicts)
```

After that you can make an iterative collecting process as follows:
```python
Data = PeopleAccData()
for item in raw_data:
	Data.next()
	# \\\ A complicated code to extract data
	name, age, interests, food, pets, sport, politics, _ = extract_data(item)
	Data.append(name, age, interests,
		    pref=[food, pets, sport, politics])
	
```

It is simple to get data:
```python
names = Data.name
# Make the dataframe
dataframe = Data.todf()
print(dataframe.name)
```

