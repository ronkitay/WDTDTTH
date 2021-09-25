# The Code

```java
public class DateFormatter {
    public static long formatToEpoch(String format, String dateAsString) {
        SimpleDateFormat dateFormat = new SimpleDateFormat(format);
        return dateFormat.parse(dateAsString).getTime();
    }
}

public class DateFormatterTest {
    @Test
    public void test_formatToEpoch() {
        String format = "yyyy-MM-dd HH:mm:ss";
        String dateAsString = "2020-01-12 10:00:00";

        SimpleDateFormat dateFormat = new SimpleDateFormat(format);
        long expectedValue = dateFormat.parse(dateAsString).getTime();

        assertEquals(expectedValue, DateFormatter.formatToEpoch(format, dateAsString));
    }
}
```
