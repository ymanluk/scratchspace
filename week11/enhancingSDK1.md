# Cartographic enhancement for SDK

## Testing out class breaks 
Sample:
```
https://developers.arcgis.com/javascript/latest/visualization/data-driven-styles/class-breaks/
```

### Setting up the scene
- Adding API key
- Libraries and calling them (esriconfig, ClassBreaksRenderer)
- Relevant function (createSymbol) from the sample
- Making sure variable 'renderer' is defined and called 

![API key code](11_16.png "API key insert")
![createSymbol function](11_17.png "createSymbol function")

### Adjusting the input for renderer and optimizing class values
Since the crime statistics are in rates, population density is used and calculated by dividing population by SHAPE__AREA 
which is converted from square-meters to square-kilometers.

![API key code](11_18.png "API key insert")

### Output
Successful rendering of the class breaks.
```
https://ymanluk.github.io/scratchspace/week11/SDK_e1.html
```
![SDK rendered](11_20.png "SDK rendered")


### Further attempt to add a popup template triggered by clicking on a polygon (neighborhood)
Not working, possible reasons include the overlain graphic layer on the feature layer, to be investigated
![Failed popup template](11_19.png "Failed popup template")

## Next steps
- Adding legend items for population density
- Investigate why popup template is not working
