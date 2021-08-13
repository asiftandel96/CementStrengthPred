                                                    Cement Strength Prediction
                                                       
  Project Link:- https://cementstrengthpred.herokuapp.com/
  
  Project Demo:-
   
  ![PostmanCementfile](https://user-images.githubusercontent.com/61505882/129213514-d6412321-ff3c-4c82-9ce9-b35dd3985be8.gif)

  Checking the Prediction in Postman:-
 
  ![PostmanCE](https://user-images.githubusercontent.com/61505882/129214523-d104bb50-4fe5-4357-aa3a-0bbd0414bedd.gif)
  
  Problem Statement:-
  
  To build a regression model to predict the concrete compressive strength based on the different features in the training data.
  
  Project Architecture:-
  
  ![image](https://user-images.githubusercontent.com/61505882/129215404-422c4d09-5ce8-4e02-96d8-ef0ea3af8133.png)

  Data Description:-
  
  Given is the variable name, variable type, the measurement unit and a brief description. The concrete compressive strength is the regression problem. The order of this listing 
corresponds to the order of numerals along the rows of the database. 


Name | DataType | Measurement | Description
------------ | ------------- | ------------ | -------------  
Cement (component 1) | quantitative | kg in a m3 mixture | 
Blast Furnace  | quantitative | kg in a m3 |  Blast furnace
Slag (component 2) |          | mixture | slag is a nonmetallic coproduct produced in the process. It consists primarily of silicates, aluminosilicates, and calcium-alumina-                                                 silicates
Fly Ash (component 3) | quantitative | kg in a m3 mixture | It is a coal combustion product that is composed of the particulates (fine particles of burned fuel) that are driven                                                                out of coal-fired boilers together with the flue gases. 
Water (component 4) | quantitative | kg in a m3 mixture |
Superplasticizer (component 5) | quantitative | kg in a m3 mixture | Superplasticizers (SP's), also known as high range water reducers, are additives used in making high strength                                                                       concrete. Their addition to concrete or mortar allows the reduction of the water to cement ratio without                                                                           negatively affecting the workability of the mixture, and enables the production of self-consolidating                                                                               concrete and high performance concrete
Coarse Aggregate (component 6) | quantitative | kg in a m3 mixture | construction aggregate, or simply "aggregate", is a broad category of coarse to medium grained particulate                                                                          material used in construction, including sand, gravel, crushed stone, slag, recycled concrete and geosynthetic                                                                      aggregates
Fine Aggregate (component 7) | quantitative | kg in a m3 mixture | Similar to coarse aggregate, the constitution is much finer
Age| quantitative| Day (1~365)| 
Concrete compressive strength| quantitative | MPa | Output Variable


Apart from training files, we also require a "schema" file from the client, which contains all the relevant information about the training files such as:
Name of the files, Length of Date value in FileName, Length of Time value in FileName, Number of Columns, Name of the Columns, and their datatype.

![SchemaT](https://user-images.githubusercontent.com/61505882/129382967-64c0726f-fe21-4444-8382-b18b27fbba2d.JPG)


 
Data Validation:-

In this step, we perform different sets of validation on the given set of training files. 

1.	 Name Validation- We validate the name of the files based on the given name in the schema file. We have created a regex pattern as per the name given in the schema file to use for validation. After validating the pattern in the name, we check for the length of date in the file name as well as the length of time in the file name. If all the values are as per requirement, we move such files to "Good_Data_Folder" else we move such files to "Bad_Data_Folder."

2.	 Number of Columns - We validate the number of columns present in the files, and if it doesn't match with the value given in the schema file, then the file is moved to "Bad_Data_Folder."

3.	 Name of Columns - The name of the columns is validated and should be the same as given in the schema file. If not, then the file is moved to "Bad_Data_Folder".

4.	 The datatype of columns - The datatype of columns is given in the schema file. This is validated when we insert the files into Database. If the datatype is wrong, then the file is moved to "Bad_Data_Folder".

5.	Null values in columns - If any of the columns in a file have all the values as NULL or missing, we discard such a file and move it to "Bad_Data_Folder".

![rawfilecement](https://user-images.githubusercontent.com/61505882/129383554-53453036-b00e-4345-8710-afbd3ceb922d.gif)


Data Insertion in Database:-
 
1) Database Creation and connection - Create a database with the given name passed. If the database is already created, open the connection to the database. 

2) Table creation in the database - Table with name - "Good_Data", is created in the database for inserting the files in the "Good_Data_Folder" based on given column names and datatype in the schema file. If the table is already present, then the new table is not created and new files are inserted in the already present table as we want training to be done on new as well as old training files.     

3) Insertion of files in the table - All the files in the "Good_Data_Folder" are inserted in the above-created table. If any file has invalid data type in any of the columns, the file is not loaded in the table and is moved to "Bad_Data_Folder".

 ![dbcement](https://user-images.githubusercontent.com/61505882/129383974-6fe9832c-d7ee-4ce3-8238-ab0d5080df8f.gif)

Model Training:-

1) Data Export from Db - The data in a stored database is exported as a CSV file to be used for model training.

2) Data Preprocessing  

   a) Check for null values in the columns. If present, impute the null values using the KNN imputer.
   
   b) transform the features using log transformation.
   
   c) Scale the training and test data separately.
   
   
3) Clustering - KMeans algorithm is used to create clusters in the preprocessed data. The optimum number of clusters is selected by plotting the elbow plot, and for the dynamic selection of the number of clusters, we are using "KneeLocator" function. The idea behind clustering is to implement different algorithms
   To train data in different clusters. The Kmeans model is trained over preprocessed data and the model is saved for further use in prediction.
   
4) Model Selection - After clusters are created, we find the best model for each cluster. We are using two algorithms, "Random forest Regressor" and “Linear Regression”. For each cluster, both the algorithms are passed with the best parameters derived from GridSearch. We calculate the Rsquared scores for both models and select the model with the best score. Similarly, the model is selected for each cluster. All the models for every cluster are saved for use in prediction. 


![trainmodel](https://user-images.githubusercontent.com/61505882/129384761-ad06dc99-b87b-4b85-8ab9-c6345a582e4d.gif)


 
Prediction Data Description:-
 
Client will send the data in multiple set of files in batches at a given location. Data will contain climate indicators in 8 columns.
Apart from prediction files, we also require a "schema" file from client which contains all the relevant information about the training files such as:
Name of the files, Length of Date value in FileName, Length of Time value in FileName, Number of Columns, Name of the Columns and their datatype.

Data Validation:-

In this step, we perform different sets of validation on the given set of training files.

1) Name Validation- We validate the name of the files on the basis of given Name in the schema file. We have created a regex pattern as per the name given in schema file, to use for validation. After validating the pattern in the name, we check for length of date in the file name as well as length of time in the file name. If all the values are as per requirement, we move such files to "Good_Data_Folder" else we move such files to "Bad_Data_Folder". 

2) Number of Columns - We validate the number of columns present in the files, if it doesn't match with the value given in the schema file then the file is moved to "Bad_Data_Folder". 

3) Name of Columns - The name of the columns is validated and should be same as given in the schema file. If not, then the file is moved to "Bad_Data_Folder". 

4) Datatype of columns - The datatype of columns is given in the schema file. This is validated when we insert the files into Database. If dataype is wrong then the file is moved to "Bad_Data_Folder". 

5) Null values in columns - If any of the columns in a file has all the values as NULL or missing, we discard such file and move it to "Bad_Data_Folder".
  
Data Insertion in Database:-

  1) Database Creation and connection - Create database with the given name passed. If the database is already created, open the connection to the database. 
  
  2) Table creation in the database - Table with name - "Good_Data", is created in the database for inserting the files in the "Good_Data_Folder" on the basis of given column         names and datatype in the schema file. If table is already present then new table is not created, and new files are inserted the already present table as we want training to      be  done on new as well old training files.     
  
  3) Insertion of files in the table - All the files in the "Good_Data_Folder" are inserted in the above-created table. If any file has invalid data type in any of the columns,      the file is not loaded in the table and is moved to "Bad_Data_Folder".


Prediction 
 
1) Data Export from Db - The data in the stored database is exported as a CSV file to be used for prediction.
2) Data Preprocessing   
   a) Check for null values in the columns. If present, impute the null values using the KNN imputer
   
   b) transform the features using log transformation
   
   c) Scale the training and test data separately 
   
3) Clustering - KMeans model created during training is loaded, and clusters for the preprocessed prediction data is predicted.

4) Prediction - Based on the cluster number, the respective model is loaded and is used to predict the data for that cluster.

5) Once the prediction is made for all the clusters, the predictions along with the original names before label encoder are saved in a CSV file at a given location and the location is returned to the client.
 
Deployment:-

We will be deploying the model to the Heroku Platform. 

This is a workflow diagram for the prediction of using the trained model.   

Now let’s see the Cement_Strength project folder structure.

![image](https://user-images.githubusercontent.com/61505882/129224410-83fd8565-377b-4d6a-aec3-a6e2391da8bf.png)

requirements.txt file consists of all the packages that you need to deploy the app in the cloud.

![image](https://user-images.githubusercontent.com/61505882/129224490-44a6b2b5-c772-4020-87fd-18a49fa2bf5c.png)

app.py is the entry point of our application, where the flask server starts. 


![image](https://user-images.githubusercontent.com/61505882/129224721-8cd39135-fe59-4d97-8e93-c1efb35b2f64.png)

This is the predictionFromModel.py file where the predictions take place based on the data we are giving input to the model.

![image](https://user-images.githubusercontent.com/61505882/129224923-43222506-9a7a-4299-a3c6-edce8396308d.png)

manifest.yml:- This file contains the instance configuration, app name, and build pack language.

![CementProc](https://user-images.githubusercontent.com/61505882/129226907-c3b31da6-7287-4e5a-b577-1cc86d209072.JPG)

Procfile :- It contains the entry point of the app.

![runtime](https://user-images.githubusercontent.com/61505882/129228524-6542f2d3-d14d-4655-ac16-e2edfde9150a.jpg)

runtime.txt:- It contains the Python version number.

                                                      




  
  

                                                             
 
