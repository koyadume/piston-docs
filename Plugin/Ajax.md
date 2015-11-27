## Invoking plugin action asynchronously
```xml
<pButton class="pseudo-siteLink"> 
	<c:out value="Site 1" />
</pButton>
```

### Submitting a new form with custom plugin action
```javascript
$('.pseudo-siteLink').click(function() {
	var siteId = $(this).attr('id');
	var form = createPluginForm($(this), '<plugin_action>');
	form.append(createHidden('siteId', siteId));
	$.ajax({
   		async : false,
        url: '/piston/ajaxPlugin',
        type: 'POST',
		data: form.serializeArray(),
        success: function(data) {
			$('#resChildren').html(data);
        }
	});
});
```

### Submitting enclosing form with custom plugin action
```javascript
$('.pseudo-siteLink').click(function() {
	var siteId = $(this).attr('id');
	var form = getPluginFormWithAction($(this), '<plugin_action>');
	form.append(createHidden('siteId', siteId));
	$.ajax({
   		async : false,
        url: '/piston/ajaxPlugin',
        type: 'POST',
		data: form.serializeArray(),
        success: function(data) {
			$('#resChildren').html(data);
        }
	});
});
```
