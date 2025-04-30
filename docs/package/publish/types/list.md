# List

A list of [View](../types/View.md) objects.  
  

### Arguments

- **#1**: A table with the views.

### Usage

```
import("publish")
local list = List{
    limit = View{
         description = "Bounding box of Caraguatatuba.",
         color = "goldenrod"
    },
    regions = View{
         description = "Regions of Caraguatatuba.",
         select = "name",
         color = "Set2"
    }
}

print(list)
print(#list)
```