##Vector

```java
public class Vector<E>
    extends AbstractList<E>
    implements List<E>, RandomAccess, Cloneable, java.io.Serializable{
        ...
    }
```


#### Overall
- The {@code Vector} class implements a growable array of objects. Like an array, it contains components that can be accessed using an integer index. The size of the array can grow or shrink
- Fail-fast. Thus, in the face of concurrent modification, the iterator fails quickly and cleanly, rather than risking arbitrary, non-deterministic behavior at an undetermined time in the future.

#### Attributes
- `Object[] elementData`: the array buffer
- `int capacityIncrement`: the capacity of the vector is doubled each time if this value is less or equal to zero

#### Methods
- `copyInto`, notice the **usage of `System.arraycopy`**
```java
public synchronized void copyInto(Object[] anArray) {
        System.arraycopy(elementData, 0, anArray, 0, elementCount);
    }
```
- `trimToSize`, notice the **usage of `Arrays.copyof`**
```java
public synchronized void trimToSize() {
        modCount++;
        int oldCapacity = elementData.length;
        if (elementCount < oldCapacity) {
            elementData = Arrays.copyOf(elementData, elementCount);
        }
    }
```
－ `grow()`, which grows the size of the vector, also calls `Arrays.copyOf()`