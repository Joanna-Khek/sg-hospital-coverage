# Are there sufficient hospitals in Singapore?

## Project Description
As part of my final project for module [CS5228](https://nusmods.com/modules/CS5228/knowledge-discovery-and-data-mining) at NUS, we were given three tasks to complete. 
- **Task 1:**  Prediction of Property Resale Prices - given the information about a property, predict the price.
- **Task 2:** Property Recommendation - given the information about a property a user is interested in,  find "meaningful" alternatives that can be shown to the users in the form of recommendations
- **Task 3:** Open Task - given the provided property dataset, explore your own ideas ato gain interesting insights into the data.

For task 3, I chose to analyse the hospital coverage in Singapore. One of the key amenity for a neighbourhood is a hospital. For a household with elderly or whose family members have chronic conditions, staying near a hospital would translate into less travelling time or even a matter of life or death in a critical situation. 

Since the project involves working with geospatial data, the ``GeoPandas`` package for python was used. From the official [GeoPandas](https://geopandas.org/en/stable/index.html) documentation, GeoPandas extends the datatypes used by pandas to allow spatial operations on geometric types. Geometric operations are performed by shapely.

## Getting the data
There is no existing hospital data directly available so I had to first scrape my own data. The web scraping script can be found in ``scrape.py``. The data is obtained from [Healthhub Singapore](https://www.healthhub.sg/directory/hospitals). Only the names of the hospital were collected. The coordinates of the hospitals were obtained from [OneMap RestAPI](https://www.onemap.gov.sg/docs/#onemap-rest-apis)

![healthhub](https://github.com/Joanna-Khek/sg-hospital-coverage/blob/main/images/healthhub.png)

Here is an example of the scraped information
| Name | Latitude | Longitude |
| ------------- | :-------------: | :----------:|
| ALEXANDRA HOSPITAL | 1.28812220833697 |	103.799444839251|
| ANG MO KIO - THYE HUA KWAN HOSPITAL | 1.38403248432085	| 103.840356912671 |
| BRIGHT VISION HOSPITAL | 1.37203701009478	| 103.878031146933 |
| CHANGI GENERAL HOSPITALL | 1.34131853771386 | 103.948193352903 |
| COMPLEX MEDICAL CENTRE | 1.35817565889842 |	103.973191628726 |

## Results
After experimenting with different coverage radius, I eventually settled with looking at 3km as the radius is not overly large or small. 
In the image below, black pins represent the hospitals and the orange radius represents 3km buffer radius. 

![task3_hospital_coverage](https://user-images.githubusercontent.com/53141849/206888565-dc697e8d-0e2a-43c4-bc0e-4f52bf5539e7.png)

After looking into the coverage of each planning area, 15.53% of the the listings are not within 3km of any hospitals. Further breaking down into the individual planning area, we see that Woodlands and Bukit Panjang have 0% hospital coverage. Flat buyers should avoid these areas if hospital care is a concern for them.

![df_no_hosp_planning_area](https://user-images.githubusercontent.com/53141849/206888689-6af976df-56d7-40b9-a568-80466c178820.png)

## Conclusion
This analysis only considered hospitals in Singapore. There are other healthcare groups in Singapore such as the National Healthcare Group, National University Polyclinics as well as Singhealth Polyclinics in Singapore which we did not take into account. We only focused on hospitals as they are better able to handle complex conditions and would have a wider range of medication for different patient types. If a flat buyer does not require specialised treatments, then not having enough hospital coverage might not be an issue for them. For example, although Woodlands is not within 3km of any hospitals, they do have a polyclinic within the planning area itself. For future improvement, we could also include other healthcare groups to make our analysis more thorough.
