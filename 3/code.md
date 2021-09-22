# The Code

```java
class MyComparator implements java.util.Comparator<MyObject> {
        @Override
        public int compare(MyObject o1, MyObject o2) {
            return ((Long) o2.creationDate()).compareTo(o1.creationDate());
        }
};

...

public String stringify(int i) {
    return new Integer(i).toString();
}

...

public void setMode(int mode) {
    this.mode = new Integer(mode).shortValue();
}
```
