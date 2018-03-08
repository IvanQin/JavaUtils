## Map
```java
public interface Map<K,V> {
    ...
}
```

#### Overall
- Unlike `Set`, `Map` does not extends `Collection`

#### Methods 
- `boolean containsKey(Object key)`. `null` key is allowed but at most one.
```java
boolean containsKey(Object key);
```
- `getOrDefault()` java 1.8
```java
default V getOrDefault(Object key, V defaultValue) {
        V v;
        return (((v = get(key)) != null) || containsKey(key))
            ? v
            : defaultValue;
    }
```
- `putIfAbsent()` java 1.8
```java
default V putIfAbsent(K key, V value) {
        V v = get(key);
        if (v == null) {
            v = put(key, value);
        }

        return v;
    }
```
- `replace()` java 1.8
```java
default boolean replace(K key, V oldValue, V newValue) {
        Object curValue = get(key);
        if (!Objects.equals(curValue, oldValue) ||
            (curValue == null && !containsKey(key))) {
            return false;
        }
        put(key, newValue);
        return true;
    }
```
