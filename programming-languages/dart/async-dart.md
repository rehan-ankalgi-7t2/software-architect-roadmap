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

