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