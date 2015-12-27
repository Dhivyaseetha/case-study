
#**Restful Design Pattern : **
    
#####**Restful Design pattern :**
   
   REST (REpresentation State Transfer) is an API,Which is the basic architectural design pattern.
   REST observes how the web pages are organized and how they are linked to each other, REST is modeled around a large number of "Resources" which "link" among each other.
   REST down play the "Procedure" aspect and define a small number of "action" based on existing HTTP Methods.
    *HTTP GET is used to get a representation of the resource.
    *To modify a resource, REST use HTTP PUT with the new representation embedded inside the HTTP Body.
    *To delete a resource, REST use HTTP DELETE.
    *To get metadata of a resource, REST use HTTP HEAD.

   
#####**How REST design pattern handles in application ?**   

   Client-request with state of particular request and server response with particular resource.
   Our android application should integrate with android platform .
   REST API uses HTTP.
   Facebook,Twitter uses REST API>
   To catch the data from memory by using content provider.


#####**Benefits of using RESTFUL Design Pattern :**

    REST provides
      1. Security 
      2. Performance 
      3. Interface complexity


  1. Security :

  Neither is inherently more secure than the other. Use good security principles:

  Encrypt communications
  Make sure you authenticate and authorize users before processing
  Good coding habits to avoid direct attacks

  2. Performance :

  Both raw performance and scalability will go to REST due to the request following simple HTTP protocols.

  3. Interface Complexity :

  With REST the onus is on you to perform the preprocessing work (authentication/authorization/etc) while with SOAP much of that can be accomplished with a pluggable processing chain.


#####**Solution : **

#####**Design pattern to handle REST Methods :**
   
   There are three design pattern to handle methods:
    
     *Use a service API.
     *Use the Content Provider API.
     *Use the Content Provider API and a Sync Adapter.


#####**Use of Service API :**

    Service API is an android component.
    In REST method an entity which
      *Prepares the Http URL and Http request body.
      *Executes the transaction.
      *Process the Http response.

    Service API select the optimal content type for responses.
      *Binary JSON,XML.
      *Service is the state of the operation.All pending operations would be shutdown by service.

   *ServiceHelper*
     
      Exposes an asynchronous API for the front-end application that provides access to resources. 
      Translates a resource request from the UI layer into service invocation. 
      Immediately returns a unique request id to a caller, and later broadcasts the result of the request, once completed by the service layer. 
      Maintains the state of all pending requests.


#####**Use of ContentProvider API :**      

      Using Content Provider the user can Insert,Update and Delete the data from DataBase.
      The reason for keeping the local SQLite database in sync with the REST API is you will not be required call the REST API to transfer redundant data. 
      The demo app only retrieves data that is newer than the most recent GET request. 
      Each request type is mapped to a different method the ContentProvider. 
      Here is the mapping:
       *GET    - query()
       *POST   - insert()
       *PUT    - update()
       *DELETE - delete()

      Database columns used to store transitional state, with valid values where indicated:

      status: http method or new row
      
       * GET    -  query
       * POST   -  insert
       * PUT    -  update
       * DELETE -  delete
       * NEW    -  a new row retrieve by a GET request
      

   **Benefits are: **

      Saved bandwidth.
      Maximized battery life.
      Improved performance.
      Data is persisted even if the app process is killed due to device memory overload.


 ** Use the ContentProvider API and Sync Adapter : **

    The sync adapter framework queues sync requests if there are other sync operations queued or in-progress. 
    A sync operation will also be queued if the device is busy.
    SyncAdapter is used in Gmail,Facebook,Twitter.

    Reasons for using the SyncAdapter:

     *Coordinate sync operations with other applications on the device. 
     *Automatically handle exponential back-off with soft errors.
     *Enable the application to function off-line.
     *Will not execute a sync operation while the device is not connected to a network. Will automatically sync when a connection becomes available.
     *It minimize the network storage.


#####** Implementation :**

  GET statuses/retweet-of-me

   - Returns the most recent tweets authored by the authenticating user that have been retweeted by others.

   *Prepare to tweet :*
    
    Use the Shared Preferences to instantiate our Twitter object:

     //get preferences for user twitter details 
      
      tweetPrefs = getSharedPreferences("TwitNicePrefs", 0); 
	             
    //get user token and secret for authentication 
      
      String userToken = tweetPrefs.getString("user_token", null); 
      String userSecret = tweetPrefs.getString("user_secret", null); 
			       
    //create a new twitter configuration usign user details 

    Configuration twitConf = new ConfigurationBuilder() 
			         .setOAuthConsumerKey(TWIT_KEY) 
				 .setOAuthConsumerSecret(TWIT_SECRET) 
				 .setOAuthAccessToken(userToken) 
			         .setOAuthAccessTokenSecret(userSecret) 
				 .build(); 
						

    //create a twitter instance 

     tweetTwitter = new TwitterFactory(twitConf).getInstance();
     
    //get any data passed to this intent for reply

     Bundle extras = getIntent().getExtras();

     If the tweet is an ordinary update rather than a reply, there will be no extras. 
     If there are extras, we know the tweet is a reply:

     if(extras !=null) 
     { 
       //get the ID of the tweet we are replying to 
 
        tweetID = extras.getLong("tweetID"); 
 
       //get the user screen name for the tweet we are replying to 
 	
       tweetName = extras.getString("tweetUser"); 
 				   					     
   }


     Here we retrieve the ID and screen-name for the tweet to reply to. Next we use this information to add the username to the text-field, still inside the "if" statement:

					  
     //get a reference to the text field for tweeting 

     EditText theReply = (EditText)findViewById(R.id.tweettext); 

    //start the tweet text for the reply @username 
 
     theReply.setText("@"+tweetName+" "); 

    //set the cursor to the end of the text for entry 

    theReply.setSelection(theReply.getText().length());





