# Project_4

 #### State column has the following invalid values:
 +-----+
|State|
+-----+
|   AB|
|   BC|
|   IT|
|   MB|
|   MH|
|   NB|
|   NF|
|   NS|
|   ON|
|   PE|
|   PQ|
|   QC|
|   SK|
|   US|
|   XX|
|   YT|
+-----+

#### DL State column has the following invalid values:
DL State|
+--------+
|      AB|
|      BC|
|       F|
|      IT|
|       M|
|      MB|
|      MH|
|      NB|
|      NF|
|      NS|
|      NU|
|      ON|
|      PE|
|      PQ|
|      QC|
|      SK|
|      US|
|      XX|
|      YT|

    Query used:
    spark.sql(""" select distinct (`DL State`) from traffic_data
          where UPPER(`DL State`) not in ('AL','AK','AZ','AR','AS','CA','CO','CT','DE','DC','FL','GA','GU','HI','ID','IL',
          'IN','IA','KS','KY','LA','ME','MD','MA','MI','MN','MS','MO','MT','NE','NV','NH','NJ','NM','NY','NC','ND',
          'MP','OH','OK','OR','PA','PR','RI','SC','SD','TN','TX','TT','UT','VT','VA','VI','WA','WV','WI','WY')
          order by 1  
          """).show()


State Shortcuts in the following table are considered valid:

![Alt text](image.png)
