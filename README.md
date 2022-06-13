import pytrends
import pandas as pd
import matplotlib.pyplot as plt
from pytrends.request import TrendReq
trends = TrendReq()

irasas_pn= input("Iveskite norimą Šalį")

data = trends.trending_searches(pn=irasas_pn)
print("GoogleTrends įdėjos pagal ivestą šalį")
print(data.head(25))

irasas_kw= input("Įveskite Keyword pagal šalyje trendinantį keyword")

trends.build_payload(kw_list=[irasas_kw])
data = trends.interest_by_region()

saliu_kw_list = data[data[irasas_kw] > 35].sort_values(irasas_kw, ascending=False)
print(saliu_kw_list)

saliu_kw_list.reset_index().plot(x="geoName", y=irasas_kw, figsize=(5,5), kind="bar")
plt.show()

keyword = trends.suggestions(keyword=irasas_kw)
data = pd.DataFrame(keyword)
print("Google įdėjos/pasiūlymai pagal įvestą Keyword")
print(data.head())
