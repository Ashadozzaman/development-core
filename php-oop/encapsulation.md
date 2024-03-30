```
class Car {
    private $brand;
    private $model;

    public function __construct($brand, $model) {
        $this->brand = $brand;
        $this->model = $model;
    }

    public function getBrand() {
        return $this->brand;
    }

    public function getModel() {
        return $this->model;
    }
}

$car = new Car("Toyota", "Camry");
echo "Brand: " . $car->getBrand() . "\n";
echo "Model: " . $car->getModel() . "\n";
```
In this example, we have a Car class with private properties $brand and $model. These properties are encapsulated within the class, meaning they cannot be accessed directly from outside the class. To access the values of these properties, we provide public getter methods getBrand() and getModel().