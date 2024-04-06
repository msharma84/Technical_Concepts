# Functional Programming in Java

Advantage : 
1.   no boilerplate code in java
2.   move from declarative programming to imperative programming

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
1. **intermediate operations** - such as filter, map or sort return a stream so we can chain multiple intermediate operations.
            anyMatch(), distinct(), filter(), findfirst(), flatMap(), map(), skip(), sorted()
2. **terminal operations** - such as forEach, collect or reduce are either void or return a non-stream result. Only one terminal operation has been allowed.
        Collect saves the elements into a Collection, other operations reduces the stream into a single summary element.
        count(), max(), min(), reduce(), summaryStatistics
