# Air-Pollution-Prediction
This projects use various data sources and structures to predict spatio-temporal pattern of air pollution in urban areas.


Throughout recent decades from 19's to present, although the urbanization enhanced the quality of life, it has brought about voluminous environmental issues through the world(Wang et al., 2020 ). Numerous studies have demonstrated a link between air pollution and death rates in various nations(Cohen et al., 2017 ; Huang et al., 2018 ). For efficient environmental management and the preservation of public health, accurate air pollution forecasting is crucial( Jelonek et al., 2020 ). Given the significance of reliable air pollution forecasting, this project endeavors to employ Multilayer Perceptron (MLP) and Radial Basis Function (RBF) neural networks as methods to predict air pollution levels in London.

**Study Area:**

The study area spans over a western part of London city. As far as the stations for meteorology data and stations for air pollution measurement are apart from each other, this area was the result of an overlap(clipping tool in ArcGIS) between the area covered by the meteorology stations and the area covered by the air pollution stations. 

**Dataset:**

The dataset used in this research includes different types of data including PM2.5 data downloaded from the website of the Department for Environment Food and Rural Affairs(DEFRA) and meteorology data requested from the Digital Library and Archive for Met Office. Regarding the temporal aspect, the data is for the period from January 2020 to December 2021 on a daily basis which due to it huge volume is converted to monthly mean.


**Preprocessing:**

After obtaining data, it has to be in the format eligible to import as stations in ArcGIS environment. To do this, the Pandas library in Python is used as a tool for preprocessing tabular data. Each station is represented in a distinctive row and the entire columns in a row are the station’s location and monthly air pollution(PM2_5.ipynb) or meteorology (Handling_meteorology_data.ipynb) data for that station. Moreover, There are some rows in dataset that include null values and these values can be deleted or imputed. In this research, the missing values are imputed using proper method(look at preprocessing in Spatiotemporal prediction of air quality based on LSTM neural network).

**Research methodology:**

After preprocessing, data is ready to be imported into the ArcGIS environment. After importing, on each group of data (meteorology data and PM2.5) an interpolation is used to create estimated data for the parts of the area without stations. To do this, Inverse Distance Weighted (IDW) interpolation is used. Then, the Clipping tool in ArcGIS is used to crop the overlap area between these layers. After obtaining the optimal area, the main road shape file is downloaded from https://www.data.gov.uk/dataset/95f58bfa-13d6-4657-9d6f-020589498cfd/ major-road-network and imported to ArcGIS and the Euclidean distance for each pixel to the main roads is calculated using the ArcGIS Euclidean Distance tool and saved in a raster file over the overlap area. All these raster data are then exported from ArcGIS to the notebook for running models. To illustrate more, over the area of interest, there are 24 raster files each for one month regarding each variable either independent variable or target/dependent variable. All these raster files are converted to the numpy arrays using the arcpy library and then preprocessed for feeding into neural networks.



**references:**

1. Cohen, A. J., Brauer , M., Burnett, R., Anderson, H. R., Frostad , J., Estep, K., Balakrishnan , K., Brunekreef , B., Dandona , L., Dandona , R., Feigin , V., Freedman, G., Hubbell, B., Jobling , A., Kan , H., Knibbs , L., Liu, Y., Martin, R., Morawska , L., . . . Forouzanfar , M. H. 2017 ). Estimates and 25 year trends of the global burden of disease attributable to ambient air pollution: an analysis of data from the Global Burden of Diseases Study 2015 . The Lancet, 389 10082 ), 1907-1918 . https://doi.org/ 10.1016 /S 0140 6736 17 30505 6
2. Huang, J., Pan, X., Guo , X., & Li, G. 2018 ). Health impact of China's Air Pollution Prevention and Control Action Plan: an analysis of national air quality
monitoring and mortality data. The Lancet Planetary Health, 2 7 ), e 313 e 323 https://doi.org/ 10.1016 /S 2542 5196 18 30141 4
3. Jelonek , Z., Drobniak , A., Mastalerz , M., & Jelonek , I. 2020 ). Environmental implications of the quality of charcoal briquettes and lump charcoal used for
grilling. Science of The Total Environment, 747 , 141267 https://doi.org/https:// doi.org/ 10.1016 /j. 2020.141267
4. Wang, S., Gao, S., Li, S., & Feng, K. ( 2020 ). Strategizing the relation between urbanization and air pollution: Empirical evidence from global countries. Journal
of Cleaner Production , 243 , 118615 . https://doi.org/https://doi.org/ 10.1016 /j. 2019.118615
