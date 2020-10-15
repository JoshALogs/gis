# Guides for GIS

## Add "Enable Undo" toggle to tools/models

1. Find the file `C:\Program Files\ArcGIS\Pro\Resources\ArcToolBox\Toolboxes\editsession.txt` and edit in a text editor.
2. Add a new line at the bottom with `<yourtoolboxalias>.<yourtoolname>`.
3. Save and close the file.
4. Save and close Pro.
5. Reopen Pro and open the tool to see the Undo toggle at the bottom next to the Run button.

Thanks to Drew Flater @ GeoNet

## Extract phone numbers from a field with multiple contact info strings

With the Calculate Field tool:

```expression_name(!selected_field!)```

```
import re
def expression_name(selected_field):
    match = re.search('(\d{3}[-\.\s]??\d{3}[-\.\s]??\d{4}|\(\d{3}\)\s*\d{3}[-\.\s]??\d{4}|\d{3}[-\.\s]??\d{4})', selected_field)
    if match:
        return match.group()
# thank you, Auguste @ stackoverflow.com        
```

## Extract emails from a field with multiple contact info strings

With the Calculate Field tool:

```expression_name(!selected_field!)```

```
import re
def expression_name(selected_field):
    match = re.search('\w+@.*?(?=,|\s|$)', selected_field)
    if match:
        return match.group()
# thank you, steveoh @ The Spatial Community                    
```

## Split full names into first and last

With the Calculate Field tool:

First Name

```expression_name(!first_name_field!)```

```
import re
def expression_name(first_name_field):
    div = first_name_field.split()  
    return div[0]
```

Last Name

```expression_name(!last_name_field!)```

```
import re
def expression_name(last_name_field):
    div = last_name_field.split()  
    return div[-1]
```

## Remove all but first and last name

```expression_name(!Contact!)```

```
import re
def expression_name(Contact):
    div = Contact.split()  
    return div[0] + " " + div[-1]
```

## List and count all features in a map

```
for l in arcpy.mp.ArcGISProject("CURRENT").listMaps()[0].listLayers():
    try:print (l.name, ": ", arcpy.management.GetCount(l))
    except:pass
# thank you, slibby @ The Spatial Community    
```

# Add-Ins

## Streetview

https://github.com/roemhildtg/arcgis-pro-addins
