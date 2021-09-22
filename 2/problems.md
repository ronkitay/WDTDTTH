# The Problems

There are several issues with this code:

- The code does a lot of processing on the client side (The JVM) that could be done on server side (the Data Base).  
  The code also assumes that all the list can be loaded into memory – which may not be the case.  
  An example code using the database’s abilities would look like this:

  ```java
  public String getOlderstPersonName() {
    try {
        Person olderstPerson = personDao.getOldestPerson());
        return olderstPerson == null ? null : olderstPerson.getName();
    } catch (Exception e) {
        LOG.error("error getting persons", e);
        return null;
    }
  }
  ```

- The API returns null when there are no persons / an error occurred – returning an `Optional<String>` may be more appropriate.
- The codes performs a *sort* on the data ( `O(N*log(N))` ) when it can use *max* ( `O(N)` ) instead (and also duplicates the array to avoid sorting the original data)  
  An example code using max would look like this:

  ```java
  public String getOlderstPersonName() {
      List<Person> list = null;
      try {
          list = Lists.newArrayList(personDao.getAllPersons());
          if (list != null) {
            return list.stream().
                    .max(Comparator.comparingInt(Person::getAge))
                    .map(Person::getName);
          }
      } catch (Exception e) {
          LOG.error("error getting persons", e);
      }

      return Optional.empty();
  }
  ```
