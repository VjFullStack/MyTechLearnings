# How HashSet Works internally in Java. 

# Ans :

In Java, a HashSet is a collection that stores unique elements by hashing them. The internal working of HashSet can be summarized as follows:

* When a HashSet is created, an internal array is created to store the elements.

```
HashSet<String> set = new HashSet<String>();
```
* When an element is added to the HashSet, its hash code is calculated using the hashCode() method of the object. The hash code is then used to determine the index in the internal array where the element should be stored.
```
String element = "hello";
int hashCode = element.hashCode();
int index = hashCode % set.length;
```

* If the index is empty, the element is stored in that index. If the index already contains an element, the new element is compared with the existing element using the equals() method. If the two elements are equal, the new element is not added. If they are not equal, the HashSet uses a technique called "chaining" to store the two elements in the same index as a linked list.
```
if (set[index] == null) {
    set[index] = element;
} else {
    boolean found = false;
    Node<String> current = set[index];
    while (current != null) {
        if (current.value.equals(element)) {
            found = true;
            break;
        }
        current = current.next;
    }
    if (!found) {
        current.next = new Node<String>(element);
    }
}
```

* When an element is removed from the HashSet, its hash code is used to determine the index in the internal array where the element should be located. If the index contains a linked list, the equals() method is used to find the element in the list and remove it.
```
if (set[index] != null) {
    Node<String> previous = null;
    Node<String> current = set[index];
    while (current != null) {
        if (current.value.equals(element)) {
            if (previous == null) {
                set[index] = current.next;
            } else {
                previous.next = current.next;
            }
            break;
        }
        previous = current;
        current = current.next;
    }
}
```
* The size of the HashSet is calculated by counting the number of elements in the internal array.
```
int size = 0;
for (int i = 0; i < set.length; i++) {
    Node<String> current = set[i];
    while (current != null) {
        size++;
        current = current.next;
    }
}
```
* The capacity of the HashSet is determined by the initial capacity specified when the HashSet is created. If the number of elements in the HashSet exceeds a certain threshold, the capacity is increased by creating a new internal array with a larger size and rehashing all the elements.
```
if (size > capacity * loadFactor) {
    int newCapacity = capacity * 2;
    HashSet<String> newSet = new HashSet<String>(newCapacity);
    for (int i = 0; i < set.length; i++) {
        Node<String> current = set[i];
        while (current != null) {
            newSet.add(current.value);
            current = current.next;
        }
    }
    set = newSet;
    capacity = newCapacity;
}

```

---