# App Architecture

-----
TL;DR: 

In order to recreate what we did today, and based on how the current mapnificent app is structured:

1. Setup a cloud db (Firebase Firestore, Firebase Realtime Database, Cloud SQL, etc.) for static (scheduled) data (this can be done locally by writing scripts that take GTFS txt files, structure them appropriately, and upload them to the database)
2. Setup Firebase Storage (or some equivalent service) to hold realtime GTFS files
3. Write frontend scripts to request (using transitfeeds API), upload (to Firebase Storage or equivalent) and parse (from Firebase Storage or equivalent) realtime GTFS data
-----

Upon browsing through the original codebase, here's what I've understood, coming from a perspective of someone who doesn't have much familiarity with Jekyll:

## Static Site + Frontend scripts
The ```_cities``` folder outlines the content (city name, coordinates, cityid, etc.) and the ```_layouts``` outlines the format (html/css).

Jekyll refers to <a href="https://github.com/vishalbakshi/mapnificent/blob/master/_layouts/city.html">_layouts/city.html</a> for the general layout for a "city" page (i.e. any city that you can click on from the home page).

The configuration of the Jekyll site (<a href="https://github.com/vishalbakshi/mapnificent/blob/master/_config.yml#L5-L10" >which can be seen here</a>) basically says: the **scope** of this website is to convert all files in the **cities** folder and transform them into an html file following "city.html" **layout**.

The two main snippets of code in this ```city.html``` layout that instantiates the mapnificent object to unlock all the magic is:

```
// This grabs the city information from the cityname.md file (i.e. bayarea.md)

var city = {
    cityid: {{ page.cityid | jsonify }},
    cityname: {{ page.cityname | jsonify }},
    coordinates: {{ page.coordinates | jsonify }},
    options: {{ page.options | jsonify }} || {},
    zoom: {{ page.zoom | jsonify }}
  };


// This instantiates the Mapnificent object using that city info
var mapnificent = new Mapnificent(map, city, {
    baseurl: '{{ site.baseurl }}/'
  });
  
// This triggers mapnificent to do all of the things
mapnificent.init();
```

```Mapnificent``` is a global variable which is exported from their main module ```mapnificent.js``` This is the module which does all the cool stuff like calculate the number of stations + walking radius you can travel from one point to the next in some given time.

For our intents and purposes right now, the most important lines in this module are 391 to 433, their ```loadData``` and ```prepareData``` functions. ```loadData``` parses the ```.bin``` file and converts it to an Array which is then used in ```prepareData``` to do all the necessary calcs for generating the approriate circles on the map:

Here are the function definitions for ```loadData```
https://github.com/vishalbakshi/mapnificent/blob/master/static/js/mapnificent.js#L391-L433

and ```prepareData```
https://github.com/vishalbakshi/mapnificent/blob/master/static/js/mapnificent.js#L443-L487

Here's where they are used:

https://github.com/vishalbakshi/mapnificent/blob/master/static/js/mapnificent.js#L300-L340

My best guess for why they used this whole setup (Jekyll for static pages + scripts for data parsing/prep) is that since they are doing all of their file streaming (reading) on the frontend, they need it to be light/quick.

Protocol Buffers can be read about <a href="https://developers.google.com/protocol-buffers/">here</a>. It takes a JSON data structure and then parses a binary file that was originally in that structure. That JSON data structure is given in line 398 of ```mapnificent.js```.

What we did today was to generate the binary file from a folder of tables (in the form of .txt files) and the ```go``` command essentially took those files and converted them to binary following the nested JSON structure. Not sure where the nested JSON structure was implied but that will require some digging into the ```mapnificent.go``` script in the mapnificent generator repo where this command that did the trick:

```go run mapnificent.go -d ~/gtfs/ -o bayarea.bin -v```

Not sure how to spin up a Go environment on a server that is only hosting static files, so we may have to find some JavaScript equivalent package. But that's a hunch right now.

As it stands, the Mapnificent process relies pretty heavily on the binary file. That being said, we have (I think) two options:

1. Continue with this binary file philosophy and come up with a JavaScript way to handle that with realtuime GTFS data
2. Rewrite the ```loadData``` function (line 391 in mapnificent.js) and replace it with something that reads a file that's not binary

Either option is cool so maybe doing it in parallel will save us time in the long run.




