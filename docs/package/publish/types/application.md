# Application

Creates a web page to visualize the published data.  
  

### Arguments

- **base**: An optional string with the base map, that can be "roadmap", "satellite", "hybrid", or "terrain". The default value is "satellite".
- **center**: An optional named table with two values, lat and long, describing the initial central point of the application.
- **clean**: An optional boolean value indicating if the output directory could be automatically removed. The default value is true.
- **code**: An optional boolean value indicating whether the source code of the application should be copied to the directory of the final application. Note that only the script that was passed as argument to TerraME will be copied. If it include other files, they will not be copied. The default value is true.
- **description**: An optional string with the application's description. It will be shown as a box that is shown in the beginning of the application and can be closed.
- **display**: An optional boolean value indicating whether the application should be opened in a Web Browser after being created. The default value is true.
- **fontSize**: An optional number with the font size.
- **key**: An optional string with 39 characters describing the Google Maps key (see [https://developers.google.com/maps/documentation/javascript/get-api-key](https://developers.google.com/maps/documentation/javascript/get-api-key)). The Google Maps API key monitors your Application's usage in the Google API Console. This parameter is compulsory when the Application has at least 25,000 map loads per day, or when the Application will be installed on a server.
- **layers**: An optional value with the title of the layers box. The default value is 'Layers'.
- **legend**: An optional value with the title of the legend box. The default value is 'Legend'.
- **loading**: An optional string with the name of loading icon. The loading available are: "balls", "box", "default", "ellipsis", "hourglass", "poi", "reload", "ring", "ringAlt", "ripple", "rolling", "spin", "squares", "triangle", "wheel" (see [http://loading.io/](http://loading.io/)). The default value is "default".
- **logo**: An optional string with the logo file path. The logo is an image and the supported extensions are: 'bmp', 'gif', 'jpeg', 'jpg', 'png', 'svg'.
- **maxZoom**: An optional number with the maximum zoom allowed. The default value is 20.
- **minZoom**: An optional number with the minimum zoom allowed. The default value is 0.
- **order**: An optional vector of strings with the order of the [Views](../types/View.md) to be displayed, from top to bottom. The elements of the vector are the names of each View.
- **output**: A mandatory [Directory (base package)](../../../base/types/directory.md) or directory name where the output will be stored. The default value is the name of the project followed by "WebMap".
- **progress**: An optional boolean value indicating if the progress should be shown. The default value is true.
- **project**: An optional [Project (gis package)](../../gis/types/project.md) or string with the path to a .tview file.
- **report**: An option [Report](../types/report.md) with data information.
- **simplify**: An optional boolean value indicating if the data should be simplified. The default value is false.
- **template**: An optional named table with two string elements called navbar and title to describe colors for the navigation bar and for the background of the upper part of the application, respectively.
- **title**: An optional string with the application's title. The title will be placed at the left top of the application page. If Application is created from [Project (gis package)](../../gis/types/project.md) the default value is project title.
- **zoom**: An optional number with the initial zoom, ranging from 0 to 20. The default value is the center of the bounding box containing all geometries.

### Usage

```
import("publish")

Application{
    project = filePath("brazil.tview", "publish"),
    title = "Brazil Application",
    description = "Small application with some data related to Brazil.",
    progress = false,
    biomes = View{
        select = "name",
        color = "Set2", -- instead of using value/color
        description = "Brazilian Biomes, from IBGE.",
    }
}

Directory("brazilWebMap"):delete()
```