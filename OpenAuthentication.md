 
#**OpenAuthentication**

  **Open Authentication : **

       OAuth (Open Authorization) is an open standard for token-based authentication and authorization on the Internet.
       OAuth is an authorization protocol - or in other words, a set of rules - that allows a third-party website or application to access a user’s data without the user needing to share login credentials.
       OAuth is also known as OAuth Core.


 ** Why OAuht is introduced ?**

      OAuth acts as an intermediary on behalf of the end user, providing the service with an access token that authorizes specific account information to be shared. The process for obtaining 
 the token is called a flow.
      OAuth, which was first released in 2007, was conceived as an authentication method for the Twitter application program interface (API).
      
  
 **Why to use OAuth ? **
      
       From user point of view OAuth
         *Increase trust
	 *Decrease user sensitivity
	 *No more expanded access and risk
	 *Easy service revocation
         *Password isn't required anymore
	 *Easier to implement stronger authentication.


 ** Process of OAuth :**	 
     
       A main point of the OAuth specs is for a content provider (e.g. Facebook, Twitter, etc.) to assure a server (e.g. a Web app that wishes to talk to the content provider on behalf of the client) that the client has some identity.
       *The client submits an authorization request to the server, which validates that the client is a legitimate client of its service.
       *The server redirects the client to the content provider to request access to its resources.
       *The content provider validates the user's identity, and often requests their permission to access the resources.
       *The content provider redirects the client back to the server, notifying it of success or failure. This request includes an authorization code on success.
       *The server makes an out-of-band request to the content provider and exchanges the authorization code for an access token.

       The server can now make requests to the content provider on behalf of the user by passing the access token.


 **Benefits of OAuth : **     
     
     Compared to sessions OAuth provides several benefits.
       * The Important one we can use the same login for web as well as native(mobile) apps
       * You don't have to save session information on the server
       * You can easily set expiry date in token itself
       * OAuth provides security
         Security : 
	    OAuth data transfers must take place on SSL (Secure Sockets Layer) to ensure the most trusted cryptography industry protocols are being used to keep data as safe as possible.

         Popularity :
	    OAuth has already been adopted by Google, Facebook, Twitter, and Yahoo, so even if only a slice of their users have made the transition, that still equates to many millions of 
      current users.


 ** Benefits of using OAuth as login provider :**

       OAuth has become a popular mechanism to facilitate sharing of data between applications.
       To use OAuth for login, all you have to do is to use some OAuth code library and create a consumer application that will connect to an existing OAuth provider such as twitter, linkedIn, Facebook etc.
       The alternative to using OAuth as the login provider can be to implement OpenId or some proprietary login mechanism. 
       Here are some advantages for login and profile management.
         We don't have to create another profile on the net.
	 Fewer passwords to remember.
	 Do not have to submit a password to your application if he / she does not completely trust us.
	 User can prevent access to the application from the OAuth provider.
	 Allows for exciting extra functionality and synergies when taking advantage of the social graph and other data and features made available by the OAuth provider.


 **Solutions :**
   
    The android-oauth-client library helps you to easily add an OAuth flow to your existing Android application.
    It automatically shows a customizable Android dialog with WebView to guide the user to eventually grant you an access token.
    To help you manage access tokens, the library also includes an out-of-the-box credential store which stores tokens in SharedPreferences.
    This client library is an Android extension to the Google OAuth Client Library for Java.

    *OAuth flow you intend to incorporate into the Android application, the android-oauth-client library can be used in 2 simple steps:

      *Obtain an instance of OAuthManager by supplying the following 2 parameters:
        An *AuthorizationFlow* instance which automatically handles the OAuth flow logic,
        An *AuthorizationUIController* which manages the UI.
    
        Call one of the 3 possible authorize methods on OAuthManager. The call may be called from any thread either synchronously or asynchronously with an OAuthCallback<Credential>.
           * OAuthManager.authorize10a()
           * OAuthManager.authorizeExplicitly()
           * OAuthManager.authorizeImplicitly()


 **Implementation :**
 
 **Obtaining an OAuthManager instance**

        OAuthManager can be obtained by direct instantiation.

        OAuthManager oauth = new OAuthManager(flow, controller);

 **Obtaining an access token via the OAuthManager**

    To start the OAuth flow and obtain an access token, call one of the authorize() methods according to the authorization flow of your choice.
    You may invoke the authorize() method synchronously:

     Credential credential = oauth.authorizeImplicitly("userId", null, null).getResult();
     // continue to make API queries with credential.getAccessToken()

     You may also invoke the authorize() method asynchronously with an OAuthCallback, executed on a android.os.

      OAuthCallback<Credential> callback = new OAuthCallback<Credential>() {
        @Override public void run(OAuthFuture<Credential> future) {
          Credential credential = future.getResult();
	   // make API queries with credential.getAccessToken()
             }
	};
			
      oauth.authorizeImplicitly("userId", callback, handler);

  
 **CredentialStore**

      Use the provided SharedPreferencesCredentialStore, which automatically serializes access tokens to and from SharedPreferences in JSON format.

      SharedPreferencesCredentialStore credentialStore =new SharedPreferencesCredentialStore(context,"preferenceFileName", new JacksonFactory());


 **AuthorizationFlow**

  An AuthorizationFlow instance may be obtained via its Builder:

  AuthorizationFlow.Builder builder = new AuthorizationFlow.Builder(
                                      BearerToken.authorizationHeaderAccessMethod(),
                                      AndroidHttp.newCompatibleTransport(),
                             	      new JacksonFactory(),
                        	      new GenericUrl("https://socialservice.com/oauth2/access_token"),
		                      new ClientParametersAuthentication("CLIENT_ID", "CLIENT_SECRET"),
		                      "CLIENT_ID",
			              "https://socialservice.com/oauth2/authorize");
   builder.setCredentialStore(credentialStore);
   AuthorizationFlow flow = builder.build();


   For OAuth 2.0 flows, you may wish to add OAuth scopes:

       builder.setScopes(Arrays.asList("scope1", "scope2"));

