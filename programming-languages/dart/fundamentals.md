Dart Fundamentals in Detail

Dart is an object-oriented, garbage-collected, and compiled language optimized for UI development. Let's go step by step into its core fundamentals.


---

1. Variables & Data Types

Dart supports strongly typed variables with both explicit and inferred types.

Declaring Variables

int age = 24;           // Explicitly defining type
var name = "Rehan";     // Dart infers type as String
final country = "India"; // Immutable variable
const pi = 3.14159;     // Compile-time constant

var: Type inferred at compile-time, cannot be changed later.

dynamic: Allows reassignment to different types.

final: Value assigned once but evaluated at runtime.

const: Compile-time constant.


Dynamic vs var

var x = "Hello"; // x is inferred as String, cannot change type
x = "World";     // ✅ Allowed
// x = 42;       // ❌ Error, type mismatch

dynamic y = "Hello"; 
y = 42;          // ✅ Allowed


---

2. Data Types

Dart has several built-in types:

Numbers → int, double

Text → String

Boolean → bool

Lists → List<T>

Sets → Set<T>

Maps → Map<K, V>


Numbers

int a = 10;
double b = 3.14;
num c = 42; // Can hold both int and double

Strings

String single = 'Hello';
String multiLine = '''This is 
a multi-line string''';
String interpolation = "Dart version: ${3 + 3}";

Boolean

bool isFlutterAwesome = true;

Lists (Arrays)

List<String> fruits = ['Apple', 'Mango', 'Banana'];
fruits.add('Orange');
print(fruits[0]); // Apple

Sets (Unique Elements)

Set<int> numbers = {1, 2, 3, 3}; // Duplicates are ignored

Maps (Key-Value Pairs)

Map<String, int> marks = {'Math': 90, 'Science': 85};
print(marks['Math']); // 90


---

3. Operators

Dart provides various operators:

Arithmetic Operators

int a = 10, b = 4;
print(a + b);  // 14
print(a - b);  // 6
print(a * b);  // 40
print(a / b);  // 2.5 (returns double)
print(a ~/ b); // 2 (integer division)
print(a % b);  // 2 (modulus)

Comparison Operators

print(a > b);  // true
print(a < b);  // false
print(a == b); // false
print(a != b); // true

Logical Operators

bool isActive = true;
bool isVerified = false;

print(isActive && isVerified); // false (AND)
print(isActive || isVerified); // true (OR)
print(!isActive);              // false (NOT)


---

4. Control Flow Statements

Conditional Statements

If-Else

int age = 18;
if (age >= 18) {
  print("You are an adult");
} else {
  print("You are a minor");
}

Switch-Case

String grade = "A";
switch (grade) {
  case "A":
    print("Excellent");
    break;
  case "B":
    print("Good");
    break;
  default:
    print("Invalid grade");
}


---

Loops

For Loop

for (int i = 0; i < 5; i++) {
  print("Hello Dart $i");
}

While Loop

int num = 5;
while (num > 0) {
  print(num);
  num--;
}

Do-While Loop

int count = 1;
do {
  print("Iteration $count");
  count++;
} while (count <= 3);


---

5. Functions

Dart functions can have optional parameters and named parameters.

Basic Function

void greet() {
  print("Hello, Dart!");
}
greet();

Function with Parameters

void sum(int a, int b) {
  print(a + b);
}
sum(5, 3);

Returning Values

int multiply(int a, int b) {
  return a * b;
}
print(multiply(3, 4)); // 12

Optional Parameters

void display(String name, [int? age]) {
  print("Name: $name, Age: ${age ?? 'Not provided'}");
}
display("Rehan"); // Name: Rehan, Age: Not provided

Named Parameters

void userInfo({required String name, int age = 18}) {
  print("Name: $name, Age: $age");
}
userInfo(name: "Rehan", age: 24);

Arrow Functions

int square(int num) => num * num;
print(square(5)); // 25


---

6. Exception Handling

Dart uses try-catch blocks to handle errors.

try {
  int result = 10 ~/ 0; // Division by zero error
} catch (e) {
  print("Error: $e");
} finally {
  print("Execution completed");
}


---

7. Null Safety

Dart uses null safety to prevent runtime errors due to null values.

String? name; // Nullable variable
name = "Rehan";
print(name.length); // ✅ No error

String? nullableName;
print(nullableName?.length); // ✅ Safe access

? → Marks a variable as nullable

! → Tells Dart that a variable is definitely non-null


String? data;
print(data!.length); // ⚠️ Throws error if null


---

Conclusion

These are the core Dart fundamentals you need to master before diving into Flutter development.

Would you like practice exercises for each section?

