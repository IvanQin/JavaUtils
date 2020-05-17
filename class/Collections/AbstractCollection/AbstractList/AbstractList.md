## AbstractList

```java
public abstract class AbstractList<E> extends AbstractCollection<E> implements List<E> {
    ...
}
```


#### Overall
- This class provides a skeletal implementation of the {@link List} interface to minimize the effort required to implement this interface backed by a "random access" data store (such as an array).

#### Methods 
- `set()`. **Interesting** thing here, why this method only throws an Exception, because set should be overridden in any non-abstract children class. Thus if this method is called, the child class has not `set()` method.
```java
public E set(int index, E element) {
        throw new UnsupportedOperationException();
    }
```
- In this class, a class Itr and a class ListItr extends to it has been created.
    + use two variables to check concurrent modification
    + **ALL** the functions like `removeRange()` calls the iterator's `remove` and the iterators `remove` calls the class's `remove` which is not implemented in this abstract class.
- `hashCode()` see how to implement the hash code of list
```java

    /**
     * Returns the hash code value for this list.
     *
     * <p>This implementation uses exactly the code that is used to define the
     * list hash function in the documentation for the {@link List#hashCode}
     * method.
     *
     * @return the hash code value for this list
     */
    public int hashCode() {
        int hashCode = 1;
        for (E e : this)
            hashCode = 31*hashCode + (e==null ? 0 : e.hashCode());
        return hashCode;
    }
```
