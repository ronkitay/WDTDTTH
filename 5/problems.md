# The Problems

The point was to show that the logic in both if and else are the same besides the addition or the new list to the map.

Here is how this would look prior to java8:

```java
private void addToMultimap(String key, Long value, Map<String, List<Long>> multiMap) {
    List<Long> values = multiMap.get(key);
    if (values == null) {
        values = new ArrayList<>();
        multiMap.put(key, values);
    }
    values.add(value);
}
```

And in java8:

```java
private void addToMultimap(String key, Long value, Map<String, List<Long>> multiMap) {
    List<Long> values = multiMap.computeIfAbsent(key, key -> new ArrayList<>());
    values.add(value);
}
```

Or in “one” line of java8:

```java
private void addToMultimap(String key, Long value, Map<String, List<Long>> multiMap) {
    multiMap
        .computeIfAbsent(key, key -> new ArrayList<>())
        .add(value);
}
```

Of course – if you already have `Guava` in the classpath – you can use the `Multimap` interface to do exactly that – behind the scenes it does the exact same logic:

```java
Multimap<String, Long> multiMap = new HashMultimap<>();
multiMap.put(key, value);
...
Map<String, List<Long>> javaMultimap = multiMap.asMap();
```

Don’t worry – `asMap` is **O(1)** computation and memory. Do note that Guava returns a `Collection<Long>` and not `List<Long>`.
