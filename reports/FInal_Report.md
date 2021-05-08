# INSIDERS PROGRAM
## High Value Customers Identification

![ecommerce](https://user-images.githubusercontent.com/71295866/117546030-bf3e0980-affe-11eb-9df3-2b366c5dfedd.jpg)

## The Challenge

You are part of a Data Scientists team from the All In One Place company, that needs to determine who are the clients eligible to participate of the “Insiders Program”. With this clients list on hand, the marketing team will a sequency of a custom and exclusive actions for this group, in order to rise the revenues and the purchase frequency. 
As result for this project is expected that you deliver a list with eligible clients to participate of the “Insiders Program”, as well a report answering the following questions:

1. Who are the elegible customers to participate in the “Insiders Program”?
2. How many clients will be part of the group?
3. Where are the "Insiders" customers from?
4. Which is the revenues percentage that comes from the group?

**All this questions will be answerd in a final report, in the end of this README.**

## The Data

The data set is available on the Kaggle platform, through this link:

https://www.kaggle.com/vik2012kvs/high-value-customers-identification

Each row represents a sell transaction that happened between November 2016 and December 2017. The dataset includes the following informations:

• **Invoice Number:** unique id from each purchase.

• **Stock Code Product:** item code.

• **Description Product:** item name.

• **Quantity:** the quantity of each item purchased per transaction.

• **Invoice Date:** the day that the purchase occurred.

• **Unit Price:** product price per unit.

• **Customer ID:** client id.

• **Country:** the client country.


## The Solution

To solve this problem, some clustering algorithms were used, which, after processing the data, were modeled and tested, in order to find an algorithm that best performs for this data set. In this project we've tested KMeans, DBSCAM and Mean Shift clustering algorithms, from Scikit-Learn library.

### EDA - Exploratory Data Analysis

The next image shows us the average sales by month. The best month to sales is Octobera and the worst is April.

![sales_by_month](https://user-images.githubusercontent.com/71295866/117546091-1217c100-afff-11eb-9e7e-8de97cfd477b.png)


The dataset has no fridays and we haven't been able to find out why. Despite that, we plot the total sales and the average sales by day of week.

![tot_sales_by_day_week](https://user-images.githubusercontent.com/71295866/117546099-20fe7380-afff-11eb-9a3c-f824f8aeb15d.png)

![avg_sales_by_day_week](https://user-images.githubusercontent.com/71295866/117546115-383d6100-afff-11eb-91f0-72d8c30c8023.png)

UK is the home country of the vast majority of customers. In order to see from which country are the foreigns customers, we plot a bar graph showing us that besides UK, German and France has the biggest customers quantities.

![customers_by_country](https://user-images.githubusercontent.com/71295866/117546126-573bf300-afff-11eb-9961-6e298a0b9fbc.png)

![customers_no_UK_by_country](https://user-images.githubusercontent.com/71295866/117546150-6ae75980-afff-11eb-86dc-cf234d6ff1c9.png)

Besides UK, the countryes with majos sales values are Netherlands, Ireland and German.

![spends_no_UK_by_country](https://user-images.githubusercontent.com/71295866/117546169-7c306600-afff-11eb-838c-f1ccd96d1cf6.png)
![scatter_spends_by_cluster](https://user-images.githubusercontent.com/71295866/117546199-9f5b1580-afff-11eb-927f-e04073ad892d.png)

### Machine Learning Model Selection

To figure out who are the customers eligible to insiders Program, we performed sevearal tests with 3 different clustering algorithms, KMmeans, DBSCAM and Mean Shift, analyzing the performance metrics of each one. After the tests, we come to the conclusion that the groups clustered by DBSCAM algorithm performed better than the other ones.


|    | Model      |   Number of cluesters |   Mean Silhouette Score |   Davies-Boudin Index |   Calinski Harabasz Index 
|---:|:-----------|----------------------:|------------------------:|----------------------:|--------------------------:|
|  0 | KMeans     |                     3 |                0.346804 |              0.922579 |                   2050.19 |
|  1 | DBSCAN     |                     2 |                0.890368 |              0.934715 |                   1908.19 |
|  2 | Mean Shift |                    38 |                0.52136  |              0.311105 |                    268.16 |

As metrics evaluation we used Mean Silhouette Score, Davies-Boudin Index and Calinski Harabasz Index. For Mean Silhouette Score, as the closest to 1, the better. For Davies-Boudin Index, as the closest to 0, the better. For Calinski Harabasz Index, the bigger, the Better.

## Customer Segmentation Analysis

DBSCAN was selected as the better clustering algorithm for this dataset. The DBSCAM select two diferent groups and we called them "Insiders Program Custoomer" and "Not Insiders".

|    | clusters         |   CustomerID |   perc_customer |   AVG_total_spend |   AVG_total_invoices |   AVG_last_purchase |   AVG_total_itens_purchased 
|---:|:-----------------|-------------:|----------------:|------------------:|---------------------:|--------------------:|----------------------------:
|  0 | Insiders Program |           40 |        0.922935 |          66601    |            1155.55   |              28.125 |                   38826.5  
|  1 | Not Insiders     |         4294 |       99.0771   |           1414.34 |              80.3277 |              93.833 |                     835.752 |



**1. Who are the elegible customers to participate in the “Insiders Program”?**

The "Insiders" are a group with high value customers. They are the customer who has bought high amounts of items, with high amounts spent and with high recency of purchases.

**2. How many clients will be part of the group?**

The DBSCAM Original "Insiders" group has 40 members of high value customers.

The following graph shows us the distribution of the customers by total value spend.

![scatter_spends_by_cluster](https://user-images.githubusercontent.com/71295866/117546208-ab46d780-afff-11eb-82ac-998341a823c5.png)

The red points are the "Insiders". How we can see, they have the bigger spends.

**3. Where are the "Insiders" customers from?**

* UK - 32
* Ireland - 2   
* Sweden - 1    
* Netherlands - 1    
* Australia - 1

![insiders_dist_by_country](https://user-images.githubusercontent.com/71295866/117546232-c4e81f00-afff-11eb-93f8-e21b6afc20fc.png)

The 40 members of "Insiders" group represents 30.49% from the total revenues.

![spends_proportion_by_cluster](https://user-images.githubusercontent.com/71295866/117546266-f365fa00-afff-11eb-936a-aa94ead40d79.png)

## Insiders Customer Group

|    |   CustomerID | Country        |   total_invoices |   total_spend |   total_itens_purchased |   last_purchase_(days) |
|---:|-------------:|:---------------|-----------------:|--------------:|------------------------:|-----------------------:|
|  0 |        12346 | United Kingdom |                1 |      77183.6  |                   74215 |                    326 |
|  1 |        12415 | Australia      |              713 |     124565    |                   77373 |                     25 |
|  2 |        12748 | United Kingdom |             4397 |      31650.8  |                   25051 |                      1 |
|  3 |        12901 | United Kingdom |              116 |      17654.5  |                   23075 |                      9 |
|  4 |        12931 | United Kingdom |               82 |      42056    |                   28004 |                     22 |
|  5 |        13027 | United Kingdom |               26 |       6912    |                   17280 |                    114 |
|  6 |        13081 | United Kingdom |             1024 |      28337.4  |                   19068 |                     12 |
|  7 |        13089 | United Kingdom |             1814 |      58762.1  |                   31025 |                      3 |
|  8 |        13098 | United Kingdom |              572 |      28882.4  |                   15968 |                      2 |
|  9 |        13263 | United Kingdom |             1662 |       7411.71 |                    4761 |                      2 |
| 10 |        13408 | United Kingdom |              478 |      28117    |                   16232 |                      2 |
| 11 |        13694 | United Kingdom |              568 |      65039.6  |                   63312 |                      4 |
| 12 |        13798 | United Kingdom |              349 |      37153.8  |                   23948 |                      2 |
| 13 |        14088 | United Kingdom |              589 |      50491.8  |                   12665 |                     11 |
| 14 |        14096 | United Kingdom |             5095 |      53258.4  |                   16336 |                      5 |
| 15 |        14156 | EIRE           |             1382 |     116560    |                   57755 |                     10 |
| 16 |        14298 | United Kingdom |             1637 |      51527.3  |                   58343 |                      9 |
| 17 |        14606 | United Kingdom |             2674 |      11926.2  |                    6177 |                      2 |
| 18 |        14646 | Netherlands    |             2060 |     279138    |                  196844 |                      2 |
| 19 |        14911 | EIRE           |             5584 |     136162    |                   80154 |                      2 |
| 20 |        15039 | United Kingdom |             1477 |      19766.6  |                    9131 |                     10 |
| 21 |        15061 | United Kingdom |              403 |      54534.1  |                   28920 |                      4 |
| 22 |        15098 | United Kingdom |                3 |      39916.5  |                     121 |                    183 |
| 23 |        15311 | United Kingdom |             2366 |      60632.8  |                   38147 |                      1 |
| 24 |        15749 | United Kingdom |               10 |      44534.3  |                   18028 |                    236 |
| 25 |        15769 | United Kingdom |              130 |      56252.7  |                   29672 |                      8 |
| 26 |        15838 | United Kingdom |              167 |      33643.1  |                   18368 |                     12 |
| 27 |        16013 | United Kingdom |              139 |      37130.6  |                   15536 |                      4 |
| 28 |        16029 | United Kingdom |              240 |      72708.1  |                   40107 |                     39 |
| 29 |        16333 | United Kingdom |               45 |      26626.8  |                   32184 |                      8 |
| 30 |        16422 | United Kingdom |              369 |      34684.4  |                   33704 |                     18 |
| 31 |        16446 | United Kingdom |                3 |     168472    |                   80997 |                      1 |
| 32 |        16684 | United Kingdom |              277 |      66653.6  |                   50255 |                      5 |
| 33 |        17381 | United Kingdom |              109 |      20275.6  |                   25649 |                      9 |
| 34 |        17404 | Sweden         |              195 |      31781.8  |                   32744 |                      5 |
| 35 |        17450 | United Kingdom |              336 |     194391    |                   69973 |                      9 |
| 36 |        17511 | United Kingdom |              963 |      91062.4  |                   64549 |                      3 |
| 37 |        17841 | United Kingdom |             7667 |      40496    |                   22816 |                      2 |
| 38 |        17949 | United Kingdom |               69 |      58030.5  |                   30450 |                      2 |
| 39 |        18102 | United Kingdom |              431 |     259657    |                   64124 |                      1 |
