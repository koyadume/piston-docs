## Invoking a plugin action
```xml
<plugin:actionURL action="pluginAction2">
	<c:out value="Jump to Page2" />
</plugin:actionURL>
```

## Invokding a plugin action with parameters
```xml
<plugin:actionURL action="pluginAction3">
	<plugin:param name="param1" value="value1" />
</plugin:actionURL>
```

## Rendering plugin action link as button
```xml
<plugin:actionURL action="pluginAction4" title="Go to Page4" class="img-btn">
</plugin:actionURL>
```

## Using Font Awesome
```xml
<plugin:actionURL action="pluginAction5" title="Go to Page5" class="img-btn" faClass="fa fa-gear fa-lg" faStyle="font-size: 1.2em;">
</plugin:actionURL>
```								