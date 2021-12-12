# `JDK-1.8`源码阅读
## 集合框架
### `ArrayList`
```test
transient Object[] elementData; 
private int size;
```
> 底层为`Object`数组。内部操作的基本都是这个数组和这个整数，
elementData会随着实际元素个数的增多而重新分配，而size则始终记录实际的元素个数。
- 数组扩容(1.5倍)
```text
private void grow(int minCapacity) {
        // overflow-conscious code
        int oldCapacity = elementData.length;
        //新的数组容量，右移一位，相当与除以2
        int newCapacity = oldCapacity + (oldCapacity >> 1);
        if (newCapacity - minCapacity < 0)
            newCapacity = minCapacity;
        if (newCapacity - MAX_ARRAY_SIZE > 0)
            newCapacity = hugeCapacity(minCapacity);
        // minCapacity is usually close to size, so this is a win:
        elementData = Arrays.copyOf(elementData, newCapacity);
}
```