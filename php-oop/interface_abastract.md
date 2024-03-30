## Abstract Class
An abstract class is a class that cannot be instantiated on its own; it serves as a blueprint for other classes. Abstract classes can contain both regular and abstract methods. Abstract methods are declared without an implementation and must be implemented by any concrete subclass that extends the abstract class. Abstract class have `Abstract Methode` or `Non Abstract Methode` if we want add methode body in abstract class.
```
abstract class Shape {
    protected $color;
    
    public function __construct($color) {
        $this->color = $color;
    }

    abstract public function getArea();
}

class Circle extends Shape {
    protected $radius;

    public function __construct($color, $radius) {
        parent::__construct($color);
        $this->radius = $radius;
    }

    public function getArea() {
        return pi() * pow($this->radius, 2);
    }
}

$circle = new Circle("red", 5);
echo $circle->getArea(); // Output: 78.539816339745

```

## Interface:
An interface defines a contract that classes can implement. It contains only method signatures without any implementation. Classes that implement an interface must provide an implementation for all methods declared in the interface.

`Interface just decler methode sign.`

```
interface Shape {
    public function getArea();
}

class Circle implements Shape {
    protected $color;
    protected $radius;

    public function __construct($color, $radius) {
        $this->color = $color;
        $this->radius = $radius;
    }

    public function getArea() {
        return pi() * pow($this->radius, 2);
    }
}

$circle = new Circle("red", 5);
echo $circle->getArea(); // Output: 78.539816339745

```

In summary, abstract classes are used when you want to provide a common base for related classes, while interfaces are used to define a contract that multiple unrelated classes can implement.

**Note: For Abstract class must be used Abstract methode in extanded class. For interfaces all methodes must be used in implementes classes.**