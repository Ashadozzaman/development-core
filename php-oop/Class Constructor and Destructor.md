## Constructor:
A constructor is a special method in a class that gets called automatically when an object of the class is created.

## Destructor:
A destructor is a special method in a class that gets called automatically when an object is destroyed or goes out of scope.

```
class Connection {
    public function __construct() {
        echo "Connected to database.";
    }

    public function __destruct() {
        echo "Connection closed.";
    }
}

$connection = new Connection();
// Other operations...
unset($connection); // Manually destroying the object

```