# The Code

```java
private void handleAllData() {
    Map<String, SomeData> dataById = getData();

    Iterator<String> ids = dataById.keySet().iterator();

    while (ids.hasNext()) {
        String id = ids.next();
        SomeData someData = dataById.get(id);
        handleData(id, someData);
    }
}
```
