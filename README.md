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

## Convert String to Float

```
float(!STRING_FIELD!)
# thank you, slibby @ The Spatial Community    
```

## Convert All String Records to Uppercase

```
import arcpy

fc = r'C:\temp\test.gdb\yourFC'

desc = arcpy.Describe(fc)
fields = desc.fields

for field in fields:
    if field.Type == "String":
        with arcpy.da.UpdateCursor(fc, str(field.name)) as cursor:
            for row in cursor:
                if row[0] == None:  # Check for "<Null>"
                    continue
                else:
                    any(x.islower() for x in row[0]) == True
                    row[0] = row[0].upper()
                    cursor.updateRow(row)
                    
Thank you Aaron @ GIS Stack Exchange
```

## Remove Leading/Trailing Spaces From All String Records

```
import arcpy

fc = r'C:\temp\test.gdb\yourFC'

fieldlist=[i.name for i in arcpy.ListFields(fc) if i.type=='String']

with arcpy.da.UpdateCursor(fc,fieldlist) as cursor:
    for row in cursor:
        row=[i.strip() if i is not None else None for i in row]
        cursor.updateRow(row)

Thank you BERA @ GIS Stack Exchange
```

# Add-Ins

## Streetview

https://github.com/roemhildtg/arcgis-pro-addins
