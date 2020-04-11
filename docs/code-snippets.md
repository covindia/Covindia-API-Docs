# Code Snippets

For the latest code snippets, visit [https://github.com/covindia/CovIndia_analysis](https://github.com/covindia/CovIndia_analysis)

For data scientists and researchers who use Python3, this iPython Notebook (Jupyter Notebook) will come in handy:

* to directly generate CSVs (that can be opened in Microsoft Excel)
* to do some basic analysis like day-wise state and district numbers.
* to demonstrate a small example of plotting the infected numbers for a given state and doing some curve fitting to smoothen the graph.
* to demonstrate an example of the kind of analysis possible with this data.

Best viewed at this link for seeing the outputs and graphs: [CovIndia API Basic Analysis](https://github.com/covindia/CovIndia_analysis/blob/master/CovIndia_API_basic_analysis.ipynb)

Python3
```python
import requests		# Needs to be installed (pip3 install requests)
import json
import pandas as pd	# Needs to be installed (pip3 install pandas)

url = 'https://v1.api.covindia.com/covindia-raw-data'
raw_data = requests.get(url=url).json()

# Next line is just to change the type of keys from string to int
# This is required for making the dataframe automatically
raw_data = {int(old_key): val for old_key, val in raw_data.items()}

# print(raw_data)

raw_data_df = pd.DataFrame.from_dict(raw_data, orient='index')
raw_data_df = raw_data_df [['date','time','district','state','infected','death','source']]
raw_data_df["date"] = pd.to_datetime(raw_data_df["date"],dayfirst=True)
raw_data_df.to_csv('raw_data.csv', index = False)

raw_data_df.head()

# Finding the total infected and death
print('Total Infected : ' + str(raw_data_df['infected'].sum()))
print('Total Death : ' + str(raw_data_df['death'].sum()))

# Aggregating the data daywise and districtwise
dist_day_df = raw_data_df.groupby(['date', 'district'], as_index=False)['infected','death'].sum()
dist_day_df = dist_day_df.sort_values('date', ascending = True)

dist_day_df.head()

# Aggregating the data daywise and statewise
state_day_df = raw_data_df.groupby(['date', 'state'], as_index=False)['infected','death'].sum()

state_day_df.head()

# Plotting infected numbers for a particular state
%matplotlib inline
from matplotlib import pyplot as plt

maharashtra_df = state_day_df[state_day_df['state']=='Maharashtra']
# maharashtra_df = maharashtra_df.sort_values('date', ascending=True)

plt.plot(maharashtra_df['date'], maharashtra_df['infected'])
plt.xticks(rotation='vertical')
plt.title('Infected numbers for Maharashtra')

from scipy.ndimage.filters import gaussian_filter1d
import numpy as np

ysmoothed = gaussian_filter1d(np.array(maharashtra_df['infected']), sigma=1.5)

plt.plot(np.array(maharashtra_df['date']), ysmoothed, color='orange')
plt.plot(maharashtra_df['date'], maharashtra_df['infected'])
plt.xticks(rotation='vertical')

plt.show()
```