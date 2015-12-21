# case-study

1 Session based authentication
   
#**Session based authentication:**

  **Authentication :**

  	Authentication begins when a user tries to access information. 
	First, the user must prove his access rights and identity.
	When logging into a computer, users commonly enter usernames and passwords for authentication purposes.This login combination, which must be assigned to each user, authenticates 
access.
        A better form of authentication, biometrics, depends on the user’s presence and biological makeup (i.e.,retina or fingerprints). This technology makes it more difficult for hackers to break into computer systems.


  **Authorization :**
 
        Authorization is the function of specifying access rights to resources related to information security and computer security
        Authorization is a process by which a server determines if the client has permission to use a resource or access a file.
	In multi-user computer systems, a system administrator defines which users are allowed access to the system, as well as the privileges of use for which they are eligible (e.g., access to file directories, hours of access).


   **Session :**

         A session refers to all the requests that a single client makes to a server.
	 A session is specific to the user and for each user a new session is created to track all the request from that user.
	 A session is a semi-permanent interactive information interchange, also known as a dialogue, a conversation or a meeting, between two or more communicating devices, or between a 
computer and user.
         A session is set up or established at a certain point in time, and torn down at a later point in time. An established communication session may involve more than one message in each 
direction. 

##**Session Based Authentication :**

         Session-based authentication is much more secure than basic authentication.
         In Session-based Authentication the Server does all the heavy lifting server-side.
	 Session-based authentication saves credentials using a cookie.
	 Cookies are usually small text files, given ID tags that are stored on your computer's browser directory or program data subfolders. 
	

   **Why Session Based Authentication is come into existence ?**

         In Session-based Authentication the Server does all the heavy lifting server-side. 
	 Broadly speaking a client authenticates with its credentials and receives a session_id (which can be stored in a cookie) and attaches this to every subsequent outgoing request.
	 It is just an identifier and the server does everything else. It is stateful. It associates the identifier with a user account (e.g. in memory or in a database). So this could be     considered as a "token". 
         It can restrict or limit this session to certain operations or a certain time period and can invalidate it if there are security concern and more importantly it can do and change all of this on the fly. 
	 Furthermore it can log the users every move on the website(s). Possible disadvantages are bad scale-ability (especially over more than one server farm) and extensive memory usage.
	 Http-authentication is sent with each single request. This means that the request remains autonomous of any previous requests (also known as being stateless). 
	 So session Based Authentication is come into existence.


   **Benefits of Session Based Authentication :**	 
      
         *The main reason for using session-based logins are the following:
              *Aesthetics : You can't style the http-authentication box.
              *Usability  : You can't put descriptive text or a link to "forgotten password" or "create new account" in the box.

###**SOLUTIONS : **
 
          The Android does not support *Session Based Authentication* and we can use Basic HTTP Authentication solution for Android.

	  *Client-Server communication**
              *The Client sends the HTTP Request with no credentials
	      *The Server sends back a challenge
	      *The Client negotiates and identifies the right authentication scheme
	      *The Client sends a second Request, this time with credentials

	   Basic Authentication on the HttpClient – via a CredentialsProvider:
	        
		 CredentialsProvider provider = new BasicCredentialsProvider();

		 UsernamePasswordCredentials credentials = new UsernamePasswordCredentials("user1", "user1Pass");

		 provider.setCredentials(AuthScope.ANY, credentials);

		 HttpClient client = HttpClientBuilder.create().setDefaultCredentialsProvider(provider).build();
		  
		 HttpResponse response = client.execute(new HttpGet(URL_SECURED_BY_BASIC_AUTHENTICATION));

		 int statusCode = response.getStatusLine().getStatusCode();

		 assertThat(statusCode, equalTo(HttpStatus.SC_OK));
		 
	    As we can see, creating the client with a credentials provider to set it up with Basic Authentication is not difficult.

            Using HTTP basic authentication is not preferable. It's unsafe, since it sends the username and the password through the request headers. We should consider something like 
OAuth instead of using HTTP basic authentication.
 
   **OAuth Process : **
        
	*User App make a RequestCode to server.
	*Sever send the URL and Authentication code.
	*The Browser on seperate device.
	*The user send the userlogin and context to server.
	*User App Poll the server.
	*Server send the token response to UserApp.
	*UserApp usetoken to call Google API.

       
###**IMPLEMENTATION**       

      An implementation of authentication class is able to obtain authentication information for a connection in several ways.
      Authenticator which extends Authenticator by setDefault(Authenticator a).
      Then it should override getPasswordAuthentication() which dictates how the authentication info is obtained.
       
      * Methods in Authenticator:
          *setDefault(Authenticator a)
          *getPasswordAuthentication

      * Public Constructor
           * Authenticator()

 ** Public Methods :**

         * synchronized static PasswordAuthentication requestPasswordAuthentication(String rHost, InetAddress rAddr, int rPort, String rProtocol, String rPrompt, String rScheme)

             -Invokes the methods of the registered authenticator to get the authentication info.
	   
	  * static PasswordAuthentication requestPasswordAuthentication(String rHost, InetAddress rAddr, int rPort, String rProtocol, String rPrompt, String rScheme, URL rURL, Authenticator.
   RequestorType reqType)
	  
	      -Invokes the methods of the registered authenticator to get the authentication info.

	  * synchronized static PasswordAuthentication requestPasswordAuthentication(InetAddress rAddr, int rPort, String rProtocol, String rPrompt, String rScheme)

              -Invokes the methods of the registered authenticator to get the authentication info. 

	  * static void	setDefault(Authenticator a)
         
	      -Sets a as the default authenticator.
   
   ***Parameters**

              rHost  - 	host name of the connection that requests authentication.
              rAddr  -  address of the connection that requests authentication.
              rPort  -   port of the connection that requests authentication.
          rProtoco   -   protocol of the connection that requests authentication.
            rPrompt  -	 realm of the connection that requests authentication.
            rScheme  -	 scheme of the connection that requests authentication.
    
   **Returns**
       
            password authentication info or null if no authenticator exists.
 

   **Protected Methods**

      * protected PasswordAuthentication getPasswordAuthentication ()

	  Returns the collected username and password for authorization. The subclass has to override this method to return a value different to the default which is null.
	  Returns null by default.

	  Returns
	  collected password authentication data.

       * protected final String getRequestingHost ()
	  -Returns the host name of the connection that requests authentication or null if unknown.

	  Returns
	   -name of the requesting host or null.

       * protected final int getRequestingPort ()
	  -Returns the port of the connection that requests authorization.

	  Returns
	   -port of the connection.

       * protected final String getRequestingPrompt ()
	  -Returns the realm (prompt string) of the connection that requests authorization.

	  Returns
	   -prompt string of the connection.

       * protected final String getRequestingProtocol ()
	   -Returns the protocol of the connection that requests authorization.

	  Returns
	   -protocol of the connection.

       * protected final String getRequestingScheme ()
	  -Returns the scheme of the connection that requests authorization, for example HTTP Basic Authentication.

	  Returns
	   -scheme of the connection.

       * protected final InetAddress getRequestingSite ()
	  -Returns the address of the connection that requests authorization or null if unknown.

	  Returns
	   -address of the connection.

       * protected URL getRequestingURL ()
	  -Returns the URL of the authentication request.

	  Returns
	   -authentication request url.

       * protected Authenticator.RequestorType getRequestorType ()
	  -Returns the type of this request, it can be PROXY or SERVER.

	  Returns
	   -RequestorType of the authentication request.



