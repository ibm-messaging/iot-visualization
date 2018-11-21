IOT Visualization:
==================

[![Deploy to IBM Cloud](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/nabeelvalley/rickshaw4iot)

 Please refer to the [recipe] for running the application.

 This is a stand alone web app written on top of [node.js] to visualize IOT data.Additionally it uses the following frameworks.



 [express] :  Server side routing

 [JQuery] :  UI and REST calls

 [Rickshaw]  : Visualisation of data

 [MQTT paho client] : Subscribing to the IBM Internet of Things(IOT) Cloud 
using mqtt protocol and receiving messages from registered devices from 
IBM IOT Cloud.

### Visualization in the application: 


 This page uses the  [Rickshaw] charting library to visualize real time and historical data.


#### Historical data: 

   The components for the historical data visualization are placed in the files historian.js and historianGraph.js in this folder.

        iot-visualization\public\js\historian\
    
        \historian.js
    
        \historianGraph.js


 

 *historianGraph.js*: This file contains the graph and it's related function.



 *Change the color of the graph*: In the below section of code you can change the hexadecimal codes to change the color of the graph data.
    
        this.palette = new Rickshaw.Color.Palette( { scheme: [
          "#7f1c7d",
          "#00b2ef",
          "#00649d",
          "#00a6a0",
          "#ee3e96"
          ] } );


 The function drawGraph(seriesData) is called from historian.js when we receive device data from IBM IOT Cloud.It instantiates the graph for the first time and set te renderer , hover details , x-axis and y-axis formatting.

        this.drawGraph = function(seriesData) 


 This instantiates the graph and set the intial renderer to line.

        this.graph = new Rickshaw.Graph( {
            element: document.getElementById("chart"),
          width: 900,
          height: 500,
          renderer: 'line',
          stroke: true,
          preserve: true,
          series: seriesData  
        } );



 This defines the time fixture(e.g. year, month, day, hour) and the formatting of each) for the x-axis. 

        this.xAxis = new Rickshaw.Graph.Axis.Time( {
          graph: this.graph,
          ticksTreatment: this.ticksTreatment,
          timeFixture: new Rickshaw.Fixtures.Time.Local()
        } );



 This defines the number formatting for y axis.

    this.yAxis = new Rickshaw.Graph.Axis.Y( {
      graph: this.graph,
      tickFormat: Rickshaw.Fixtures.Number.formatKMBT,
      ticksTreatment: this.ticksTreatment
    } );



 This function gets called from historian.js and create the array which is used to plot the graph.

        this.displayHistChart = function(device,data)


 *historian.js* : This file intializes the graph and makes REST API calls to get the historian data. 



        this.initialize = function() {
        historianGraph = new HistorianGraph();
      }


 The function  this.plotHistoricGraph handles the ui control selections and 
make the REST call to get the historical data

        this.plotHistoricGraph 


#### Realtime data: 

   The components for the realtime data visualization are placed in the files realtime.js and realtimeGraph.js in this folder.

        iot-visualization\public\js\realtime\
    
        \realtime.js
    
        \realtimeGraph.js


 

 *realtimeGraph.js*: This file contains the graph and it's related functions.This is written in the same style as historianGraph.js above.So you can follow the guidelines for historianGraph.js to customize the code.



 *realtime.js* : This file intializes the graph and subscribes to the mqtt topics to get realtime device data from IBM IOT cloud.


 You can download the iot-visualization project zip and use the above guidelines to customize the graphs to change the visualization.

[node.js]:http://nodejs.org
[jQuery]:http://jquery.com
[express]:http://expressjs.com
[Rickshaw]:http://code.shutterstock.com/rickshaw/
[MQTT paho client]:http://www.eclipse.org/paho/clients/js/
[recipe]:https://developer.ibm.com/recipes/tutorials/visualizing-your-data/
