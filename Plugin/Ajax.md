## Invoking plugin action asynchronously
```xml
<pButton class="pseudo-siteLink"> 
	<c:out value="Site 1" />
</pButton>
```

```javascript
$('.pseudo-siteLink').click(function() {
	var siteId = $(this).attr('id');
	var form = createPluginForm($(this), 'ajaxGetSitePageChildren');
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
