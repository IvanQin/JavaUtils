## HashSet

```java
public class HashSet<E>
    extends AbstractSet<E>
    implements Set<E>, Cloneable, java.io.Serializable{}
```

#### Overall
- Actually the `HashSet` is a **`HashMap` instance**!
- Iterating over this set requires time proportional to the sum of the <tt>HashSet</tt> instance's size (the number of elements) **plus** the "capacity" of the backing <tt>HashMap</tt> instance (the number of buckets).  Thus, it's very important **not** to set the initial capacity too high (or the load factor too low) if iteration performance is important.
- HashSet is **NOT** thread-safe.
- If the set is modified at any time after the iterator is created, in any way except through the iterator's own <tt>remove</tt> method, it will **immediately** throw a `ConcurrentModificationException`.

#### Attributes
- A map
```java
    private transient HashMap<E,Object> map;
```
- dummy value
```java
// Dummy value to associate with an Object in the backing Map
    private static final Object PRESENT = new Object();
```

#### Methods 
- constructor (default initial capacity (16) and load factor (0.75))
```java
public HashSet() {
        map = new HashMap<>();
    }
```
- an interesting constructor used only by `LinkedHashSet`.
    + notice no explicit `public` before the constructor name
    + boolean variable `dummy` is used to distinguishes this constructor from others
```java
/**
     * Constructs a new, empty linked hash set.  (This package private
     * constructor is only used by LinkedHashSet.) The backing
     * HashMap instance is a LinkedHashMap with the specified initial
     * capacity and the specified load factor.
     *
     * @param      initialCapacity   the initial capacity of the hash map
     * @param      loadFactor        the load factor of the hash map
     * @param      dummy             ignored (distinguishes this
     *             constructor from other int, float constructor.)
     * @throws     IllegalArgumentException if the initial capacity is less
     *             than zero, or if the load factor is nonpositive
     */
    HashSet(int initialCapacity, float loadFactor, boolean dummy) {
        map = new LinkedHashMap<>(initialCapacity, loadFactor);
    }
```
- private method `writeObject`
```java
/**
     * Save the state of this <tt>HashSet</tt> instance to a stream (that is,
     * serialize it).
     *
     * @serialData The capacity of the backing <tt>HashMap</tt> instance
     *             (int), and its load factor (float) are emitted, followed by
     *             the size of the set (the number of elements it contains)
     *             (int), followed by all of its elements (each an Object) in
     *             no particular order.
     */
    private void writeObject(java.io.ObjectOutputStream s)
        throws java.io.IOException {
        // Write out any hidden serialization magic
        s.defaultWriteObject();

        // Write out HashMap capacity and load factor
        s.writeInt(map.capacity());
        s.writeFloat(map.loadFactor());

        // Write out size
        s.writeInt(map.size());

        // Write out all elements in the proper order.
        for (E e : map.keySet())
            s.writeObject(e);
    }
```
