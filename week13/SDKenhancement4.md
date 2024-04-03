# SDK enhancement 4

## Story so far
- Successfully got SDK working
- SDK enhancement 1: introducing class breaks
- SDK enhancement 2: introducing customizable class breaks, UI optimization
- SDK enhancement 3: UI/UX optimization

## SDK enhancement 4
Building upon previous enhancements, the current enhancement explores data enrichment, more functional widgets, and alternative designs.


## Data enrichment

### Rationale
The idea to enrich the data for the chart comes from the current theme mismatch between the chart function and the class breaks function: the former only shows three but the latter shows seven types of crime. As a result, attempt is made to include the same seven types of crime while reducing the number of years from five to three (to avoid visual cluster)

### Steps
The steps are quite similar to the initial work involved to get the SDK running: changing the data input for the chart

Changing the 'statDefinitions' in terms of theme and year
    
    ```javascript
          let statDefinitions = [];
          let time = 2021;
          while (time <= 2023) {
            statDefinitions.push(createPopupStats("HOMICIDE", time));
            time += 1;
          }

          time = 2021;
          while (time <= 2023) {
            statDefinitions.push(createPopupStats("SHOOTING", time));
            time += 1; 
          }

          time = 2021;
          while (time <= 2023) {
            statDefinitions.push(createPopupStats("THEFTOVER", time));
            time += 1; 
          }

          time = 2021;
          while (time <= 2023) {
            statDefinitions.push(createPopupStats("ROBBERY", time));
            time += 1; 
          }

          time = 2021;
          while (time <= 2023) {
            statDefinitions.push(createPopupStats("BREAKENTER", time));
            time += 1; 
          }

          time = 2021;
          while (time <= 2023) {
            statDefinitions.push(createPopupStats("AUTOTHEFT", time));
            time += 1; 
          }

          time = 2021;
          while (time <= 2023) {
            statDefinitions.push(createPopupStats("ASSAULT", time));
            time += 1; 
          }
    ```

Add data storage for new crime types
    
    ```javascript
          async function queryLayerViewAgeStats(buffer) {
            // Data storage for the chart
            let homiData = [], 
            shootData = [],
            theftData = [],
            robberyData = [],
            breakData = [],
            autotheftData = [],
            assaultData = [];
          }
    ```

Change chart labels

Push data for different crimes
    
    ```javascript
            // Statistics query returns a feature with 'stats' as attributes
            const attributes = results.features[0].attributes;
            // Loop through attributes and save the values for use in the chart.
            for (let key in attributes) {
              if (key.includes("HOMI")) {
                homiData.push(attributes[key]);
              } else if (key.includes("SHOOT")) {
                shootData.push(attributes[key]);
              } else if (key.includes("THEFTO")) {
                theftData.push(attributes[key]);
              } else if (key.includes("ROBB")) {
                robberyData.push(attributes[key]);
              } else if (key.includes("BREAK")) {
                breakData.push(attributes[key]);
              } else if (key.includes("AUTOT")) {
                autotheftData.push(attributes[key]);
              } else if (key.includes("ASS")) {
                assaultData.push(attributes[key]);
              } 
            }
            // Return information, seperated by crime type
            return [homiData, shootData, theftData, robberyData, autotheftData, breakData, assaultData];
    ```

Output data for chart
    
    ```javascript
        function updateChart(newData) {
            const homiData = newData[0];
            const shootData = newData[1];
            const theftData = newData[2];
            const robberyData = newData[3];
            const breakData = newData[4];
            const autotheftData = newData[5];
            const assaultData = newData[6];
        }
    ```
    
    ```javascript
            datasets: [
                    {
                      label: "Homicide",
                      backgroundColor: "red",
                      borderColor: "#004C99",
                      borderWidth: 0.25,
                      data: homiData
                    },{
                      label: "Shooting",
                      backgroundColor: "orange",
                      borderColor: "#7F00FF",
                      borderWidth: 0.25,
                      data: shootData
                    },
                    {
                      label: "Theft Over $5,000",
                      backgroundColor: "yellow",
                      borderColor: "#FF0000",
                      borderWidth: 0.25,
                      data: theftData
                    },
                    {
                      label: "Robbery",
                      backgroundColor: "green",
                      borderColor: "#FF0000",
                      borderWidth: 0.25,
                      data: robberyData
                    },                  
                    {
                      label: "Break and Enter",
                      backgroundColor: "blue",
                      borderColor: "#FF0000",
                      borderWidth: 0.25,
                      data: breakData
                    },
                    {
                      label: "Auto Theft",
                      backgroundColor: "purple",
                      borderColor: "#FF0000",
                      borderWidth: 0.25,
                      data: autotheftData
                    },
                    {
                      label: "Assault",
                      backgroundColor: "brown",
                      borderColor: "#65350F",
                      borderWidth: 0.25,
                      data: assaultData
                    },
                  ]
    ```

#### Intermediate output
Not ideal: very wide data ranges i.e. homicides not showing up well
```
https://ymanluk.github.io/scratchspace/week13/SDK_e4_data.html
```
![image](https://github.com/ymanluk/scratchspace/assets/146376058/12c20599-6737-498e-84ac-c6e9ca294846)
Also adjusted bar width to prevent overlap of bars

> [!TIPS]
> Change the following line to change the order of crimes in the chart

       ```javascript
        return [homiData, shootData, theftData, robberyData, autotheftData, breakData, assaultData];
          }
        ```

### Evaluation for Data Enrichment
Given the visual cluster and data range issue, it is not ideal to cramp everything in one chart. Making two charts might work but it is not the best solution.

### Next steps
Give up on this objective, turn to the UI: attempt to add more useful widgets instead of showing more data.


## Adding widgets
A very straightforward process, where fullscreen button, home button, and compass widgets are added to the SDK.

### Steps
Load the required libraries for the widgets.
  
    ```javascript
      require([
        "esri/config",
        "esri/widgets/Sketch/SketchViewModel",
        "esri/geometry/Polyline",
        "esri/geometry/Point",
        "esri/Graphic",
        "esri/Map",
        "esri/views/MapView",
        "esri/layers/FeatureLayer",
        "esri/layers/GraphicsLayer",
        "esri/geometry/geometryEngineAsync",
        "esri/widgets/Expand",
        "esri/widgets/Legend",
        "esri/widgets/Search",
        "esri/core/reactiveUtils",
        "esri/core/promiseUtils",
        "esri/widgets/BasemapToggle",
        "esri/smartMapping/renderers/color",
        "esri/smartMapping/statistics/histogram",
        "esri/widgets/smartMapping/ClassedColorSlider",
        //Enhancement 4: Fullscreen, home button, and compass
        "esri/widgets/Fullscreen",
        "esri/widgets/Home",
        "esri/widgets/Compass"
      ], (
        esriConfig,
        SketchViewModel,
        Polyline,
        Point,
        Graphic,
        Map,
        MapView,
        FeatureLayer,
        GraphicsLayer,
        geometryEngineAsync,
        Expand,
        Legend,
        Search,
        reactiveUtils,
        promiseUtils,
        BasemapToggle,
        colorRendererCreator,
        histogram,
        CLassedColorSlider,
        Fullscreen,
        Home,
        Compass
      )
    ```

Add the widget and decide on the placement

    ```javascript
              // enhancement 4: Fullscreen, home button, and compass
              fullscreen = new Fullscreen({
                view: view
              });

              let homeWidget = new Home({
                view: view
              });

              let compass = new Compass({
                view: view
              });

              // Add our components to the UI
              view.ui.add(homeWidget, "bottom-leading");
              view.ui.add(chartExpand, "bottom-leading");
              view.ui.add(search, "top-right");
              view.ui.add(legendExpand, "bottom-right");
              view.ui.add(crimeExpand, "top-trailing");
              view.ui.add(fullscreen, "top-leading");
              view.ui.add(compass, "top-leading")
            });
    ```

### Output
Successful. The home button can be used to return to the initial extent; the compass shows the direction and allow orientation back to north since panning while right clicking can change map orientation.
```
https://ymanluk.github.io/scratchspace/week13/SDK_e4_widgets.html
```
![13_02](https://github.com/ymanluk/scratchspace/assets/146376058/13615d95-c7a8-4d82-a92b-7ba425322ebf)

### Next steps
Look into an information widget which may be beneficial to the presentation of the SDK.

#### Rationale
Came across the below widget when researching on useful widgets to add. Since the current SDK solution offers quite some functionalities, it would be nice to include an info pop-up to help reader navigate the map.
![13_03](https://github.com/ymanluk/scratchspace/assets/146376058/fc36e35e-0a01-4293-9cc2-6987385b35d0)

#### Problem encountered
The original expectation for implementing the info widget is very easy given previous successful attempts. However, I have 
failed to find any related documentation apart from popup which is basically for clicking on features on a map. Moreover, examining 
the example using the console/inspector function shows the popup is not straightforward to replicate after all:
![13_04](https://github.com/ymanluk/scratchspace/assets/146376058/97173a8e-3b67-4350-bdfc-f6ce78d05633)
![13_05](https://github.com/ymanluk/scratchspace/assets/146376058/84e9771f-8ae5-4a49-84af-fea9cd9e2cd9)

At last, it seems to be quite time-consuming to replicate and therefore not going to delve further into it.

### Next steps
The above discovery in turn sheds light on the Calcite Design System. Might be interesting to incorporate into the current project.
![13_06](https://github.com/ymanluk/scratchspace/assets/146376058/ef8c938c-a49d-4805-9460-44999735390a)
![13_07](https://github.com/ymanluk/scratchspace/assets/146376058/2d2c9254-194a-4a2a-ab1b-ca145e8ed9fa)
![13_08](https://github.com/ymanluk/scratchspace/assets/146376058/e71facf2-a8c2-4b0c-aea7-f9de7d3f6a14)
```
https://developers.arcgis.com/calcite-design-system/tutorials/create-a-mapping-app/
```

## Alternative design: Calcite Design System
Also failed to get to work due to numerous errors, will take too much time to configure.

### Examples of error
![13_09](https://github.com/ymanluk/scratchspace/assets/146376058/f38bef35-7009-4c6b-aa74-234926438c8d)
Solution: remove duplicate calling of the libraries
![13_10](https://github.com/ymanluk/scratchspace/assets/146376058/60986818-5c09-4ab2-91ca-9e27016af617)
Solution: very careful re-organization of the codes

The document showing the failed attempt:
```
https://ymanluk.github.io/scratchspace/week13/SDK_e4_calcite.html
```










