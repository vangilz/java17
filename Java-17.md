# Java 17
* 11: 25-sept-2018
* 17: 14-sept-2021

## Why Java 17
* Many bug fixes and security improvements
* Premier support for Java 11 ends Sept-2023. Extended support ($$) after that.
* Instant performance boost. 
  Java 17 is about 8.5% faster than Java 11 on G1 GC and 6.5% on parallel GC ([source](https://www.optaplanner.org/blog/2021/09/15/HowMuchFasterIsJava17.html)).
* Spring Boot 3+ requires it.
* ABN-AMRO and Microsoft support it completely.
* It makes sense to use it for new projects.
* No need to immediately use all new features.
* It's fun to use new things!

## Why not?
* Requires new skills, also for future maintainers
* Infra might not be up to date (IDE, SonarQube, build agents)
* Exisiting projects: not enough benefit
* Libraries that do not work on a Java 17 JVM
* It might be scary to do things differently

## Some of the new features
### Records
Implictly final, immutable. More readable/understandable. No more getters/setters/toString/hashCode/equals methods. Efficient on JVM. No need for Lombok.
```java
record Point(long x, long y) { }

var p = new Point(15,20);
var x = p.x();
```

### Text blocks
```java
String newTextBlock = """
    <html>
        <body>
            <em>Cool LTS Java 17 Features</em>\
        </body>
    </html>
    """;
```

### Helpful NullPointerException guidance
In case of NPE, the exact name of the variable that was null is logged.


### Better instanceOf
```java
if (obj instanceof Person p) {
    System.out.println("obj is a Person: " + p.getName());
}
```


### Switch expression
Without the error-prone fall-through, pattern matching

```java
enum PaymentStatus {
    UNPAID, PARTPAID, PAID, DISPUTED, UNKNOWN;
}

public class Main {
    public static void main(String[] args) {
        PaymentStatus paymentStatus = PaymentStatus.PARTPAID;

        String message = switch (paymentStatus) {
            case UNPAID -> "The order has not been paid yet.";
            case PARTPAID -> "The order is partially paid.";
            case PAID -> "The order is fully paid.";
            default -> throw new IllegalStateException("Invalid status: " + paymentStatus);
        };

        System.out.println(message);
    }
}
```

### Sealed classes
Avoid the `default` case in switches or if/then/else.
```java
public abstract sealed class Animal
    permits Dog, Cat {
}
public final class Dog extends Animal {
}
public final class Cat extends Animal {
}
```

### Improved streams API
For example, instead of
```java
myStream.collect(Collectors.toList())
```
simply do
```java
myStream.toList();
```

