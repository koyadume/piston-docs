# Context root
```
/piston-service/v2.0/
```

## App config
### Getting app edit preferences
```
GET /prefs/app/{appId}
```

### Getting plugin edit preferences
```
GET /prefs/plugin/{pluginId}
```

### Getting tile edit preferences
```
GET /prefs/tile/{tileId}
```

### Getting user edit preferences
```
GET /prefs/tile/{tileId}/{userId}/editPrefs
```

### Save preferences
```
POST /prefs

[
	{
	
	},
	{
		
	}
]
```

### Getting user effective preferences
```
GET /prefs/tile/{tileId}/{userId}/effectivePrefs
```



