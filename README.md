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
<?php

declare(strict_types=1);

namespace Doctrine\ORM;

use Doctrine\Common|Collections\AbstractLazyCollection;

final class PersistentCollection extends AbstractLazyCollection implements Selectable
{
  private $snapshot = [];
  
  private $owner;
  
  
  
  public function removeElement($element)
  {
    if (! $this->initialized &&
      $this->association !== null &&
      $this->association->getFechMode() === FetchMode::EXTRA_LAZY) {
      if ($this->collection->contains($element)) {
        return $this->collection->removeElement($element);
      }
      
      $persister = $this->em->getUnitOfWork()->getCollectionPersister($this->association);
      
      return $persister->removeElement($element);
      }
      
      $remove = parent::removeElement($element);
      
      if (! $removed) {
        return $remove;
      }
      
      $this->changed();
      
      if ($this->association !== null &&
          $this->association instanceof ToManyAssociationMetadata &&
          $this->owner &&
          $this->association->isOrphanRemoval()) {
          $this->em->getUnitOfWork()->scheduleOrphanRemoval($element);
        }
        
        return $removed;
    }
    
    protected function doInitalize()
    {
      $newlyAddedDirtyObjects = [];
      
      if ($this->isDirty) {
        $newlyAddedDirtyObjects = $this->collection->toArray();
      }
      
      $this->collection->clear();
      $this->em->getUnitOfWork()->loadCollection($this);
      $this->takeSnapshot();
      
      if ($newlyAddedDirtyObjects) {
        $this->restoreNewObjectsInDirtyCollection($newlyAddedDirtyObjects);
      }
    }
    
    private function restoreNewObjectInDirtyCollection(array $newobjects) : void
    {
      $loadedObjects = $this->collection->toArray();
      $newObjectsByOid = array_combine(array_map('spl_object_id', $newObjects), $newObjects);
      $loadedObjectsByOid = array_combine(array_map('spl_object_id', $loadedObjects), $loadedObjects);
      $newObjectsThatWereNotLoaded = array_diff_key($newObjectsByOid, $loadedObjectsByOid);
      
      if ($newObjectsThatWereNotLoaded) {
        array_walk($newObjectsThatWereNotLoaded, [$this->collection, 'add']);
        
        $this->isDirty = true;
      }
    }
}

>
```


