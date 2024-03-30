## Final class
In PHP, you can define a class as `final` to prevent it from being extended by other classes. When a class is marked as `final`, it means that it cannot be subclassed or extended further. This can be useful when you want to enforce that a class should not have any child classes.

```
final class FinalClass {
    public function hello() {
        echo "Hello from FinalClass!";
    }
}

// Attempting to extend the final class will result in a fatal error
// class SubClass extends FinalClass {
// }
// Fatal error: Class SubClass may not inherit from final class (FinalClass) in ...

$obj = new FinalClass();
$obj->hello(); // Output: Hello from FinalClass!
```

Use `final` classes when you want to prevent further extension or inheritance of a class to ensure that its behavior remains `unchanged` and `its functionality is not altered by subclasses`.