
#**Token Based Authentication**
  

 **Authentication :**

     Authentication begins when a user tries to access information.
     First, the user must prove his access rights and identity.
     When logging into a computer, users commonly enter usernames and passwords for authentication purposes.This login combination, which must be assigned to each user, authenticate access.
     A better form of authentication, biometrics, depends on the user’s presence and biological makeup (i.e.,retina or fingerprints). This technology makes it more difficult for hacikers to 
 break into computer systems.


 **Authorization :**
   
     Authorization is the function of specifying access rights to resources related to information security and computer security
     Authorization is a process by which a server determines if the client has permission to use a resource or access a file.
     In multi-user computer systems, a system administrator defines which users are allowed access to the system, as well as the privileges of use for which they are eligible (e.g., access to file directories, hours of access).


  **Token Based Authentication :**
   
      Token based authentication is stateless.
      In token-based authentication, cookies and sessions will not be used. 
      A token will be used for authenticating a user for each request to the server.
      Token-Based Authentication, relies on a signed token that is sent to the server on each request.
      We are not storing any information about the user on the server or in a session.
  

  **Benefits of using Token Based Authentication :**

   **Cross-domain :** 
    
        cookies don't play well across different domains.
	A token-based approach allows you to make call to any server, on any domain because you use an HTTP header to transmit the user information.

   **Stateless :** 
    
        There is no need to keep a session store, the token is a self-contanined entity that conveys all the user information. 
	The rest of the state lives in cookies or local storage on the client side.

   **CDN :** 
   
        We can serve all the assets of your app from a CDN and your server side is just the API.

   **Decoupling :** 
   
        We are not tied to a particular authentication scheme.
	The token might be generated anywhere, hence your API can be called from anywhere with a single way of authenticating those calls.

   **Mobile ready :** 
   
        when we start working on a native platform (iOS, Android, Windows 8, etc.) cookies are not ideal when consuming a secure API (you have to deal with cookie containers). 
	Adopting a token-based approach simplifies this a lot.



###**Solutions :**

       Before using token based authentication,earlier server based authentication was used.
       Token based authentication concept alone takes care of many of the problems with having to store information on the server.
       No session information in application can scale and add more machines as necessary without worrying about where a user is logged in.

       Process of Token Based Application :
         
          User Requests Access with Username/Password.
	  Application validates credentials.
	  Application provides a signed token to the client.
	  Client stores that token and sends it along with every request.
	  Server verifies token and responds with data.
	  Once we have authenticated with our information and we have our token, we are able to do many things with this token.


###***IMPLEMENTATION : *

       For each and every applications there is "Token" to access the access the data and user-information.
       For example in gmail Application,to get TOKEN we have to call the GoogleAuthUtil() method.
           token = GoogleAuthUtil.getToken(MainActivity.this, Plus.AccountApi.getAccountName(mGoogleApiClient), scope);
      
       To fetch the data from Google API

          *AccessToken is shortlived. It expires in shor duration.*
	  *In OAuth insted of using AccessToken it that we can use "RefreshTokens"*   

            GoogleCredential credential = new GoogleCredential().setAccessToken(token);
	 
	    
         



