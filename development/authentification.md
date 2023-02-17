
# Authentification

## Definitions 📚

## Encrypt VS Encode - todo

## Password encryption
Passwords mustn't be stored in clear text in databases. They must be encrypted using hashing algorithms. 
Even if hackers get the content of the passwords table, they won't get the clear version. 

Once encrypted, a password cannot be decrypted but clear-password-to-hash dictionaries (e.g rainbow tables) can be used to reverse the hashing. 

To make the decryption harder and to avoid people having the same hashed password, hashing password libraries add salt to the hashing process.

|        | Password     | Salt Value | Salted Password    | MD5 Hash                         |
|--------|--------------|------------|--------------------|----------------------------------|
| You    | iL0veCh3ese! | Am4la!     | iL0veCh3ese!Am4la! | 31fda55ee57bc4c49ef6e0c99b0ba904 |
| Chioma | iL0veCh3ese! | ew3du?     | iL0veCh3ese!ew3du? | cf0bea59647ba39e058a20c14fc10b0d |


## Authentication 🔒
Authentication confirms that the user says who he is. 

The user is authenticated by calling a login endpoint. The server is checking against the database if the user does exist. 

Then it usually sends back a token to the client a JSON Token which includes user's datas : his id, a session id, his roles and more...


## Authorization 🗃️
Authorization allows the user to access restricted ressources, endpoints, functions. 
Authorizations are often related to the user's roles : admin, super-admin, moderator, etc.

### Where to store roles ?
User's roles could be stored directly into the JWT payload but it must be wisely thought. 

Informations stored in the JWT can be outdated. An user who has his roles revoked could still access restricted endpoints because his JWT is not synchronized with the database.

A good practice is to store the user's id in the token and then retreive the user's roles from the database right after receiving the request.

## JWT : JSON Web Token

### Definition
A JWT is a JSON object which can be returned after a successfully login. It is splitted in 3 parts : the header, the payload and the signature.
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
* header: the type of the object, the algorithm used to compute the signature
* payload: user's informations and token creation date
* signature: hash code to verify the integrity of the token.

#### Encryption
When the JWT has its header, payload and signature defined, it is encoded in base 64 and then transmitted.
```javascript
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.
eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.
SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```
#### Verifying
The JWT's content can be decoded converting it from base64 to UTF8. Its content can be altered by malicious persons. 

The signature is used to check the token integrity. When creating a token, the server calls a hash function to encrypt the exact content of the header and  payload using a private secret key 🔑 that only the server knows about. 

After receiving a token, the server will decode it, retrieve the header and the payload and compute the signature. If the signature of the token matches with the computed one, then received token is valid. If not, the token was corrupted.

## Session Token
A session token contains a session id that points to a session entry in the back-office database. Datas are stored in the session's database entry. Like JWT, sessions have a defined lifetime.

## Transportation 🚌
Tokens can either be used with cookies or/and by filling the request header with the token.

### Cookies 🍪 
Cookies can store many things, not only tokens. Cookies are sent to client's browser from the server. By default, a cookie has a session lifetime. When the browser's process is closed, the cookie is deleted. 

The browser automatically sends cookie in the request header. It is recommended to use HTTP ONLY (to avoid JS attack on cookies -- look for reference).

### Request header
When cookies can not be used (e.g : native app), it is possible to attach the token to the request's header.
To do so, an 'Authorization' property must be set.
```javascript
Authorization: Bearer xxxxx.yyyyyy.zzzzz
```

### Implementation - todo
