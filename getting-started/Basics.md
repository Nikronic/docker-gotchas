## Persist the DB
| <div style="width:290px"></div> | Named volumes | Bind mounts |
| :---: | :---: | :---: |
| Host location | Docker chooses | You decide |
| Mount example (using `--mount`) | `type=volume,src=my-volume,target=/usr/local/data` | `type=bind,src=/path/to/data,target=/usr/local/data` |
| Populates new volume with container contents | Yes | No |
| Supports Volume Drivers | Yes | No |
