# The Problems

## String

Strings in Java are immutable, so there is no need to create a new object for them. Instead use:

```java
String myString = someObject.toString();
```

## Boolean

`boolean` is a primitive, so it can be assigned directly to a `Boolean` object like this:

```java
Boolean myBoolean = true;
```

Which is syntactic suger for:

```java
Boolean myBoolean = Boolean.valueOf(true);
```

Last, if the value is hard-coded, you should use the `static` member:

```java
Boolean myBoolean = Boolean.TRUE;
```
