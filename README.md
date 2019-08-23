### persistent-collection
---
https://pcollections.org/

.php
https://github.com/doctrine/orm/blob/master/lib/Doctrine/ORM/PersistentCollection.php


```java
Collection x2 = new HashSet(x);
x2.add(e);

PCollection y2 = y.plus(e);

import org.pcollections.*;

public class Example {
  public static void main(String... args) {
    PSet<String> set = HashTreePSet.empty();
    set = set.plus("something");
    
    System.out.print(set);
    System.out.println(set.plus("something else"));
    System.out.println(set);
  }
}
```

```
```

```php

```


