# BA_ClusteringofRestaurants
 Team Project 5 - Clustering of Resaurants in Seoul and Vancouver

Find the best location to open a restaurant of a specific cuisine in Seoul and Vancouver
K- MEANS CLUSTERING
17101936 Kim NamYeong
20102104 Kim Sua
22170091 Lea Scharpf 

  Business Analytics 


Introduction
Opening a restaurant in big capital cities can be quite a challenge. Not only good food needs to be saved in order to not go bankrupt, but also the people living there should value the food. To find the best location to open a restaurant depends on a lot of different factors. People in that area should earn enough money to be able to go to a restaurant. Next, if you want to open a restaurant with a cuisine from another country, some people from that country should live close to the restaurant, to be sure to have some customers. Also, it makes a restaurant more authentic, when people from that country enjoy the food. Third, there should not be too many competitors, since people than have to choose between your restaurant and others.
Therefore, we choose to cluster the restaurants from Seoul and Vancouver in order to find the best location to open a restaurant from a specific type of cuisine. The goal is to reduce business failures due to incorrect market analysis. 

Data Acquisition
To create such a clustering method, datasets from both cities including income, citizenship and a restaurant dataset are needed.
For the city Seoul the datasets were available on data Seoul:
	Korean dataset of restaurant: 
o	https://www.data.go.kr/data/15083033/fileData.do
	 Korean dataset of foreigner:
o	https://data.seoul.go.kr/dataList/803/S/2/datasetView.do?tab=S 
	Korean dataset of Income:
o	https://golmok.seoul.go.kr/stateArea.do

Kaggle provided the restaurant dataset for Vancouver: 
	https://www.kaggle.com/datasets/banaveenkumar/vancouver-restaurent-dataset
The dataset for the income and the citizenship was found at Opendata Vancouver:
	https://opendata.vancouver.ca/explore/?refine.theme=Demographics&disjunctive.features&disjunctive.theme&disjunctive.keyword&disjunctive.data-owner&disjunctive.data-team&sort=modified





Preprocessing
After importing these data sets it was necessary to do preprocessing steps to clean the datasets.
[Seoul]
Since we have to know the percentage of foreigners in each ‘동’. 
We have to calculate it with python codes.
Before preprocessing the foreign datasets looked like this:

![image](https://user-images.githubusercontent.com/40350018/205353920-d579c353-e422-4f8f-be84-95fa1acd248f.png)

After preprocessing the foreign datasets looked like this:
![image](https://user-images.githubusercontent.com/40350018/205353943-3f6a9d7c-0e73-4ad5-9cc8-f4ecc4e42cb1.png)

In our restaurant data set, there are all the stores in seoul so we have to exclude that redundant information.
Like foreigner data set we calculate the percentage of each restaurant.
Before preprocessing the restaurant datasets looked like this:
![image](https://user-images.githubusercontent.com/40350018/205353974-2410f2ab-d08a-46e8-9cec-f7ff7d5c3c69.png)

After preprocessing the restaurant datasets looked like this:
![image](https://user-images.githubusercontent.com/40350018/205354034-907e3ac2-c481-414a-8a35-3cce8fff8483.png)

Before preprocessing the income datasets looked like this:
![image](https://user-images.githubusercontent.com/40350018/205354077-70f9d5a6-eacb-482f-a008-a9ac58218721.png)

After preprocessing the income datasets looked like this:
![image](https://user-images.githubusercontent.com/40350018/205354108-1ec875bd-9538-4e03-8f37-b50537eb52c0.png)

After merging all korean datasets:
![image](https://user-images.githubusercontent.com/40350018/205354136-e7714d46-fb4f-4c77-bcdb-47f1ad05f59f.png)


-------------------------------------------------------------------------------------------------------------------------
[Vancouver]
Since the Vancouver census datasets consists of a lot of different spreadsheets, it was necessary to extract the important information. Therefore, two new datasets were created out of the census dataset only containing the necessary information.
Before preprocessing the datasets looked like this:

![image](https://user-images.githubusercontent.com/40350018/205354185-2a36a11c-de8e-427a-9859-7b0f13a397f1.png)

![image](https://user-images.githubusercontent.com/40350018/205354196-690e761d-b002-4aa8-a47f-de5fa3ba82c2.png)

-	Pre-processing of Vancouver income dataset
The Vancouver income dataset contains the features: total income and the districts of Vancouver.  24 districts of Vancouver are included. Every instance is about the range of income, going from under 10 000$ in 12 steps up to 150 000$ income and more.
The row “$100.000 and over” needs to be dropped because it only contains the information found in the rows before and after.
We are only interested in the weighted average income from each district. Therefore, it is necessary to calculate the average income first and then calculate the total weighted average income for every district.
After applying these calculations, the dataset looked like this:
![image](https://user-images.githubusercontent.com/40350018/205354228-913e9a9a-fa23-4b0c-b82d-ee1b9d39e505.png)

Pre-processing of Vancouver citizenship dataset

The citizenship dataset from Vancouver includes features of the place of birth and number of people of that birthplace in every district.
First, the ID column had to be dropped.
Then, I transposed the dataset to better calculate the average population of each district. Since we decided to do the clustering only for the categories: Western, Japanese, Koreans, Chinese, South- East Asians, I summarized these origins, calculated the total population and the percentage of the population in every district and dropped the rest. As Western people I included people from Europe, the USA and Canada. After the preprocessing the dataset looked like this:

![image](https://user-images.githubusercontent.com/40350018/205354274-b597bbae-7721-440e-a1bc-ffae5d4fcbd7.png)

These two datasets are now ready to be merged.
To get a better overview of the districts of Vancouver a folium map was created with the help of Geopy. Geopy provides a class for popular mapping services. Nominatim is the service behind the popular OpenStreetMap that allows you to geocode for free. With geocode it is possible to get the longitude and latitude of a place. After merging and calculation the location the final dataset looked like this:

![image](https://user-images.githubusercontent.com/40350018/205354291-30515002-c397-43b2-bc27-da5217e6d9d2.png)

![image](https://user-images.githubusercontent.com/40350018/205354304-051a32b1-fa46-4d6b-9043-8b5034eba89d.png)

![image](https://user-images.githubusercontent.com/40350018/205354316-ca7bcc97-ea0f-43c8-8ad5-2ebc961b98f6.png)

With Folium Map it is possible to create a map displaying every district:

![image](https://user-images.githubusercontent.com/40350018/205354336-d3848f33-324c-4841-b9f4-6a7eff393f48.png)


-	Preprocessing of Vancouver restaurant dataset
The dataset provided from Kaggle contains the features: name of restaurant, type of cuisine, rating, total no of ratings, cost, landmark, opening time, current status, dine in availability, takeaway type, delivery availability and location and address. From this given features only the features: name of restaurant, type of cuisine, landmark and location and address are interesting for the given task.
In total only 384 instances are given, which makes this dataset comparably small. 
After dropping the unnecessary features, the dataset looked like this:
![image](https://user-images.githubusercontent.com/40350018/205354383-7c7c1c26-7504-4b5b-9b01-55a0c3b5f199.png)![image](https://user-images.githubusercontent.com/40350018/205354395-94029c66-62ba-4262-abd5-d7a1cb3414b7.png)


The dataset contains two duplicates, which need to be dropped at first.
Having a closer look on the instances, one can see the challenges this dataset provides:
1.	The type of cuisine is often referred to as “Restaurant”, which has no meaning at all.
2.	The Landmark and Location and Address contain a lot of NaN values. 
Since the dataset is so small it is not possible to just drop the 73 rows that contain as type of cuisine only “Restaurant”.  Therefore, it was necessary to extract the information about the type of cuisine from the restaurant’s name. After doing so from the 382 instances 325 instances were left.

![image](https://user-images.githubusercontent.com/40350018/205354422-b43f2079-1f1c-4ec6-96b6-cbb7db1a7222.png)

Our goal was to cluster the districts with the types of restaurants: Western, Chinese, Japanese, Rest of Asia. That’s why these types of cuisines need to be aggregated to the categories mentioned before. It resulted in the following number of types of cuisine:

![image](https://user-images.githubusercontent.com/40350018/205354605-48b5d33d-bff2-4c86-932d-382f95023c7a.png)

Regrettably only 177 instances are left.

![image](https://user-images.githubusercontent.com/40350018/205354624-3716d4d8-7bb6-4d39-9f1d-08821468e50c.png)

The second challenge was to find the exact location of the restaurant. I merged the Landmark and Location and Address since they have the same meaning into a new column “place”. To be able to get the exact location with the help of geopy meaningful addresses need to be provided. Having a look at the type of places leads to a sobering result. 82 instances are located in Vancouver, but do not contain a specific address. I choose to add the name of the restaurant to the first three instances, so geopy might locate the restaurants. Another problem are the addresses containing “#” or “ú”. With some more feature engineering it was possible to get more exact locations. After applying the geopy location function I choose to drop the instances that still couldn’t be found. That resulted in a dataset with 138 instances left. With the help of folium map we could visualize to location of the restaurants.
![image](https://user-images.githubusercontent.com/40350018/205354640-ab72325f-1fda-43d7-8eca-d5a0d109b137.png)

The final restaurant dataset is visualized in the following figure:
![image](https://user-images.githubusercontent.com/40350018/205354666-6f6c749a-edad-42a0-9061-a0b98a4de006.png)

	Final merge of the datasets
Now, the two resulting datasets need to be merged. The challenge hereby is to merge the datasets on the feature district/ neighborhood. Since the latitude and longitude of the restaurant and the neighborhood are given, I merged the datasets using the Haversine Distance. 
“The Haversine formula calculates the shortest distance between two points on a sphere using their latitudes and longitudes measured along the surface.” (Haversine formula to find distance between two points on a sphere - GeeksforGeeks) Mathematically is can be expressed as:  haversine(θ)= 〖sin〗^2 (θ/2). Calculating the central angle of the haversine and solving it for d results in: 
d=2*r*〖sin〗^(-1) (√(〖sin〗^2 ((Φ_2-Φ_1)/2)+cos⁡(Φ_1 )*cos⁡(Φ_2 )*〖sin〗^2 ((λ_2-λ_1)/2) ))
Applying this formula on the longitude of the restaurant and the neighbourhood, it was possible to find the closest neighbourhood for every restaurant.
The restaurants are mostly distributed over Downtown, Vancouver, as the following figure shows.

![image](https://user-images.githubusercontent.com/40350018/205354713-c3c25feb-185f-4870-90ff-33fb5819e5e2.png)

Next step is to use one hot encoding to create numerical values from the four types of cuisine: Chinese, Japanese, Asian and Western Restaurant:

![image](https://user-images.githubusercontent.com/40350018/205354726-949ea026-61f7-401c-95ba-71ae1ff8b260.png)

Depending on which restaurant type we want to create the clustering for, the “str_cluster” needs to be adjusted. 
In the following example I will make the analysis for Chinese restaurants. The dataset shown in the previous figure can therefore be adjusted to only the neighbourhood and the type of restaurant we want to do the clustering for.
After merging the datasets on “neighbourhood”, the final dataset is shown in the following figure:

![image](https://user-images.githubusercontent.com/40350018/205354745-94d18b64-4ed1-496c-92fb-8eae8c3e4541.png)

Still, we need to normalize our data. In this case using Standard Scaler.




  
