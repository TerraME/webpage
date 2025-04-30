# Report

Creates a page with data information.  
  

### Arguments

- **author**: An optional string with the Report's author.
- **title**: An optional string with the Report's title.

### Usage

```
import("publish")
local report = Report{
    title = "Social Classes 2010 Real",
    author = "Feitosa et al. (2012)"
}

report:addImage("urbis_2010_real.PNG", "publish")
report:addText("This is the main endogenous variable of the model.")
```

## Functions

|   |   |
|---|---|
|[addGraphic](#addGraphic)|Add a new graphic to the Report.|
|[addHeading](#addHeading)|Add a new heading to the Report.|
|[addImage](#addImage)|Add a new image to the Report.|
|[addMatrix](#addMatrix)|Add a new matrix (table) to the Report.|
|[addMult](#addMult)|Add a new text or multiple data to the Report.|
|[addSeparator](#addSeparator)|Add a line in the Report.|
|[addText](#addText)|Add a new text to the Report.|
|[addVideo](#addVideo)|Add a palyer of video to the Report.|
|[get](#get)|Return the Report created.|

## **addGraphic** 

Add a new graphic to the Report.  
  

### Arguments

- **#1**: accept string and data to the report.

### Usage

```
import("publish")
local report = Report()
report:addGraphic("My graphic")
```

## **addHeading** 

Add a new heading to the Report. A heading element briefly describes the topic of the section it introduces.  
  

### Arguments

- **#1**: A mandatory string with the heading of the report.

### Usage

```
import("publish")
local report = Report()
report:addHeading("My Heading", "publish")
```

## **addImage** 

Add a new image to the Report.  
  

### Arguments

- **#1**: A mandatory string or [File (base package)](../../../base/types/file.md) with the image of the report. The supported extensions are: bmp, gif, jpg, jpeg, png, and svg.
- **#2**: An optional string with the name of the package.

### Usage

```
import("publish")
local report = Report()
report:addImage("urbis_2010_real.PNG", "publish")
```

## **addMatrix** 

Add a new matrix (table) to the Report.  
  

### Arguments

- **#1**: accept text and data to the report.

### Usage

```
import("publish")
local report = Report()
report:addMatrix("My matrix")
```

## **addMult** 

Add a new text or multiple data to the Report.  
  

### Arguments

- **#1**: is not mandatory string the text to the report.

### Usage

```
import("publish")
local report = Report()
report:addMult("My text")
```

## **addSeparator** 

Add a line in the Report.  
  

### Usage

```
import("publish")
local report = Report()
report:addSeparator()
```

## **addText** 

Add a new text to the Report.  
  

### Arguments

- **#1**: A mandatory string with the text to the report.

### Usage

```
import("publish")
local report = Report()
report:addText("My text")
```

## **addVideo** 

Add a palyer of video to the Report.  
  

### Arguments

- **#1**: accept URL string only.

### Usage

```
import("publish")
local report = Report()
report:addVideo("My video youtube/vimeo")
```

## **get** 

Return the Report created.  
  

### Usage

```
import("publish")
local report = Report()
report:addText("My text")
report:get()
```