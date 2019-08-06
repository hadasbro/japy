![picture](https://img.shields.io/badge/Java-11.0.1-brightgreen.svg)
![picture](https://img.shields.io/badge/Python-3.7.4-blue.svg)

**Python equivalent in Java for bilingual developers**

Table of contents.

1. Data structures
    
    a) Lists
    
    
    b) Tuples
    
    
    c) Sets
    
    
    d) Maps and dictionaries
    
    
    e) List comprehension
    
    
    f) Popular data structures
    
2. General programming
    
    a) Method signatures & type hints
    
    b) Lambda expressions
    
    c) Simple file read / write
    
    d) Basic HTTP client
    
    e) Errors & exceptions handling
    
    f) Generics
    

3. OOP

    a) Objects encapsulation
    
    b) Inner classes
    
    c) Multiple inheritance
    
    d) Singleton patterns
    
    e) Polymorphism example

4. Decorators & design patterns

    a) Decorator and monkey patching

    b) Builder pattern
    
---

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

### Popular data structures

##### Python

Python Data Structures - https://docs.python.org/3/tutorial/datastructures.html

##### Java 

Collection interface - https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Collection.html

Set - https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Set.html

List - https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/List.html

Map - https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Map.html

SortedSet - https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/SortedSet.html

SortedMap - https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/SortedMap.html

HashSet - https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/HashSet.html

TreeSet - https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/TreeSet.html

ArrayList - https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/ArrayList.html

LinkedList - https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/LinkedList.html  

Vector - https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Vector.html

Collections - https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Collections.html

AbstractCollection - https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/AbstractCollection.html



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

from typing import (Any,
                    Callable,
                    Dict,
                    Tuple,
                    TypeVar)

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


# callale
AnyCallable = Callable[..., Any]

# type var
Domain = TypeVar('Domain')

# map
Operator = Map[Domain, Domain]

# tuple with strings only (no matter how many)
Keys = Tuple[str, ...]

# tuple with Domain type objects
Types = Tuple[Domain , ...]

# dict
Registry = Dict[int, Dict[Types, Dict[Keys, Dict[Types, AnyCallable]]]]


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

### Lambda expressions
##### Python

Basic examples of lambda expression
```python
from functools import reduce
from typing import Tuple, Dict, Any

import math


## Example 1

# normal function
def cube(y):
    return y * y * y;


# lambda version of the same function
cube_lambda = lambda x: x * x * x

print(cube_lambda(5))  # 125

## Example 2

square_root = lambda x: math.sqrt(x)

print(square_root(16))  # 4.0

## Example 3

power_sum = lambda *a, **b: list(map(lambda x: x ** b.get("power", 1) * b.get("multiplier", 1) % b.get("modulo", 1), a))

res = power_sum(1, 2, 3, power=2, multiplier=2, modulo=100)
print(res)
```

**Mappers, Filters, Reducers**

```python
from functools import reduce
from typing import Dict, Any
from typing import Tuple


## Example 4

my_list = [1, 5, 6, 9, 11, 14, 15, 16]

my_list = list(filter(lambda x: (x % 2 == 0), my_list))

# Output: [4, 6, 8, 12]
print(my_list)

# 125
# 4.0
# [2, 8, 18]
# [6, 14, 16]


### Filter
mylist = [5, 7, 22, 97, 54, 62, 77, 23, 73, 61]
mylist_result = list(filter(lambda x: (x % 2 == 0), mylist))
print(mylist_result)  # [22, 54, 62]

### Mapper
items = [1, 2, 3, 4, 5]
def sqr(x): return x ** 2
list(map(sqr, items))

### Reducer example
my_list = [15, 81, 10, 20, 52, 100]
sum = reduce((lambda x, y: x + y), my_list)
print(sum)  # 278

# another reducer
res = reduce(lambda x, y: x + y, [1, 2, 3, 4, 5, 6])
print(res)  # 21

## Filter and mapper
words = ["my", "passion", "is", "hehe", "programming", "and", "finding", "new", "haha", "great", "ways"]
forbidden_words = ["hehe", "haha"]
final_list = " ".join(map(lambda y: y.upper(), filter(lambda x: not forbidden_words.__contains__(x), words)))
print(final_list)

# MY PASSION IS PROGRAMMING AND FINDING NEW GREAT WAYS

# Another filter and mapper example
class Amount:

    default_rates: Dict[str, float] = {
        "EUR": 1.0,
        "RON": 5.2,
        "PLN": 4.5
    }

    def __str__(self) -> str:
        return "amount: {}, curency: {}".format(self.amount, self.curency)

    def __init__(self, amount: float, curency: str) -> None:
        self.amount = amount
        self.curency = curency

    def calcAmountInEur(self) -> float:
        return self.amount * Amount.default_rates

    @staticmethod
    def get_big_wins_in_eur(wins: Tuple["Amount",...]) -> Any:

        mappedToEur = map(lambda x: Amount(x.amount * Amount.default_rates.get(x.curency), "EUR"), wins).__iter__()

        bigwin = lambda x: x.amount > 100

        return list(filter(bigwin, mappedToEur))


list_of_wins: Tuple[Amount, ...] = (Amount(110, "EUR"), Amount(25, "EUR"), Amount(520, "RON"), Amount(30, "PLN"))

res: Tuple[Amount, ...] = Amount.get_big_wins_in_eur(list_of_wins)
print(list(map(lambda x: str(x), res)))
# ['amount: 110.0, curency: EUR', 'amount: 2704.0, curency: EUR', 'amount: 135.0, curency: EUR']


# Example - mapping dictionaries with lambda expressions
mydict = [{'name': 'english', 'rate': 10}, {'name': 'german', 'rate': 8}]

mydict_r1 = map(lambda x: x['name'], mydict)
print(*mydict_r1)  # english german

mydict_r2 = map(lambda x: x['rate'] * 10, mydict)
print(*mydict_r2)  # 100 80

mydict_r3 = map(lambda x: x['name'] == "german", mydict)  # Output: [True, False]
print(*mydict_r3)  # False True


## More examples

# sort list
cities = ["New York", "Tokyo", "Warsaw", "London"]
print(sorted(cities, key = lambda k: k.casefold())) # ['London', 'New York', 'Tokyo', 'Warsaw']

nums = [-1, 14, -29, 33]
print(sorted(nums, key = lambda n: n)) # [-29, -1, 14, 33]


# sorting list of tuples
def order_by_amount(point):
    return point.amount

listofw: Tuple[Amount, ...] = (Amount(110, "EUR"), Amount(25, "EUR"), Amount(520, "RON"), Amount(30, "PLN"))
res = sorted(listofw, key=order_by_amount)
print(list(map(lambda x: str(x), res)))
# ['amount: 25, curency: EUR', 'amount: 30, curency: PLN', 'amount: 110, curency: EUR', 'amount: 520, curency: RON']


```

Basic lambda expressions in Java.

##### Java
```java
package tests;
import lombok.Data;
import java.util.ArrayList;
import java.util.List;
import java.util.Optional;
import java.util.function.*;

/**
 * Functional interface
 */
interface Testable {
    int test(String a, Student b);
}

class Index {
    int num;
    Index(int num){
        this.num = num;
    }
    int getIndexNumber(){
        return num;
    }
}

// example Student object
// Lombok
@Data
class Student {

    private String name;
    private int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public Optional<Index> getIndex() {
        return Optional.of(new Index(331));
    }
}

class Operations {

    public static void consumeStudents(List<Student> students, Function<Student, String> function, Consumer<String> consumer) {
        for (Student s : students) {
            consumer.accept(function.apply(s));
        }
    }

    public static List<Student> filterStudents(Supplier<List<Student>> supplier, Predicate<Student> predicate) {
        List<Student> result = new ArrayList<>();

        List<Student> students = supplier.get();

        for (Student s : students) {
            if (predicate.test(s)) { //sprawdz wzgledem predykatu Predicate i jak OK to OK
                result.add(s);
            }
        }

        return result;
    }

    public static List<Student> createData() {
        List<Student> result = new ArrayList<>();
        result.add(new Student("Adam", 31));
        result.add(new Student("John", 29));

        return result;
    }

    public static void testujStatycznaFunkcje(Student student) {
        System.out.println("to jest nasz consumer");
    }

    public static void testujFuncReference(Consumer<Student> consumer) {
        consumer.accept(new Student("Billy", 32));
    }
}

public class App {

    public static void main(String[] args) {


        // ########## Example 1

        // classic anonymous class on Runnable
        Runnable r = new Runnable() {
            @Override
            public void run() {
                System.out.println("runnable");
            }
        };

        // lambda version
        Runnable r2 = () -> {
            System.out.println("runnable");
        };


        // ##### Example 2

        // classic comparable
        Comparable<String> comp1 = new Comparable<String>() {
            @Override
            public int compareTo(String o) {
                return 0;
            }
        };

        // lambda version
        Comparable<String> comp2 = o -> 0;


        // ##### Example 3

        // lambda expression based on custom functional interface
        Testable testElem = (String a, Student stnd) -> {
            return 123;
        };


        // ##### Example 4 - Predicate, Consumer, Supplier, Function
        
        Predicate<Student> over30 = student -> student.getAge() > 30;
        Predicate<Student> nameNotAdam = student -> student.getName() != "Adam";
        Predicate<Student> nameNoIvan = student -> student.getName() != "Ivan";

        // join predicates
        Predicate<Student> polaczonaWartoscWieluPred = over30.and(nameNotAdam).or(nameNoIvan).negate();

        // Consumer example
        Consumer<String> print = text -> System.out.println(text);
        Consumer<String> changeName = s -> {
            System.out.println(s + "-superman");
        };

        // joining consumers together
        Consumer<String> lancuchKonsumerow = print.andThen(changeName);

        // Supplier example
        Supplier<List<Student>> supplyPredefinedStudents = () -> Operations.createData();

        // Function
        Function<Student, String> getStudentName = student -> student.getName();

        // Bi Function
        BiFunction<Student, String, Integer> obrabiajZwrocWiek = (student, co) -> {
            if (co == "wiek") return student.getAge();
            return 20;
        };

        // BinaryOperator - classic anonymous class based on interface
        BinaryOperator<Student> wspolnyKolega = new BinaryOperator<Student>() {
            @Override
            public Student apply(Student student, Student student2) {
                return new Student("Ann", 23);
            }
        };

        // lambda version
        BinaryOperator<Student> wspolnyKolegaLambda = (student, student2) -> new Student("Ann", 23);


        // ##### Example 5 - lambda expresssions based on primitive predicates

        IntPredicate predInt2 = new IntPredicate() {
            @Override
            public boolean test(int value) {
                return false;
            }
        };

        IntSupplier is132 = () -> 0;
        IntConsumer ic134 = value -> {
        };
        IntFunction if136 = value -> null;
        IntSupplier is1322 = () -> 0;
        IntConsumer ic1343 = value -> {
        };
        IntFunction if1362 = value -> null;


        // ##### Example 6 - method's references

        Consumer<Student> consStud = (Student s) -> Operations.testujStatycznaFunkcje(s);
        Consumer<Student> consStud2 = Operations::testujStatycznaFunkcje;
        Consumer<String> print179 = System.out::println;
        Operations.testujFuncReference(Operations::testujStatycznaFunkcje);
        Supplier<List<Student>> supplyPredefinedStudents4 = Operations::createData;
        Function<Student, String> getStudentName192 = Student::getName;
        Supplier<List<Student>> supplyPredefinedStudents210 = Operations::createData;


        // ##### Example 7 - Optional

        Student student = new Student("Ann", 23);
        Optional<Index> index = student.getIndex();
        if (index.isPresent()) {}
        try {
            Index indexOrThrow = student.getIndex().orElseThrow(() -> new Exception("No Index"));
            Index indexOrNull = student.getIndex().orElseGet(null);
            index.ifPresent(i -> {
                System.out.println("index is fine");
            });
        } catch (Exception e) {
            e.printStackTrace();
        }


        index.orElse(new Index(1222));

        // chaining map, filter and optional
        index
                //map
                .map(i -> i.getIndexNumber())
                //filter
                .filter(indexNumber -> indexNumber.equals("213"))
                //handle optional
                .ifPresent(indexNumber -> System.out.println(indexNumber));



        // chaining filter and supplied
        Operations.consumeStudents(
                Operations.filterStudents(supplyPredefinedStudents, over30), getStudentName, print
        );

    }

}

```

Filters, transformers, mappers, generators.

```java
import lombok.Data;

import java.util.*;
import java.util.function.*;

class Index {
    int num;
    Index(int num){
        this.num = num;
    }
    int getIndexNumber(){
        return num;
    }
}

@Data
class Student {

    private String name;
    private int age;

    public Student() {
        this.name = "no name";
        this.age = 20;
    }
    public Student(String name) {
        this.name = name;
        this.age = 0;
    }
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public Optional<Index> getIndex() {
        return Optional.of(new Index(123));
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                '}';
    }
}

/* custom functional interfaces */
@FunctionalInterface
interface MyProcessor<T>{
    T process(T element);
}

@FunctionalInterface
interface FilterInter<S>{
    boolean testMatchB(S element);
}

@FunctionalInterface
interface MyTransformer<T,S>{
    T transform(S v);
}

@FunctionalInterface
interface Operator<R,T,S>{
    R oper(T v1, S v2);
}

class FilterTransformerGenerator {

    static <T> List<T> findAll(Collection<T> src, Predicate<T> p) {
        List<T> trg = new ArrayList<>();
        for(T e : src) if(p.test(e)) trg.add(e);
        return trg;
    }

    static <S,T> List<T> transform(Collection<S> src, Function<S,T> f) {
        List<T> trg = new ArrayList<>();
        for(S e : src) trg.add(f.apply(e));
        return trg;
    }

    static <T> List<T> generate(int n, Supplier<T> s) {
        List<T> trg = new ArrayList<>();
        for(int i = 0; i < n; i++){
            trg.add(s.get()); 
        }
        return trg;
    }

    static <T> void process(Collection<T> src, Consumer<T> c) {
        for(T e : src) c.accept(e);
    }

    public static <T,S> List<T> create(List<S> src, MyTransformer<T,S> t){
        List<T> target = new ArrayList<>();
        for(S s : src){
            target.add(t.transform(s));
        }
        return target;
    }

    public static <R,T,S> List<R> create(List<T> src1, List<S> src2, Operator<R,T,S> o){
        List<R> res = new ArrayList<>();
        for(int i = 0; i < src1.size(); i++){
            res.add(o.oper(src1.get(i), src2.get(i)));
        }
        return res;
    }

    public static FilterInter<String> funcDecorator(int argument){
        return (String x) -> argument == 1 && x == "show_only_that";
    }

    static <T> T sConverter(T elementAlboCos, MyProcessor<T> funkcja){
        return funkcja.process(elementAlboCos);
    }

}




public class Main {

    public static void main(String[] args) {

        List<Student> t = FilterTransformerGenerator.generate(10, Student::new);
        List<Student> out = FilterTransformerGenerator.findAll(t, e -> e.getName() == "Adam");
        FilterTransformerGenerator.process(out, e->e.setName(e.getName() == "no name" ? "John Doe" : e.getName()));
        List<String> eett = FilterTransformerGenerator.transform(t, Student::getName);

        Predicate<Student> mojPredykat1 =  e -> e.getName() == "Marc";
        Predicate<Student> mojPredykat2 =  e -> e.getName() != "Ivan";
        Predicate<Student> mojPredykat3 =  e -> e.getName() != "Adam";

        // chained predicates
        List<Student> out2 = FilterTransformerGenerator.findAll(t, mojPredykat1
                .and(mojPredykat2)
                .or(mojPredykat3)
                .negate()
        );

        // compose operators
        UnaryOperator<String> italic = e -> "<italic>" + e + "</italic>" ;
        UnaryOperator<String> bold = e -> "<bold>" + e + "</bold>" ;
        Function<String,String> kompoz1 = italic.compose(bold);
        Function<String,String> kompoz2 = italic.andThen(bold);
        String s5666 = "Abc def ghi";
        kompoz1.apply(s5666);   //<bold><italic>Abc def ghi</italic></bold>
        kompoz2.apply(s5666);   //<italic><bold>Abc def ghi</bold></italic>

        //Konsumery [Consumer, BiConsumer]
        Consumer<Student> podwyzszNumer = e -> e.setName("No name");
        Consumer<Student> podizelPrzez10 = e -> e.setAge(e.getAge() - 1);
        podwyzszNumer.andThen(podizelPrzez10);

        // creators

        List<String> s = Arrays.asList("dog", "cat", "fish");
        List<String> sn = Arrays.asList("111", "222", "333");
        List<Integer> pos = Arrays.asList(1,3);

        List<String> outtest = FilterTransformerGenerator.create(s, e -> e.toUpperCase());
        // or
        List<String> outtest2 = FilterTransformerGenerator.create(s, String::toUpperCase);


        List<Integer> l2 = FilterTransformerGenerator.create(sn, e -> Integer.parseInt(e));
        // or
        List<Integer> l3 = FilterTransformerGenerator.create(sn, Integer::parseInt);


        List<Student> l4  = FilterTransformerGenerator.create(s, e -> new Student("d"));
        // or
        List<Student> l5 = FilterTransformerGenerator.create(s, Student::new);

        String tekst_a = "dog and cat are at home";
        List<Integer> l6 = FilterTransformerGenerator.create(s, e -> tekst_a.indexOf(e));
        // or
        List<Integer> l7 = FilterTransformerGenerator.create(s, tekst_a::indexOf);

        // 3-args create
        List<String> l8 = FilterTransformerGenerator.create(s, pos, (e1, e2) -> e1.substring(e2));
        // or
        List<String> l9 = FilterTransformerGenerator.create(s, pos, String::substring);

        FilterInter<String> myFunc = FilterTransformerGenerator.funcDecorator(12);
        myFunc.testMatchB("aba"); // false
        myFunc.testMatchB("show_only_that"); // true


        Integer intres = FilterTransformerGenerator.sConverter(10, n -> n * n * n);
        String strres = FilterTransformerGenerator.sConverter(
                "My String", n -> n + " add this ");
    }

}
```

Popular functional interfaces in Java API.
```java
import java.util.*;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class Main {

    public static void main(String[] args) {

        /* A) ActionListener  */

        javax.swing.Timer timer5400 = new javax.swing.Timer(1000, e -> {
            //do something
        });


        /* B) FileFilter, method: actionPerformed */

        java.io.File[] files3408 = new java.io.File("/dir").listFiles(
                f -> f.isFile()
                        && f.getName().endsWith(".php")
                        && f.lastModified() >= 1234567.12
        );


        /* C) Comparator (compare) */

        List<String> myList = Arrays.asList("abcd", "efg", "hijk");

        Collections.sort(myList, (s1, s2) -> s1.length() - s2.length());

        SortedSet<String> testA5 = new TreeSet<>(
                (s1, s2) -> {
                    return 456;
                }
        );


        /* D) Runnable - run() */

        Future<?> ftask = Executors.newSingleThreadExecutor().submit(
                () -> {
                    int abc = 1;
                }
        );

        
        /* E) Callable - call() */

        ExecutorService ex = Executors.newCachedThreadPool();
        Future<String> task = ex.submit(
                () -> new String("xxx")
        );

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

### Generics
##### Python
Approach with **Singledispatch**. 

see https://pypi.org/project/singledispatch/

Example:

```python
import logging
from abc import ABC, abstractmethod
from datetime import datetime
from functools import singledispatch
from typing import Union, Dict


############# classes ##################

class Stringifable(ABC):
    """
    The Stringifable interface
    """

    @abstractmethod
    def get_as_string(self) -> str:
        pass



class ObjectStateLogger(ABC):
    """
    The Loggable interface
    """

    def __init__(self,plevel=logging.INFO,pname='general.log'):
        logging.basicConfig(level=plevel)
        self.__logger = logging.getLogger(pname)

    def log_stringifable(self) -> None:
        if isinstance(self, Stringifable):
            self.__logger.info(self.get_as_string())
        else:
            raise Exception("Not Stringifable element")


class StaticLogger:
    """
    Default, simple static logger
    """
    _logger = None

    @staticmethod
    def log(msg: str, name: str = 'static_logger') -> None:
        if StaticLogger._logger is None:
            logging.basicConfig(plevel=logging.INFO)
            StaticLogger._logger = logging.getLogger(name)

        StaticLogger._logger.info(msg)



############# example of objects (entities) ##################

class EntityTag(ABC):
    pass

class SimpleEntityTag(ABC):
    pass

class Entity(ObjectStateLogger, Stringifable, EntityTag):
    """
    Example of Entity object
    """
    def __str__(self) -> str:
        key_val: Dict[str,str] = {}
        for i in vars(self):
            istr: str = i.strip(' ').replace('_ObjectStateLogger','').replace('_Stringifable','')
            if istr.startswith('__'):
                continue
            key_val[istr] = vars(self)[i]

        return key_val

    def __init__(self, name: str = None):
        super().__init__()
        self.name = name

    def get_as_string(self) -> str:
        return f'[ {datetime.now().strftime("%Y-%m-%d %H:%M:%S")} ] [ {self.__class__} ] {self.__str__()}'



class SimpleEntity(Stringifable,SimpleEntityTag):
    """
    Another example of entity
    """
    def __init__(self, name: str = None):
        super().__init__()
        self.name = name

    def get_as_string(self) -> str:
        return f'[ {datetime.now().strftime("%Y-%m-%d %H:%M:%S")} ] [ {self.__class__} ] {self.name}'




############# Single Dispatch - register some loggers ##################

@singledispatch
def log_state(obj):
    raise NotImplementedError("Cannot log state for this object")


"""
Register logger objects with included logger (extending ObjectStateLogger)
"""
@log_state.register(ObjectStateLogger)
def _(obj:Union[ObjectStateLogger,Stringifable]):

    if not (isinstance(obj,ObjectStateLogger) and isinstance(obj,Stringifable)):
        raise NotImplementedError("Object must be Union[ObjectStateLogger, Stringifable]")

    try:
        obj.log_stringifable()
    except Exception as e:
        print(e)


"""
Register another logger for siple objects without any other logger inside
"""
@log_state.register(Stringifable)
def _(obj: Stringifable):
    try:
        StaticLogger.log(obj.get_as_string())
    except Exception as e:
        print(e)

"""
Register one more logger for simple integers
"""
@log_state.register(int)
def _(*obj: int):
    try:
        StaticLogger.log(f'List of integers: {obj}')
    except Exception as e:
        print(e)



log_state(Entity("My entity"))
log_state(SimpleEntity("My simple entity"))
log_state(1, 2, 3, 4, 5)


# Results:
# INFO:general.log:[ 2019-07-14 20:47:56 ] [ <class '__main__.Entity'> ] {'name': 'My entity'}
# INFO:static_logger:[ 2019-07-14 20:47:56 ] [ <class '__main__.SimpleEntity'> ] My simple entity
# INFO:static_logger:List of integers: (1, 2, 3, 4, 5)

```

Example with custom logger/printer and handler passed to logger as a parameter.

```python

###### test classes ######

class User:
    """
    User class
    """
    def __str__(self) -> Any:
        return f'{self.__class__.__name__ } {{{self.name}}}'

    def __init__(self, name):
        self.name = name


class GreatUser(User):
    """
    GreatUser class
    """
    def __init__(self, name):
        super().__init__(name)


class SuperUser(User):
    """
    SuperUser class
    """
    def __init__(self, name):
        super().__init__(name)




###### static logger  ######

class StaticLogger:
    """
    Default, simple static logger
    """
    _logger = None

    @staticmethod
    def log(obj: List[User], log_producer: Callable[[Type[User]], str] = lambda el: str(el)) -> None:
        if StaticLogger._logger is None:
            logging.basicConfig(level=logging.INFO)
            StaticLogger._logger = logging.getLogger("static_logger")
            pass

        """
        call custom handler
        """
        for i in obj:
            log_producer(i)



######### Logger registration ########

@singledispatch
def log_objects(obj):
    raise NotImplementedError("Cannot log state for this object")


"""
Register logger 
"""
@log_objects.register(User)
def _(*obj:User):
    try:
        StaticLogger.log(obj, lambda uobj: print("User Logger: " + str(uobj)))
    except Exception as e:
        print(e)


log_objects(User("Normal user"), GreatUser("Great user"), SuperUser("Great user"))

# Result:
# User Logger: User {Normal user}
# User Logger: GreatUser {Great user}
# User Logger: SuperUser {Great user}



```

##### Java
Example of generics in Java.

Generic class and methods.

```java
import lombok.*;
import java.util.*;
import java.util.function.Function;

interface DomainObject{}
interface DtoAble {}
interface Dto{}
interface ComparableByExperience<T extends Employee>{
    int compareByExperience(T obj2);
}

@Data
abstract class Person implements DomainObject {
    protected String name;
    protected int age;
    protected int personUniqueId;

    @Override
    public String toString() {
        return "[person]["+personUniqueId+"]";
    }
}

@Getter @Setter @ToString(callSuper=true)
class Employee extends Person implements ComparableByExperience<Employee> {

    private int yearsOfExperience = 0;
    private String name;

    public Employee(String name) {
        this.name = name;
    }

    @Override
    public int compareByExperience(Employee obj2) {
        if(this.getYearsOfExperience() == obj2.getYearsOfExperience()){
            return 0;
        } else if(this.getYearsOfExperience() > obj2.getYearsOfExperience()) {
            return 1;
        } else {
            return -1;
        }
    }
}

/**
 * Contractor is not an Employee
 */
@Getter @Setter @ToString(callSuper=true)
class Contractor extends Person {
    public Contractor() {}
}

/**
 * Supplier is not an Employee
 */
@Getter @Setter @ToString(callSuper=true)
class Supplier extends Person {
    public Supplier() {}
}

@Getter @Setter @ToString(callSuper=true)
class Manager extends Employee {
    public Manager(String name) {
        super(name);
    }
}

@Getter @Setter @ToString(callSuper=true)
class UpperManager extends Manager {
    public UpperManager(String name) {
        super(name);
    }
}

@Getter @Setter @ToString(callSuper=true)
class Director extends UpperManager {
    public Director(String name) {
        super(name);
    }
}

class EmployesByExperience<T extends Employee>
{
    private SortedSet<T> allEmployes = new TreeSet<T>(T::compareByExperience);

    public EmployesByExperience(T ...employes) {
        allEmployes.addAll(Arrays.asList(employes));
    }

    public T getTheMostExperienceEmployee(){
        return this.allEmployes.first();
    }

    public T getTheLessExperiencedEmployee(){
        return this.allEmployes.last();
    }
}

class HROperations {

    public static <S extends Employee, T extends Employee> List<T> updatePosition(List<S> employes, Function<S,T> update) {
        List<T> trg = new ArrayList<>();
        for(S e : employes) trg.add(update.apply(e));
        return trg;
    }

    public static Map<? super Director, Boolean> informUpperManagement(
            List<? super Director> people,
            List<Class<? extends Person>> importantPositions
    ) {

        Map<Person, Boolean> informedPeople = new HashMap<>();

        people.stream().filter(
                p -> importantPositions
                        .stream()
                        .anyMatch(pos -> pos.isAssignableFrom(p.getClass()))
        ).forEach(importantPerson -> {
            // do some stuff... inform needed people
            informedPeople.put((Person) importantPerson, true);
        });

        return informedPeople;
    }

}

```

Test 
```java
import lombok.*;
import java.util.*;
import java.util.function.Function;

public class Main {

    public static void main(String[] args) {

        Director director = new Director("John Doe");

        UpperManager upperManager = new UpperManager("John Alan");
        UpperManager upperManager2 = new UpperManager("Marie Dane");
        UpperManager upperManager3 = new UpperManager("Adrien Doe");

        Manager manager = new Manager("Miroslav Doe");
        Manager manager2 = new Manager("Aaron Doe");
        Manager manager3 = new Manager("Nikita Doe");

        Employee employee = new Employee("Ivan Bee");
        Employee employee2 = new Employee("Mark Doe");
        Employee employee3 = new Employee("Johny Lee");

        // ### test generic method with wildcards

        List<Employee> people = Arrays.asList(
                director,
                upperManager,
                upperManager2,
                upperManager3,
                manager,
                manager2,
                manager3,
                employee,
                employee2,
                employee3
        );

        List<Class<? extends Person>> upperManagement = new ArrayList<>();
        upperManagement.add(Director.class);
        upperManagement.add(UpperManager.class);

        // inform all upper managers
        Map<? super Director, Boolean> informedPeople = HROperations.informUpperManagement(people, upperManagement);

        System.out.println(informedPeople);
        // {UpperManager(super=Manager(super=Employee(super=[person][0], yearsOfExperience=0, name=John Alan)))=true,
        // UpperManager(super=Manager(super=Employee(super=[person][0], yearsOfExperience=0, name=Adrien Doe)))=true,
        // UpperManager(super=Manager(super=Employee(super=[person][0], yearsOfExperience=0, name=Marie Dane)))=true,
        // Director(super=UpperManager(super=Manager(super=Employee(super=[person][0], yearsOfExperience=0, name=John Doe))))=true}



        // ### test generic class

        director.setYearsOfExperience(20);
        upperManager.setYearsOfExperience(4);
        manager.setYearsOfExperience(22);
        employee.setYearsOfExperience(24);

        EmployesByExperience<Employee> EmployesByExperience = new EmployesByExperience(
            director,
            upperManager,
            manager,
            employee
        );

        System.out.println(EmployesByExperience.getTheLessExperiencedEmployee());
        System.out.println(EmployesByExperience.getTheMostExperienceEmployee());

        /* result
        Employee(super=[person][0], yearsOfExperience=24, name=Ivan Bee)
        UpperManager(super=Manager(super=Employee(super=[person][0], yearsOfExperience=4, name=John Alan)))
        */



        // ### test another generic method - transformer

        // give a bonus to all managers or upper managers or director with more then 20 years of experience

        HROperations.updatePosition(people, person -> {

            if(person instanceof Manager) {
                if(person.getYearsOfExperience() > 20){
                    System.out.println("Give a bonus to: " + person);
                }
            }

            return person;
        });

        /*
        result:
        Give a bonus to: Manager(super=Employee(super=[person][0], yearsOfExperience=22, name=Miroslav Doe))
         */

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

### Inner classes

##### Python
```python
class Outer:
    """Outer Class"""

    def __init__(self):
        # instantiating the 'Inner' class
        self.inner = self.Inner()

    def reveal(self):
        # calling the 'Inner' class function inner_method
        self.inner.inner_method("Call inner_method")

    class Inner:
        """Inner Class"""

        def inner_method(self, msg):
            print(msg)

    class InnerAnother:
        """Inner Class"""

        def another_inner_method(self, msg):
            print(msg)


# Access to inner class
Outer().Inner().inner_method("Calling inner_method from Inner class")

# Another example - instantiating InnerAnother class
outer = Outer()
inner = outer.InnerAnother()
inner.another_inner_method("Done!")
```
##### Java
```java
/**
 * Outer and inner class
 */
class Outer {

    /**
     * inner class
     */
    private class Inner {
        public void print() {
            System.out.println("Inner class");
        }
    }

    /**
     * Accessing class inner inside method
     */
    void doSomething() {
        Inner inner = new Inner();
        inner.print();
    }

    void testLocalInnerClass()
    {
        /**
         * method-local inner class
         */
        class LoalInner {
            public void print() {
                System.out.println("Local inner class");
            }
        }

        LoalInner inner = new LoalInner();
        inner.print();
    }
}

/**
 * Example of interface as a base for Anonymous inner class
 */
interface MyInterface {
    public abstract void doSomething();
}

/*public*/
class Test {

    public static void main(String args[]) {
        // Instantiating the outer class
        Outer outer = new Outer();

        // Accessing the doSomething() method.
        outer.doSomething();

        // test local inner class
        outer.testLocalInnerClass();

        /*
         Example of anonymous inner class based on interface
         */
        MyInterface obj = new MyInterface() {
            @Override
            public void doSomething() {
                System.out.println("Anonybous inner class");
            }
        };

        /*
         The same example as above - Lambda expression approach
         */
        MyInterface obj2 = () -> System.out.println("Anonybous inner class");


        /*
        annonymous inner class' object as a parameter of method
         */
        testAnonymous(() -> System.out.println("Anonybous inner class"));

    }

    protected static void testAnonymous(MyInterface obj){
        obj.doSomething();
    }
}
```


### Multiple inheritance

##### Python

Multiple inheritance example:

```python
class MathA:
    def add(self, a, b):
        return a + b;


class MathB:
    def multiply(self, a, b):
        return a * b;


class MathC:
    def power(self, a, b):
        return a ** b;


class Calculation(MathA, MathB, MathC):
    def divide(self, a, b):
        return a / b;


d = Calculation()
print(d.add(10, 30))
print(d.multiply(10, 30))
print(d.divide(20, 50))
print(d.power(2, 4))


# 40
# 300
# 0.4
# 16

```

Resolving "Diamond problem":
```python
class MathAD:
    def calculate(self, a, b):
        print("do sum")
        return a + b


class MathBD:
    def calculate(self, a, b):
        print("do multiply")
        return a * b


class MathCD:
    def calculate(self, a, b):
        print("do power")
        return a ** b


class Calculation(MathAD, MathBD, MathCD):
    def calculate(self, a, b):
        result = MathAD.calculate(self, a, b), MathBD.calculate(self, a, b), MathCD.calculate(self, a, b)
        print("job done")
        return result


calc = Calculation()
res = calc.calculate(2, 3)
print(res)
# do sum
# do multiply
# do power
# job done
# (5, 6, 8)
```
##### Java

Multiple inheritance and solving Diamond Problem based on Interface's default method.

```java
import java.util.HashMap;
import java.util.Map;

interface MathAD{
    default int sum(int a, int b){
        System.out.println("do sum");
        return a + b;
    }

    default int calculate(int a, int b){
        System.out.println("do sum as a calculation");
        return sum(a, b);
    }
}


interface MathBD{
    default int multiply(int a, int b){
        System.out.println("do multiply");
        return a * b;
    }

    default int calculate(int a, int b){
        System.out.println("do multiply as a calculation");
        return this.multiply(a, b);
    }
}

interface MathCD{
    default int power(int a, int b){
        System.out.println("do power");
        return (int) Math.pow(a, b);
    }

    default int calculate(int a, int b){
        System.out.println("do power as a calculation");
        return this.power(a, b);
    }
}


/*public*/
class Calculation implements MathAD, MathBD, MathCD {

    public Map<String, Integer> testCalculate(int a, int b) {

        Map<String, Integer> res = new HashMap<>();
        res.put(MathAD.class.getName(), MathAD.super.calculate(a, b));
        res.put(MathBD.class.getName(), MathBD.super.calculate(a, b));
        res.put(MathCD.class.getName(), MathCD.super.calculate(a, b));

        System.out.println(res);

        return res;
    }

    @Override
    public int calculate(int a, int b) {
        int res = MathBD.super.calculate(a, b);
        System.out.println(res);
        return res;
    }

}




public class Main {
    public static void main(String[] args) {

        Calculation calc = new Calculation();
        calc.calculate(2,3);
        calc.testCalculate(3,4);

//        do multiply as a calculation
//        do multiply
//        6
//        do sum as a calculation
//        do sum
//        do multiply as a calculation
//        do multiply
//        do power as a calculation
//        do power
//        {MathBD=12, MathAD=7, MathCD=81}


    }
}
```

### Singleton patterns

##### Python

Approach with __new__ method.

```python
class Logger():
    def __new__(cls, *args, **kwds):
        it = cls.__dict__.get("__it__")
        if it is not None:
            return it
        cls.__it__ = it = object.__new__(cls)
        it.init(*args, **kwds)
        return it

    def init(self, *args, **kwds):
        pass

    def log(self, msg):
        pass
    
logger = Logger()
logger.log("abc")

another_logger = Logger()
another_logger.log("abc")

print(id(logger))
print(id(another_logger))

# 23358832
# 23358832

```

Metaclass approach

```python
class Singleton(type):
    _instances = {}
    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super(Singleton, cls).__call__(*args, **kwargs)
        return cls._instances[cls]

class Logger(metaclass=Singleton):
    __metaclass__ = Singleton

    def __init__(self, start_point=0):
        self.start_point = start_point;

    def log(txt):
        print("log", txt, 0)

class DifferentLogger(metaclass=Singleton):
    __metaclass__ = Singleton



a = Logger(1)
b = Logger(2)
c = DifferentLogger()
d = DifferentLogger()
print(a is b) # True
print((a is c) or (a is d)) # FALSE
print(c is d) # True

# True
# False
# True
```

Singleton via decorator approach
```python
def singleton(cls):
    instances = {}
    def getinstance():
        if cls not in instances:
            instances[cls] = cls()
        return instances[cls]
    return getinstance

@singleton
class Logger:
    def log(self, txt):
        print("log", txt, 0)

@singleton
class AnotherLogger:
    def log(self, txt):
        print("another log", txt, 0)

logger = Logger()
another_logger = Logger()
another_different_logger = AnotherLogger()
another_different_logger_two = AnotherLogger()

print(logger is another_logger)
logger.log("abc")
another_logger.log("def")
another_different_logger.log("a")
another_different_logger_two.log("b")
print(logger is another_different_logger)
print(another_different_logger is another_different_logger_two)

# True
# log abc 0
# log def 0
# another log a 0
# another log b 0
# False
# True

```

##### Java
```java
class Logger {

    // private constructor to block typical instantiation via new Logger()
    private Logger() {}

    public static Logger getInstance() {
        return SingletonHolder.INSTANCE;
    }

    // any method
    public void log() {}

    /*
        private, static, final inner class - will be available in outer class at all time
        this class will be loaded only if method Logger.getInstance will be called
        and then SingletonHolder.INSTANCE will instantiate Logger object
    */
    private static class SingletonHolder {
        private static final Logger INSTANCE = new Logger();
    }
}

public class Main {
    public static void main(String[] args) {

        /* usage example */
        Logger.getInstance().log();
    }
}

```


### Polymorphism example

##### Python

Polymorphism on class and method level example (implementation with ABC - Abstract Base Classes)


```python
import abc
from typing import Type, Tuple


# Interface Repository
class Repository(abc.ABC):
    @abc.abstractmethod
    def save_data(self) -> None:
        pass

# DB_Repository
class DB_Repository(Repository):
    def __init__(self):
        pass

    def save_data(self, data: str) -> None:
        print("Save data to DB_Repository", " ", data)


# File_Repository
class File_Repository(Repository):
    def __init__(self):
        pass

    def save_data(self, data: str) -> None:
        print("Save data to File_Repository", " ", data)


class Test():
    @staticmethod
    def save_data_to_repository(obj: Type[Repository], data: str) -> Repository:
        obj.save_data(data)

    @staticmethod
    def test_polymorphism_on_class_methods(repos: Tuple[Repository], data: str) -> None:
        for repo in repos:
            repo.save_data(data)


db_repo:DB_Repository = DB_Repository();
file_repo:File_Repository = File_Repository();

Test.save_data_to_repository(db_repo, "Data example 1")
Test.save_data_to_repository(file_repo, "Data example 2")

# Save data to DB_Repository   Data example 1
# Save data to File_Repository   Data example 2

Test.test_polymorphism_on_class_methods((db_repo, file_repo), "test")
# Save data to DB_Repository   test
# Save data to File_Repository   test

```

##### Java
Example of polymorphism.

```java

import java.util.Arrays;

interface Repository{void save_data(String data);}

class DB_Repository implements Repository{
    @Override
    public void save_data(String data) {
        System.out.println("Save data to DB_Repository " + data);
    }
}

class File_Repository implements Repository{
    @Override
    public void save_data(String data) {
        System.out.println("Save data to File_Repository " + data);
    }
}



public class Main {

    public static void main(String[] args) {

        Repository dbRepo = new DB_Repository();
        Repository fileRepo = new File_Repository();

        dbRepo.save_data("data 1");
        fileRepo.save_data("data 2");
        
        testMethods(dbRepo, fileRepo);

        // Save data to DB_Repository data 1
        // Save data to File_Repository data 2
        // Save data to DB_Repository test data
        // Save data to File_Repository test data
    }

    public static void testMethods(Repository ...repos) {
        Arrays
                .stream(repos)
                .forEach(repo -> repo.save_data("test data"));
    }

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

### Builder pattern
##### Python
```python
from abc import ABC, abstractmethod
from typing import Any


class Builder(ABC):
    """
    The Builder interface
    """

    @abstractmethod
    def set_name(self, name: str) -> None:
        pass

    @abstractmethod
    def set_price(self, price: float) -> None:
        pass

    @abstractmethod
    def set_amount(self, amount: int) -> None:
        pass

    @abstractmethod
    def add_ingredient(self, ingredient: str) -> None:
        pass

    @abstractmethod
    def calculate_calories(self) -> int:
        pass

    @abstractmethod
    def pack_product(self) -> None:
        pass

    @abstractmethod
    def build(self) -> None:
        pass


class Product():

    def __init__(self) -> None:
        """
        non arguments constructor
        """
        self.__name = ""
        self.__price = None
        self.__amount = None
        self.__callories = None
        self.parts = [] # ingredients

    def __str__(self) -> None:
        return f"Produc: {self.name}, price:{self.price}, ingredients: {', '.join(self.parts)}"

    @property
    def name(self) -> str:
        return self.__name

    @name.setter
    def name(self, name: str) -> None:
        self.__name = name

    @property
    def price(self) -> float:
        return self.__price

    @price.setter
    def price(self, price: float) -> None:
        self.__price = price

    @property
    def amount(self) -> int:
        return self.__amount

    @amount.setter
    def amount(self, amount: int) -> None:
        self.__amount = amount

    def add_ingredient(self, part: str) -> None:
        self.parts.append(part)

    def calculate_calories(self) -> int:
        print("calculate callories")
        for i in self.parts:
            self.__callories += 10

        return self.__callories

    def pack_product(self) -> None:
        print("pack product")
        pass

class ProductBuilder(Builder):
    """
    The Concrete Builder classes follow the Builder interface and provide
    specific implementations of the building steps. Your program may have
    several variations of Builders, implemented differently.
    """

    def __init__(self) -> None:
        """
        A new builder instance should contain a blank product object
        """
        self.reset()

    def reset(self) -> None:
        """
        Reset builder, create a new empty opject inside
        """
        self.__product = Product()

    def __product(self) -> Product:
        """
        private product method, to disallow getting Product
        and force us to use build() method instead
        """
        pass

    def build(self) -> Product:
        """
        Build a Product object and return.
        After build reset Builder to be prepared for further
        usage and for any new builds
        """
        product = self.__product
        self.reset()
        return product

    def set_name(self, name: str) -> None:
        self.__product.name = name

    def set_price(self, price: float) -> None:
        self.__product.price = price

    def set_amount(self, amount: int) -> None:
        self.__product.amount = amount

    def add_ingredient(self, ingredient: str) -> None:
        self.__product.add_ingredient(ingredient)

    def calculate_calories(self) -> int:
        return self.__product.calculate_calories()

    def pack_product(self) -> None:
        self.__product.pack_product()


class Director:
    """
    The Director is used if we want to order building steps in a
    particular sequence.
    """

    def __init__(self) -> None:
        self._builder = None

    @property
    def builder(self) -> Builder:
        return self._builder

    @builder.setter
    def builder(self, builder: Builder) -> None:
        """
        The Director works with any builder instance that the client code passes
        to it. This way, the client code may alter the final type of the newly
        assembled product.
        """
        self._builder = builder

    """
    We can set up many various sequences of building process
    """

    def build_product_with_calories_info(self, name: str, amount: int) -> Any:
        self.builder.set_name(name)
        self.builder.set_amount(amount)
        self.builder.calculate_calories()
        return self.builder.build()

    def build_product_and_pack(self, name: str, amount: int) -> Any:
        self.builder.set_name(name)
        self.builder.set_amount(amount)
        self.builder.pack_product()
        return self.builder.build()


if __name__ == "__main__":

    builder = ProductBuilder()

    # #### build products

    builder.set_name("Product 1")
    builder.set_price(122.12)
    builder.set_amount(30)
    builder.add_ingredient("Ingredient A")
    builder.add_ingredient("Ingredient B")
    product1: Product = builder.build();

    builder.set_name("Product 2")
    builder.set_price(31.12)
    builder.set_amount(10)
    product2: Product = builder.build();

    print(product1, product2)
    print(product1 is product2)

    # Produc: Product 1, price:122.12, ingredients: Ingredient A, Ingredient B Produc: Product 2, price:31.12, ingredients:
    # False

    # #### using Director for setting up building steps in an order
    director = Director()
    my_builder = ProductBuilder()
    director.builder = my_builder
    product3: Product = director.build_product_with_calories_info("Procut 3", 1)
    product4: Product = director.build_product_and_pack("Procut 4", 1)
    print(product3, product4)
    # calculate
    # callories
    # pack product
    # Produc: Procut 3, price: None, ingredients: Produc: Procut 4, price: None, ingredients:

```
##### Java
```java
import lombok.Data;

import java.math.BigDecimal;
import java.math.RoundingMode;

@Data
class Product {

    private String name;
    private BigDecimal price;
    private Integer amount;

    private Product(String name, BigDecimal price, Integer amount) {
        this.name = name;
        this.price = price;
        this.amount = amount;
    }

    /**
     * Builder as an inner class inside our outer class
     */
    public static class ProductBuilder {

        // some default values (recommended)
        private String name;
        private BigDecimal price;
        private Integer amount = 1;

        public ProductBuilder setName(String name) {
            this.name = name;
            return this;
        }

        public ProductBuilder setPrice(BigDecimal price) {
            this.price = price.setScale(2, RoundingMode.HALF_DOWN);
            return this;
        }

        public ProductBuilder setAmount(Integer amount) {
            this.amount = amount;
            return this;
        }


        public Product build() {

            // Inner class ProductBuilder has an access to private constructor
            // from outer class Product, so we can instantiate Product object here

            return new Product(name, price, amount);
        }
    }
}


public class Main {

    public static void main(String[] args) {

        Product Product = new Product.ProductBuilder()
                .setName("Car")
                .setAmount(3)
                .setPrice(new BigDecimal(10.15))
                .build();

        System.out.println(Product);
        
        // Product(name=Car, price=10.15, amount=3)
    }

}
```
