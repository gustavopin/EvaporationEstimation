# The Project
This project involves the calculation of the estimation of the evaporation of water bodies in the city of Campo Verde, Mato Grosso, Brazil.

It is divided in two phases:
 - First we will take a look in a more Analytic environment with a descriptive and exploratory analysis.
 - Second Phase involves the calculation and interpretation of the Machine Leaning Model.
 
## The Data
 - Tmax: Maximum temperature of the day (°C)
 - Tmin: Minimum temperature of the day (°C)
 - RHmax: Maximum relative air umidity (%)
 - RHmin: Minimum relative air umidity (%)
 - Radiation: Sun radiation measured in mJ/m².day
 - Pressure: Atmospheric pressure
 - Tdew : Temperature of the dew point (°C)
 - Wind Speed: in m/s
 - Wind Gust: in m/s
 - Evaporation: measure in mm³/day
 - Evaporation (Original): os equal to the previous evaporation and renamed to be different of the next one.
 - Evaporation (ML): this is the evaporation calculated by the machine leaning model.
 
## Phase One
Stating with a distribution. In the histogram grid below we can see how the distribution the the variables work within the data:

![Distribution](Images/distribution.png 'Distribution')

 - Windspeed and Windgust have a relatively equal distribution
 - There are more data in January and December
 - Most of the radiation is around 20000 mJ/m.day
 - RH max (maximum relative umidity) have more counts between 80 and 100
 - for the minimum, most of the data is between 40 and 60, with low quantities in the high measures (80+)
 - Maximum temperature stands around the 30°C, while the minimum is around 20°C
 
For a research purpose, we could use the average data by each month to know how the climate works in the region:

![Data By Month](Images/data_by_month.png 'Data By Month')

Here we can see how August, September and October have a hotter and more dry climate (represented by the columns Tmax/Tmin and RHmax/RHmin respectively), representing the months of drought.

I'll show the correlation matrix here for a first visualization of the interaction between the data, but I'll show a more complete one using dispersions, distributions and the correlation coefficient later in this project:

![Correlation Matrix](Images/corr_matrix.png 'Correlation Matrix')

 - Looking at the matrix we can already see how the correlation between the variables are high.
 - Wind Speed and Wind Gust are exceptions here, as they probably don't have any correlation with the variables.

This high correlation is import to choose our model for the Machine Learning.
 - The variables shown are all continuous (numeric)
 - The interaction between variables are high.
 - This indicates that we can use a Linear model, instead of the logistic one.

Below we have a more complex and complete grid of graphs:
 - The Top Half Triangule shows the correlation coefficient.
 - The Diagonal shows the distribution.
 - The Bottom Half Triangule shows the dispersion graphs with trend lines.
 
![First Grid](Images/super_matrix.png 'First Grid')

In the upper half triangule we have the correlation coefficient of the variables, here we can see that the correlation between some of the variables are really high, like the interaction between Temperatue and (Tmax/Tmin) and relative air umidity (RHmax/RHmin).
 - This high correlation is simple: the higher the temperature, less umidity in the air.
 - But we can see that Temperature and Evaparation are also highly correlatable. This being due to the high evaporation levels the higher the temperature is.
 - Radiation is also a high correlation with temperature, as it is one of the sources of heat.
 - One of the highest correlation is shown between Tdew (temperature in which dew is formed) and RHmax (the maximum air umidity measured by the station), being 0.865, showing that both are basicaly linked to one another: The higher the the umidity is within the air, the more dew is formed.

The middle part of this grid is shown as a distribution:
 - The interaction between the variable and itself createas a distribution of their values.
 - It is represented by a black curve with grey area.
 
The bottom half of the triangule of the grid are the dispersion graphs:
 - This shows the interaction between 2 different variables and how they behave.
     - We can see that some variables have a bigger tendency, emphasizing their correlation, for examples, looking at the dispersion graph generated between Radiation and Evaporation, their dispersion is concentrated within the tendency lines and their coefficient is 0.88.
     - Some dispersions are not that related and their graphs are more scattered.
 - The trend line is shown as a red line and indicates the behavior of the variable's interaction.
 
## Phase Two
Here we develop the machine learning model.

As explained before, I chose to use the Linear Regression because the variables are all numeric and they have high correlation.

To calculate the values of evaporation the data was divided 25/75, being 25% for the test and 75% for the training.

The 'Evaporarion' column was removed from the test dataset and it was added after all the calculation so we could compared the original evaporation and the calculated one.

The error between the original and calculaterd version were calculated and added in a column at the and of the dataset, as shown by the table below:

![Calculated Evap and Error](Images/calculated_evap_error.png 'Calculated Evap and Error')

A boxplot was generated to visualize how the distribution of the errors worked within the data:

![Error Boxplot](Images/error_boxplot.png, 'Error Boxplot')

In general, the linear regression that was used here had most of it's measures with less than 10% difference from the original values.

This can indicate that the code was able to estimate the evaporation of the region with a good accuracy.

It would be necessary to have a deeper search within pappers to see if the calculated error was acceptable for academic and research purposes, but for this project it is a good measure.

The next grid is the same of the first one, but it now includes the calculated evaporation:

![Grid With Calculated Evap](Images/super_matrix_mod.png 'Grid with calculated evap')

We can see that the correlation between the calculated evaporation and the original one is extremely high but it is not 1, indicating the errors that were shown before.

Using the original Evaporation we can compare all of its coeffiecnts with the calculated evaporation coefficients, showing that our code have a good result be cause both coefficients are almost equal to one another.