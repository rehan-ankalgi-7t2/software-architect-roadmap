Asynchronous Programming in Dart (In-Depth Guide)

Dart is single-threaded but supports asynchronous programming using Future and Stream. This allows applications (like Flutter apps) to remain responsive while handling I/O operations, HTTP requests, file reading, or database interactions.


---

1. Synchronous vs Asynchronous Execution

Synchronous (Blocking) Execution

In synchronous execution, each task waits for the previous one to complete before moving forward.

void main() {
  print("Task 1");
  print("Task 2");
  print("Task 3");
}

// Output:
// Task 1
// Task 2
// Task 3


---

Asynchronous (Non-Blocking) Execution

In asynchronous execution, tasks can run independently, and the program doesn't wait for them to finish before moving on.

void main() {
  print("Task 1");

  Future.delayed(Duration(seconds: 2), () {
    print("Task 2 (after delay)");
  });

  print("Task 3");
}

// Output:
// Task 1
// Task 3
// Task 2 (after delay)

Here, "Task 3" runs before "Task 2" because Future.delayed() is non-blocking.


---

2. Futures in Dart

A Future represents a potential value or error that will be available at some point in the future.

Creating and Using a Future

void main() {
  print("Fetching data...");

  fetchData().then((value) {
    print(value);
  }).catchError((error) {
    print("Error: $error");
  });

  print("Processing...");
}

Future<String> fetchData() {
  return Future.delayed(Duration(seconds: 3), () {
    return "Data retrieved successfully!";
  });
}

// Output:
// Fetching data...
// Processing...
// Data retrieved successfully! (after 3 seconds)

fetchData() returns a Future that completes after 3 seconds.

.then() handles the successful response.

.catchError() handles errors.



---

Handling Errors in Future

Errors in a Future can be caught using catchError() or a try-catch block inside async-await.

Future<int> divideNumbers(int a, int b) {
  return Future.delayed(Duration(seconds: 2), () {
    if (b == 0) {
      throw Exception("Division by zero is not allowed!");
    }
    return a ~/ b;
  });
}

void main() {
  divideNumbers(10, 0).then((result) {
    print("Result: $result");
  }).catchError((error) {
    print("Error: $error");
  });

  print("Operation started...");
}

// Output:
// Operation started...
// Error: Exception: Division by zero is not allowed! (after 2 seconds)


---

3. async-await in Dart

The async and await keywords simplify working with Futures.

Using async-await

void main() async {
  print("Fetching data...");
  String data = await fetchData();
  print(data);
  print("Processing complete.");
}

Future<String> fetchData() async {
  await Future.delayed(Duration(seconds: 2));
  return "Data retrieved!";
}

// Output:
// Fetching data...
// (2 seconds delay)
// Data retrieved!
// Processing complete.

await pauses execution until the Future completes.

The function must be marked async if it contains await.



---

Handling Errors with try-catch

void main() async {
  try {
    int result = await divideNumbers(10, 0);
    print("Result: $result");
  } catch (error) {
    print("Error: $error");
  }

  print("Operation finished.");
}

Future<int> divideNumbers(int a, int b) async {
  await Future.delayed(Duration(seconds: 2));

  if (b == 0) {
    throw Exception("Cannot divide by zero");
  }

  return a ~/ b;
}

// Output:
// Error: Exception: Cannot divide by zero (after 2 seconds)
// Operation finished.


---

4. Streams in Dart (Handling Multiple Values Over Time)

A Stream is used for handling multiple asynchronous events (like WebSockets, API polling, or user input).

Creating and Listening to a Stream

void main() {
  Stream<int> numberStream = getNumbers();

  numberStream.listen(
    (number) => print("Received: $number"),
    onDone: () => print("Stream closed."),
    onError: (error) => print("Error: $error"),
  );
}

Stream<int> getNumbers() async* {
  for (int i = 1; i <= 5; i++) {
    await Future.delayed(Duration(seconds: 1));
    yield i; // Emit values
  }
}

// Output:
// Received: 1
// Received: 2
// Received: 3
// Received: 4
// Received: 5
// Stream closed.

async* is used to create a Stream generator.

yield emits values one by one.



---

Transforming a Stream

You can modify stream data using map().

void main() {
  Stream<int> numberStream = getNumbers();

  numberStream.map((num) => num * 2).listen((doubleNum) {
    print("Doubled: $doubleNum");
  });
}

Stream<int> getNumbers() async* {
  for (int i = 1; i <= 3; i++) {
    await Future.delayed(Duration(seconds: 1));
    yield i;
  }
}

// Output:
// Doubled: 2
// Doubled: 4
// Doubled: 6


---

5. StreamController (Manually Controlling Streams)

A StreamController allows us to add values dynamically.

import 'dart:async';

void main() {
  StreamController<int> controller = StreamController<int>();

  controller.stream.listen(
    (data) => print("Received: $data"),
    onDone: () => print("Stream closed"),
  );

  controller.add(10);
  controller.add(20);
  controller.add(30);

  controller.close(); // Closing the stream
}

// Output:
// Received: 10
// Received: 20
// Received: 30
// Stream closed


---

6. Combining Futures and Streams

Sometimes you need to wait for multiple asynchronous operations.

Using Future.wait() to Handle Multiple Futures

void main() async {
  List<Future<String>> futures = [
    fetchData(1),
    fetchData(2),
    fetchData(3),
  ];

  List<String> results = await Future.wait(futures);
  print(results);
}

Future<String> fetchData(int id) async {
  await Future.delayed(Duration(seconds: id));
  return "Data from task $id";
}

// Output (after max delay):
// [Data from task 1, Data from task 2, Data from task 3]

Future.wait() waits for all tasks to complete.



---

Summary

Would you like a real-world example or practice exercises next?


---
Real-World API Data Fetching in Dart (Async Programming Example)

When working with real-world applications, fetching data from an API (e.g., weather, user profiles, or news) is a common task. This example demonstrates how to make HTTP requests asynchronously in Dart using the http package.


---

1. Setup: Install the HTTP Package

To fetch data from an API in Dart, you need the http package.

If you're using Dart CLI, run:

dart pub add http

If you're using Flutter, add this to pubspec.yaml:

dependencies:
  http: ^0.13.6


Then run:

flutter pub get


---

2. Fetching API Data Using async-await

This example fetches user data from a public API (https://jsonplaceholder.typicode.com/users).

Example: Fetching and Displaying User Data

import 'dart:convert';  
import 'package:http/http.dart' as http;  

// Function to fetch user data from API
Future<void> fetchUsers() async {
  final url = Uri.parse("https://jsonplaceholder.typicode.com/users");

  try {
    final response = await http.get(url);

    if (response.statusCode == 200) {
      List<dynamic> users = jsonDecode(response.body);
      print("User Data:");
      for (var user in users) {
        print("Name: ${user['name']}, Email: ${user['email']}");
      }
    } else {
      print("Failed to load users. Status code: ${response.statusCode}");
    }
  } catch (e) {
    print("Error: $e");
  }
}

void main() {
  print("Fetching users...");
  fetchUsers();
}

Output (Example)

Fetching users...
User Data:
Name: Leanne Graham, Email: Sincere@april.biz
Name: Ervin Howell, Email: Shanna@melissa.tv
Name: Clementine Bauch, Email: Nathan@yesenia.net
...


---

3. Fetching API Data with Stream (Real-time Data)

In some cases, data is continuously updated (e.g., stock prices, weather updates). You can use Streams for real-time updates.

Example: Fetching API Data Every 5 Seconds

import 'dart:convert';  
import 'dart:async';  
import 'package:http/http.dart' as http;  

Stream<List<dynamic>> fetchUsersPeriodically() async* {
  while (true) {
    final url = Uri.parse("https://jsonplaceholder.typicode.com/users");
    
    try {
      final response = await http.get(url);

      if (response.statusCode == 200) {
        List<dynamic> users = jsonDecode(response.body);
        yield users; // Emit the user list as a stream event
      } else {
        print("Failed to fetch data. Status: ${response.statusCode}");
      }
    } catch (e) {
      print("Error: $e");
    }

    await Future.delayed(Duration(seconds: 5)); // Fetch every 5 seconds
  }
}

void main() {
  print("Starting user data stream...");
  
  fetchUsersPeriodically().listen((users) {
    print("\nUpdated User Data:");
    for (var user in users.take(3)) { // Limit to first 3 users for display
      print("Name: ${user['name']}, Email: ${user['email']}");
    }
  });
}

Output (Updates Every 5 Seconds)

Starting user data stream...

Updated User Data:
Name: Leanne Graham, Email: Sincere@april.biz
Name: Ervin Howell, Email: Shanna@melissa.tv
Name: Clementine Bauch, Email: Nathan@yesenia.net

(5 seconds later...)

Updated User Data:
Name: Leanne Graham, Email: Sincere@april.biz
Name: Ervin Howell, Email: Shanna@melissa.tv
Name: Clementine Bauch, Email: Nathan@yesenia.net
...

This continuously fetches user data every 5 seconds.

yield emits data to all listeners.



---

4. Handling Errors Properly

When making API calls, network issues or server failures may occur. Proper error handling ensures smooth user experience.

Example: Handling API Errors

Future<void> fetchUser(int id) async {
  final url = Uri.parse("https://jsonplaceholder.typicode.com/users/$id");

  try {
    final response = await http.get(url);

    if (response.statusCode == 200) {
      var user = jsonDecode(response.body);
      print("User: ${user['name']}, Email: ${user['email']}");
    } else if (response.statusCode == 404) {
      print("User not found.");
    } else {
      print("Server error: ${response.statusCode}");
    }
  } catch (e) {
    print("Network error: $e");
  }
}

void main() {
  fetchUser(1);
  fetchUser(999); // Non-existent user (404)
}

Output

User: Leanne Graham, Email: Sincere@april.biz
User not found.


---

5. Combining Multiple API Calls Using Future.wait()

Sometimes, you need to make multiple API requests simultaneously.

Example: Fetching Multiple Users at the Same Time

Future<List<dynamic>> fetchUser(int id) async {
  final url = Uri.parse("https://jsonplaceholder.typicode.com/users/$id");
  final response = await http.get(url);
  
  if (response.statusCode == 200) {
    return jsonDecode(response.body);
  } else {
    throw Exception("Failed to load user $id");
  }
}

void main() async {
  try {
    List<dynamic> users = await Future.wait([
      fetchUser(1),
      fetchUser(2),
      fetchUser(3),
    ]);

    print("Users Fetched:");
    for (var user in users) {
      print("${user['name']} - ${user['email']}");
    }
  } catch (e) {
    print("Error: $e");
  }
}

Output

Users Fetched:
Leanne Graham - Sincere@april.biz
Ervin Howell - Shanna@melissa.tv
Clementine Bauch - Nathan@yesenia.net

Future.wait() fetches all users simultaneously, reducing API response time.



---

Summary


---

Next Steps

Want a Flutter version of API fetching?

Need an API CRUD example (GET, POST, PUT, DELETE)?

Want to implement caching for API responses?


Let me know how you’d like to proceed!

