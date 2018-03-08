## AbstractMap
```java
public abstract class AbstractMap<K,V> implements Map<K,V>{}
```

#### Overall
- AbstractMap provides a skeletal implementation of the `Map` interface to minimize the effort required to implement this interface.
- The `transient` keyword in Java is used to indicate that a field should not be serialized.

#### Methods
- `containsValue()` allows `null` value. It iterates through the `entrySet()` iterator.
```java
public boolean containsValue(Object value) {
        Iterator<Entry<K,V>> i = entrySet().iterator();
        if (value==null) {
            while (i.hasNext()) {
                Entry<K,V> e = i.next();
                if (e.getValue()==null)
                    return true;
            }
        } else {
            while (i.hasNext()) {
                Entry<K,V> e = i.next();
                if (value.equals(e.getValue()))
                    return true;
            }
        }
        return false;
    }
```
- `get` methods actually iterate the whole entrySet in the implementation in `abstractMap`. But many implementations will **override** this method.
- `toString()` returns the string representation of the map *useful*!
```java
public String toString() {
        Iterator<Entry<K,V>> i = entrySet().iterator();
        if (! i.hasNext())
            return "{}";

        StringBuilder sb = new StringBuilder();
        sb.append('{');
        for (;;) {
            Entry<K,V> e = i.next();
            K key = e.getKey();
            V value = e.getValue();
            sb.append(key   == this ? "(this Map)" : key);
            sb.append('=');
            sb.append(value == this ? "(this Map)" : value);
            if (! i.hasNext())
                return sb.append('}').toString();
            sb.append(',').append(' ');
        }
    }
```