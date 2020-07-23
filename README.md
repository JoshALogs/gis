# Guides for GIS

## Extract phone numbers from a field with multiple contact info strings

With the Calculate Field tool:

```expression_name(!selected_field!)```

```
import re
def expression_name(selected_field):
    match = re.search('(\d{3}[-\.\s]??\d{3}[-\.\s]??\d{4}|\(\d{3}\)\s*\d{3}[-\.\s]??\d{4}|\d{3}[-\.\s]??\d{4})', selected_field)
    if match:
        return match.group()
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
```

## Split full names into first and last

With the Calculate Field tool:

First Name

```expression_name(!first_name_field!)```

```
import re
def expression_name(first_name_field):
    div = first_name_field.split()  
    return div[-1]
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
