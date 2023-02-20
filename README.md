# 4square

First I went through the companies database and found all the other gaming offices because these are likely to be suitable for our gaming company

Secondly I found the top 3 cities (based on number of offices)

Then I created a dataframe where I kept just offices in the top 3 cities: New York, San Francisco and Los Angeles

Next I got the category  for all the venues that I wanted to optimise for: International Airport, Train station, 
Nightclub, Pet grooming, Vegan restaurant, Basketball stadium, Design studio, Daycare, Preschool and High school.

I then created a function which used the FourSquare API to pull the Name and Distance of the closest venue to each office for each of the categories. 

I created a dataframe which conatained the offices, their cooardinates and teh results from the API call for all the categories that I was looking for, the names of the closest venue and the distance from the office. 

To avoid pulling from Foursquare every time that I restarted the kernel, I saved this dataframe to a CSV file.

I then created a new notebook to build my model for choosing the office and loaded this CSV file. 

I created a new column called Points. I award 10 points to an office if it had the nearest eg Nightclub and 9 points if it had the second nearest etc. If it was lower than 10th in terms of proximity rank it received 0 points (and if the distance value was NaN because eg it did not have a nightclub in the chosen proximity, it also receievd 0 points)

I created a new column called Multiplier. This multiplier was to weight the score based on how many people in the office it affected. If it was important for everyone in the office then it received a multiplier of 1. If it affected half of the people in the office, it received a multiplier of 0.5. The higher the proportion of people in the office that it affected, the higher the multiplier. For example, everyone in the office like to go out, so Nightclub received a multiplier of 1. While only 1 person wanted a vegan restaurant, so it received a multiplier of 0.2

I then created a column called Weighted Score which was the product of the product of the Points column multiplied by the Multiplier value for that column (Eg International Airport: Points * International Airport: Multiplier = International Airport: Weighted Score)

I then created a column called Final score which was the sum of all the weighted scores for each office. 

Finally, to choose the office for my company, I selected the office which had the highest Final Score and printed its name as well as the details for that office. 

The office that i have chosen for my company is MindSmack!