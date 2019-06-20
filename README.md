
## Data structures

#### List comprehension

* Python
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

* Java

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



##### Object encapsulation


* Python

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
    
* Java
    
    ```java
    
    // class with private constructor and builder as an inner class inside
    
    public class House {
    
        String adress;
        Integer floorsNumer;
        Integer doorsNumber;
    
        // private constructor to disallow developer to instantiate class via this constructor
        // this constructor will be used only internally, in the self::build() method
    
        private House(String adress, Integer floorsNumer, Integer doorsNumber) {
            this.adress = adress;
            this.floorsNumer = floorsNumer;
            this.doorsNumber = doorsNumber;
        }
    
        // Builder as an inner class inside our outer class
    
        public static class HouseBuilder {
    
            // some default values (recommended)
            // here we can set up default values we want to have if they are not settled
    
            private String adress;
            private Integer floorsNumer = 1;
            private Integer doorsNumber = 1;
    
            public HouseBuilder setAdress(String adress) {
                this.adress = adress;
                return this;
            }
    
            public HouseBuilder setFloorsNumer(Integer floorsNumer) {
                this.floorsNumer = floorsNumer;
                return this;
            }
    
            public HouseBuilder setDoorsNumber(Integer doorsNumber) {
                this.doorsNumber = doorsNumber;
                return this;
            }
    
    
            public House build() {
    
                // Inner class HouseBuilder has an access to provate constructor
                // from outer class House, so we can instantiate House object here
    
                return new House(adress, floorsNumer, doorsNumber);
            }
        }
    }
    ```