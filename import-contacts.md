# Import Contacts
## CSV Import
You can easily import (and export) contacts for your campaign in the form of a CSV file. Here's a list of supported header fields.

| Field | Is Required |
| --- | --- |
| email | yes |
| firstName | no |
| lastName | no |
| companyName | no |

Other fields will be ignored at this point, we are working on adding support for custom fields.

Here's an example of a valid csv file to import
```csv
email;firstName
john@example.com;John
david@example.com;David
```
