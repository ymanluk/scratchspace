# Objective 
Getting the below ArcGIS SDK JavaScript sample to work with selected data from group project. (Too stubborn to give up)

```
[https://maps.googleapis.com/maps/api/directions/json?origin=Disneyland&destination=Universal+Studios+Hollywood&key=YOUR_API_KEY](https://developers.arcgis.com/javascript/latest/sample-code/layers-scenelayerview-query-stats/)https://developers.arcgis.com/javascript/latest/sample-code/layers-scenelayerview-query-stats/
```

# Results
Building on experience obtained from failures in the previous week, finally able to get it to work with major steps detailed in the following.

# Major steps
Basic configurations --> Change query data (statdefinitions) --> Change information returned --> Change chart output

## 0) Basic configurations
Building on the basis of the last attempt (sample_test2.html) and the sample code, with major changes being the loading of the targeted feature layer (by url or id), the zoom, the center, and constraints of scale.

## 1) Change query data (statdefinitions)
This section outlines the inspiration leading to the solution and actual steps employed.

### Inspiration 
Going through the original sample, the part of the code responsible for extracting the statistical fields from the data is identified, further cross-checked by the field names in the original sample from the rest endpoint URL and the use of the code in conducting the client-side spatial query.
![Pic 1](11_1.png "Pic 1")



### Actual steps
