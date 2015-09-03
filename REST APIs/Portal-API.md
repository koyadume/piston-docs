# Context root
```
/piston-service/v2.0/
```

## Portal
### Register apps
```
POST /portal/apps

[
	{
		
	},
	{
		
	}
]
```

### Get apps
```
GET /portal/apps
```

### Update app
```
PUT /portal/apps

{
	
}
```

### Enable apps
```
PUT /portal/apps/enable?appIds=<comma separated list of app ids>
```

### Disable apps
```
PUT /portal/apps/disable?appIds=<comma separated list of app ids>
```

### Enable plugins
```
PUT /portal/plugins/enable?appIds=<comma separated list of plugin ids>
```

### Disable plugins
```
PUT /portal/plugins/disable?appIds=<comma separated list of plugin ids>
```

### Update plugin
```
PUT /portal/plugins

{

}
```

### Create frame
POST /portal/frames

{

}
```

### Update frame
```
PUT /portal/frames

{

}
```

### Get all frames
```
GET /portal/frames
```

### Get frame details
```
GET /portal/{frameId}
```

### Delete frames
```
DELETE /portal/frames?frameIds=<Comma seperated list of frame ids>
```


