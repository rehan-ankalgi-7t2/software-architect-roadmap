# Encapsulation 💊
![](https://www.scientecheasy.com/wp-content/uploads/2018/06/encapsulation-in-java.png)

> wrapping of data under a single unit
- binds to code a data together
- variables (data) are hidden from other classes
- variables can only be accessed using member functions declared inside the class
- `DATA HIDING`

## Key Components of Encapsulation
1. Data hiding
2. access modifiers
3. getters and setters

### Access Modifiers

- **default** - access within the package
- **Private** - access within the declaring class
- **Protected** - access within the declaring class and inherited subclasses (using parent constructor)
- **Public** - accessible from anywhere, no restrictions

Accessibility Matrix

![](https://stackify.com/wp-content/uploads/2017/11/word-image-20.png)

### Getters & Setters

**Getter Method**
- retrieves a private variables value from within the class
- provides controlled access to thhe variables
    ````Java
    public class Person {
        private String name;

        public Person(String name) {
            this.name = name;
        }

        public String getName() {
            return name;
        } 
    }
    ````

**Setter Method**
- updates the value os a private variable
    ````Java
    public class Person {
        private String name;

        public Person(String name) {
            this.name = name;
        }

        public void setName(String newName) {
            name = newName;
        } 
    }
    ````

### Encapsulation example in java
````Java
public class Person {
     private String name;
     private int age;

     // Constructor
     public Person(String name, int age) {
         this.name = name;
         this.age = age;
     }

     // Getters
     public String getName() {
         return name;
     }

     public int getAge() {
         return age;
     }

     // Setters
     public void setName(String name) {
         this.name = name;
     }

     public void setAge(int age) {
         if (age >= 0) {
             this.age = age;
         } else {
             System.out.println("Invalid age");
         }
     } 
}
````