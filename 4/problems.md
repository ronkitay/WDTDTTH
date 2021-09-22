# The Problems

The major issue here is the incorrect manner in which the iteration over all the entries of the map is performed. The major problem is in the `dataById.get(id)` which is redundant and adds time complexity to the solution (in Theory it is a constant time for HashMaps, but not so for other implementations).

This code has several evolutions to make it as clean as possible:

## Step #1 – lose the iterator

Since java 5 0 java has a syntactic sugar for iterators which is the foreach loop (for (Type variable : collection))
Using it cleans up the code a bit:

```java
private void handleAllData() {
    Map<String, SomeData> dataById = getData();

    while (String id : dataById.keySet()) {
        SomeData someData = dataById.get(id);
        handleData(id, someData);
    }
}
```

## Step #2 – use the `entrySet`

Using the iterator of the `entrySet` instead of the `keySet` saves you the time of retrieving each value by its key

```java
private void handleAllData() {
    Map<String, SomeData> dataById = getData();

    while (Map.Entry<String, SomeData> idAndData : dataById.entrySet()) {
        handleData(idAndData.getKey(), idAndData.getValue());
    }
}
```

## Step #3 – be functional


Since java 8 – the `foreach` syntactic sugar has a `lambda` based replacement which makes the code much clearer:

```java
private void handleAllData() {
    Map<String, SomeData> dataById = getData();

    dataById.forEach( (key, value) -> handleData(key, value) );
    }
}
```

## Step #4 – remove redundancies in the lambda by using a function refenrece.

The definition of the `forEach` method receives a `BiConsumer` which is a functional interface receiving (“consuming”) two arguments (“Bi”)

So we can just pass it a reference to the handleData function which is in fact a valid BiConsumer:

```java
private void handleAllData() {
    Map<String, SomeData> dataById = getData();

    dataById.forEach( this::handleData );
    }
}
```

Naturally we need to be certain dataById is never null but that is a topic for another lesson.
