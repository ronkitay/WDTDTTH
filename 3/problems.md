# The Problems

In all theese  examples there is a common problem of `Boxing` of primitives.

`Boxing`/`UnBoxing` is the act of converting a primitive to its object type or vise-versa. E.g. int -> Integer, or Boolean -> boolean.

These steps are in many cases redundant and consume unneeded CPU. (Don’t worry if you do it in low throughput scenarios like some management service or during your process init, but worry if you do it for every record in a map-reduce/spark job).

In the first example – `o2.creationDate()` is a `long` and we cast it to a `Long` – what the compiler does for you implicitly when you do it is replace the code with `Long.valueOf(o2.creationDate())`.

Note that `valueOf` has some optimization in it – but in most cases it will create a new object:

```java
public static Long valueOf(long l) {
    final int offset = 128;
    if (l >= -128 && l <= 127) { // will cache
        return LongCache.cache[(int)l + offset];
    }
    return new Long(l);
}
```

In the above case, `Long.compare(o2.createDate(), o1.createDate())` would have saved two object creations.

In the second and third examples - `new Integer(i)` and `new Integer(mode)` are both redundant object creations, but for different reasons:

- `new Integer(i).toString()` will invoke the static method `Integer.toString(value)` with the internal value of the `int` boxed within the `Integer` – so we created the object for no reason what so ever here.
- `Integer.valueOf(i)` would have saved a potential object creation if the value was within the cached range – however, the `toString` conversion does not require an object but a primitive.
- `new integer(mode).shortValue()` is also redundant as it basically does `(short)mode` but with an extra object creation.

So to summarize – when you have a primitive you should:

- Check if you can use it as is without converting to an object – it is faster and in most cases more readable.
- Use the JVM’s caching to prevent unneeded object creations – e.g. `Boolean.valueOf(someBoolean)` vs `new Boolean(someBoolean)`
- Don’t use `new SomeClass(thePrimitiveValue)` to convert a primitive to an object.
