---
id: qkymmf9pxbnd040tq1xob74
title: Schema_as_column
desc: ''
updated: 1750753902751
created: 1750753725382
---

```bash

changes_df.schema
# Get name-type pairs as a dictionary
schema_dict = {field.name: str(field.dataType) for field in changes_df.schema.fields}

# Print the schema dictionary in a readable format
print("\nColumn Name : Data Type")
print("-----------------------")
for name, dtype in schema_dict.items():
    print(f"{name.ljust(30)} : {dtype}")
```

