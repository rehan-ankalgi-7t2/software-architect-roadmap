Collections in Dart (In-Depth Guide)

Dart provides a powerful set of collection types to handle data efficiently. The three main collection types are:

1. Lists (Ordered collection, like arrays)


2. Sets (Unordered collection of unique items)


3. Maps (Key-value pairs, like objects in JavaScript or dictionaries in Python)



Dart collections are defined in the dart:core library, so no additional imports are required.


---

1. Lists in Dart (Ordered Collection)

A List is an ordered collection of elements, similar to arrays in other languages.

Creating a List

void main() {
  List<int> numbers = [10, 20, 30, 40, 50];
  print(numbers); // [10, 20, 30, 40, 50]
}

List Properties & Methods

void main() {
  List<String> fruits = ["Apple", "Banana", "Mango"];

  print(fruits.length);    // 3
  print(fruits.isEmpty);   // false
  print(fruits.isNotEmpty); // true
  print(fruits.first);     // Apple
  print(fruits.last);      // Mango
}

Adding & Removing Elements

void main() {
  List<int> numbers = [1, 2, 3];

  numbers.add(4); // Add single item
  print(numbers); // [1, 2, 3, 4]

  numbers.addAll([5, 6]); // Add multiple items
  print(numbers); // [1, 2, 3, 4, 5, 6]

  numbers.insert(1, 10); // Insert at index
  print(numbers); // [1, 10, 2, 3, 4, 5, 6]

  numbers.remove(3); // Remove value 3
  print(numbers); // [1, 10, 2, 4, 5, 6]

  numbers.removeAt(2); // Remove from index 2
  print(numbers); // [1, 10, 4, 5, 6]
}

Iterating Over a List

void main() {
  List<String> names = ["John", "Jane", "Alice"];

  // Using for loop
  for (int i = 0; i < names.length; i++) {
    print(names[i]);
  }

  // Using for-in loop
  for (var name in names) {
    print(name);
  }

  // Using forEach
  names.forEach((name) => print(name));
}

Mapping and Filtering a List

void main() {
  List<int> numbers = [1, 2, 3, 4, 5];

  // Map: Multiply each element by 2
  var doubled = numbers.map((num) => num * 2).toList();
  print(doubled); // [2, 4, 6, 8, 10]

  // Filter: Get even numbers
  var evens = numbers.where((num) => num % 2 == 0).toList();
  print(evens); // [2, 4]
}


---

2. Sets in Dart (Unique Collection)

A Set is an unordered collection of unique elements.

Creating a Set

void main() {
  Set<int> uniqueNumbers = {1, 2, 3, 4, 4, 5}; // Duplicate 4 is ignored
  print(uniqueNumbers); // {1, 2, 3, 4, 5}
}

Adding & Removing Elements

void main() {
  Set<String> colors = {"Red", "Green", "Blue"};

  colors.add("Yellow");
  print(colors); // {Red, Green, Blue, Yellow}

  colors.remove("Green");
  print(colors); // {Red, Blue, Yellow}
}

Checking for Elements

void main() {
  Set<int> numbers = {10, 20, 30};

  print(numbers.contains(20)); // true
  print(numbers.contains(40)); // false
}

Set Operations

void main() {
  Set<int> setA = {1, 2, 3, 4};
  Set<int> setB = {3, 4, 5, 6};

  print(setA.union(setB));        // {1, 2, 3, 4, 5, 6}
  print(setA.intersection(setB)); // {3, 4}
  print(setA.difference(setB));   // {1, 2}
}


---

3. Maps in Dart (Key-Value Pairs)

A Map is a collection of key-value pairs, similar to JSON or dictionaries in Python.

Creating a Map

void main() {
  Map<String, int> ages = {
    "Alice": 25,
    "Bob": 30,
    "Charlie": 28,
  };

  print(ages); // {Alice: 25, Bob: 30, Charlie: 28}
}

Adding & Updating Entries

void main() {
  Map<String, String> countries = {};

  countries["India"] = "New Delhi";
  countries["USA"] = "Washington DC";

  print(countries); // {India: New Delhi, USA: Washington DC}

  // Update a value
  countries["India"] = "Delhi";
  print(countries); // {India: Delhi, USA: Washington DC}
}

Accessing & Removing Elements

void main() {
  Map<String, int> scores = {"Alice": 90, "Bob": 85, "Charlie": 88};

  print(scores["Alice"]); // 90
  scores.remove("Bob");
  print(scores); // {Alice: 90, Charlie: 88}
}

Checking for Keys and Values

void main() {
  Map<String, String> capitals = {"India": "Delhi", "USA": "Washington DC"};

  print(capitals.containsKey("India")); // true
  print(capitals.containsValue("Paris")); // false
}

Iterating Over a Map

void main() {
  Map<String, int> marks = {"Math": 90, "Science": 85, "English": 88};

  // Using forEach
  marks.forEach((subject, mark) {
    print("$subject: $mark");
  });

  // Using for-in loop
  for (var key in marks.keys) {
    print("$key: ${marks[key]}");
  }
}


---

4. List, Set, and Map Conversion

List to Set (Remove Duplicates)

void main() {
  List<int> numbers = [1, 2, 2, 3, 4, 4, 5];
  Set<int> uniqueNumbers = numbers.toSet();
  print(uniqueNumbers); // {1, 2, 3, 4, 5}
}

Set to List

void main() {
  Set<int> numSet = {10, 20, 30};
  List<int> numList = numSet.toList();
  print(numList); // [10, 20, 30]
}

Map Keys and Values as Lists

void main() {
  Map<String, int> studentScores = {"Alice": 90, "Bob": 85, "Charlie": 88};

  print(studentScores.keys.toList()); // [Alice, Bob, Charlie]
  print(studentScores.values.toList()); // [90, 85, 88]
}


---

Conclusion

Lists → Ordered, allows duplicates.

Sets → Unordered, unique values only.

Maps → Key-value pairs, fast lookups.


Would you like exercises on these concepts?

