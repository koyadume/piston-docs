```java
//normal
URI uri = new URI("http", "localhost", path, null);

//with query
URI uri = new URI("http", "localhost", path, query, null);

Result result = RestServiceUtil.get(uri);
LOGGER.debug("Response code : " + result.getCode());

// for non streaming rest service	
String json = result.getBody();

//handle array
JSONObject[] array = JsonProcessor.getAsObject(json, JSONObject[].class);
String[] array = JsonProcessor.getAsObject(json, String[].class);

//handle json object
JSONObject obj = JsonProcessor.getAsObject(json, JSONObject.class);
```