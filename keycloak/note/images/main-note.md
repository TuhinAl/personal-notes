


#### 11. Authorization Code and Refresh Token Grants:

![alt text](/note/images/grant-types.png)
We will use Spring Boot to demonstrate specifically the authorization code with and without PKCE, refresh token and the client credentials. These are the most important. You see all the main players in the diagram the resource owner, the client, the authorization server
and the resource server.

Step-1: user or the resource owner will send the request to connect
to the resource server or in our example, get the photos of the resource owner.

Step-2: client will send an authorized request to the authorization endpoint of the authorization server, asking for the permission to call the resource server on the users behalf. It will do so in the form of scopes. Basically, the intent here is to get an access token with those scopes.

But before getting the access token, the resource owner needs to authorize the request.
Specifically, the authorization request is asking the authorization server to get that authorization from the resource owner.

Step-3: If the user has not already been authorized before, the authorization server will first ask for the user credentials and then specifically ask for permission.

Step-4: After the resource owner approves it, the authorization server will send an authorization code to the client at its redirection Uri. This authorization code is very short lived.

Also, how does the authorization server know the redirect Uri when the client was registered?
We also provided the redirect Uri as part of the registration, basically telling it where to send the authorization code when the authorization request comes in.

Now our client or the application already has an authorization code.
So authorization has already been given by the resource owner.But we still do not have the access token.

Step-5: The client will then send a request to the token endpoint of the authorization server with a grant type of code, and specify the authorization code as part of that request. Basically, the client will exchange the authorization code for an access token.

In doing so, the client will have to specify the client_ID and the client_secret as well, because the authorization server needs to authenticate the client itself

you might be wondering why the authorization server does not send the access token
directly to the client instead of sending the authorization code?

The reason for this is security. The client is not dealing directly with the authorization server. Remember, theres a browser in the middle. Its going through this browser and that makes it less secure. This whole path via the browser is called the front channel. And we do not want to expose our access token in that front channel. Thats why an authorization code is sent in the front channel. And later on, this authorization code is exchanged with the access token in the back channel. The back channel here being the direct communication between the client and the authorization server. 

Now, the token response that we get for the token request is a Json response, and it contains several things the access token for sure, but it also contains an optional ID_token and also something called as the refresh_token.

`Refresh Token:` Remember that I said that the expiry date of the access token can be extremely low of the order of five minutes. Does that mean that we have to go through this entire process to get an access token every five minutes?
**No**.
The refresh token comes to the rescue here. If the access token has expired, the client can make a call to the token endpoint again with a grant type of refresh token to get another access token. A refresh token has a much higher expiry time, at least until the web session ends.
Lets say 30 minutes.

Now this is where the grand type of refresh token is used to continuously get new access tokens periodically, without going through the entire process of authorization.

Step-6: If OpenID is one of the scopes used, then the client can also call the Userinfo endpoint to get more information about the user.
Note that with OpenID scope, the client already has access to the ID token, which will give client some user information, but the client can get additional information about the user by calling this Userinfo endpoint. If the access token does not contain the scope of OpenID, then the Userinfo endpoint will return an error. Its an authorization error.

Step-7: The client now already has a signed access token. Whats the client going to do? The client can then call the resource API with that access token.


Step-8: The resource server on its part will verify the sign token because remember, it needs to verify the signature.
It needs to make sure that the scopes are correct in order for this request to pass through. How does it verify it? 
If the token is an `opaque-token`, then the resource server will call the authorization server introspection endpoint to make sure that the access token is valid.
If the token is a `JWT-token`, then the resource server can do the verification itself. As a part of the verification, it will have to do some important checks the signature verification, the expiry time check and some other checks.

If your token is used, the resource server would also need to pull the public keys from the authorization server, and it can do that with the JWKS endpoint. Now the signature verification will happen as follows.

Step-9: If your token is used, the resource server would also need to pull the public keys from the authorization server, and it can do that with the JWKS endpoint. Now the signature verification will happen as follows.
The header of the access token has a reference to the public key, which is used to sign up.
This reference field is called the key_ID.`kid`.

The exact public key used for the signature can be found from the list of public keys that was retrieved from the JCS endpoint and the kid reference. Once the public key is identified, the signature can then be verified using that public key.

This summarizes the flow for the authorization code Grant type.

Now, in this diagram there are several important endpoints which are not shown because otherwise theres too much clutter. One is the revocation endpoint, which can be used to revoke an access token or a refresh token. Another endpoint that is not shown is the optional end session endpoint that is used to log out of the session of the resource owner with the authorization server. Thats the global logout.


![alt text](/note/images/authz-and-refresh-token-grants.png)

There is also a problem with this architecture. The architecture works great if the client or the application is on the back end. What happens if the client is running inside the browser or a mobile client? These are public clients. Remember, we need to send the client ID and secret to get the token from the token endpoint. But there is no safe place to keep the secret in public clients. Thats the reason authorization code grant was extended to use.
PKCE.


### 12. Implicit Grant and PKCE:
All of what we talked about in the last lecture is valid for public clients, except for one small detail. The proper use of `client_ID` and `client_secret` for public clients.

It's not possible to send the client_secret along with the token request. So what can we do?
Ans: The authorization code flow was modified to fix the client secret problem using PKCE.

Before we look at PKCE, let's briefly look at the `implicit grant type`, which is deprecated but still available in most authorization servers.

In authorization code flow, the authorization server will return the authorization code in response to the authorized request for the implicit grant type. The authorization server will return the access_token and the ID_token directly in the front channel. So basically the token endpoint is not used to issue any tokens at all. And that means we don't use any client secret.

![alt text](/note/images/authz-and-refresh-token-grants.png)

Here's the flow from the implicit token grant type. Note here that the client is a JavaScript program running inside the browser.

This JavaScript program is served as part of an HTML page from an Http server, and that's not shown in the diagram. The client could also be a mobile application. What's common between the two? They both are categorized as public clients.

From `Step-2`, An authorized request is sent with the response type as token instead of response type as code. This indicates to the authorization server that it should return the `token` directly. Response type could even be ID token or a combination of token and ID token.

From `Step-3` Just like before, the authorization server will send a web page to the user for approval and credentials.

From `Step-4`  you will see that the access token is directly returned as part of the URL fragment to the JavaScript program. This is considered a security risk because the token is part of the URL and can be bookmarked or logged accidentally.

From `Step-5` Once the JavaScript client gets hold of the access token, the rest of the flow is the same. It can use the token to get user information. 

From `Step-6` It can also call the resource server with the token to get the necessary information.

`Now. A better way to achieve this is by using authorization code with PKCE.`
The original problem with authorization code grant type for public clients is that in the case
where a malicious user intercepts the authorization code and somehow knows about the client ID and secret, then that user can use the token endpoint to get an access token, effectively hacking into the resource API.

As we said before, the client secret is no longer a secret for public clients, and a hacker can get hold of the secret pretty easily. The use of secrets from public client is no security at all.

**OAuth 2.0- PKCE[Proof Key For Code Exchange] Extension:**
1. Proof Key For Code Exchange
2. Extension of the Authorization Code grant type
3. Usually used by public clients
4. Generate a **code_verifier**
    1. Min = 43 chars and Max = 128 chars
    2. Random and Impractical to guess
5. Sent code_challenge with <u>authorize request</u> <br>
    ```code_challenge = BASE64URL-ENCODE(SHA256(ASCII(code_verifier)))```
6. Send **code_verifier** with <u> token request</u> for grant type = code


In PKCE, the client first generates a random code verifier string. This code verifier is unique for that authorized request, and it's anywhere between 43 to 128 characters in length.

![alt text](/note/images/pkce-extension.png)

Most importantly, though, it should be completely random and impossible to guess.This can be considered like a dynamically generated client secret.
Once the code_verifier is generated, the client generates the code_challenge from the code verifier.
The way it does that is, it applies the Sha256 hash algorithm to it, and then applies the base64 URL encoding to the result. That's how it gets the code challenge.

The big deal here is that, you can go from `code_verifier` to `code_challenge`, but you cannot go from `code_challenge` to `code_verifier`. That's because you cannot get to the original data from hashed Sha 256 data.

Let's see how to use the code verifier and the code challenge in the PKCE flow.

![alt text](/note/images/pkce.png)

From `Step-2` Here you have the exact same diagram with minor changes when the user clicks on the connect button and just before the authorize request is sent, the client will generate this random code verifier that we talked about from the code verifier. The code challenge is created, and this code challenge is sent as part of the authorized request.

The authorization server will generate an authorization code and return the authorization code as part of for as before, but the authorization server will also associate the code challenge with the auth code.

When the client sends a token request `Step-5`Y, it will also send the code verifier. The authorization server will then convert the code verifier to the code challenge using the same Sha256 algorithm.

If the code challenge matches with that send as From `Step-2`, then the authorization server knows that the request is legitimate and it returns the token back.
 
In Short: Code verifier acts like a dynamic secret, only for that particular authorized request. For the next authorization request, a different code verifier will be generated by the client. The rest of the requests and responses remain the same.

If you use a library like Spring Boot, the code verifier and the code challenge are automatically generated and the developers do not need to do much except maybe enable PKCE.

Finally, one last thing that is worth mentioning here is that the use of Pixi is recommended for confidential clients as well. When used with confidential clients, the token request would be sent with the client secret as well as the code verifier.

### Client Credentials and Password Grants:

### OpenID Connet
//todo add image fopenID-connect-core.png

### Enterprise OpenID connect and Roles:
 Keycloak does provide a mapping between scopes and roles, which allow scopes to be used at enterprise level as welll.
 //todo add image enterprise-openID-connect.png

 Technology List:
    1. Microservice[API Gateway, Service Discovery]
    2. SAGA (Orcestration)
    3. SAGA (Choreography)
    4. Kafka
    5. Kafka Stream
    6. Keyclock
    7. DDD
    8. Hexagonal Architecture
    9. gRPC
    10. GraphQL
    11. Asynchronous Architecture using VThread, Groutine
    12. Promethous 
    13. Grafana
    14. Docker
    15. Kubernetes
    16. Optimize Query and Join
    17. Database Normalization
    18. Serverless REST API
    19. CI/CD Pipeline
    20. AWS
    21. Caching Implementaion using Redis
    22. Cassendra
    23. Linux
    24. Database Multimaster asynchronous replication(PostgreSQL).
    25. Nginx
    26. Networking
    27. Docker portainer


