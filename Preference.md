Preferences are an important aspect of any portal framework/server. Preferences in piston are implemented in a slightly different manner than other portals.

In piston preferences can be defined at two levels -

* App

An app level preference works as a global preference for all the plugins defined under that app. Preferences of an app are defined in app.xml file for that app.

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<app>
	<name>app_name</name>
	<title>app_title<title>
	<resFolder>res_folder</resFolder>
	<preference>
		<name>pref_name</name>
		<value>default_value</value>
		<scope>APP</scope>
		<scope>PLUGIN</scope>
	</preference>
</app>
```

* Plugin

A plugin preference is unique to that plugin and overwrites a preference with same name defined at app level. Plugin preferences are defined in Plugin class using 'AnnoPreference' annotation.

```java
@AnnoPlugin(name = "timesheet", title = "Timesheet", 
	defaultAction = GetTimesheetPluginAction.ACTION_NAME,
	preferences = {
			@AnnoPreference(name = "JIRA_USER", scopes = {"USER"}),
			@AnnoPreference(name = "JIRA_PWD", scopes = {"USER"})
	}
)
public class TimesheetPlugin extends Plugin {
```

### Preference scopes

Scope of a preference defines levels which a preference can be modified. Possible values are APP, PLUGIN, TILE and USER. TILE level preferences can be modified only by portal administrators while USER level preferences can be modified by non admin users.

Blank value for scopes at a level means that preference can be modified at that level only. For example, in app.xml JIRA_HOST has been defined without any scope and so this preference can be modified at APP level only.

However if a value or values are defined for scopes then the preference can be modified at those scopes only. As the scope for corresponding level is not included automatically, you should explicitly define level in scopes. For example, JIRA_USER has been defined with scope as USER which means this preference can be modified at USER level but not on PLUGIN level.

### Preference inheritance/overwriting
Following is the order of various preference levels in increasing order of priority -

* APP
* PLUGIN
* TILE
* USER

A level with high priority will inherit preferences from lower levels. Also a preference defined/modified at higher level will overwrite preferences with same names at lower levels. 
