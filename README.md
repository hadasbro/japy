
## Data structures

### List comprehension

#### Python
```python

# Example 1
list_using_comp = [var**2 for var in range(1, 10) if x%2 == 0] 
# [4, 16, 36, 64]

# Example 2
char_list = ['', '    a','b', '\t']
[x.strip() for x in char_list if x.strip()]
# ['a', 'b']

# Example 3
nums = [1, 2, 3, 4]
fruit = ["Apples", "Peaches", "Pears", "Bananas"]
[(i, f) for i in nums for f in fruit if f[0] == "P" if i%2 == 1]
# [(1, 'Peaches'), (1, 'Pears'), (3, 'Peaches'), (3, 'Pears')]
```

#### Java

in Java there is not simple equivalent for Python's syntax. 
We can use Java Streams (Java 8+), additional Java libraries e.g. https://github.com/farolfo/list-comprehensions-in-java

```java
public class Main {

    public static void main(String[] args) {

        // Example 1
        List<Integer> integers =
                // list of integers from range
                IntStream.range(0, 10).boxed()
                        .filter(n -> n % 2 == 0)
                        .map(n -> Math.pow(n, 2)).map(Double::intValue)
                        .collect(Collectors.toList());

        // [0, 4, 16, 36, 64]

        // Example 2
        // https://github.com/farolfo/list-comprehensions-in-java
        Predicate<Integer> even = x -> x % 2 == 0;

        List<Integer> evens = new ListComprehension<Integer>()
                .suchThat(x -> {
                    x.belongsTo(Arrays.asList(1, 2, 3, 4));
                    x.is(even);
                });
        // evens = {2,4};

    }
}
```


* * *



#### Object encapsulation


#### Python

```python

# !/usr/bin/env python
class Vehicle:
    pass

class Car(Vehicle):

    def __repr__(self):
        return f'Car({[self.__name, self.speed, self._shortname]!r})'

    def __init__(self, name="MyCar", speed=100, shortname="car short", supername="super"):

        # private field
        self.__name = name

        # public field
        self.speed = speed

        # convension from PEP 8 - protected field
        self._shortname = shortname

        # private field decorated by @property
        self.__supername = supername

        # test private method
        self.__privateMethod()

    # setter for private field
    def set_name(self, name):
        self.__name = name + "[setter 1]"

    # getter for private field
    def get_name(self):
        return self.__name + "[getter 1]"

    # getter by property decorator
    @property
    def supername(self):
        return self.__supername + "[getter 2]"

    # setter by property decorator
    @supername.setter
    def supername(self, supername):
        self.__supername = supername + "[setter 2]"
        print(self.__supername)

    # deleter by decorator
    @supername.deleter
    def supername(self):
        del self.__supername

    # private method
    def __privateMethod(self):
        print("__privateMethod")

    # public method
    def publicMethod(self):
        pass

    # public class method (is bound to the class object itself)
    @classmethod
    def giveMeAnyFastCar(cls, speed = 200):
        return cls("Fast Car", speed)

    # static method (knows nothing about the class and just deals with the parameters)
    @staticmethod
    def getSpeedInKmPerHour(speedInMilesPerHour):
        return speedInMilesPerHour * 1.60

```

Test
```python




car = Car()

# get name via getter
print("1. " + car.get_name())
# 1. MyCar[getter 1]

# set via setter
car.set_name("New car 2")

# try to get property normally (ERROR, property is private)
# print("2. " + car.name)

# try to get property "speed" normally (OK, property is public)
print(car.speed)  # 100

# try to get property "_shortname" normally (OK, property is public/protected - bad practice but there is no any error)
print("3. " + car._shortname)  # 3. car short

# try to get private property "supername" normally (OK but property is returned through getter supername()
print("4. " + car.supername)  # 4. super[getter 2]

# try to set private property "supername" normally (OK but property is settled through setter supername()
car.supername = "another super name"  # another super name[setter 2]

# try to run private method (ERROR)
# car.privateMethod()

# try to run public method (OK)
car.publicMethod()

car.publicMethod()  # OK

# class method usage
fast_car = Car.giveMeAnyFastCar(300)
print(fast_car) # Car(['Fast Car', 300, 'car short'])

# static method usage
speed = Car.getSpeedInKmPerHour(100)
print(speed) # 160.0
```

Descriptor example

```pyhton

class Email():

    EMAIL_REGEX = re.compile(
        r"[A-Za-z0-9-_]+(.[A-Za-z0-9-_]+)*@"
        "[A-Za-z0-9-]+(.[A-Za-z0-9]+)*(.[A-Za-z]{2,})"
    )

    """Descriptor class for an email address."""

    def __init__(self):
        self.pool = {}

    def __get__(self, instance, owner):
        print("get Email through descriptor")
        return self.pool.get(instance, 0)

    def __set__(self, instance, email_address):
        if not Email.EMAIL_REGEX.match(email_address):
            raise ValueError
        print("set Email through descriptor")
        self.pool[instance] = email_address


class User:
    email = Email()
    def __init__(self, name, email):
        self.email = email
        self.name = name

# test get/set through descriptor
user = User("Sla", "test@mail.com") # OK (set Email through descriptor)
print(user.email) # OK (get Email through descriptor), result: test@mail.com


```

#### Java

```java
interface VehicleInterface {
    void drive();
}

class Vehicle implements VehicleInterface {
    /**
     * interfaces' method implementation
     */
    public void drive() {}

    /**
     * doSomethingInProtected - Protected method
     *
     * @return boolean
     */
    protected boolean doSomethingInProtected(){
        return true;
    }
}

/**
* Class can be public, private or protected (inner class) or 
* can don't have any modifier
*/
public class Car extends Vehicle {

    /**
     * public static property
     */
    public static int staticProperty = 1;

    /**
     * constant
     */
    public static final char CONSTANT = 'C';

    /**
     * getName - getter for provate property
     *
     * @return
     */
    public String getName() {
        return name;
    }

    /**
     * setName - setter for provate property
     *
     * @param name
     */
    public void setName(String name) {
        this.name = name;
    }

    /**
     * private property name
     * (access only in this class)
     */
    private String name;

    /**
     * property without any modifier
     * (access in the same package, in class and subclasses but only in the same package)
     */
    String supername;

    /**
     * protected property shortname
     * (access in the same package, in class and subclasses in any package)
     */
    protected String shortname;

    /**
     * public property speed
     * (access everywhere, even outside the package)
     */
    public Integer speed = 100;

    /**
     * Constructor
     *
     * @param name
     * @param supername
     * @param shortname
     */
    Car(String name, String supername, String shortname) {

        this.name = name;
        this.supername = supername;
        this.shortname = shortname;

        // call protected method in subclass
        this.doSomethingInProtected();

        // call private (possible only in this class)
        this.doSomethingInPrivate();

        // run static method (outside the object context)
        Car.doSomethingStatically();
    }

    /**
     * Another constructor with different signature
     *
     * @param name
     * @param supername
     */
    Car(String name, String supername) {
        this(name, supername, "Default name");
    }

    /**
     * doSomethingInPublic - Public method
     *
     * @return boolean
     */
    public boolean doSomethingInPublic(){
        return true;
    }

    /**
     * doSomethingInPrivate - Private method
     *
     * @return boolean
     */
    private boolean doSomethingInPrivate(){
        return true;
    }

    /**
     * doSomethingStatically - public static method
     *
     * @return
     */
    public static boolean doSomethingStatically(){
        return true;
    }

}
```

Testing
```java
public class Main {
    public static void main(String[] args) {
        System.out.println("test");

        Car car = new Car("Truck","My great car");

        // set private property through setter
        car.setName("Carname");

        // get private property through getter
        System.out.println(car.getName());

        // access to protected properties (access in the same package, in class and subclasses in any package)
        car.shortname = "Shortname";
        System.out.println(car.shortname); // Shortname

        // access to public property (access everywhere, even outside the package)
        System.out.println(car.speed ); // 100

        // car.doSomethingInPrivate(); // this doesnt work (method is private)

        car.doSomethingInProtected(); // this will work (the same package)

        // call static method in class', not an object context
        Car.doSomethingStatically();

        // call public method in object's context
        car.doSomethingInPublic();

        // use static property
        System.out.println(Car.staticProperty); // 1

        // public constant
        System.out.println(Car.CONSTANT); // C

    }
}
```


Lombok style (@see https://projectlombok.org)

```java

/**
 * CarShort
 *
 * Lombok Style
 * all properties are private and there are Getters and Setters for each one
 * also constructor with required args (see @NonNull annotation)
 */
@Data
class CarShort extends Vehicle {

    public static int staticProperty = 1;
    public static final char CONSTANT = 'C';

    @NonNull // if we want to have this property in "Required args constructor"
    private String name;
    private String supername;
    private String shortname;
    private Integer speed = 100;

}
```

* * *

#### Method signatures

#### Python

Example 1
```python
def f(x, y, w=0, h=0):
    print "position: %s, %s -- shape: %s, %s"%(x, y, w, h)

position = (3,4)
size = {'h': 10, 'w': 20}

>>> f( *position, **size)
position: 3, 4 -- shape: 20, 10
```

Example 2
```python
def f(*args, **kwargs):
    print "the positional arguments are:", args
    print "the keyword arguments are:", kwargs

In [389]: f(2, 3, this=5, that=7)
the positional arguments are: (2, 3)
the keyword arguments are: {'this': 5, 'that': 7}
```

#### Java
Example 1
```java
@Data
class CarAnother extends Vehicle {

    /**
     * doSomething - method with many params of many kinds
     *
     * @param a
     * @param b
     * @param strObject
     * @param car
     * @param vehicles
     * @param anything
     */
    public void doSomething(int a, char b, String strObject, Car car, List<Vehicle> vehicles, Object anything) {

        a += 1;
        strObject.trim();
        car.setName("Newname");
        vehicles.stream().forEach(Vehicle::drive);

    }

    /**
     * doSomething - method with many params - collections and arrays
     *
     * @param vehicles
     * @param colOfVehicles
     * @param integers
     * @param cars
     */
    public void doSomething(Set<Vehicle> vehicles, Collection<? extends Vehicle> colOfVehicles, int[] integers, Car[] cars) {}

    /**
     * doSomethingOnSetsOfVehicles - varargs of sets of vehicles
     *
     * @param setsOfVehicles
     */
    public void doSomethingOnSetsOfVehicles(Set<Vehicle> ... setsOfVehicles) {
        for (Set<Vehicle> setv : setsOfVehicles) {
            System.out.println(setv.toArray());
        }
    }

    /**
     * doSomethingOnManyStrings - varargs with strings
     *
     * @param str
     */
    public void doSomethingOnManyStrings(String ...str) {

        String res = Arrays.stream(str)
                .map(String::trim)
                .collect(Collectors.joining(" "));

        System.out.println(res);

    }

    /**
     * joinDictionaries - join dictionaries, no matter how many
     * here we have varargs of maps and filter predicate as a positional parameter
     *
     * @param filter
     * @param dicts
     */
    public void joinDictionaries(Predicate<Map<String, Integer>> filter, Map<String, Integer>...dicts) {

        Map<String, Integer> mergedMap = Arrays.stream(dicts).filter(filter)

                .map(Map::entrySet)
                .flatMap(Collection::stream)
                .collect(
                        Collectors.toMap(
                                Map.Entry::getKey,
                                Map.Entry::getValue,
                                Integer::max
                        )
                );

        System.out.println(mergedMap);

    }
}

```
Test
```java
public class Main {
    public static void main(String[] args) {

        CarAnother carAnother = new CarAnother();

        // Example 1 - varargs
        carAnother.doSomethingOnManyStrings("one", "two", "three", "four"); // one two three four

        // the same function but more params
        carAnother.doSomethingOnManyStrings("one", "two", "three", "four", "five", "six"); // one two three four five six


        // Example 2 - varargs of sets
        Map<String, Integer> dict1 = new HashMap<String, Integer>() {{
            put("key1", 1);
            put("key2", 2);
        }};

        Map<String, Integer> dict2 = new HashMap<String, Integer>() {{
            put("key3", 3);
            put("key4", 4);
        }};

        Map<String, Integer> dict3 = new HashMap<String, Integer>() {{
            put("key5", 5);
        }};

        // run on 2 dictionaries
        carAnother.joinDictionaries(dict -> dict.size() > 0, dict1, dict2); // {key1=1, key2=2, key3=3, key4=4}

        // run on 3 dictionaries (no matter how many dictionaries we want to use - it will work properly)
        carAnother.joinDictionaries(dict -> dict.size() > 0, dict1, dict2, dict3); // {key1=1, key2=2, key5=5, key3=3, key4=4}

        List<Vehicle> vehicles = new ArrayList<>();
        Set<Vehicle> uniqueVehicles = new HashSet<>(vehicles);
        Car[] cars = new Car[2];

        // run method with mane different params
        carAnother.doSomething(1, 'x', "str", new Car("",""), vehicles, null);

        // run method with mane different params (collections and arrays)
        carAnother.doSomething(uniqueVehicles, vehicles, new int[]{1,2,3}, cars);

    }
}
```

Simulateing Python's Dictionary parameters.

```java
@Data
class CarAnother extends Vehicle {

    /**
     * doSomethingOnDictParams
     *
     * @param normalPositionalParam - normal integer param on first position
     * @param dict - map/dictionary
     * @param strParams - vararg (we can put here many strings)
     */
    public void doSomethingOnDictParams(int normalPositionalParam, Map<String, String> dict, String ...strParams) {

        String res = Arrays.stream(strParams).collect(Collectors.joining(" "));

        System.out.println(normalPositionalParam);
        System.out.println(dict);
        System.out.println(res);

    }
}
```

Testing with few dictionary creation approaches.
```java
public class Main {
    public static void main(String[] args) {

        CarAnother carAnother = new CarAnother();

        // dict, style 1
        Map<String, String> myDict = new HashMap<>();
        myDict.put("key1", "val1");
        myDict.put("key2", "val2");

        // dict, style 2
        Map<String, String> myDict2 = Stream.of(new String[][] {
                { "key1", "val1" },
                { "key2", "val2" },
        }).collect(Collectors.toMap(data -> data[0], data -> data[1]));


        // dict, style 3
        Map<String, String> myDict3 = Map.of(
                "key1", "val1",
                "key2", "val2"
        );

        // dict, style 4
        Map<String, String> myMap = new HashMap<>() {{
            put("key1", "val1");
            put("key2", "val2");
        }};

        // testing
        carAnother.doSomethingOnDictParams(12, myDict,"a");
        carAnother.doSomethingOnDictParams(12, myDict2,"a");
        carAnother.doSomethingOnDictParams(12, myDict3,"a");
        carAnother.doSomethingOnDictParams(12, myDict, "a", "b", "c");
        carAnother.doSomethingOnDictParams(12, myDict, "a", "b", "c", "d", "e");
    }
}
```