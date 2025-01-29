War Predictor
*************         
   ******
War Predictor user guide 
***********************
PYTHON VERSION:Python 3.13.0
open the file war_Predictor_2.py in its directory , and write function : War_Predictor_2(year,country1,country2), where in which 
you are interested to know how many predicted years are left before the possible war, and country1/country2 should be two countries
based on their world bank names, provided the data for some economic varaibles are avaliable in interested year, the model will provide prediction
else it will tell you that there is no sufficient data. HOWEVER! please try to predict wars that make sense based on geopolitical/politicla logic, since this is pure numeric statistical model , and does not take into consideration non-numeric information (whether countries have border, or any reason of war).




What is War Predictor?
*********************
War Predictor is a statistical model that uses economic and demographic variables like age dependency ratio, % of population female,
GDP per capita growth etc, to see howt this variables are related to closeness of war. In essence, War Predictor is based on the
Econometric analysis of data frame that for given country has variable "years before the war" (how many years before the war was there for country at given time)
and many economic variables over some years. Then "years before the war" is regressed on all other economic varaibles and as result
we see how different variables are related to closeness of war, then based on ols coefficients, the prediction model is built , that for a country takes a
statistics (similar to one in OLS), and then multiplies statistics on coefficients to get prediction value. To predict war between two countries, for both countries
the war is predicted and statistical mean is found. 





How War Predictor Proccesses data To Predict Wars (CODE EXPLAINED):
**********************************
War Predictor starts with csv_of_wars.txt data, which contains info about combatants,and year
of big interstate wars from last 60 years.Based on Csv of wars combatants, we download world bank data
aboud combatants (in format of row indexes corresponding to different variables and columns to years)
and store them in "big data".in "SHAVING OFF EXTRA DATA" section we use python and pandas
manipulation to forge from raw data, data with disrable years and variables, first round of filtering stores
data in filtered data.

Second round of data cleaning, namd "NA",data frames are transposed and Na cleaned through interpolate.
Along the way Na statistics are recorded. Second round of filtering puts Na cleaned data in "Formated and Na filtered"
folder.

Third stage "Final filtering and joining of datas" sees the creation of the data frames for each conflicts 
in "csv_of_wars.txt" by this rule: for each conflict, two
csvs are created ,one for each participant, and in both cases there is new column added "years before the war", which to each row assigns
years before the conflict. This data is stored in the folder called "war data frames" , and each df is named by name of the conflicts in which 
countr that this df is about participated, and from years when this war happened (thus there is two version for each conflict).
Finally all data frames are unified into one along the rows (since columns are identical) it is stored in "unified dataframe for ols"
, and for good econometric analysis, all remaining Na's that survived interpolation in above statge are removed. Final df is stored in "FINAL NA FREE"


Fourth stage "OLS MODEL AND WAR PREDICTOR FUNCTION" creates an OLS regression, regressing "years before the war" on all other
variables thus seeing how change in different variables changes closeness of war for given country the results are stored
in the OLS_resuts.txt. The backbone of War Predictor is created, by writting down beta coefficients of the regression, 
and making funciton
that takes some values of variables that were independent variables in OLS regression, and multiplies them by coefficient beta values
and prints out prediction. War Predictor takes folder where country csv (in a format which is just for single year, and regressed variables)
and two country names and calculates their "Years before the War" average.
"2023 data" is created to make a data ready to be plugged into War Predictor, first file in the "2023 data" is WDCISV.csv file that is massive
world bank data for all countries , all regions and all variables avaliable over 1960-2023 years. Function  data_of_2023(): only takes 2023 portion, and only for variables
used in OLS model. THen many_2023_datas() creates small data frame for 2023, and only for OLS variables for each country. This files also end up in dat_of_2023().


Stage Five: 'Making massive prediction data". Is section where we make it super easy to use War PRedictor for any year and any country in UN dataframe provided that data does exist/
From "data of 2023" again takes massive "WDCISV.csv" file and creates data frame containing information about OLS variables, for
all years for all countries, and stores them in "data for predictions" file.In "data for prediction" for each year there is separate file which contains data frame of countries 
during that year. This whole data manipulation takes around 30 minutes by computer, and is advised not to be run again. 

stage six: War_Predictor_2(year,country1,country2) is a final function that utilizes data structure created above to for all years and all UN defined countries 
predict a years before the war. Last function in block test_the_model(conflicts_csv) tests the validity of model based on data, and since we found that model
under rpedicted (predicted war to happen later than it actually did) , we added -3.7 to the model in fourth stage.

Stage seven: build scatterplots and regression lines based on the data used for OLS regression to visualize how years before the war and the variables are related.
Build GUI for the model so that user can simply choose coutnry from scroll down list, year and ask for prediction




Data Journay                     File: "big data"---------------------->>"filtered data"----------------->>"Formated and Na Filtered"----------------------
********************************* 
                                 Data:  row un data per country           filtered data per country        Transposed data interpolated-NA-removal            

           
                                 File:->>"war data frames"------------->>"unified dataframe for ols------>>"FINAL NA FREE"
            
                                 Data:    selected years based on war     united war data frames based      Unified df cleaned of all NA
                                          plus "years before the war"           on row





Date Journey2                   File:"2023 data"------------->"2023 data"------------------------->"data for prediction"
********************************
                                Data:WDICSV.csv               2023 csv, 2023 csv per country       per year, data frame for all countries in given year
                                                                containing only OLS vars                     containing only ols vars



File meaning
*****************
*****************
All_COuntries_OF_The_world.txt:   from large databse of world bank there is written down all country names avaliable
csv_of_wars.txt:                  data frame/csv that contains interstate wars in last 60 years , participants and year of start
handy_picked_variables.txt:       it is handy picked variables from the many that were chosen by computer in "unfiltered_matching_variables.txt"
Na_statistics_final.txt:          Na Statistics after removing extra vars ,and before removing all Na columns in unified data
Na_statistics_postscriptum.txt:   Na statistics after interpolation
Na_statistics.txt:                Na statistics in the unified data frame before any change
OLS_results.txt:                  self explanatory, OLS coefficients,sds and other statistics from regressing years_before_the_war on other variables
Prediction_accuracy_of_War_Predictor.csv:      How accurately were conflicts in csv_of_wars.csv predicted
requierements.txt:                requiered libraries and their version to run this code
steps to building project.txt:    detailed explanation how project was made
unfiltered_matching_variables.txt: variables matched by keyword search in all vars in section 1
war_Predictor_OLD_VERSION.py:     first version of predictor 
war_Predictor_2.py:               war Predictor code
what_data_I_have_downloaded.txt:  detailed guide of what I downloaded from internet
what_data_to_look_for.txt:        this is reflection in beggining what data I needed when i first started model
world.png:                        background for GUI
images:                           file that stores graph
