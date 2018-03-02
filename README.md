
# Summary

I was not able to do the calculations by separating the city types, then doing the averaging.
I needed to create those before I can put together my bubble chart. I've started doing the bubble chart.

I needed these variables with the calculations first before I can do the pie chart as well.



```python
# Import Dependencies
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
import seaborn as sns
import csv
```


```python
city_data = pd.read_csv("raw_data/city_data.csv")
city_data.head()
ride_data = pd.read_csv("raw_data/ride_data.csv")
ride_data.head()

merged = ride_data.merge(city_data, on='city', how='outer')
merged.drop_duplicates('city')
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
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>27</th>
      <td>South Roy</td>
      <td>2016-01-02 18:42:34</td>
      <td>17.49</td>
      <td>4036272335942</td>
      <td>35</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Wiseborough</td>
      <td>2016-01-21 17:35:29</td>
      <td>44.18</td>
      <td>3645042422587</td>
      <td>55</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>68</th>
      <td>Spencertown</td>
      <td>2016-07-31 14:53:22</td>
      <td>6.87</td>
      <td>2242596575892</td>
      <td>68</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>94</th>
      <td>Nguyenbury</td>
      <td>2016-07-09 04:42:44</td>
      <td>6.28</td>
      <td>1543057793673</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>120</th>
      <td>New Jeffrey</td>
      <td>2016-02-22 18:36:25</td>
      <td>36.01</td>
      <td>9757888452346</td>
      <td>58</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>145</th>
      <td>Port Johnstad</td>
      <td>2016-06-07 02:39:58</td>
      <td>17.15</td>
      <td>4352278259335</td>
      <td>22</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>179</th>
      <td>Jacobfort</td>
      <td>2016-09-20 20:58:37</td>
      <td>22.98</td>
      <td>1500221409082</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>210</th>
      <td>Travisville</td>
      <td>2016-01-15 17:32:02</td>
      <td>27.39</td>
      <td>850152768361</td>
      <td>37</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>233</th>
      <td>Sandymouth</td>
      <td>2016-11-16 07:27:00</td>
      <td>21.61</td>
      <td>2389035050524</td>
      <td>11</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>260</th>
      <td>New Andreamouth</td>
      <td>2016-04-11 07:20:48</td>
      <td>7.72</td>
      <td>9992929847990</td>
      <td>42</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>288</th>
      <td>New Christine</td>
      <td>2016-09-13 15:06:42</td>
      <td>24.89</td>
      <td>7918411468537</td>
      <td>22</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>310</th>
      <td>Stewartview</td>
      <td>2016-03-29 05:15:56</td>
      <td>23.88</td>
      <td>6778235889588</td>
      <td>49</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>340</th>
      <td>Rodriguezburgh</td>
      <td>2016-09-05 05:20:39</td>
      <td>4.54</td>
      <td>9650770953139</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>363</th>
      <td>West Sydneyhaven</td>
      <td>2016-08-02 21:18:44</td>
      <td>12.87</td>
      <td>7994760397230</td>
      <td>70</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>381</th>
      <td>Swansonbury</td>
      <td>2016-07-11 18:42:11</td>
      <td>39.30</td>
      <td>744481862626</td>
      <td>64</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>415</th>
      <td>Lisatown</td>
      <td>2016-07-05 18:09:14</td>
      <td>5.82</td>
      <td>6370359473201</td>
      <td>47</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>438</th>
      <td>East Erin</td>
      <td>2016-11-03 01:03:05</td>
      <td>7.51</td>
      <td>4744239092530</td>
      <td>43</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>466</th>
      <td>Port Martinberg</td>
      <td>2016-01-06 17:11:30</td>
      <td>8.66</td>
      <td>7298562820881</td>
      <td>44</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>487</th>
      <td>Edwardsbury</td>
      <td>2016-02-27 03:55:54</td>
      <td>20.17</td>
      <td>8514523868075</td>
      <td>11</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>514</th>
      <td>Pamelahaven</td>
      <td>2016-03-26 12:56:57</td>
      <td>36.43</td>
      <td>3015329826849</td>
      <td>30</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>529</th>
      <td>Fosterside</td>
      <td>2016-08-12 11:52:41</td>
      <td>28.08</td>
      <td>133077693483</td>
      <td>69</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>553</th>
      <td>West Alexis</td>
      <td>2016-01-16 00:33:02</td>
      <td>26.62</td>
      <td>1574788996743</td>
      <td>47</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>573</th>
      <td>Carrollfort</td>
      <td>2016-06-24 20:11:11</td>
      <td>6.45</td>
      <td>1092683495142</td>
      <td>55</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>602</th>
      <td>New David</td>
      <td>2016-01-12 20:48:43</td>
      <td>38.68</td>
      <td>5229089333754</td>
      <td>31</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>630</th>
      <td>Williamshire</td>
      <td>2016-06-22 07:53:44</td>
      <td>39.81</td>
      <td>5322918326146</td>
      <td>70</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>661</th>
      <td>Torresshire</td>
      <td>2016-10-29 12:28:18</td>
      <td>23.50</td>
      <td>6168304478087</td>
      <td>70</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>687</th>
      <td>New Aaron</td>
      <td>2016-08-12 17:14:50</td>
      <td>34.63</td>
      <td>6249037081192</td>
      <td>60</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>709</th>
      <td>Kelseyland</td>
      <td>2016-08-19 04:27:52</td>
      <td>5.51</td>
      <td>6246006544795</td>
      <td>63</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>737</th>
      <td>Lake Sarashire</td>
      <td>2016-07-16 02:33:56</td>
      <td>34.69</td>
      <td>7536776262746</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2134</th>
      <td>West Evan</td>
      <td>2016-08-09 02:20:20</td>
      <td>39.26</td>
      <td>2350874801479</td>
      <td>4</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>2146</th>
      <td>Sarahview</td>
      <td>2016-01-24 01:34:09</td>
      <td>21.42</td>
      <td>4350977208586</td>
      <td>18</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>2161</th>
      <td>South Jennifer</td>
      <td>2016-10-05 12:22:37</td>
      <td>39.24</td>
      <td>1148273096494</td>
      <td>6</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>2177</th>
      <td>Floresberg</td>
      <td>2016-07-03 11:24:38</td>
      <td>18.21</td>
      <td>4098574795183</td>
      <td>7</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>2187</th>
      <td>Williamchester</td>
      <td>2016-08-28 17:40:49</td>
      <td>30.72</td>
      <td>8203822920323</td>
      <td>26</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>2198</th>
      <td>Martinmouth</td>
      <td>2016-10-01 16:59:07</td>
      <td>15.78</td>
      <td>7253951228785</td>
      <td>5</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>2207</th>
      <td>Port Guytown</td>
      <td>2016-05-23 23:19:25</td>
      <td>23.37</td>
      <td>2895832299221</td>
      <td>26</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>2222</th>
      <td>New Cindyborough</td>
      <td>2016-09-25 16:34:43</td>
      <td>35.80</td>
      <td>3880166548267</td>
      <td>20</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>2235</th>
      <td>New Michelleberg</td>
      <td>2016-11-17 19:04:51</td>
      <td>27.33</td>
      <td>4786622689927</td>
      <td>9</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>2246</th>
      <td>North Tracyfort</td>
      <td>2016-05-07 11:43:48</td>
      <td>19.69</td>
      <td>4573622856127</td>
      <td>18</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>2256</th>
      <td>Tiffanyton</td>
      <td>2016-03-18 22:23:02</td>
      <td>27.56</td>
      <td>9111212410554</td>
      <td>21</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>2269</th>
      <td>East Cherylfurt</td>
      <td>2016-08-02 14:26:36</td>
      <td>36.94</td>
      <td>6776337445619</td>
      <td>9</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>2282</th>
      <td>Horneland</td>
      <td>2016-07-19 10:07:33</td>
      <td>12.63</td>
      <td>8214498891817</td>
      <td>8</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2286</th>
      <td>Kinghaven</td>
      <td>2016-05-18 23:28:12</td>
      <td>20.53</td>
      <td>6432117120069</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2292</th>
      <td>New Johnbury</td>
      <td>2016-04-21 08:30:25</td>
      <td>56.60</td>
      <td>9002881309143</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2296</th>
      <td>South Joseph</td>
      <td>2016-02-17 01:41:29</td>
      <td>57.52</td>
      <td>7365786843443</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2308</th>
      <td>Kennethburgh</td>
      <td>2016-10-19 13:13:17</td>
      <td>24.43</td>
      <td>2728236352387</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2318</th>
      <td>East Stephen</td>
      <td>2016-02-16 11:58:06</td>
      <td>22.43</td>
      <td>8118042484039</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2328</th>
      <td>Stevensport</td>
      <td>2016-02-14 15:52:14</td>
      <td>22.20</td>
      <td>341262393081</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2333</th>
      <td>West Kevintown</td>
      <td>2016-11-27 20:12:58</td>
      <td>12.92</td>
      <td>6460741616450</td>
      <td>5</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2340</th>
      <td>East Troybury</td>
      <td>2016-02-21 06:07:18</td>
      <td>45.12</td>
      <td>1607319707836</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2347</th>
      <td>Erikport</td>
      <td>2016-01-01 18:05:56</td>
      <td>11.76</td>
      <td>3568184448232</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2355</th>
      <td>Hernandezshire</td>
      <td>2016-02-20 08:17:32</td>
      <td>58.95</td>
      <td>3176534714830</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2364</th>
      <td>Jacksonfort</td>
      <td>2016-10-09 02:18:33</td>
      <td>10.33</td>
      <td>1819118738960</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2370</th>
      <td>East Leslie</td>
      <td>2016-04-21 18:44:59</td>
      <td>19.26</td>
      <td>5836114186294</td>
      <td>9</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2381</th>
      <td>North Whitney</td>
      <td>2016-04-01 21:21:37</td>
      <td>51.01</td>
      <td>612689673941</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2391</th>
      <td>Manuelchester</td>
      <td>2016-03-21 22:15:25</td>
      <td>49.62</td>
      <td>6045427401799</td>
      <td>7</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2392</th>
      <td>Shelbyhaven</td>
      <td>2016-05-24 15:29:59</td>
      <td>18.11</td>
      <td>1144791937271</td>
      <td>9</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2398</th>
      <td>South Elizabethmouth</td>
      <td>2016-04-03 11:13:07</td>
      <td>22.79</td>
      <td>8193837300497</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2403</th>
      <td>Matthewside</td>
      <td>2016-02-23 17:46:29</td>
      <td>59.65</td>
      <td>241191157535</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
  </tbody>
</table>
<p>125 rows × 6 columns</p>
</div>




```python
merged.dtypes
```




    city             object
    date             object
    fare            float64
    ride_id           int64
    driver_count      int64
    type             object
    dtype: object




```python

#plt.scatter(x=total_rides_per_city, y=average_fare, s=driver_count_per_city, alpha=0.5, c=colors)
```

#total_rides_per_city, average_fare, driver_count_per_city = x, y, s

plt.scatter(urban_rides_per_city_alph, urban_avg_fare_per_city_alph, s=[x * 10 for x in urban_driver_count_alph], facecolor='gold', alpha=.75,  label='Urban', edgecolors='black', marker="o", linewidth=1.5)

plt.scatter(suburban_rides_per_city_alph, suburban_avg_fare_per_city_alph, s=[x * 10 for x in suburban_driver_count_alph], facecolor='skyblue', alpha=.75,  label='Suburban', edgecolors='black', marker="o", linewidth=1.5)

plt.scatter(rural_rides_per_city_alph, rural_avg_fare_per_city_alph, s=[x * 10 for x in rural_driver_count_alph], facecolor='coral', alpha=.75,  label='Urban', edgecolors='black', marker="o", linewidth=1.5)

plt.legend(title="City Types", loc='best')


colors = ['gold', 'lightskyblue', 'lightcoral']
plt.title('Pyber Ride Sharing Data (2016)')
plt.xlabel('Total Number of Rides (Per City)')
plt.ylabel('Average Fare ($)')

plt.figure(figsize=(12,10))
plt.show()


```python
type_df = merged.groupby('type')
totalfarebycity = ["Urban", "Rural", "Suburban"]
#total_fare_bycity = [index[3]]
colors = ["lightcoral","gold","lightskyblue"]
explode = (0.1,0,0)

plt.type_df(total_fare_bycity, explode=explode, labels=totalfarebycity, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=140)

plt.title('% of Total Fares by City Type')
plt.axis("equal")
plt.show()
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-9-440f5632b8ee> in <module>()
          5 explode = (0.1,0,0)
          6 
    ----> 7 plt.type_df(total_fare_bycity, explode=explode, labels=totalfarebycity, colors=colors,
          8         autopct="%1.1f%%", shadow=True, startangle=140)
          9 
    

    AttributeError: module 'matplotlib.pyplot' has no attribute 'type_df'

