# The Code

```java
public String getOlderstPersonName() {
    List<Person> list = null;
    try {
        list = Lists.newArrayList(personDao.getAllPersons());
    } catch (Exception e) {
        LOG.error("error getting persons", e);
    }
    if (list == null || list.isEmpty()) {
        return null;
    }
    Collections.sort(list, (p1, p2) -> ((Short) p2.getAge()).compareTo(p1.getAge()));

    return list.get(0).getName();
}
```
