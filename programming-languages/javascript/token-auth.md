# Token Auth 🪙
> a token typically refers to a piece of data that serves as a proof of the authentication or authorization of a user. Tokens are commonly used to enhance security in web applications, especially in scenarios where traditional username/password authentication may not be sufficient or secure enough.
> 
- Token-based authentication is a protocol which allows users to verify their identity, and in return receive a unique [access token](https://www.okta.com/identity-101/access-token/). During the life of the token, users then access the website or app that the token has been issued for, rather than having to re-enter credentials each time they go back to the same webpage, app, or any resource protected with that same token.
- Auth tokens work like a stamped ticket. The user retains access as long as the token remains valid. Once the user logs out or quits an app, the token is invalidated.
- Token-based authentication is different from traditional password-based or server-based authentication techniques. Tokens offer a second layer of security, and administrators have detailed control over each action and transaction.

There are different types of tokens used in web security, including:

1. **Authentication Tokens:**
    - **Session Tokens:** These are commonly used in web applications to maintain a user's session after they have logged in. Once a user successfully logs in, a session token is generated and sent to the user's browser. The browser includes this token in subsequent requests, allowing the server to identify and authenticate the user for the duration of the session.
    - **JSON Web Tokens (JWT):** JWT is a compact, URL-safe means of representing claims to be transferred between two parties. It is commonly used for authentication and information exchange. JWTs consist of three parts: a header, a payload, and a signature.
2. **CSRF Tokens (Cross-Site Request Forgery):**
    - CSRF tokens are used to protect against Cross-Site Request Forgery attacks. These tokens are embedded in web forms or included in requests as headers. The server validates the presence and correctness of the token before processing the request, ensuring that the request is legitimate and not the result of a malicious action.
3. **OAuth Tokens:**
    - OAuth tokens are used in the OAuth 2.0 framework for authorization. They are issued by an authorization server and can be used by a client to access protected resources on behalf of a resource owner (user).
4. **Access Tokens and Refresh Tokens:**
    - In some authentication systems, access tokens are used to grant limited access to a resource, while refresh tokens are used to obtain a new access token when the current one expires.

# Token Auth in 4 steps

- **Request:** The person asks for access to a server or protected resource. That could involve a login with a password, or it could involve some other process you specify.
- **Verification:** The server determines that the person should have access. That could involve checking the password against the username, or it could involve another process you specify.
- **Tokens:** The server communicates with the authentication device, like a ring, key, phone, or similar device. After verification, the server issues a token and passes it to the user.
- **Storage:** The token sits within the user's browser while work continues.

If the user attempts to visit a different part of the server, the token communicates with the server again. Access is granted or denied based on the token.

Administrators set limits on tokens. You could allow a one-use token that is immediately destroyed when the person logs out. Or you could set the token to self-destruct at the end of a specified time period.

![](https://www.okta.com/sites/default/files/styles/tinypng/public/media/image/2020-12/TokenBasedAuthentication.png?itok=zXMogDjG)

# JSON Web Token (JWT): A Special Form of Auth Token

Because so many users are accessing systems via mobile phones (apps) and web apps nowadays, developers need a secure way to authenticate that’s appropriate for those platforms.

To solve that challenge, many developers turn to JSON Web Tokens (JWTs) when working on tokens for their applications.

A JSON web token (JWT) is an [open standard](https://tools.ietf.org/html/rfc7519). The finished product allows for safe, secure communication between two parties. Data is verified with a digital signature, and if it's sent via HTTP, encryption keeps the data secure.

JWTs have three important components.

1. **Header:** Define token type and the signing algorithm involved in this space.
2. **Payload:** Define the token issuer, the expiration of the token, and more in this section.
3. **Signature:** Verify that the message hasn't changed in transit with a secure signature.

Coding ties these pieces together. The finished product looks something like this.