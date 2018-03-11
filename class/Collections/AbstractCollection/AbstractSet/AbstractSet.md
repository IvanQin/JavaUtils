## AbstractSet
```java
public abstract class AbstractSet<E> extends AbstractCollection<E> implements Set<E> {
    ...
}
```

#### Overall

- AbstractSet provides a skeletal implementation of the `Set` interface to minimize the effort required to implement this interface.
- Abstract class can have non-abstract methods.

#### Methods 
- `equals` methods, notice `instanceof`
```java
  public boolean equals(Object o) {
        if (o == this)
            return true;

        if (!(o instanceof Set))
            return false;
        Collection<?> c = (Collection<?>) o;
        if (c.size() != size())
            return false;
        try {
            return containsAll(c);
        } catch (ClassCastException unused)   {
            return false;
        } catch (NullPointerException unused) {
            return false;
        }
    }
```

- `hashCode` method. The hash code of a set is defined to be the **sum** of the hash codes of the elements in the set
```java
public int hashCode() {
        int h = 0;
        Iterator<E> i = iterator();
        while (i.hasNext()) {
            E obj = i.next();
            if (obj != null)
                h += obj.hashCode();
        }
        return h;
    }
```

- `removeAll` method
    + iterate over the **smaller** set
    + notice there are two `remove()`, one from `set`'s (implement in class `AbstractCollection`) and another from `iterator`'s
```java
public boolean removeAll(Collection<?> c) {
        Objects.requireNonNull(c);
        boolean modified = false;

        if (size() > c.size()) {
            for (Iterator<?> i = c.iterator(); i.hasNext(); )
                modified |= remove(i.next());
        } else {
            for (Iterator<?> i = iterator(); i.hasNext(); ) {
                if (c.contains(i.next())) {
                    i.remove();
                    modified = true;
                }
            }
        }
        return modified;
    }
```
