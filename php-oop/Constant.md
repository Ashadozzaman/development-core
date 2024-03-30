## Constants
Constants are defined using the `const` keyword inside classes. `Constants` are accessed using the scope resolution operator `::`.
```
class MathOperations {
    const PI = 3.14159;

    public function calculateArea($radius) {
        return self::PI * $radius * $radius;
    }
}

$math = new MathOperations();
echo $math::PI; // Output: 3.14159
echo MathOperations::PI; // Output: 3.14159
echo $math->calculateArea(5); // Output: 78.53975

```
**Note:** Constants are useful for storing values **that do not change** and are relevant to a class.