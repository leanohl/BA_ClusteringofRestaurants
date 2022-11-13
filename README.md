# BA_ClusteringofRestaurants
 Team Project 5 - Clustering of Resaurants in Seoul and Vancouver

Preprocessing reponsibility
1. NamYeong Kim Korean restaurant data set + data scaling
2. Sua Kim korean foreign data sets 
3. Lea Vancouver data sets + data scaling

---------------------------------------------------------------------------------------------------------------
Vancouvver / Seoul 
clustering the type of restaurants in specific rergion -> we can know what kind of restaurant will be opened(Japanese, Chinese, Asian, Western) 

1. number of competitors / type of restaurants 
2.  income per household   (purchasing power)
3. the percentage of foreign people 

- Korean dataset of restaurant 
https://data.seoul.go.kr/dataList/OA-16094/S/1/datasetView.do?tab=S
- Korean dataset of foreigner
https://data.seoul.go.kr/dataList/803/S/2/datasetView.do?tab=S

- Vancouver dataset of restaurants
https://www.kaggle.com/datasets/yelp-dataset/yelp-dataset?select=yelp_academic_dataset_business.json
or
https://www.kaggle.com/datasets/banaveenkumar/vancouver-restaurent-dataset

- Vancouver dataset: cencus including income and foreigners
https://opendata.vancouver.ca/explore/?refine.theme=Demographics&disjunctive.features&disjunctive.theme&disjunctive.keyword&disjunctive.data-owner&disjunctive.data-team&sort=modified

https://towardsdatascience.com/strategic-location-for-establishing-an-asian-restaurant-c3aecf2496b1

Presentation_proposal:
https://docs.google.com/presentation/d/1S7PtsZcltAvBRVWNfxYOq8n8C-J9iMK5DJ1AyKs_qx8/edit?usp=sharing

Presentation_mid : 
https://docs.google.com/presentation/d/1tTpX0eMBt7jy07XvRNR9kcnZQgEgCwAAp-yL5cLEEM4/edit?usp=sharing



# Preprocessing of the Vancouver Dataset:
## Challenges:
1. The dataset of the restaurants if relatively small
2. The feature "Type of cuisine" is not really specific and we can not use the instance "Restaurant"
3. The Landmark is only an adress not a point or district
4. Many addresses are just "Vancouver, BC, Canada"

## Possible solutions:
1. The instances of the feature "Type of cuisine" that are just named restaurant: 
	- not only delet the instance but try to find the type of cuisine with the help of the name of the restaurant
2. With the help of geopy I try to transfer the address to a point containing longitude and latitude
	- benefit: with folium we can create an interactive map


