                                                       Cement Strength Prediction
                                                       
  Project Link:- https://cementstrengthpred.herokuapp.com/
   
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




  
  

                                                             
 
