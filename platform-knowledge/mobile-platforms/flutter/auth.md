Authentication in Flutter can be implemented in several ways depending on the backend and the authentication provider you choose. Here’s a breakdown of the common authentication methods:


---

1. Firebase Authentication

Firebase Authentication provides an easy way to handle user sign-in with email/password, Google, Facebook, Apple, and more.

Steps:

1. Add Dependencies

dependencies:
  firebase_auth: latest_version
  firebase_core: latest_version
  google_sign_in: latest_version # For Google sign-in


2. Initialize Firebase in main.dart

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(MyApp());
}


3. Sign Up with Email & Password

Future<User?> signUp(String email, String password) async {
  try {
    UserCredential userCredential = await FirebaseAuth.instance.createUserWithEmailAndPassword(
      email: email,
      password: password,
    );
    return userCredential.user;
  } catch (e) {
    print(e);
    return null;
  }
}


4. Sign In

Future<User?> signIn(String email, String password) async {
  try {
    UserCredential userCredential = await FirebaseAuth.instance.signInWithEmailAndPassword(
      email: email,
      password: password,
    );
    return userCredential.user;
  } catch (e) {
    print(e);
    return null;
  }
}


5. Google Sign-In

Future<User?> signInWithGoogle() async {
  final GoogleSignInAccount? googleUser = await GoogleSignIn().signIn();
  final GoogleSignInAuthentication googleAuth = await googleUser!.authentication;
  final AuthCredential credential = GoogleAuthProvider.credential(
    accessToken: googleAuth.accessToken,
    idToken: googleAuth.idToken,
  );
  UserCredential userCredential = await FirebaseAuth.instance.signInWithCredential(credential);
  return userCredential.user;
}




---

2. Custom Authentication (Node.js / FastAPI / Django)

If you're using your backend, you’ll need:

API for authentication (JWT-based)

Storing user tokens securely (Shared Preferences, Secure Storage)


Steps:

1. Install Dependencies

dependencies:
  http: latest_version
  flutter_secure_storage: latest_version


2. Login with API (JWT Token)

import 'dart:convert';
import 'package:http/http.dart' as http;
import 'package:flutter_secure_storage/flutter_secure_storage.dart';

final storage = FlutterSecureStorage();

Future<void> login(String email, String password) async {
  final response = await http.post(
    Uri.parse('https://yourapi.com/login'),
    headers: {'Content-Type': 'application/json'},
    body: jsonEncode({'email': email, 'password': password}),
  );

  if (response.statusCode == 200) {
    final data = jsonDecode(response.body);
    await storage.write(key: 'token', value: data['token']);
  } else {
    throw Exception('Failed to login');
  }
}


3. Auto-login with Secure Token

Future<bool> checkLogin() async {
  String? token = await storage.read(key: 'token');
  return token != null;
}




---

3. OAuth Authentication (Google, Facebook, Apple)

You can use flutter_appauth or oauth2 for OAuth-based authentication.

Example (Google Sign-In via OAuth)

1. Add Dependencies

dependencies:
  flutter_appauth: latest_version


2. Authenticate User

import 'package:flutter_appauth/flutter_appauth.dart';

final FlutterAppAuth appAuth = FlutterAppAuth();

Future<void> loginWithOAuth() async {
  final AuthorizationTokenResponse? result = await appAuth.authorizeAndExchangeCode(
    AuthorizationTokenRequest(
      'your-client-id',
      'your-redirect-url',
      scopes: ['email', 'profile'],
    ),
  );

  if (result != null) {
    print('Access Token: ${result.accessToken}');
  }
}




---

4. Biometric Authentication (Fingerprint/FaceID)

1. Add Dependency

dependencies:
  local_auth: latest_version


2. Authenticate with Fingerprint/FaceID

import 'package:local_auth/local_auth.dart';

final LocalAuthentication auth = LocalAuthentication();

Future<bool> authenticate() async {
  bool isAuthenticated = await auth.authenticate(
    localizedReason: 'Authenticate to access the app',
  );
  return isAuthenticated;
}




---

Choosing the Right Authentication Method

Would you like help setting up authentication in a specific Flutter project?

