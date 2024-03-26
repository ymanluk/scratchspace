# Objective 
Building upon the second SDK enhancement for class breaks selection, perform general enhancement/optimization 
on the SDK, particularly the UI.


# Method
Start by evaluating alternative chart formats to existing bar charts, then setting up icons to access functionalities,
troubleshooting in the process. 


# Results
Largely successful.
```
https://ymanluk.github.io/scratchspace/week12/SDK_e3.html
```

# Major steps
0) Explore Alternative Chart Formats
1) Setting up icons to access functionalities
2) Results



## 0) Explore Alternative Chart Formats

### Rationale
Find the bar chart a bit difficult to navigate while observing a line chart which might be decent to show trend
in the external library documentation.
![Line Chart](12_12.png "Line Chart")
### Line Chart attempt
Step: As simple as changing the expandIcon property.
![Line Chart change](12_13.png "Line Chart change")
Outcome: not looking good; problem with data input; more importantly problem with different crime rate data ranges.
![Line Chart problems](12_14.png "Line Chart problems")
Next steps: try out another chart format
### RADAR chart attempt
Step: same as above
![RADAR chart](12_15.png "RADAR chart")\
Outcome: Also not looking good; same problem with data input; ultimately not appropriate to show trend but a snapshot.\
Next steps: Just keep the existing bar charts, they look fine now


## 1) Modification/Combination of the code
This section outlines the major issues encountered and respective solutions in combining the codes together.

### Rationale
Whilst working on the charts, noticed that the tiny icon (on the bottom left of the image below)
 for the chart is useful and aesthetic, should be used systematically across other functionalities 
![Icon on bottom left](12_16.png "Icon on bottom left")

### General workflow
- Set up the view ui icon
- Set up the expand variable (crimeExpand)
- Add to UI display
- Set the infoDiv to expand when clicking the icon

### Troubleshooting
This section documents the troubleshooting pattern of how one fix shows another issue and another fix.
#### Text display in layer selection
It started well with the clickable icon of layer selection. 
![Layer icon added](12_17.png "Layer icon added")
Yet the display is not that good. Particularly the placement of the breaks in the same line as the choice for classification.
![Breaks placement](12_18.png "Breaks placement")
Optimized the breaks placement by simply making it a div.
![Fixed layer selection](12_19.png "Fixed layer selection")
#### Placement of Manual class breaks chart
When manual classification is selected, the selection box is covered.
![Selection box covered](12_20.png "Selection box covered")
Trying out alernative positions for chart placement but not getting good results.
![Poor bar placement](12_21.png "Poor bar placement")
Trying out stacking the selection box in a single row to make space for the chart: seems feasible.
![Selection box on one line](12_22.png "Selection box on one line")
Then the next step will just be moving the chart back to top right following the selection box/icon.

#### Minor issue: infoDiv showing up when the page initializes 
When the page initializes, the infoDiv shows up momentarily, somewhat affecting user experience.


https://github.com/ymanluk/scratchspace/assets/146376058/044f9f4f-1a53-4251-a677-0ecc4a198a4f


Tried hiding and then display infoDiv but no use.
![No use hiding infoDiv](12_23.png "No use hiding infoDiv")
After some research, tried window.onload but also not working, while not wanting to use jQuery.
![windodw onload code 1](12_24.png "windodw onload code 1")
![windodw onload code 2](12_25.png "windodw onload code 2")
At last, all the problem-solving is just commenting out the view ui since the infoDiv is called upon already when selecting manual classification.
![comment out view ui](12_25.png "comment out view ui")


## 2) Results
Looks tidy and works smoothly now!
![SDK enhancement 3](12_26.png "SDK enhancement 3")
https://github.com/ymanluk/scratchspace/assets/146376058/38c070b7-28a9-4925-96bb-9fd757dffb8c


# Next steps
Continue to enhance the SDK. Perhaps adding more crime data that correspond to the layer selection.








