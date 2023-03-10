# Q. Internal working of Hashmap in java

In Java, a HashMap is a class that implements the Map interface and stores key-value pairs. It uses a
hash table to store the keys, which allows for efficient insertion, deletion, and lookup operations.

Here's how HashMap works internally:

+ When you create a HashMap, you can specify the initial capacity and load factor. The capacity is the
number of buckets in the hash table, and the load factor is a measure of how full the hash table is
allowed to get before it is resized.

+ When you add a key-value pair to the HashMap, the key is passed through a hash function, which
produces a hash code. This hash code is then used to determine which bucket in the hash table the
key-value pair should be stored in.

+ If there are multiple key-value pairs that hash to the same bucket, they are stored in a linked list
within that bucket. This is known as a collision.

+ To retrieve a value from the HashMap, you pass the key to the get method, which uses the same hash
function to determine which bucket to look in. It then searches the linked list within that bucket for
the key-value pair and returns the value if it is found.

+ If the HashMap becomes too full (i.e., the load factor exceeds the specified threshold), it is
automatically resized to a larger capacity and all of the key-value pairs are rehashed and reinserted
into the new, larger hash table.

Overall, HashMap provides fast insertion, deletion, and lookup operations, making it a useful data
structure for many types of applications.

****************************************************************************************************************

# Q. What is the importance of equals and hashcode method in Hashmap.

The equals and hashCode methods are important in HashMap because they are used to determine whether two
keys are equal and to determine the bucket in which a key-value pair is stored.

The equals method is used to determine whether two keys are equal. When you call the put method of a
HashMap and pass it a key and a value, the HashMap will first call the equals method on the key to see if
it is equal to any other keys that are already in the map. If the key is equal to an existing key, the
HashMap will replace the old value with the new value. If the key is not equal to any existing keys, the
HashMap will add a new key-value pair to the map.

The hashCode method is used to determine the bucket in which a key-value pair is stored. When you call the
put method of a HashMap, the HashMap will call the hashCode method on the key to produce a hash code. It
will then use the hash code to determine which bucket in the hash table the key-value pair should be
stored in.

It's important to override the equals and hashCode methods correctly when using a HashMap, because if they
are not implemented correctly, the HashMap may not function as expected. For example, if the equals method
does not correctly determine when two keys are equal, the HashMap may not be able to find and replace the
old value when a new value is added for an existing key. Similarly, if the hashCode method does not
produce a unique hash code for each key, multiple keys may end up being stored in the same bucket, leading
to poor performance.

****************************************************************************************************************

# Q. what is load factor of hashmap. Explain in detail.

The load factor of a HashMap is a measure of how full the hash table is allowed to get before it is
resized to a larger capacity. It is a floating point number between 0 and 1, and it is specified when
the HashMap is created.

For example, if the load factor is 0.75 and the HashMap has a capacity of 10 buckets, it will be resized
to a larger capacity once the number of key-value pairs in the HashMap exceeds 7.5 (0.75 * 10).
The purpose of the load factor is to control the size of the hash table and the number of
collisions (i.e., the number of key-value pairs that hash to the same bucket).

A lower load factor can lead to fewer collisions and better performance, but it also means that the
hash table will be resized more frequently, which can be costly in terms of time and space. On the
other hand, a higher load factor can lead to more collisions and poorer performance, but it also
means that the hash table will be resized less frequently, which can be more efficient.

It's important to choose an appropriate load factor for your HashMap based on the expected number of
key-value pairs and the performance requirements of your application. A common choice is 0.75, which
provides a good balance between performance and efficiency.

****************************************************************************************************************

# Q. What we need to do if our key is some custom class in hashmap?

If you want to use a custom class as the key in a HashMap, you will need to override the equals and
hashCode methods in your custom class. These methods are used by the HashMap to determine whether two
keys are equal and to determine the bucket in which a key-value pair is stored.

Here's an example of how you might override the equals and hashCode methods in a custom class:

```
class CustomKey {
    private int id;
    private String name;

    public CustomKey(int id, String name) {
        this.id = id;
        this.name = name;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        CustomKey that = (CustomKey) o;
        return id == that.id &&
                Objects.equals(name, that.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(id, name);
    }
}
```

In this example, the equals method compares the id and name fields of two CustomKey objects to determine
if they are equal, and the hashCode method uses the Objects.hash method to generate a hash code based on
the id and name fields.

Once you have overridden the equals and hashCode methods in your custom class, you can use it as the key
in a HashMap like this:
```
Map<CustomKey, Integer> map = new HashMap<>();
map.put(new CustomKey(1, "a"), 1);
map.put(new CustomKey(2, "b"), 2);
```
****************************************************************************************************************

# Q. Can you explain equals method code in detail of above customerKey class.

```
@Override
public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    CustomKey that = (CustomKey) o;
    return id == that.id &&
            Objects.equals(name, that.name);
}
```

Certainly! Here is an explanation of the equals method code for the CustomKey class:

```
@Override
public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    CustomKey that = (CustomKey) o;
    return id == that.id &&
            Objects.equals(name, that.name);
}
```
The equals method has the following logic:

+ It checks if this object (i.e., the current CustomKey object) is the same as the object passed as an
argument (o). If they are the same, it returns true. This check is done using the == operator.

+ It checks if the object passed as an argument is null or if it is not an instance of the CustomKey
class. If either of these conditions is true, it returns false. This check is done using the null keyword
and the getClass method.

+ It casts the object passed as an argument to a CustomKey object and assigns it to a local variable
that.

+ It compares the id fields of this object and the that object using the == operator. If they are not
equal, it returns false.

+ It uses the Objects.equals method to compare the name fields of this object and the that object.
If they are not equal, it returns false. If both the id and name fields are equal, it returns true.

Overall, the equals method compares the id and name fields of two CustomKey objects and returns true if
they are equal, and false otherwise. It is used by the HashMap to determine whether two keys are equal.

****************************************************************************************************************

# Q. What is drawback of above equals method.

the if (o == null || getClass() != o.getClass()) return false; statement is not sufficient to check if
the object passed as an argument is null or if it is not an instance of the CustomKey class. This is
because the getClass method returns the runtime class of an object, which may be a subclass of the
CustomKey class.

For example, consider the following code:
```
class SubclassKey extends CustomKey {
    // ...
}
```
If you create an instance of SubclassKey and pass it to the equals method of a CustomKey object, the
getClass method will return SubclassKey.class, which is not equal to CustomKey.class. Therefore, the
equals method will return false, even though the two objects may be considered equal according to the
logic of the equals method.

To correctly check if the object passed as an argument is null or if it is not an instance of the
CustomKey class, you should use the instanceof operator instead of the getClass method. Here is the
revised equals method:
```
@Override
public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || !(o instanceof CustomKey)) return false;
    CustomKey that = (CustomKey) o;
    return id == that.id &&
            Objects.equals(name, that.name);
}
```
With this revised equals method, the if (o == null || !(o instanceof CustomKey)) return false; statement
will correctly check if the object passed as an argument is null or if it is not an instance of the
CustomKey class.

****************************************************************************************************************

# Q. why  if (this == o) return true; is not enough. this will ultimately compare object. right?

if (this == o) return true; statement is sufficient to check if this object (i.e., the current CustomKey
object) is the same as the object passed as an argument (o). If they are the same, the equals method
should return true, as required by the contract of the equals method.

However, the equals method is also required to return true if the two objects being compared have the
same values for their fields, even if they are not the same object. This is why the CustomKey class
also compares the values of the id and name fields in its equals method.

For example, consider the following code:
```
CustomKey key1 = new CustomKey(1, "a");
CustomKey key2 = new CustomKey(1, "a");
if (key1.equals(key2)) {
    System.out.println("key1 and key2 are equal");
}
```

In this example, key1 and key2 are not the same object, but they have the same values for their id and
name fields. Therefore, the equals method should return true when called on key1 with key2 as the
argument.

If the equals method only used the if (this == o) return true; statement, it would always return false
for key1 and key2, because they are not the same object. This is why the CustomKey class also compares
the values of the id and name fields in its equals method.

****************************************************************************************************************



