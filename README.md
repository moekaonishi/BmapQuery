BmapQuery.js  v0.8.7
==========

BmapQuery is a Microsoft BingMaps V8 functions. to be used inside web pages.
component to be used as part of web applications and websites.


## Checking Your Installation

To test your installation, just call the following page at your website:

[[BmapQuery.js] (https://mapapi.org/indexb.php)]

![default](https://user-images.githubusercontent.com/1481062/52621258-2b963500-2eea-11e9-8c55-43c97d2da0ac.png)



## Installation

Installing BmapQuery is an easy task. Just follow these simple steps:

 1. **Download** the latest version from the Github website:
    https://github.com/yamazakidaisuke/BmapQuery.
    ( Example Site: https://mapapi.org/indexb.php )
    You should have already completed this step, but be sure you have the very latest version.

2. BmapQuery is by default installed in the `js` folder. You can
place the files in whichever you want though. Operation check with index.html.



## Directory Structure

It's opinionated about how you organize your repositories.


    ├── index.html               (Link to example)
    ├── js/
    │   └── BmapQuery.js         (ES5: BingMaps Library)
    ├── src/
    │   └── BmapQuery.js         (ES6: Before BABEL execution.)
    ├── img/
    │   └── poi_custom.png
    ├─── example/                (All example files)
    │   ├── map_start.html
    │   ├── map_event.html
    │   ├── map_changeView.html
    │   ├── pushpin.html
    │   ├── ...
    │   ...
    │
    ├── README.md
    └── LICENSE


## Getting Started

1. <script src="...?Callback=GetMap&..." is specified in the URL."GetMap" runs first.

2. Please get BingMapsKey from "BingMaps Dev Center" site.
   [Get BingMapsKey >> BingMaps Dev Center](https://www.bingmapsportal.com/)

3. Replace [ *** YOUR MY KEY *** ] in the example code with BingMapsKey.

**[html: index.html]**

    <!-- 1.Load BingMapsControl api [callback=GetMap] -->
    <script src='https://www.bing.com/api/maps/mapcontrol?callback=GetMap&key=[***Your My Key***]' async defer></script>

    <!-- 2.Load BmapQuery -->
    <script src="js/BmapQuery.js"></script>

    <!-- 3.BmapQuery Start -->
    <script>
    //init
    function GetMap(){
        
        //Start
        const map = new Bmap("#myMap); //Preparation
        
        //Map
        map.startMap(47.6149, -122.1941, "load", 10); //Run on one line
        
        //Pin
        let pin = map.pin(47.6149, -122.1941, "#ff0000"); //Run on one line
        
        //infobox
        map.infobox(47.6149, -122.1941, "Title", "Description"); //Run on one line
    
    }





## Documentation

#### Examples
**Sample files for each function are prepared in the "example" folder.**

#### Map Start!!

    //*Sample
    //----------------------------------------------------
    // Instance...
    //----------------------------------------------------
    let map = new Bmap("#myMap");
    
    //----------------------------------------------------
    // Show Map
    // startMap(lat, lon, "MapType", Zoom[1~20]);
    //----------------------------------------------------
    map.startMap(47.6149, -122.1941, "load", 16);//MapType[load, aerial,canvasDark,canvasLight,birdseye,grayscale,streetside]


#### Map Event


    //----------------------------------------------------
    // Map:Events
    // onMap("event", callback);
    // [event:click,dblclick,rightclick,mousedown,mouseout,mouseover,mouseup,mousewheel,maptypechanged,viewchangestart,viewchange,viewchangeend]
    //----------------------------------------------------
    map.onMap("click",function(){
        alert("MapEvent!");
    });


#### Pushpin


    //----------------------------------------------------
    // Pushpin
    // pin(lat, lon, "color", [drag:true|false], [click:true|false], [hover:true|false], [visible:true|false]);
    //----------------------------------------------------
    let pin1 = map.pin(47.6149, -122.1941, "#ff0000");


#### Get Map infomation


    //----------------------------------------------------
    // Get Map infomation
    // map.map.*****();
    //----------------------------------------------------
    let str =  `<p>Map Height: ${map.map.getHeight()} </p>
                <p>Map center: ${map.map.getCenter()}</p>
                <p>Map Width:  ${map.map.getWidth()}</p>
                <p>Map bounds: ${map.map.getBounds()}</p>
                <p>Map PageX:  ${map.map.getPageX()}</p>
                <p>Map PageY:  ${map.map.getPageY()}</p>
                <p>Map zoom:   ${map.map.getZoom()}</p>
                <p>Map type:   ${map.map.getMapTypeId()}</p>`;
    //id="controll"にstr変数（Map情報）を表示
    document.getElementById("controll").innerHTML = str;
    
    
#### PushpinText


    //----------------------------------------------------
    // Pushpin:Text
    // pinText(lat, lon, "title", "subtitle", "text");
    //----------------------------------------------------
    let pin2 = map.pinText(47.6160, -122.1950, "title","subtitle","A");


#### PushpinIcon


    //----------------------------------------------------
    // Pushpin:Icon
    // pinIcon(lat, lon, icon, scale, anchor_x, anchor_y);
    //----------------------------------------------------
    let pin3 = map.pinIcon(47.6130, -122.1945, "img/poi_custom.png", 1.0, 0, 0);


#### PushpinEvent


    //----------------------------------------------------
    // pushpin:Events
    // onPin(pushpin, "event", callback);
    // [event: click,mousedown,mouseout,mouseover,mouseup]
    //----------------------------------------------------
    map.onPin(pin1, "click", function(){
        alert("PinEvent1");
    });


#### Layer->Pushpin


    //----------------------------------------------------
    // Layer: Add Pushpin
    // pinLayer(lat, lon, "color", [drag:true|false], [click:true|false], [hover:true|false], [visible:true|false]);
    //----------------------------------------------------
    const pin1 = map.pinLayer(47.6149, -122.1941, "#ff0000");
    const pin2 = map.pinLayer(47.6155, -122.1945, "#0000ff");
    const pin3 = map.pinLayer(47.6160, -122.1940, "#00ff00");


#### Layer->One Pushpin Delete


    //----------------------------------------------------
    // layer One delete
    //----------------------------------------------------
     map.pinLayerClear(pin2);
     
     
#### Layer->Allclear

     
    //----------------------------------------------------
    // layer Allclear
    //----------------------------------------------------
     map.pinLayerClear();

     
#### Circle->Location Add


    //------------------------------------------------------------------------
    // Circle&Location Add
    // circle( Meter, style={pinColor,fillColor,strokeWidth} );
    //------------------------------------------------------------------------
    //Circle Style
     const style = {
         pinColor:"#0000ff",
         fillColor:"rgba(0,0,100,0.6)",
         strokeWidth:1
     };
     //Circle Create
     map.circle(1000, style); //1000m = 1km, 2000 = 2Km
     map.circle(3000, style); //1000m = 1km, 2000 = 2Km

     
#### Circle->Location Event


    //------------------------------------------------------------------------
    // [Event] Circle&Location Add
    // circle( Meter, style={pinColor,fillColor,strokeWidth},"event", callback );
    //------------------------------------------------------------------------
    //Circle Style
     const style = {
         pinColor:"#0000ff",
         fillColor:"rgba(0,0,100,0.6)",
         strokeWidth:1
     };
     //Circle Create //3000=3Km
     map.circle(3000, style, "click", function(){
         const lat = map.getCenter().latitude;  //Get MapCenter Latitude
         const lon = map.getCenter().longitude; //Get MapCenter Longitude
         map.infobox(lat, lon, "Title", "Description");
     });

     
#### Circle->Set Location


    //------------------------------------------------------------------------
    // Circle&SetLocation Add
    // circleSet( lat, lon, Meter, style={pinColor,fillColor,strokeWidth} );
    //------------------------------------------------------------------------
    //Circle Style
    const style = {
        pinColor:"#0000ff",
        fillColor:"rgba(0,0,100,0.4)",
        strokeWidth:10
    };
    //Circle Create
    map.circleSet(47.6200, -122.1100, 2000, style); //1000=1km, 2000=2Km
    map.circleSet(47.6000, -122.1599, 3000, style); //1000=1km, 2000=2Km
    map.circleSet(47.6149, -122.1941, 1000, style); //1000=1km, 2000=2Km
    
       
#### Circle->Set Location Event


    //------------------------------------------------------------------------
    // [Event] Circle&SetLocation Add
    // circleSet( lat, lon, Meter, style={pinColor,fillColor,strokeWidth},"event", callback );
    //------------------------------------------------------------------------
    //Circle Style
    const style = {
        pinColor:"#0000ff",
        fillColor:"rgba(0,0,100,0.4)",
        strokeWidth:10
    };
    
    //CircleSet:Event1 //1500=1.5Km
    map.circleSet(47.6200, -122.1100, 1500, style, "click", function(){
        map.infobox(47.6200, -122.1100, "Title1", "Description1");
    });
    
    //CircleSet:Event2 //2000=2Km
    map.circleSet(47.5500, -122.1299, 2000, style, "click", function(){
        map.infobox(47.5500, -122.1299, "Title2", "Description2");
    });

    //CircleSet:Event3 //3000=3Km
    map.circleSet(47.6149, -122.1941, 3000, style, "click", function(){
        map.infobox(47.6149, -122.1941, "Title3", "Description3");
    });

       
#### infobox


    //----------------------------------------------------
    // Infobox
    // infobox(lat, lon, "title", "description");
    //----------------------------------------------------
    map.infobox(47.6149, -122.1941, "1 step", "Start");

       
#### infoboxHtml

    //----------------------------------------------------
    // Infobox:html
    // infoboxHtml(lat, lon, html);
    //----------------------------------------------------
    map.infoboxHtml(47.6160, -122.1950, '<div style="background:red;">Hello,world</div>');
    
    
#### infoboxIframe

    //----------------------------------------------------
    // Infobox:Iframe
    // infoboxIframe(lat,lon,width,height,title,iframe)
    //----------------------------------------------------
    const title = "Movie";
    const iframe = '<iframe src="https://channel9.msdn.com/Events/Build/2016/B867/player#time=0h15m26s:paused" width="400" height="225" allowFullScreen frameBorder="0"></iframe>';
    map.infoboxIframe(47.6149, -122.1941, 300, 420, title, iframe);


#### onInfobox

    //----------------------------------------------------
    // Infobox:Actions
    // map.onInfobox(lat, lon, "title","description", "text or html");
    //----------------------------------------------------
     //Configuration
     const title = "Title";
     const discript = '<div style="width:200px;color:red;">discription</div>';
     const actions =
         [
             //1.action
             {
                 label: 'Click1',
                 eventHandler: function () { //function
                     alert('Click1');
                 }
             },
             //2.action
             {
                 label: 'Click2',
                 eventHandler: function () { //function
                     alert('Click2');
                 }
             }
         ];
     //Create Event to Infobox
     map.onInfobox(47.6160,-122.1950, title, discript, actions);
     
     
     
#### polyline

    //----------------------------------------------------
    // polyline
    // polyline(locations, "color", lineBold, [lineWidth,lineSpace] );
    //----------------------------------------------------
    // location points.(array)
    const locations = [
        new Microsoft.Maps.Location(lat + 0.01, lon - 0.03),
        new Microsoft.Maps.Location(lat + 0.02, lon + 0.03),
        new Microsoft.Maps.Location(lat + 0.03, lon - 0.03),
        new Microsoft.Maps.Location(lat + 0.04, lon + 0.03),
        new Microsoft.Maps.Location(lat + 0.05, lon - 0.03)
    ];
    // A Type: polyline create
    map.polyline(locations,"#ff0000",3);
    // B Type: polyline create
    map.polyline(locations,"#ff0000",3,[2,2]);


#### ChangeView

    //----------------------------------------------------
    // MapChangeView(after 2 seconds.)
    // changeMap(lat, lon, "MapType", Zoom[1~20]);
    //----------------------------------------------------
    setTimeout(function(){
        map.changeMap(47.6150, -122.1950, "load", 17);
    },2000);

#### Geocode

    //----------------------------------------------------
    // Geocode(2 patterns & after 4 seconds.)
    // getGeocode("searchQuery",callback);
    //----------------------------------------------------
    setTimeout(function () {
        //A. Address
        map.getGeocode("Seattle", function(data){
            alert("A. getGeocode");
            document.querySelector("#geocode").innerHTML=data;
        });
        //B. Click Event
        map.onGeocode("click", function(data){
            alert(data.location);
        });
    },4000);


#### Reverse Geocode


    //------------------------------------------------------------------------
    //Get Reverse Geocode
    //2 patterns
    //after 6,8 seconds.
    //------------------------------------------------------------------------
    //A Type: Set location data for BingMaps
    setTimeout(function () {
        const location = map.setLocation(47.6130, -122.1945);
        map.reverseGeocode(location, function(data){
            alert("A. Reverse Geocode");
            document.querySelector("#geocode").innerHTML=data;
        });
    },6000);

    //B Type: Get MapCenter location
    setTimeout(function () {
        const mapCenter = map.getCenter();
        map.reverseGeocode(mapCenter, function(data){
            alert("B. Reverse Geocode");
            document.querySelector("#geocode").innerHTML=data;
        });
    },8000);


#### Directions Search


    //----------------------------------------------------
    //Directions:Search.
    // !! For confirmation, set the parameters for each country !!
    // +  [ English => https://www.bing.com/...&setLang=en&setMkt=en-US ]
    // +  [ Japan   => https://www.bing.com/...&setLang=ja&setMkt=ja-JP ]
    //------------------------------------------------------------------------
    document.getElementById("search").onclick = function () {
        const from  = document.getElementById("from").value;  //StartPoint
        const to    = document.getElementById("to").value;    //EndPoint
        const mode  = document.getElementById("mode").value;  //RouteMode[walking,driving]
        const array = ["Bellevue", "Yarrow Point"];           //Waypoints...
        map.direction("#direction", mode, from , to, array);  //Direction Methed
    };


#### AutoSuggest

    //-----------------------------------------------------
    // AutoSuggest
    // !! Only viewing user's region can be displayed !!
    //-----------------------------------------------------
    // HTML:Add !!
    // <h1>AutoSuggest(Enter city in text box)</h1>
    // <div id='searchBoxContainer'>
    //     <input type='text' id='searchBox'><button id="clear">Clear</button>
    // </div>
    //-----------------------------------------------------
    map.selectedSuggestion("#searchBox","#searchBoxContainer");

#### Traffic

    //----------------------------------------------------
    // Traffic
    // map.traffic();
    //----------------------------------------------------
    map.traffic();

#### get Boundary

    //----------------------------------------------------
    // get Boundary
    // map.getBoundary("type");
    //----------------------------------------------------
    // [ "type" ]
    // *CountryRegion:Country or region.
    // *AdminDivision1:First administrative level within the country/region level, such as a state or a province.
    // *AdminDivision2:Second administrative level within the country/region level, such as a county.
    // *PopulatedPlace:A concentrated area of human settlement, such as a city, town or village.
    // *Neighborhood:A section of a populated place that is typically well-known, but often with indistinct boundaries.
    // *Postcode1:The smallest post code category, such as a zip code.
    // *Postcode2:The next largest post code category after Postcode1 that is created by aggregating Postcode1 areas.
    // *Postcode3:The next largest post code category after Postcode2 that is created by aggregating Postcode2 areas.
    // *Postcode4:The next largest post code category after Postcode3 that is created by aggregating Postcode3 areas.
    // Note: Not all entity types are available in all areas.
    //---------------------------------------------------
    map.getBoundary("PopulatedPlace");

#### Get multiple boundaries

    //----------------------------------------------------
    // Get multiple boundaries
    //  map.getMultiBoundary(["Postcode"...]);
    //----------------------------------------------------
    const zipCodes = ['98004', '98005', '98007', '98008', '98039'];
    map.getMultiBoundary(zipCodes);

#### Get Search boundaries

    //----------------------------------------------------
    // Get Search Boundary
    // @method getSearchBoundary
    // @param  search  (string)  'New York City'
    // @param  type    (string)
    //----------------------------------------------------
    // [ "type" ]
    // *CountryRegion:Country or region.
    // *AdminDivision1:First administrative level within the country/region level, such as a state or a province.
    // *AdminDivision2:Second administrative level within the country/region level, such as a county.
    // *PopulatedPlace:A concentrated area of human settlement, such as a city, town or village.
    // *Neighborhood:A section of a populated place that is typically well-known, but often with indistinct boundaries.
    // *Postcode1:The smallest post code category, such as a zip code.
    // *Postcode2:The next largest post code category after Postcode1 that is created by aggregating Postcode1 areas.
    // *Postcode3:The next largest post code category after Postcode2 that is created by aggregating Postcode2 areas.
    // *Postcode4:The next largest post code category after Postcode3 that is created by aggregating Postcode3 areas.
    // Note: Not all entity types are available in all areas.
    //---------------------------------------------------
    document.getElementById("search").onclick=function(){
        //text value.
        const searchBox = document.getElementById("searchBox").value;
        //BingMaps Serch
        map.getSearchBoundary(searchBox, 'PopulatedPlace');
    }
    
#### SetLocation multiple boundaries
    
    //----------------------------------------------------
    //  SetLocation multiple boundaries
    //  map.setLocationBoundary(location[array], Zoom[array], 'CountryRegion');
    //----------------------------------------------------
    const location = ['Russia', 'France', 'Italy'];
    const zoom     = [
        [1,5], //'Russia'
        [1,5], //'France'
        [1,5]  //'Italy'
    ];
    map.setLocationBoundary(location, zoom , 'CountryRegion');



#### Tracking Event[Start&Stop]

    //------------------------------------------------------------------------
    // Tracking Event
    // 1. <button id="start_tracking"....
    // 2. <button id="stop_tracking"....
    //------------------------------------------------------------------------
    //Start
    document.getElementById("start_tracking").onclick=function(){
        map.startTracking(true); //console.log => true or false
    }
    //Stop
    document.getElementById("stop_tracking").onclick=function(){
        map.stopTracking();
    }




## Author

Copyright (c) 2018-2019, BingMapsGO! - DaisukeYamazaki. All rights reserved.
https://mapapi.org - See LICENSE.md for license information.


