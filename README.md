
## Data structures

### List comprehension

#### Python
```python
from typing import *

# Example 1
list_using_comp: List[int] = [var ** 2 for var in range(1, 10) if var % 2 == 0]
# [4, 16, 36, 64]

# Example 2
char_list: List[chr] = ['', '    a', 'b', '\t']
[x.strip() for x in char_list if x.strip()]
# ['a', 'b']

# Example 3
nums: List[int] = [1, 2, 3, 4]
fruit: List[str] = ["Apples", "Peaches", "Pears", "Bananas"]
[(i, f) for i in nums for f in fruit if f[0] == "P" if i % 2 == 1]
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

class Vehicle:
    pass


class Car(Vehicle):

    def __repr__(self) -> str:
        return f'Car({[self.__name, self.speed, self._shortname]!r})'

    def __init__(self, name: str = "MyCar", speed: int = 100, shortname: str = "car short",
                 supername: str = "super") -> None:
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
    def set_name(self, name: str) -> None:
        self.__name = name + "[setter 1]"

    # getter for private field
    def get_name(self) -> str:
        return self.__name + "[getter 1]"

    # getter by property decorator
    @property
    def supername(self) -> str:
        return self.__supername + "[getter 2]"

    # setter by property decorator
    @supername.setter
    def supername(self, supername: str) -> None:
        self.__supername = supername + "[setter 2]"
        print(self.__supername)

    # deleter by decorator
    @supername.deleter
    def supername(self) -> None:
        del self.__supername

    # private method
    def __privateMethod(self) -> None:
        print("__privateMethod")

    # public method
    def publicMethod(self) -> None:
        pass

    # public class method (is bound to the class object itself)
    @classmethod
    def giveMeAnyFastCar(cls: 'Car', speed: int = 200) -> 'Car':
        return cls("Fast Car", speed)

    # static method (knows nothing about the class and just deals with the parameters)
    @staticmethod
    def getSpeedInKmPerHour(speedInMilesPerHour: int):
        return speedInMilesPerHour * 1.60

```

Test
```python

car: Car = Car()

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
fast_car: Car = Car.giveMeAnyFastCar(300)
print(fast_car)  # Car(['Fast Car', 300, 'car short'])

# static method usage
speed: int = Car.getSpeedInKmPerHour(100)
print(speed)  # 160.0
```

Descriptor example

```pyhton
class Email():
    EMAIL_REGEX: Pattern[str] = re.compile(
        r"[A-Za-z0-9-_]+(.[A-Za-z0-9-_]+)*@"
        "[A-Za-z0-9-]+(.[A-Za-z0-9]+)*(.[A-Za-z]{2,})"
    )

    """Descriptor class for an email address."""

    def __init__(self) -> None:
        self.pool = {}

    def __get__(self, instance: Any, owner: Any) -> Any:
        print("get Email through descriptor")
        return self.pool.get(instance, 0)

    def __set__(self, instance: Any, email_address: str) -> None:
        if not Email.EMAIL_REGEX.match(email_address):
            raise ValueError
        print("set Email through descriptor")
        self.pool[instance] = email_address


class User:
    email: Email = Email()

    def __init__(self, name: str, email: str) -> None:
        self.email = email
        self.name = name


# test get/set through descriptor
user: User = User("Sla", "test@mail.com")  # OK (set Email through descriptor)
print(user.email)  # OK (get Email through descriptor), result: test@mail.com

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

#### Method signatures & type hints

#### Python

Example 1
```python
from typing import *

# function wirh some positional params
def test_function(x: int, y: int, w: int = 0, h: int = 0) -> None:
    print("x: %s, y: %s, w: %s, h: %s" % (x, y, w, h))


# normal function call
test_function(1, 2, 3, 4);
# x: 1, y: 2, w: 3, h: 4

# arguments unpacking function call
arg_tuple: Tuple[int] = (1, 2)
arg_dictionary: Dict[str, int] = {'w': 20, 'h': 10}

test_function(*arg_tuple, **arg_dictionary)

# x: 1, y: 2, w: 20, h: 10
```

Example 2
```python


def test_function2(arg1: List[Any], *args: int, **kwargs: str) -> None:
    print(arg1)

    for x in args:
        print("next arg is: " + str(x))

    print(kwargs)
    print(kwargs.get("this"), kwargs.get("that"))


# another call with explicit parameters
test_function2([1, 2, "three"], 4, 5, 6, this="this v", that="that v")
# [1, 2, 'three']
# next arg is: 4 next arg is: 5 next arg is: 6
# {'this': 'this', 'that': 'that'}
# this v that v

# arguments unpacking example
targs: List[int] = [4, 5, 6]
targsb: Tuple[int] = (4, 5, 6, 6)
kwargs: Dict[str, str] = {"this": "this v", "that": "that v"}
test_function2([], *targs, **kwargs)
test_function2([], *targsb, **kwargs)
# the same result as in above example
```

Example 3
```python


def test_function2(arg1: List[Any], *args: int, **kwargs: str) -> None:
    print(arg1)

    for x in args:
        print("next arg is: " + str(x))

    print(kwargs)
    print(kwargs.get("this"), kwargs.get("that"))


# another call with explicit parameters
test_function2([1, 2, "three"], 4, 5, 6, this="this v", that="that v")
# [1, 2, 'three']
# next arg is: 4 next arg is: 5 next arg is: 6
# {'this': 'this', 'that': 'that'}
# this v that v

# arguments unpacking example
targs: List[int] = [4, 5, 6]
targsb: Tuple[int] = (4, 5, 6, 6)
kwargs: Dict[str, str] = {"this": "this v", "that": "that v"}
test_function2([], *targs, **kwargs)
test_function2([], *targsb, **kwargs)
# the same result as in above example
```

More examples:
```python
# type aliases

T = TypeVar('T', int, float, complex)
Vector = Iterable[Tuple[T, T]]


def inproduct(v: Vector[T]) -> T:
    return sum(x * y for x, y in v)


def dilate(v: Vector[T], scale: T) -> Vector[T]:
    return ((x * scale, y * scale) for x, y in v)


# generics

T = TypeVar('T')  # Declare type variable


def first(l: Sequence[T]) -> T:  # Generic function
    return l[0]


# iterable

def zero_all_vars(vars: Iterable[LoggedVar[int]]) -> None:
    for var in vars:
        var.set(0)


# union types

def handle_employees(e: Union[Employee, Sequence[Employee]]) -> None:
    if isinstance(e, Employee):
        e = [e]

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

### Errors & exceptions handling

#### Python
```python
class MyException(Exception):
    def __init__(self, msg: str) -> None:
        self.msg = msg


class MyError(ValueError):
    def __init__(self, msg: str) -> None:
        self.msg = msg


try:
    # do something
    raise MyException("Bad result")

# catch one of exceptions
except (ZeroDivisionError, RuntimeError, TypeError):
    print('One of ZeroDivisionError, RuntimeError, TypeError throwed')

# custome Exception
except MyException as e:
    print("MyException: ", e.msg)

# general, another exception
except:
    print("any other error")

# continue in this block if there is no any exception catched
else:
    print("All good, lets continue")

# finally, always active, no matter if any exception throwed or not
finally:
    print("finally")

# MyException:  Bad result
# finally
```

#### Java

```java

class MyException extends Exception{
    MyException(String msg){
        super(msg);
    }
}

class MyError extends Error{
    MyError(String msg){
        super(msg);
    }
}

public class Main {

    public static void main(String[] args) {

      
        try {
            if(1==1)
                throw new MyException("My test msg");

            // int b = 1/0; // exception

        // catch concrete exception object
        } catch (MyException e){
            System.out.println("MyException throwed. Msg: " + e.getMessage());

        // catch one of ArrayIndexOutOfBoundsException | NullPointerException exception
        } catch (ArithmeticException | NullPointerException e){
            System.out.println("One of ArrayIndexOutOfBoundsException | NullPointerException throwed");

        // catch any other exception
        } catch(Exception e) {
            System.out.println("General exception");

        // run this block always - no matter if any exception trowed or not
        } finally{
            System.out.println("finally");
        }

        // MyException throwed. Msg: My test msg
        // finally

    }
    
    /**
     * testMethod
     *
     * method with possible exception to be handled
     *
     * @throws MyException
     */
    public void testMethod() throws MyException {
        if(1==1)
            throw new MyException("My test msg");

    }
}
```


* * *