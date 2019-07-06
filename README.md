
## Data structures

### Lists
##### Python
```python
mlist: List[str] = ["A", "B", "C"]
mlist.insert(4, "D")  # insert at an index 4
mlist.sort()  # in place sort
mlist.remove("C")  # remove first "C" element
popped: str = mlist.pop(2)  # remove the item at index 2
mlist.reverse()  # reverse the mlist
```

##### Java
```java
public class Main {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("A");
        list.add("B");
        list.add("C");
        list.add(3,"D");
        Collections.sort(list); //sort
        list.remove("C"); //remove first "C" element
        list.remove(2); //remove object at the index 2
        Collections.reverse(list); //reverse the list
        int n = list.indexOf("A"); //return the index of first occurrence of "A"
    }
}
```

### Tuples
##### Python
```python
words: Tuple[str] = ("A", "B")  # or words = "ABng"
print("A" in words)  # True
print(hash(words))  # tuples are hashable
a,b = words  # or a,b = "A", "B"
print(a)  # Good
print(b)  # Morning
print(len(words))  # 2
```

##### Java
Tuple is just kind of immutable list. There are many ways how to use immutable collections of any kind e.g. Map, List, Set in Java.

a) Older approach (JDK 5)
```java
public class Main {
    public static void main(String[] args) {
        // Example (immutable list)
        List<String> list = new ArrayList<String>(Arrays.asList("one", "two", "three"));
        List<String> unmodifiableList = Collections.unmodifiableList(list);
    }
}
```


b) Newer approach (JDK 9 factory methods)
```java
public class Main {
    public static void main(String[] args) {
        List<String> immutableList = List.of("A", "B");
        Set<String> immutableSet = Set.of("A", "B");
        Map<String, String> immutableMap = Map.of("key1", "Value1", "key2", "Value2", "key3", "Value3");
    }
}
```


c) Google Guava approach
An "Immutable collection" can be created in several ways:

- using the copyOf method, for example, ImmutableSet.copyOf(set)
- using the of method, for example, ImmutableSet.of("a", "b", "c") or ImmutableMap.of("a", 1, "b", 2)
- using a Builder, for example:

        public static final ImmutableSet<Color> GOOGLE_COLORS =
            ImmutableSet.<Color>builder()
               .addAll(WEBSAFE_COLORS)
               .add(new Color(0, 191, 255))
               .build();
           
```java
public class Main {
    public static void main(String[] args) {
        
        // Example 1	
        List<String> list = new ArrayList<String>(Arrays.asList("one", "two", "three"));
        List<String> unmodifiableList = ImmutableList.copyOf(list);	
            
        // Examle 2 (immutable list via builder)
        List<String> list = new ArrayList<String>(Arrays.asList("one", "two", "three"));
        ImmutableList<Object> unmodifiableList = ImmutableList.builder().addAll(list).build();

    }
}
```

Possible classes:

general schema: Immutable[XXX]
examples:
- ImmutableCollection
- ImmutableList
- ImmutableSet
- ImmutableSortedSet
- ImmutableMap
- ImmutableSortedMap
- ImmutableMultiset
- ImmutableSortedMultiset
- ImmutableMultimap
- ImmutableListMultimap
- ImmutableSetMultimap
- ImmutableBiMap
- ImmutableClassToInstanceMap
- ImmutableTable

See more: https://github.com/google/guava/wiki/ImmutableCollectionsExplained

d) Apache Commons approach 

```java
public class Main {
    public static void main(String[] args) {
        
        // Example 1 (ListUtils)
        List<String> list = new ArrayList<String>(Arrays.asList("one", "two", "three"));
        List<String> unmodifiableList = ListUtils.unmodifiableList(list);
        
        // Example 2 (Immutable classes from org.apache.commons.lang3.tuple)
        ImmutablePair<String, List<Integer>> immutablePair = new ImmutablePair<>("A", Arrays.asList(1,2,3));
        ImmutableTriple<String, Integer, Character> immutableTriple = new ImmutableTriple<>("A", 2, 'x');

    }
}
```

e) Java Tuples Library approach (see https://www.javatuples.org/)
```java
public class Main {
    public static void main(String[] args) {
        // Pair via static factory
        Pair<String, Integer> pair = Pair.with("A", 12);
        // Pair via constructor
        Pair<String, Integer> person = new Pair<String, Integer>("A", 12);
        // Quartet from collections
        List<String> listOf4Names = Arrays.asList("A1","A2","A3","A4");
        Quartet<String, String, String, String> quartet = Quartet.fromCollection(listOf4Names);
        // triplet
        Triplet<String, String, String> triplet = Triplet.with("Java", "C", "C++");
    }
}
```

### Sets
##### Python
```python
set_of_words1: Set[str] = {"A", "B", "C"}

# example2
set_of_words2: Set[str] = set()
set_of_words2.add("A")
set_of_words2.add("B")
set_of_words2.add("C")
element_is_in_set: bool = ("Boat" in set_of_words2)  # True
print(set_of_words2.intersection(set_of_words1))  # intersection
print(set_of_words2.union(set_of_words1))  # union
```

##### Java
```java
public class Main {
    public static void main(String[] args) {
        Set<String> set1 = new HashSet<>();
        Set<String> set2 = new HashSet<>() {{ add("A"); add("B");}};
        
        set1.add("A");
        set1.add("B");
        set1.add("C");
         
        //intersection
        Set<String> intersect = new HashSet<>(set1);
        intersect.retainAll(set2);
        
        //union
        Set<String> union = new HashSet<>(set1);
        union.addAll(set2);
    }
}
```

### Maps and dictionaries
##### Python
```python
phonebook: Dict[str, str] = {}
phonebook = {"Slawek": "122-99981", "Mark": "333-1111", "cAdam": "1222-112213"}
print(phonebook["Slawek"])  # value of a key
phonebook.keys()  # List of keys
phonebook.values()  # List of values
element_is_in_dict = "Slawek" in phonebook  # True
(phonebook.items())  # prints tuples of key-value pairs
```

##### Java
```java
public class Main {
    public static void main(String[] args) {
        HashMap<String, String> phoneBook = new HashMap<String, String>();
        phoneBook.put("Slawek", "111-1111");
        phoneBook.put("Lucy", "5255-2222");
        phoneBook.put("Mark", "51155-3333");
        
        //looping elements
        Map<String, String> map = new HashMap<String, String>();
        for (Map.Entry<String, String> entry : map.entrySet()) {
         System.out.println("Key = " + entry.getKey() +
           ", Value = " + entry.getValue());
        }
        
        //get key value
        phoneBook.get("Slawek");
        
        //get all key
        Set keys = phoneBook.keySet();
        
        //get number of elements
        phoneBook.size();
        
        //delete all elements
        phoneBook.clear();
        
        //delete an element
        phoneBook.remove("Slawek");    
    }
}
```


### List comprehension
##### Python
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

##### Java

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

        // Example 2 (https://github.com/farolfo/list-comprehensions-in-java)
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








## General programming
### Method signatures & type hints
##### Python

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

##### Java
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

### Simple file read / write
##### Python

```python
# read line by line
f = open("/example.txt","r")
for line in f:
  print(line)
f.close()

# read the entire file in memory
f = open("/example.txt","r")
contents = f.read()
print(contents)
f.close()

# write to a file
f = open("/example.txt","r+") # open for read and write at the same time
f.write("test content")
contents = f.read()
print(contents) # test content

```

##### Java
Approach with Buffered input and output stream
```java
public class Main {
    public static void main(String[] args) {
        String path = "/example.txt";

        // write the content in file 
        try(BufferedOutputStream bufferedOutputStream = new BufferedOutputStream(new FileOutputStream(path))) {
            String fileContent = "This is a sample text.";
            bufferedOutputStream.write(fileContent.getBytes());
        } catch (IOException e) {
            // ...
        }

        // read the content from file
        try(BufferedInputStream bufferedInputStream = new BufferedInputStream(new FileInputStream(path))) {
            int ch = bufferedInputStream.read();
            while(ch != -1) {
                System.out.print((char)ch);
                ch = bufferedInputStream.read();
            }
        } catch (FileNotFoundException e) {
            // ...
        } catch (IOException e) {
            // ...
        }
    }
}
```

Apache Commons FileUtils approach
```java
public class Main {

    public static void main(String[] args) throws IOException {

        // READ
        
        String path = "/example.txt";

        File myfile = new File(path);

        String contents = FileUtils.readFileToString(myfile, StandardCharsets.UTF_8.name());

        System.out.println(contents);

        List<String> lines = FileUtils.readLines(myfile, StandardCharsets.UTF_8.name());
            
        
        // WRITE

        String string = "Sample text";
        
        File myfile = new File(path);
        
        FileUtils.writeStringToFile(myfile, string, StandardCharsets.UTF_8.name());

    }
}
```

### Basic HTTP client
##### Python
```python
import requests
r = requests.get("https://google.com/example_data")
print(r.headers) # headers as a dictionary
print(r.status_code) # status code
print(r.content) # body
r.close()
```

##### Java
```java
public class Main {
    public static void main(String[] args) {

        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
                .url("https://google.com/example_data")
                .build();

        Response response = null;
        try {
            response = client.newCall(request).execute();
            String responseAsStr = response.body().string();
            response.code(); // code
            response.headers(); // Headers
        } catch (IOException e) {
            e.printStackTrace();
        }
	}
}
```

### Errors & exceptions handling

##### Python
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

##### Java

Example 1:

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

Example 2 (try - catch with resources)

```java
public class Main {

    public static void main(String[] args) {
        
        String path = "/";
        
        try(BufferedOutputStream bufferedOutputStream = new BufferedOutputStream(new FileOutputStream(path))) {
            // ...
        } catch (IOException e) {e.printStackTrance();}
        
    }
}
```

* * *





## OOP

### Object encapsulation

##### Python

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

##### Java

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

## Decorators

### Decorator and monkey patching
##### Python
Example 1 - function and method decoration
```python
from typing import *
import time
import types

RT = Callable[..., Dict[str, Any]]
BT = Callable[..., int]


# PythonDecorators/decorator_function_with_arguments.py
def decorator_check_duration(precision: int = 5) -> Callable[[BT], RT]:
    def wrap(f: BT) -> RT:
        def wrapped_f(**range: int) -> Dict[str, Any]:
            start: float = time.time()
            res = f(**range)
            end: float = time.time()
            return {"result": res, "time": round(end - start, precision)}

        return wrapped_f

    return wrap


# sum numbers function
def sumNumbers(**rangenum: int) -> int:
    return sum(x for x in range(rangenum.get('start'), rangenum.get('stop')) if x % 3 == 0)


# decorated sum numbers function (do the same but also calculates
# time taken and returns it as a dictionary with key "time")
@decorator_check_duration(2)
def sumNumbersWithTimeChecking(**rangenum: int) -> Any:
    return sumNumbers(**rangenum)


def sumNumbersNormally(**rangenum: int) -> int:
    return sumNumbers(**rangenum)


# normal sum
print(sumNumbersNormally(start=1, stop=10000000))  # 16666668333333

# the same function but decorated by decorator (duration checker)
print(sumNumbersWithTimeChecking(start=1, stop=10000000))  # {'result': 16666668333333, 'time': 1.39}

```

Example 2 - Logger decorator (logging function's input/output to the DB)

```python

class decorator_logger():

    def __init__(self, logger: Callable[[Dict[str, str]], None]) -> None:
        """
        register logger
        """
        if callable(logger):
            self.logger = logger
        else:
            self.logger = None

    def __call__(self, f) -> Callable[..., int]:
        """
        If there are decorator arguments, __call__() is only called
        once, as part of the decoration process! You can only give
        it a single argument, which is the function object.
        """

        def wrapped_f(**rangenum: int) -> int:
            res = f(**rangenum)

            if self.logger:
                self.logger({"input": rangenum, "output": res})

            return res

        return wrapped_f


# create callable logger
myLogger: Callable[[Dict[str, str]], None] = lambda x: print("Log to database: ", x)


# decorate function by logger, so capture and log input and output
@decorator_logger(myLogger)
def calculateSumB(**rangenum: int):
    return sum(x for x in range(rangenum.get('start'), rangenum.get('stop')) if x % 3 == 0)


print(calculateSumB(start=1, stop=10000000))


# returned result: 16666668333333
# additionally method uses callable logger so below line is printed as well
# Log to database:  {'input': {'start': 1, 'stop': 10000000}, 'output': 16666668333333}

```

Example 3 - Monkey Patching
```python
class Class():

    def power(self, x: int, y: int = 2) -> int:
        return x ** y

    def set_power_mode_x_by_x(self) -> None:
        opower = self.power

        def power_x_by_x(self, x: int) -> int:
            return opower(x, x)

        self.power = types.MethodType(power_x_by_x, self)


cls = Class()
print(cls.power(10))  # 100

cls.set_power_mode_x_by_x()
print(cls.power(10))  # 10000000000

```

##### Java

AOP/AspectJ approach. Aspect-Oriented Programming (AOP) complements Object-Oriented Programming (OOP) by providing another way of thinking about program structure. The key unit of modularity in OOP is the class, whereas in AOP the unit of modularity is the aspect. 

Simple Logger by decorator example:

```java 
package jlogger;

import lombok.extern.java.Log;
import org.apache.commons.lang3.StringUtils;
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Pointcut;
import org.aspectj.lang.reflect.MethodSignature;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;
import java.util.Arrays;
import java.util.function.Predicate;


/* --- interfaces --- */

interface LoggableRequest {String toString();}

interface LoggableResponse {String toString();}

interface LoggerHandler {
    void init();
    void end();
    <S extends LoggableRequest> void logRequest(S request);
    <T extends LoggableResponse> void logResponse(T response);
}

/**
 * Main Logger interface - kind of Decorator
 */
@Retention(
        RetentionPolicy.RUNTIME
)
@Target({
        ElementType.CONSTRUCTOR,
        ElementType.METHOD
})
//public
@interface Logger {
    enum TYPE{
        ALL,
        REQUEST,
        RESPONSE
    }
    TYPE[] logTypes() default {TYPE.ALL};
    Class<? extends LoggerHandler> loggerHandler() default DefaultLogger.class;

}

@Log
class DefaultLogger implements LoggerHandler {

    private static String JOIN_SEPARATOR = " | ";

    private StringBuilder logResult = new StringBuilder();

    @Override
    public void init() {
    }

    @Override
    public void end() {
        log.info(StringUtils.strip(logResult.toString(), JOIN_SEPARATOR));
    }

    @Override
    public void logRequest(LoggableRequest request) {
        logResult.append(" request: ").append(request).append(JOIN_SEPARATOR);
    }

    @Override
    public void logResponse(LoggableResponse response) {
        logResult.append(" response: ").append(response).append(" | ");
    }

}

/**
 * Aspect J, class with pointcuts
 */
@Log
@Aspect
class AspectLogger {

    @Pointcut(
            "execution(* *(..)) && @annotation(Logger)"
    )
    public void loggerLog() {}

    @Around("loggerLog()")
    public Object around(ProceedingJoinPoint point) {

        LoggerHandler loggerHandlerInstance = null;

        Method method = ((MethodSignature) point.getSignature()).getMethod();

        Logger logParams = method.getAnnotation(Logger.class);

        Class<? extends LoggerHandler> loggerHandler = logParams.loggerHandler();

        try {
            loggerHandlerInstance = loggerHandler.getDeclaredConstructor().newInstance();
        } catch (
                InstantiationException
                        | IllegalAccessException
                        | InvocationTargetException
                        | NoSuchMethodException e
        ) {
            log.warning(e.toString());
        }


        /*
            ----- parse RESPONSE -----
         */
        Object jpObj = null;

        /* LoggableResponse */
        LoggableResponse response = null;

        try {

            jpObj = point.proceed();

            if(jpObj instanceof LoggableResponse){
                response = (LoggableResponse) jpObj;
            }

            Class responseEntityClazz = null;

            if(responseEntityClazz.isInstance(jpObj)) {

                Method getBodyMethod = responseEntityClazz.getMethod("getBody");

                Object reqBody = getBodyMethod.invoke(jpObj);

                if(reqBody instanceof LoggableResponse) {
                    response = (LoggableResponse) reqBody;
                }

            }

        } catch (Throwable throwable) {
            log.warning(throwable.toString());
        }


        /*
            ----- parse REQUEST -----
         */
        LoggableRequest request = null;

        try {

            /* LoggableRequest */
            request = Arrays
                    .stream(
                            point.getArgs()
                    )
                    .filter(
                            obj -> obj instanceof LoggableRequest
                    )
                    .map(
                            obj -> (LoggableRequest) obj
                    )
                    .findFirst()
                    .orElse(null);

        } catch (Throwable throwable) {
            log.warning(throwable.toString());
        }

        // log only when Rqeuset containg value ...


        String requiredRequestField;

        String requiredRequestValue;


        // get log types, log only request, response, both of them, etc.

        Logger.TYPE[] logTypes = logParams.logTypes();

        Predicate<Logger.TYPE> logAll = el -> el.equals(Logger.TYPE.ALL);
        Predicate<Logger.TYPE> logRequest = el -> el.equals(Logger.TYPE.REQUEST);
        Predicate<Logger.TYPE> logResponse = el -> el.equals(Logger.TYPE.RESPONSE);

        if(loggerHandlerInstance == null) {
            return jpObj;
        } else{
            loggerHandlerInstance.init();
        }

        // log request
        if(Arrays.stream(logTypes).anyMatch(logAll.or(logRequest)) && request != null){
            loggerHandlerInstance.logRequest(request);
        }

        // log response
        if(Arrays.stream(logTypes).anyMatch(logAll.or(logResponse)) && response != null){
            loggerHandlerInstance.logResponse(response);
        }

        loggerHandlerInstance.end();

        return jpObj;

    }

}


/**
 * Test
 */
class MyController{

    /**
     * example with parameters
     */
    @Logger(logTypes = {Logger.TYPE.REQUEST, Logger.TYPE.RESPONSE}, loggerHandler=DefaultLogger.class)
    public void method(){}

    /**
     * simple decoration, without any paramters
     */
    @Logger
    public void anotherMethod(){}
}



```

See more: https://bitbucket.org/slawekhaa/jlogger-java-aspectj/src



Spring Framework example - approach with Beans and Qualifier - 
the same method in 2 different versions (normal and extended), 
depending on autowired Bean. Extended version log elapsed time of our calulation to the database and returns the same result
(uses sumNumbers() method from basic version of MathBasic - calculation class)

```java

interface Calculations{
    int sumNumbers(Range<Integer> range);
}

/**
 * Basic calc class
 */
class MathBasic implements Calculations {

    /**
     * sumNumbers
     * @param range
     * @return int
     */
    public int sumNumbers(Range<Integer> range){

        return IntStream.range(
                range.lowerEndpoint(),
                range.upperEndpoint()
        ).sum();

    }

}

/**
 * class with elapsed time
 * check on every method
 */
class MathWithTimer implements Calculations {

    /**
     * sumNumbers with logging elapsed time to the DB
     *
     * @param range
     * @return Map<String, Number>
     */
    public int sumNumbers(Range<Integer> range){

        long lStartTime = System.currentTimeMillis();

        MathBasic mb = new MathBasic();

        int result = mb.sumNumbers(range);
        
        long elapsedTime = System.currentTimeMillis() - lStartTime;

        // log elapsed time [ elapsedTime ] to DB ...

        return result;

    }

}

@Configuration
class MainConfig {

    @Primary
    @Bean(name = "MathBasic")
    public Calculations calculations() {
        return new MathBasic();
    }

    @Bean(name = "MathWithTimer")
    public Calculations calculationsWithTimer() {
        return new MathWithTimer();
    }
}


@RestController
class TestController extends BaseController {

    /**
     * normal calculator
     * standard method sumNumbers()
     */
    @Autowired
    private Calculations calculator;

    /**
     * extended calculator with timer - basic calculator decorated 
     * by elapsed time logger
     */
    @Autowired
    @Qualifier( "MathWithTimer")
    private Calculations calculatorExtended;


    @RequestMapping(value = "/sum", method = RequestMethod.GET)
    public void getSum(){
        int res = calculator.sumNumbers(Range.open(1,100000));
    }

    @RequestMapping(value = "/sum-extended", method = RequestMethod.GET)
    public void getSumExtended(){
        int res = calculatorExtended.sumNumbers(Range.open(1,100000));
    }

}
```

Java EE example - approach with Decorator annotation - method sumNumbers() may behave normally and just calculate sum of integers frm range or, if 
we register decorator - we may use extended version of that method with elapsed time logging. Decorated method 
uses the same logic and returns the same result but log in elapsed time to the DB.

```java
package mypackage;

import com.google.common.collect.Range;
import java.util.stream.IntStream;
import javax.inject.Inject;
import javax.ws.rs.GET;
import javax.ws.rs.Path;
import javax.decorator.Decorator;
import javax.decorator.Delegate;
import javax.enterprise.inject.Any;

interface Calculations{
    int sumNumbers(Range<Integer> range);
}

@Decorator
abstract class CalculatorDecorator implements Calculations {

    @Inject
    @Delegate
    @Any
    private Calculations calculator;

    public int sumNumbers(Range<Integer> range) {

        long lStartTime = System.currentTimeMillis();

        int res = calculator.sumNumbers(range);

        long elapsedTime = System.currentTimeMillis() - lStartTime;

        // log elapsed time [ elapsedTime ] to DB ...

        return res;
    }
}


class BasicCalculator implements Calculations {

    @Override
    public int sumNumbers(Range<Integer> range) {
        int sumOfRange = IntStream.range(
                range.lowerEndpoint(),
                range.upperEndpoint()
        ).sum();

        return sumOfRange;
    }
}


@Path("/")
class TestController {

    @Inject
    private Calculations calculator;

    @GET
    @Path("/")
    public void testSum() {
        int res = calculator.sumNumbers(Range.open(1,100000));
    }

}
```

Add decorator in beans.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://java.sun.com/xml/ns/javaee"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/beans_1_0.xsd">
    <decorators>
        <class>mypackage.CalculatorDecorator</class>
    </decorators>
</beans>
```

Another example of Decorator Design Pattern in Java - see https://bitbucket.org/slawekhaa/design-patterns-java-examples/wiki/Home

##### Other, related concepts in Java
Custom annotations is very powerful mechanism in Java. We may use it to 
create decorators by many ways e.g. we can track and modify or log method's I/O or extend methods and classes functionality and do 
many various things with it.

Example of custom annotations - registering buttons Event handlers.

```java
import javax.swing.*;
import java.awt.*;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;
import java.lang.reflect.Field;
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;


// --------------------- custom annotation - decorator ---------------------


/**
 * Custom annotation - action listener decorator
 */
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
/*public*/ @interface RegisterActionListener
{
    String value() default "";
    String[] values() default {};
    Class<? extends CustomHandler> handlerClass() default DefaultHandler.class;
}


// --------------------- custom handler - example of decorator's parameter ---------------------

/**
 * Custom habdler interface
 */
interface CustomHandler{
    void handle(Object element);
}

class DefaultHandler implements CustomHandler{
    @Override
    public void handle(Object element) {}
}

/**
 * my custom handler example
 */
class MyHandler implements CustomHandler{
    @Override
    public void handle(Object element) {
        System.out.println("handle");
    }
}



// --------------------- action processor, based on reflection  ---------------------

/*public*/ class ActionListenerInstaller
{
    /**
     * processAnnotations - annotation processor
     * @param obj
     */
    public static void processAnnotations(Object obj)
    {
        try
        {
            Class<?> cl = obj.getClass();


            for (Method m : cl.getDeclaredMethods())
            {
                RegisterActionListener a = m.getAnnotation(RegisterActionListener.class);
                Class<? extends CustomHandler> handler = a.handlerClass();

                if (a != null)
                {
                    if(a.values().length > 0) {
                        for (String v : a.values()) {
                            Field f = setFieldAccessible(cl, v);
                            addListener(f.get(obj), obj, m, handler);
                        }
                    }
                    if(!a.value().isEmpty()) {
                        for (String v : a.values()) {
                            Field f = setFieldAccessible(cl, v);
                            addListener(f.get(obj), obj, m, handler);
                        }
                    }

                }
            }



        } catch (Exception e) {}
    }

    private static Field setFieldAccessible(Class<?> cl, String fieldName) throws NoSuchFieldException {
        Field f = cl.getDeclaredField(fieldName);
        f.setAccessible(true);
        return f;
    }
    /**
     * Add listener to source element
     *
     * @param source
     * @param param
     * @param m
     * @throws Exception
     */
    public static void addListener(Object source, final Object param, final Method m, Class<? extends CustomHandler> customHandler)
            throws ReflectiveOperationException
    {
        InvocationHandler handler = (proxy, mm, args) -> m.invoke(param);

        Object listener = Proxy.newProxyInstance(null, new Class[] { java.awt.event.ActionListener.class }, handler);
        Method adder = source.getClass().getMethod("addActionListener", java.awt.event.ActionListener.class);
        adder.invoke(source, listener);

        // use custom handler to handle action if any
        if(customHandler != DefaultHandler.class) {
            Method method = customHandler.getMethod("handle", String.class);
            Object o = method.invoke(source);
        }
    }
}



// --------------------- decorator's/annotation's @RegisterActionListener usage   ---------------------

/**
 * Example of usage - class with 2 buttons and
 * 2 action handlers registered by annotation/decorator
 */
/*public*/ class MyButtonsFrame extends JFrame
{

    private JPanel panel;
    private JButton buttonA;
    private JButton buttonB;

    public MyButtonsFrame()
    {

        panel = new JPanel();
        add(panel);

        buttonA = new JButton("My button A");
        buttonB = new JButton("My button B");

        panel.add(buttonA);
        panel.add(buttonB);

        ActionListenerInstaller.processAnnotations(this);
    }

    /**
     * register this action to be called on buttonA click
     */
    @RegisterActionListener("buttonA")
    public void yellowBackground()
    {
        panel.setBackground(Color.YELLOW);
    }

    /**
     * register action on 2 buttons
     */
    @RegisterActionListener(values = {"buttonB", "buttonA"})
    public void blueBackground()
    {
        panel.setBackground(Color.BLUE);
    }

    /**
     * register action with custom handler class
     */
    @RegisterActionListener(values = {"buttonB", "buttonA"}, handlerClass = MyHandler.class)
    public void redBackground()
    {
        panel.setBackground(Color.RED);
    }
}
```