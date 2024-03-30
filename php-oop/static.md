## Static

- Static properties and methods are accessed using `::` operator.
- They belong to the class itself, not to instances of the class. `So, you can access them without creating an instance of the class`.

```
class Counter {
    public static $count = 0;

    public static function increment() {
        self::$count++;
    }

    public static function getCount() {
        return self::$count;
    }
}

// Accessing static property directly
echo Counter::$count; // Output: 0

// Incrementing the counter using static method
Counter::increment();
Counter::increment();
Counter::increment();

// Accessing static property after incrementing
echo Counter::$count; // Output: 3

// Accessing count using static method
echo Counter::getCount(); // Output: 3

```