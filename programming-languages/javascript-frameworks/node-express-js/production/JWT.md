# JWT

<aside style="padding: 16px; background-color: #555">
💡 Never store the JWT tokens in local storage, always sign the token and set an HTTP only cookie, the browser sends the HTTP only cookie every time a request is made.

</aside>

> A JSON web token (JWT) is an [open standard](https://tools.ietf.org/html/rfc7519). The finished product allows for safe, secure communication between two parties. Data is verified with a digital signature, and if it's sent via HTTP, encryption keeps the data secure.

JWTs have three important components.

1. **Header:** Define token type and the signing algorithm involved in this space.
2. **Payload:** Define the token issuer, the expiration of the token, and more in this section.
3. **Signature:** Verify that the message hasn't changed in transit with a secure signature.

Coding ties these pieces together. The finished product looks something like this.

# Pros & Cons of JWTs

There are many benefits of JWTs. 👍🏻

- **Size:** Tokens in this code language are tiny, and they can be passed between two entities quite quickly.
- **Ease:** Tokens can be generated from almost anywhere, and they don't need to be verified on your server.
- **Control:** You can specify what someone can access, how long that permission lasts, and what the person can do while logged on.

There are also potential disadvantages. 👎

- **Single key:** JWTs rely on a single key. If that key is compromised, the entire system is at risk.
- **Complexity:** These tokens aren’t simple to understand. If a developer doesn’t have a strong knowledge of cryptographic signature algorithms, they could inadvertently put the system at risk.
- **Limitations:** You can’t push messages to all clients, and you can’t manage clients from the server side.

# JWT implementation in Node-Express server

1. install dependency

```bash
npm install cookie-parser jsonwebtoken
```

1. token generation - /utils/generateToken.js

```jsx
import jwt from "jsonwebtoken";

/**
 * @param {*} res
 * @param {*} userId
 * @description generate jwt token to authorize the user and set cookie for 30days
 */
const generateToken = (res, userId) => {
  const token = jwt.sign({ userId: userId }, process.env.JWT_SECRET, {
    expiresIn: "30d",
  });

  res.cookie("jwt", token, {
    httpOnly: true,
    secure: process.env.NODE_ENV !== "development", // secure cookies in production
    sameSite: "strict",
    maxAge: 30 * 24 * 60 * 60 * 1000, // 30days
  });
};

export default generateToken;
```

1. login, logout, register actions

```jsx
/**
 * @description authenticate user by logging in
 * @route /api/users/login
 * @access public
 * @param {*} email
 * @param {*} password
 */
const authUser = asyncHandler(async (req, res) => {
  const { email, password } = req.body;
  // console.log(req);

  const user = await User.findOne({ email });

  if (user && (await user.matchPassword(password))) {
    generateToken(res, user._id);
    res.status(200).json({
      userData: {
        _id: user._id,
        name: user.name,
        email: user.email,
        isAdmin: user.isAdmin,
      },
      success: true,
    });
  } else {
    res.status(401).json({
      message: "not authenticated! token failed",
      success: false,
    });
  }
});
```

```jsx
const logUserOut = (req, res) => {
  res.cookie("jwt", "", {
    httpOnly: true,
    expires: new Date(0),
  });

  res.status(200).json({
    message: "logged out succesfully",
    success: true,
  });
};
```

```jsx
const registerUser = asyncHandler(async (req, res) => {
  const { name, email, password } = req.body;

  const isUserExists = await User.findOne({ email });

  if (isUserExists) {
    res.status(400);
    throw new Error("User aLready exists!");
  } else {
    const user = await User.create({
      name,
      email,
      password,
    });

    if (user) {
      generateToken(res, user._id);
      res.status(201).json({
        createdUser: {
          _id: user._id,
          name: user.name,
          email: user.email,
          isAdmin: user.isAdmin,
        },
        success: true,
      });
    } else {
      res.status(400);
      throw new Error("Invalid user data");
    }
  }
});
```

1. check whether the user is authenticated (logged in) using `auth middleware`

```jsx
const protect = asyncHandler(async (req, res, next) => {
  // console.log(req.cookies);
  let token = req.cookies.jwt;

  if (token) {
    try {
      const decoded = jwt.verify(token, process.env.JWT_SECRET);
      console.log(`decoded: ${decoded}`);
      req.user = await User.findById(decoded.userId).select("-password");

      next();
    } catch (error) {
      res.status(401);
      throw new Error("not authorized! token failed");
    }
  } else {
    res.status(401);
    throw new Error("not authorized! no token");
  }
});
```

1. establish protected routes on the backend

```jsx
router.route("/profile").get(protect, getUserProfile);
```