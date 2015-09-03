# Context root
```
/piston-service/v2.0/
```

## Site management
### Get site id from site mapping
```
GET /siteMgmt/sites/getId?mapping=<site mapping>
```

### Load site (returns metadata and all (in)direct children)
```
GET /siteMgmt/sites/{siteId}/loadSite
```

### Save or update site
```
POST/PUT /siteMgmt/sites

{
	
}
```

### Delete sites
```
DELETE /siteMgmt/sites?siteIds=<Comma seperated list of site ids>
```

### Get sites (returns metadata and permissions for all the sites)
```
GET /siteMgmt/sites
```

### Save or update page
```
POST/PUT /siteMgmt/pages

{
	
}
```

### Get page layout
```
GET /siteMgmt/pages/{pageId}/getLayout
Accept: text/plain
```

### Update page layout
```
PUT /siteMgmt/pages/{pageId}/updateLayout

Content-Type: text/plain
{
	
}
```

### Delete pages
```
DELETE /siteMgmt/pages?pageIds=<Comma seperated list of page ids>
```

### Move a page one position down
```
GET /siteMgmt/pages/{pageId}/moveDown
``` 

### Move a page one position up
```
GET /siteMgmt/pages/{pageId}/moveUp
```

### Create tile
```
POST /siteMgmt/tiles

{
	
}
```

### Get tile
```
GET /siteMgmt/tiles/{tileId}
```

