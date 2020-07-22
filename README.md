# Guides for GIS

## Extract emails from a field with multiple contact info strings

In the Calculate Field Tool:

```expression_name(!selected_field1!)```

```
import re
def expression_name(selected_field1):
    match = re.search('\w+@.*?(?=,|\s|$)', selected_field1)
    if match:
        return match.group()
```
