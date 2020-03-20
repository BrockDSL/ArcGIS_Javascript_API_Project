![DSL Logo][dsllogo]




### Introduction 

ArcGIS is a platform that allows organizations and Individuals to create, manage, and analyze spatial data. It contains desktop and mobile applications, server components and a wide variety of developer tools. The platform can be deployed on the cloud or through their own hosted option ArcGIS Online.This tuturial is about the ArcGIS API for JavaScript which is a lightweight option to embed maps and ArcGIS features.It also allows one to embed their own or others hosted ArcGIS maps.

The tutorial will walk you through Implementing the following features:

  1. Embedding a simple 2D or 3D map of Brock University
  2. Learning how to add widgets by creating a basemap selector to change the map theme
  3. Create a widget that allows the user to add graphics to the map like circles and polygons
  4. Connect an ArcGIS account to implement route mapping 
  5. Embed your own or others hosted ArcGIS map
  
### Setup

First were are going to setup a virtual enviroment that will display and update the web application with every change

  1 . Navigate to https://codepen.io/ and **Sign up** for a free account

  >**Note**: You can sign up with facebook, Email, or even Github to easily have your code written in CodePen be merged to a repository.

  ![][Logo1]
  
  2 . Once Logged in create a new **Pen(document)** by navigating to the **Top left** and clicking Pen

  >**Note**: CodePen offers the ability to also create Projects, Posts, and Collects that all can be added to a Personal Dashboard

  ![][Logo2]
  
  3 . CodePen gives the ability to write HTML, CSS, and JavaScript all on the same page. All output will be **Automatically generated in   the light gray area**

  ![][Logo3]

  4 . If you wish to change the Layout; do so by clicking **Change View** on the Top right and selecting an appropriate Layout. If not we are **Ready to Start**

  ![][Logo4]


### 2D and 3D Maps

To start off with our mapping application we will need to add in a **Map** that contains a **basemap** that controls the theme. ArcGIS offers a wide variety of default basemaps. Once we have embedded a map we must decide if we want to use a **MapView** for 2D maps or **SceneView** for 3D maps; for the purpose of this tutorial we will be using a MapView.
  
  1. . First we need to setup the HTML page by inserting the following boilerplate into the HTML window inside codepen. This will act as a standard template for ArcGIS web apps and everything you will be completing in this tutorial.
  
  ```html
  <!DOCTYPE html>
  <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="initial-scale=1, maximum-scale=1, user-scalable=no">
      <title>DSL Tutorial Web App</title>
      <style>
        html, body, #viewDiv {
          padding: 0;
          margin: 0;
          height: 100%;
          width: 100%;
        }
      </style>
    </head>
    <body>
      <div id="viewDiv"></div>
    </body>
  </html>
  ```
  
 2 . Now we need to add the links to the esris JavaScript and CSS inside the **head** tags. These references link code written by esri that will apply some styles and functionality to everything for us. You can add styles in the future to better suite your application.
 
  ```html
  <link rel="stylesheet" href="https://js.arcgis.com/4.13/esri/css/main.css">
  <script src="https://js.arcgis.com/4.13/"></script>
  ```

3 . Next is defining and generating the 2D **MapView**. To change the map location you can change the center coordinates and change the zoom levels, another option is changing the theme which is as easy as adjusting the basemap value for any of the follwing defaults provided by esri https://developers.arcgis.com/javascript/3/jsapi/esri.basemaps-amd.html. If you notice as well we are going to reference the previous **div ID** as the contianer for the map. Add the following inside the **head** tags.
  
  ```html
   <script>
    require([
        "esri/Map",
        "esri/views/MapView"
      ], function(Map, MapView) {

      var map = new Map({
        basemap: "streets-navigation-vector"
      });

      var view = new MapView({
        container: "viewDiv",
        map: map,
        center: [-79.2477, 43.1176], // longitude, latitude
        zoom: 15
      });
    });
   </script>
  ```
  Now all you have to do is click **Run** and see your first Web Application come to life. Your Web App should look like this.
  
   ![][Logo5]
   
 ### BaseMap Selector Widget
 
 The next goal will be to create and embed a **BaseMap Widget** that will allow the user to select a basemap **Theme** from a number of  options provided by esri. For the current and future sections you will be building off the previous code developed.
 
  1 . As more functionality is added the project will require more and more esri JavaScript **Packages**. Luckily esri allows you to import them into the script very easily by adjusting the **Function Method Header**. Once this is changed you will write the code to implement the widget inside the **Function within the Script**.
  
  You will need to adjust the **Function Header** from this
  
  ```html
     require([
      "esri/Map",
      "esri/views/MapView"
    ], function(Map, MapView)
  ```
  To this which adds the **BasemapToggle and BasemapGallery**
  
  ```html
     require([
      "esri/Map",
      "esri/views/MapView",
      "esri/widgets/BasemapToggle",
      "esri/widgets/BasemapGallery"
    ], function(Map, MapView, BasemapToggle, BasemapGallery)
  ```
 
 2 . Next step is to initialize the **BasemapGallery** object while setting all of its variables and attributes. The BasemapGallery object asks the user to define our **view object** and our **esri portal source**. Add the following code block inside the **script** tag after the other code.
 
 ```html
  var basemapGallery = new BasemapGallery({
    view: view,//remember that our mapview is under the variable view
    source: {//our source object 
      portal: {
        url: "http://www.arcgis.com", //the arcgis url
        useVectorBasemaps: true //tells the portal to use the vector basemap gallery
      },
    } 
  });
```

 3 . The final step is to add our implemented BasemapGallery object to our **view** objects **User Interface**. This will show the widget on our map as part of the UI. Add the follwoing code at the end of the Script 
 
 ```html 
  view.ui.add(basemapGallery, "top-right");
 ```
  If you noticed you can easily change the position of the widget to something for example **bottom-right**
  
  Once you save and run your code you will se the widget. Now try selecting the **Streets(Night)** option. It should look something like this
  
  ![][Logo6]

<!--- Please use reference style images so that it is easier to update pictures later --->
[dsllogo]: dsl_logo.png
[Logo1]: LOGO1.png
[Logo2]: LOGO2.png
[Logo3]: LOGO3.png
[Logo4]: LOGO4.png
[Logo5]: LOGO5.png
[Logo6]: LOGO6.png
