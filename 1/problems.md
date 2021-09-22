# The Problems

There were 3 basic issues in this code:

- The `assertTrue(true)` at the end is redundant for two reasons:
  - If a test reached this point – it passed, no need for any further actions.
  - It will always be true and will never throw an AssertionError – so it is completely useless.
- The `assertTrue(false)` is a very bad practice since:
  - It does not help debug why a test failed
  - It is not needed as Junit knows to fail when an unplanned exception is thrown.
- Continuing on #2 – the entire `try`/`catch` block is redundant, as Junit knows to fail a test when an exception is thrown.

The simplest alternative to this test would be:

```java
@Test
public void testSomething() {
    // ... some test code here
}
```

Obviously, the “some test code here” should contain an assertion of some sort in most cases – the only time we are OK with no assertions is when a lack of an exception is a success.

If you want to add some information – you can do this instead:

```java
@Test
public void testSomething() {
    try {
        // ... some test code here
    }
    catch (Exception ex) {
        fail("Expected a result, but threw: " + ex.getMessage());
    }
}
```

This is still redundant, but at least uses the correct APIs …
