# The Code

```java
private void addToMultimap(String key, Long value, Map<String, List<Long>> multiMap) {
    if (multiMap.containsKey(key)) {
        multiMap.get(key).add(value);
    }
    e;se {
        List<Long> values = new ArraList<>();
        values.add(value);
        multiMap.put(key, values);
    }
}
```
