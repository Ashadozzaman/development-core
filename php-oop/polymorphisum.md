### The basic of polymorphisum is inharitance and override method.

When we create subclass according parent class, we override parent class function to child class this is `polymosphisum`.

```
abstract class Animal {
    abstract public function makeSound();
}

class Dog extends Animal {
    public function makeSound() {
        echo "Woof! Woof!\n";
    }
}

class Cat extends Animal {
    public function makeSound() {
        echo "Meow! Meow!\n";
    }
}
```