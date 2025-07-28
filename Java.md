# Functional Programming in Java

Advantage : 
1.   no boilerplate code in java
2.   move from declarative programming to imperative programming (program is structured as a sequence of instructions)

Why Lamdas ?

Enables functional programming
Readable and concise code
Easier to use API and Libraries
Enables support parallel programming

Lamdas are function in isolation, they are not being part of a particular class 

Stream bring functional programming to Java, and are supported started in Java8

Advantages of Stream : 
1.   Make heavy use of Lamda expression
2.   ParallelStreams make it very easy to multi-threaded operations.

A Stream pipeline consists of a source, followed by zero or more intermediate operations and terminal operations.
Stream source
     Stream can be created from Collections, Lists, Sets,Arrays,line of files

Stream operations are either intermediate or terminal
1. **intermediate operations** - such as filter, map or sort return a stream so we can chain multiple intermediate operations. It can also transfer one stream to another       stream. They can't be executed until a terminal operation is invoked.
         distinct(), filter(), flatMap(), map(), skip(), sorted()
2. **terminal operations** - such as forEach, collect or reduce are either void or return a non-stream result. Only one terminal operation has been allowed.
        Collect saves the elements into a Collection, other operations reduces the stream into a single summary element.
         anyMatch(), allMatch(), noneMatch(), findfirst(), findAny(), count(), max(), min(), reduce(), summaryStatistics

Consumer Functional Interface - Consumer can be used in all contexts where an object needs to be consumed i.e. it takes as input, and some  
operation to be performed on the object without returning any result.

Supplier Functional Interface - Supplier functional interface can be used in all contexts where there is no input but output expected.

Predicate Functional Interface - This functional interface used for conditional check, we can use these true/false returning functions in day to day programming we should choose predicate

## Basic Level

- How do you create a stream from a list of integers
   
    ```
    List<Integer> integerList = Arrays.asList(1,2,3,4,5);
    Stream<Integer> stream = integerList.stream();
    stream.forEach(System.out::println);
   ```
    
- Find the longest String in a list

  ```
  List<String> fruits1 = List.of("apple", "pineapple", "mango", "guava", "orange", "banana");
  Optional<String> longestString = fruits1.stream().max(Comparator.comparingInt(String::length));
  System.out.println(longestString.get());
  ```
    
- How do you convert a stream back to a list
   
   ```
    Stream<Integer> stream = Stream.of(5,4,3,2,1);
    List<Integer> integerList = stream.collect(Collectors.toList());
    integerList.forEach(System.out::println);
   ```
   
- How do you find the count of elements in a stream
   
   ```  
    List<Integer> integerList = Arrays.asList(1,2,3,4);
    long count = integerList.stream().count();
    System.out.println(count);
    ```
   
- How do you filter even numbers from a list using streams
   
     ```
    List<Integer> integerList = Arrays.asList(1,2,3,4,5,6,7,8,9);
    List<Integer> evenList = integerList
            .stream()
            .filter(n->n%2==0)
            .collect(Collectors.toList());
    evenList.forEach(System.out::println);
     ```
     
- How do you transform a list of strings to uppercase using streams
   
    ```
    List<String> stringList = Arrays.asList("apple","banana","orange");
    List<String> upperStringList = stringList
            .stream()
            .map(String::toUpperCase)
            .collect(Collectors.toList());
    upperStringList.forEach(System.out::println);
     ```
    
- How do you sort a list of numbers using streams
   
    ```
    List<Integer> integerList = Arrays.asList(4,2,7,3,5,1);
    List<Integer> sortedList = integerList
            .stream()
            .sorted()
            .collect(Collectors.toList());
    sortedList.forEach(System.out::println);
     ```
    
- How do you limit a stream to the first 5 elements
   
    ```
    List<Integer> integerList = Arrays.asList(1,2,3,4,5,6,7,8,9);
    integerList
        .stream()
        .limit(5)
        .forEach(System.out::println);
     ```
    
- How do you skip the first 3 elements in a stream

    ```
    List<Integer> integerList = Arrays.asList(1,2,3,4,5,6,7,8,9);
    integerList
            .stream()
            .skip(3)
            .forEach(System.out::println);
     ```
    
- How do you find the first element of a stream

    ```
    List<Integer> integerList = Arrays.asList(8,2,3,4,5);
    Optional<Integer> firstElement = integerList.stream().findFirst();
    firstElement.ifPresent(System.out::println);
     ```
    
- How do you check if all elements in a stream match a given condition
    
     ```
    List<Integer> integerList = Arrays.asList(2,4,6,8);
    boolean allEven = integerList.stream().allMatch(n->n%2==0);
    System.out.println("All Even :- "+allEven);
     ```

- How do you check if any element in a stream matches a given condition
     ```
    List<Integer> integerList = Arrays.asList(2,4,5,6,8);
    boolean anyMatch = integerList.stream().anyMatch(n->n%2==1);
    System.out.println("Is Odd in Even list :- "+anyMatch);
     ```
     
- How do you remove duplicate elements from a list using streams
    
    ```
    List<Integer> integerList = Arrays.asList(1,2,3,4,1,5,2,7,8);
    List<Integer> distinctList = integerList.stream().distinct().collect(Collectors.toList());
    distinctList.forEach(System.out::println);
     ```
    
- How do you collect elements from a stream into a Set
    
     ```
    List<Integer> integerList = Arrays.asList(1,2,3,4,1,5,6,7,5);
    Set<Integer> integerSet = integerList.stream().collect(Collectors.toSet());
    integerSet.forEach(System.out::println);
     ```
     
- How do you create a stream from an array
    
     ```
    Integer[] numberArray = {1, 2, 3, 4, 5};
    Stream<Integer> integerStream = Stream.of(numberArray);
    integerStream.forEach(System.out::println);
     ```
     
- Find the Product of All Elements in a List
    
     ```
     List<Integer> integerList = Arrays.asList(1,2,3,4);
     int product = integerList.stream().reduce(1, (a, b) -> a * b);
     System.out.println(product);
     ```

- Convert a List of Integers to Their Squares
    
     ```
     List<Integer> integerList = Arrays.asList(1,2,3,4);
     List<Integer> squaredIntegerList =  integerList.stream().map(n -> n*n).collect(Collectors.toList());
     System.out.println(squaredIntegerList);
     ```
     
 - Find the Average of All Elements in a List
    
     ```
     List<Integer> integerList = Arrays.asList(1,2,3,4);
     double average = integerList.stream().mapToInt(Integer::intValue).average().orElse(0);
     System.out.println(average);
     ```
       
- How to sort custom objects before collecting
    
    ```
    class Person{

    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public int getAge() {
        return age;
    }

    public String getName() {
        return name;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
          }
      }
    public class SortCustomObjectsExample {

    public static void main(String[] args) {
        Person p1 = new Person("Ram",17);
        Person p2 = new Person("Shyam",19);
        Person p3 = new Person("Manish",16);
        Person p4 = new Person("Suresh",18);
        List<Person> personList = new ArrayList<>();
        personList.add(p1);
        personList.add(p2);
        personList.add(p3);
        personList.add(p4);
        /*List<Person> sortedPersonList = personList
                .stream()
                .filter(p-> p.getAge()>18)
                .collect(Collectors.toList());
        sortedPersonList.forEach(System.out::println);*/
        /*List<Person> sortedListPerson = personList
                .stream()
                .sorted((objP1,objP2)->Integer.compare(objP1.getAge(),objP2.getAge()))
                .collect(Collectors.toList());
        sortedListPerson.forEach(System.out::println);*/
        // Reverse Sort Order
        /*List<Person> sortedListPerson = personList
                .stream()
                .sorted((objP1,objP2)->Integer.compare(objP2.getAge(),objP1.getAge()))
                .collect(Collectors.toList());
        sortedListPerson.forEach(System.out::println);*/
        // Sort by Name
        List<Person> sortedListPerson = personList
                .stream()
                .sorted(Comparator.comparing(Person::getName))
                .collect(Collectors.toList());
    }
     ```
    
- How to get values from List containing Optional values
    
     ```
    List<Optional<String>> listOfOptionals = Arrays.asList(
            Optional.empty(),
            Optional.of("Element 1"),
            Optional.empty(),
            Optional.of("Element 2"));
        
    List<String> filteredList = listOfOptionals.stream()
                                    .filter(Optional::isPresent)
                                    .map(Optional::get)
                                    .collect(Collectors.toList());
        
    for(String s : filteredList) {
            System.out.println(s);
        }
     ```

## Intermediate Level

- How do you find the sum of a list of integers using streams

  ```
  List<Integer> list = Arrays.asList(1,2,3,4,5);
  int count = list.stream().mapToInt(Integer::intValue).sum();
  System.out.println(count);
  ```

- How do you find the maximum and minimum values in a stream

  ```
  List<Integer> list = Arrays.asList(1,2,3,4,5);

   Optional<Integer> max = list.stream().max(Integer::compareTo);
   Optional<Integer> min = list.stream().min(Integer::compareTo);

   max.ifPresent(System.out::println);
   min.ifPresent(System.out::println);
  ```

- How do you find the average of numbers in a list using streams

  ```
  List<Integer> list = Arrays.asList(1,2,3,4,5);
  double average = list.stream().mapToInt(Integer::intValue).average().orElse(0.0);
  System.out.println("Average - "+average);
  ```

- Find the Sum of Digits of a Number

  ```
  int number = 123456;
  int total = String.valueOf(number)
                .chars()
                .map(Character::getNumericValue)
                .sum();
  System.out.println("Total : "+total);
  ```
  
- How do you concatenate multiple lists into a single stream

  ```
   List<Integer> l1 = Arrays.asList(1,2);
   List<Integer> l2 = Arrays.asList(3,4);
   List<Integer> l3 = Arrays.asList(5,6);

   Stream<Integer> concatenatedStream  = Stream.concat(l1.stream(),l2.stream());
   concatenatedStream = Stream.concat(concatenatedStream,l3.stream());

   concatenatedStream.forEach(System.out::println);
  ```

 - How to merge two sorted list into a single sorted list using java streams

   ```
   List<Integer> list1 = Arrays.asList(1, 3, 5, 7, 9);
   List<Integer> list2 = Arrays.asList(2, 4, 6, 8, 10);

   List<Integer> sortedIntegersList =
                Stream.concat(list1.stream(),list2.stream())
                       .sorted().collect(Collectors.toList());
   System.out.println(sortedIntegersList);
   ```
   
 - How do you group a list of numbers into even and odd using streams

   ```
   List<Integer> list = Arrays.asList(1,2,3,4,5,6,7,8,9);
   Map<Boolean,List<Integer>> evenOdd = list.stream().collect(Collectors.partitioningBy(num -> num%2==0));

   List<Integer> evenList = evenOdd.get(true);
   List<Integer> oddList = evenOdd.get(false);

   System.out.println(evenList);
   System.out.println(oddList);
   ```

 - How do you group a list of employees by department using streams
   ```
   class Employee{

    private String name;
    private String department;

    public Employee(String name, String department) {
        this.name = name;
        this.department = department;
    }

    public String getName() {
        return name;
    }

    public String getDepartment() {
        return department;
    }

    @Override
    public String toString() {
        return "Employee{" +
                "name='" + name + '\'' +
                ", department='" + department + '\'' +
                '}';
       }
     }

   public class GroupByDepartmentUsingStreams {

    public static void main(String[] args) {

        List<Employee> employeeList = new ArrayList<>();
        employeeList.add(new Employee("Manish","IT"));
        employeeList.add(new Employee("Ramesh","HR"));
        employeeList.add(new Employee("Mahesh","IT"));
        employeeList.add(new Employee("Suresh","HR"));

        Map<String,List<Employee>> employeeByDepartment =  employeeList
                .stream()
                .collect(Collectors.groupingBy(Employee::getDepartment));

       employeeByDepartment.forEach( (department, emplList) ->{
           System.out.println("Department : "+department);
           emplList.forEach(System.out::println);
       });
     }
   }
      ```

- How do you find the second highest number in a list using streams

  ```
      List<Integer> list = Arrays.asList(1,2,3,4,5,6);
      Optional<Integer> second = list.stream().sorted((a, b) -> b-a).skip(1).findFirst();
      second.ifPresent(value -> System.out.println("Second : " +value));
   ```

- How do you partition a list of numbers into two groups: greater than 10 and less than 10

  ```
       List<Integer> list = Arrays.asList(3,13,4,14,5,15,6,16);

        Map<Boolean,List<Integer>> partitionMap = list.stream()
                .collect(Collectors.partitioningBy(n-> n>10 ));

        List<Integer> greaterThan10List = partitionMap.get(true);
        List<Integer> lessThan10List = partitionMap.get(false);

        System.out.println("Greater Than 10 :- "+greaterThan10List);
        System.out.println("Less Than 10 :- "+lessThan10List);
  ```

 - How do you count occurrences of each word in a list using streams

   ```
        List<String> words = Arrays.asList("apple","banana","orange","mango","apple","orange");
        Map<String,Long> wordCount =  words.stream()
                .collect(Collectors.groupingBy(word -> word,Collectors.counting()));
        wordCount.forEach((word,count) -> System.out.println(word + " : " +count));
   ```

 - How do you remove null values from a list using streams

    ```
         List<String> words = Arrays.asList("apple","banana",null,"mango",null,"orange");
         List<String> nonNullList =  words.stream()
                .filter(word -> word != null)
                .collect(Collectors.toList());

         System.out.println("Non Null List : "+nonNullList);
    ```
 - How do you concatenate all strings in a list into a single string using streams

   ```
   List<String> words = Arrays.asList("apple","banana","orange","mango");
   String concatenatedString = words.stream()
                .collect(Collectors.joining(","));

   System.out.println("Concatenated String : "+concatenatedString);
   ```

 - Find the intersection of two lists using Java streams

   ```
   List<Integer> list3 = Arrays.asList(1, 2, 3, 4, 5);
   List<Integer> list4 = Arrays.asList(3, 4, 5, 6, 7);
   List<Integer> intersection = list3.stream().filter(list4::contains).collect(Collectors.toList());
   System.out.println(intersection);
   ```
   
 - How do you find duplicate elements in a list using streams

   ```
   List<String> words = Arrays.asList("apple","banana","orange","mango","apple","orange");
   Set<String> seen = new java.util.HashSet<>();
   List<String> duplicateWords = words.stream()
                .filter(word -> !seen.add(word))
                .collect(Collectors.toList());
   duplicateWords.forEach(System.out::println);
   ```

 - How do you find the remove the duplicate from a list using streams

   ```
   List<String> words = Arrays.asList("apple","banana","orange","mango","apple","orange");
   List<String> uniqueList = words.stream().distinct().collect(Collectors.toList());
   System.out.println(uniqueList);
   ```

 - How do you get the top 3 highest numbers from a list using streams

   ```
   List<Integer> list = Arrays.asList(1,2,3,4,5,6);
   List<Integer> topThree =  list.stream()
                .sorted((a,b)-> b-a)
                .limit(3)
                .collect(Collectors.toList());
   topThree.forEach(System.out::println);
   ```

 - How do you get the kth smallest element in an array using Java streams

   ```
   int[] array = {4, 2, 7, 1, 5, 3, 6};
   int k = 5; // Find the 3rd smallest element
   int kthSmallest = Arrays.stream(array)
                .sorted()
                .skip(k-1)
                .findFirst()
                .orElse(-1);

        System.out.println(kthSmallest);
   ```  
 - How do you convert a list of strings into a map of string-length pairs

   ```
   List<String> words = Arrays.asList("apple", "banana", "orange", "grape");
   Map<String,Integer> wordLengthMap = words.stream()
                .collect(Collectors.toMap(word -> word, word -> word.length()));
   wordLengthMap.forEach((word, length) -> System.out.println(word +" : "+length));
   ```

- How do you find the longest word in a list using streams
  
  ```
  List<String> words = Arrays.asList("apple","banana","orange","mango","pineapple");
   Optional<String> longest =  words.stream()
                .max(Comparator.comparingInt(String::length));
   longest.ifPresent(word -> System.out.println("Longest Word : "+word));
  ```

- How do you merge two maps using streams
  
  ```
   Map<String,Integer> map1 = new HashMap<>();
   map1.put("apple",1);
   map1.put("banana",2);

   Map<String,Integer> map2 = new HashMap<>();
   map2.put("orange",3);
   map2.put("mango",4);

   Map<String,Integer> mergedMap = Stream
                .concat(map1.entrySet().stream(),map2.entrySet().stream())
                .collect(Collectors.toMap(
                        Map.Entry::getKey,
                        Map.Entry::getValue,
                        (value1,value2) -> value1 + value2
                ));

   mergedMap.forEach((key,value) -> System.out.println(key + " : "+ value));
  ```

- How do you extract a sublist based on a condition using streams

  ```
  List<Integer> numbers = Arrays.asList(5, 12, 3, 18, 7, 10, 21);
  List<Integer> list = numbers.stream()
                .filter(n -> n>10)
                .filter(n -> n%2==0)
                .collect(Collectors.toList());
   list.forEach(System.out::println);
  ```

- How to get Transaction based on day using streams

  ```
     class Transaction{

         private String date;
         private int amount;

         public Transaction(String date,int amount) {
             this.amount = amount;
             this.date = date;
         }
     
         public String getDate() {
             return date;
         }

         public void setDate(String date) {
             this.date = date;
         }
     
         public int getAmount() {
             return amount;
         }

         public void setAmount(int amount) {
             this.amount = amount;
         }
     }

     List<Transaction> transactions = Arrays.asList(
                new Transaction("2022-01-01", 100),
                new Transaction("2022-01-01", 200),
                new Transaction("2022-01-02", 300),
                new Transaction("2022-01-02", 400),
                new Transaction("2022-01-03", 500)
        );

        Map<String,Integer> sumByDay =
                    transactions.stream()
                            .collect(Collectors.groupingBy(Transaction::getDate,
                                    Collectors.summingInt(Transaction::getAmount)));
        sumByDay.forEach((day,amount) -> {
            System.out.println("Day :"+day +" wise Amount :"+amount);
        });

  ```
- Moved all non-zero element to left and zeros to right of a list
  
  ```
  List<Integer> numbers = Arrays.asList(1,0,3,2,-1,0,6,0,0,8);
        List<Integer> movedZeros = Stream.concat(numbers.stream().filter(n -> n!= 0),
                        numbers.stream().filter(n -> n==0))
                        .collect(Collectors.toList());
        System.out.println(movedZeros);
  ```
  
## Advanced Level

- How do you implement a custom collector

  ```
  class Person{

    private String name;
    private Integer age;

    public Person(String name, Integer age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public Integer getAge() {
        return age;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age='" + age + '\'' +
                '}';
         }
     }
  public class CustomCollector {

    public static void main(String[] args) {

        List<Person> personList = new ArrayList<>();
        personList.add(new Person("Ramesh", 35));
        personList.add(new Person("Suresh", 30));
        personList.add(new Person("Mahesh", 25));
        personList.add(new Person("Rakesh", 20));

        TreeSet<Person> sortedPerson = personList.stream()
                .collect(new TreeSetCollector<>(Comparator.comparingInt(person -> person.getAge())));

        sortedPerson.forEach(p -> System.out.println(p));
         }
     }

     class TreeSetCollector<T> implements Collector<T, TreeSet<T>, TreeSet<T>> {

    private final Comparator<? super T> comparator;

    public TreeSetCollector(Comparator<? super T> comparator) {
        this.comparator = comparator;
    }

    @Override
    public Supplier<TreeSet<T>> supplier() {
        return () -> new TreeSet<>(comparator);
    }

    @Override
    public BiConsumer<TreeSet<T>, T> accumulator() {
        return TreeSet::add;
    }

    @Override
    public BinaryOperator<TreeSet<T>> combiner() {
        return (set1, set2) -> {
            set1.addAll(set2);
            return set1;
        };
    }

    @Override
    public Function<TreeSet<T>, TreeSet<T>> finisher() {
        return Function.identity();
    }

    @Override
    public Set<Characteristics> characteristics() {
        return Collections.unmodifiableSet(EnumSet.of(Characteristics.UNORDERED));
         }
     }
  ```
- How do you sort a list of objects based on multiple fields using streamsy

   ```
   List<Person> personList = new ArrayList<>();
   personList.add(new Person("Ramesh", 35));
   personList.add(new Person("Suresh", 30));
   personList.add(new Person("Mahesh", 20));
   personList.add(new Person("Rakesh", 20));

   List<Person> sortedPeople = personList.stream()
                .sorted(Comparator.comparingInt((Person person) -> person.getAge())
                        .thenComparing(person -> person.getName()))
                .collect(Collectors.toList());

   System.out.println("Sorted people by age and name: " + sortedPeople);
   ```

 - How do you handle exceptions inside stream operations

   ```
   public class HandleExceptionsInStreams {

    public static void main(String[] args) {

        List<String> words = Arrays.asList("apple", "banana", "orange", "mango");
        List<Integer> length = words.stream()
                .map(word -> {
                    try {
                        return getLength(word);
                    } catch (Exception e) {
                        System.err.println("Error while processing the word : "+word);
                        return -1;
                    }
                }).collect(Collectors.toList());
    }


    private static int getLength(String word) throws Exception {
        if (word.equals("banana")) {
            throw new CustomException("Banana is not allowed");
        }
        return word.length();
         }
     }

   class CustomException extends Exception {
    public CustomException(String message) {
        super(message);
         }
     }
   ```

 - How do you find the most frequently occurring element in a list using streams

   ```
     List<String> list = Arrays.asList("apple","banana","orange","apple","orange","mango");
     Optional<Map.Entry<String, Long>> frequency = list.stream()
                .collect(Collectors.groupingBy(e -> e,Collectors.counting()))
                .entrySet()
                .stream()
                .max(Map.Entry.comparingByValue());

     frequency.ifPresent(entry ->{
            System.out.println("Most frequent element : "+entry.getKey() + " with frequency "+entry.getValue());
        });
   ```

 - Remove Vowel from a String

   ```
   String str = "Hello World";
   String nonVowelString = str.chars()
                .filter(ch -> !"aeiouAEIOU".contains(String.valueOf((char) ch)))
                .mapToObj(ch -> String.valueOf((char) ch))
                .collect(Collectors.joining());

   System.out.println("Removal of vowel : "+nonVowelString);
   ```
   
 -  Sort a Map according to the values

   ```
     Map<String,Integer> myMap = new HashMap<>();
        myMap.put("A",10);
        myMap.put("B",60);
        myMap.put("C",20);
        myMap.put("D",50);
        myMap.put("E",40);
        myMap.put("F",30);

       LinkedHashMap<String,Integer> sortedByValue = myMap.entrySet()
                .stream()
                .sorted(Map.Entry.comparingByValue())
                .collect(Collectors
                        .toMap(Map.Entry::getKey,
                                Map.Entry::getValue,
                                (e1,e2)->e1,
                                LinkedHashMap::new));

       sortedByValue.forEach( (key,value) ->
                       System.out.println(key +"-"+value)
               );
  ```





   




 

