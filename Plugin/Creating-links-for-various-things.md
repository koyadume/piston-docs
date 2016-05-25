## Creating a link to submit plugin form
```xml
<pButton class="pseudo-submit-button"> 
	<c:out value="Submit" />
</pButton>
```

## Render link as button
```xml
<pButton class="pt-btn pseudo-search"> 
	<c:out value="Search" />
</pButton>
```

## Render link as button (Font Awesome support)
```xml
<pButton class="pt-btn pseudo-search" faClass="fa fa-search fa-lg" faStyle="font-size: 1.2rem; padding-right: 6px;"> 
	<c:out value="Search" />
</pButton>
```

## Creating a link to process custom logic
```xml
<pButton class="pseudo-add-permission"> 
	<c:out value="Add" />
</pButton>
```

```javascript
$(function() {
    $('.pseudo-add-permission').click(function() {
    	targetRole = $(this).closest('tr').find('.pseudo-permission-container');
    	var modal = $('.pseudo-full-modal');
    	modal.show();
    	
    	modal.css('top', $(window).scrollTop() + 'px');
    	$('html, body').css({
    	    'overflow': 'hidden'
    	});
    	
    	$.ajax({
    		async : false,
            url: '/piston/web/getAjaxView?view=searchUsersGroupsDB',
            type: 'GET',
            success: function(data) {
                modal.find('.pseudo-loader').hide();
                modal.find('.pseudo-full-modal-content').html(data);
            }
    	});
    });
});
```

