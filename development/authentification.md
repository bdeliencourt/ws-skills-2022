
# Authentification

## Definitions 📚

## Authentication 🔒
Authentication confirms that the user says who he is. The user is authenticated by calling a login endpoint.
Then the server is checking against the database if the user does exist. The server sends back a token, usually a JSON Token which includes user's datas : could be his id, a session id, his roles (not recommanded) and more...


## Authorization 🗃️
Authorization allows the user to access restricted ressources, endpoints, functions. Authorizations are often related to user's roles : admin, super-admin, moderator, etc. Roles define a set of functions the user can get access to.

## JSON Token

### Definition
A JSON Token is a JSON object which can be returned after a successfully login. It is splitted in 3 parts : the header, the payload and the signature.
```javascript
// Header
{
  "alg": "HS256",
  "typ": "JWT"
}
// Payload
{
  "sub": "1234567890",
  "name": "John Doe",
  "iat": 1516239022
}
// Signature
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret_key
)
```

#### Content
* header: tells the type of the object, the algorithm used to compute the signature
* payload: user's informations and expiry date
* signature: the signature to verify the integrity of the token.

#### Encryption
When the JSON object has its header, payload and signature defined, it is encoded in base 64 and then transmitted.
```javascript
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.
eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.
SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```
#### Verifying
The JSON token content can be decoded converting base64 to UTF8. Its content can be altered by malicious persons. The signature is used to check the token integrity. When creating a token, the server calls a hash function to encrypt the exact content of the payload using a private secret key 🔑. When using a token, the server will decode the token, retrieve the payload and the header and compute the signature. If the signature of the token matched with the computed one, then the token is valid. If not, the token was corrupted.

## Session Token
A session token contains a session id that points to a session entry in the back-office database. Datas are stored in the session's database entry. Such as the JSON token, sessions have a defined lifetime.

## Transportation 🚌
Tokens can either be used with cookies or/and by filling the request header with the token.

### Cookies 🍪 
Cookies can store many things, not only tokens. Cookies are sent to client's browser from the server. By default, a cookie has a session lifetime. When the browser is closed, the cookie is deleted. The browser automatically send cookie in the request header. It is recommended to use HTTP ONLY (to avoid JS attack on cookies -- look for reference).

### Request header
When cookies can not be used (e.g : native app), it is possible to attach the token to the request's header.
To do so, an 'Authorization' property must be set.
```javascript
Authorization: Bearer xxxxx.yyyyyy.zzzzz
```
