
#**Persistent Storage**

 **Storage : **

      In a computer, storage is the place where data is held in an electromagnetic or optical form for access by a computer processor.
      * Data can be stored in two ways.
         *Volatile Storage
	 *Non Volatile Storage.(Persistent storage).


 ** Persistence Storage : **

      Persistent storage is any data storage device that retains data after power to that device is shut off.
      It is also referred to as non-volatile storage.
      Hard disk drives and solid-state drives are common types of persistent storage. 
      Persistent storage such as non-volatile RAM and flash-based RAM.


 ** Why Persistence come into existence? **

      RAM and cache are typically non-persistent, and are erased of data when power is turned off.
      Non-volatile RAM and flash-based RAM are persistent.
      Persistence is beneficial so that in the event of a crash or reboot, data is not lost.


 ** Benefits of Persistent Storage : **

      * In Persistent storage the data are stored for ***Future Reference***.
      * Persistence is implemented as a behavior.
      * The new persistence behaviors include:

          * saveFavorite  :  persists page state and information when the web page is saved as a favorite.
	  * saveHistory   :  persists page state and information within the current session's memory.
	  * saveSnapshot  :  persists page state and information directly in the page when users save the Web page to their hard disk.
	  * userData      :  persists page state and information within an XML store, a hierarchical data structure.


 ** Solutions for Persistent Storage in Android : **
      
       Android provides several options for you to save persistent application data namely
        *SharedPreference
	*Internal Storage
	*External Storage
	*SQLite Database
	*Network Connection.

    *Shared Preference*
        -Store private primitive data in key-value pairs.
	-Shared Preference is preferable to store only small amount of data.

       	To get a SharedPreferences object for your application, use one of two methods:

         *getSharedPreferences()  :  Use this if you need multiple preferences files identified by name, which you specify with the first parameter.
         *getPreferences()        :  Use this if you need only one preferences file for the Activity.

        To write values:

	 *Call edit() to get a SharedPreferences.Editor.
	 *Add values with methods such as putBoolean() and putString().
	 *Commit the new values with commit()

	To read values, use SharedPreferences methods such as getBoolean() and getString(). 

    *Internal Storage*
        -Store private data on the device memory.

      To create and write a private file to the internal storage:

	Call openFileOutput() with the name of the file and the operating mode. This returns a FileOutputStream.
	Write to the file with write().
	Close the stream with close().

       To read a file from internal storage:

	Call openFileInput() and pass it the name of the file to read. This returns a FileInputStream.
	Read bytes from the file with read().
	Then close the stream with close().

    *External Storage*
        -Store public data on the shared external storage.

    *SQLite Database*
        -Store structured data in a private database.

       To create a database in SQLITE :
         SQLiteDatabase mydatabase = openOrCreateDatabase("your database name",MODE_PRIVATE,null);

       To create and insert the database in android :
         mydatabase.execSQL("CREATE TABLE IF NOT EXISTS tablename(Username VARCHAR,Password VARCHAR);");
	 mydatabase.execSQL("INSERT INTO tablename VALUES('admin','admin');");

       To fetch the data from Database :
         Cursor resultSet = mydatbase.rawQuery("Select * from tablename",null);
	 resultSet.moveToFirst();
	 String username = resultSet.getString(1);
	 String password = resultSet.getString(2);

    *Network Connection*
        -Store data on the web with your own network server.

      We can use the network (when it's available) to store and retrieve data on your own web-based services. To do network operations, use classes in the following packages:
       * java.net.*
       * android.net.*


 **Implementations :**

      Implementation of Shared Preference in android.

 **SharedPreferenceActivity.java :**
 

      /* In this file the shared preference is declared */
      public class SharedPref_activity
      {
      	public SharedPreferences sh;
        public SharedPreferences.Editor sh_editor;
 			
	public static final String PREFS_NAME = "mysharedpreference";

					
	String fname="fname";
        
	public SharedPref_activity(Context context) {
        // TODO Auto-generated constructor stub
 	sh=context.getSharedPreferences(PREFS_NAME,Context.MODE_PRIVATE);
	sh_editor = sh.edit();
																		
	}

    public String getFname() {
																									return sh.getString(fname,"");																					}
																								    public void setFname(String fname1) {																				sh_editor.putString(fname,fname1);
																								        sh_editor.commit(); 
																									}


 **MainActivity.java : **

    public class MyActivity extends Activity {
        EditText f_name;
	Button submit;
	SharedPref_activity obj_sp;

	protected void onCreate(Bundle savedInstanceState) {
	 super.onCreate(savedInstanceState);
         setContentView(R.layout.main);
			   
        obj_sp=new SharedPref_activity(getApplicationContext());
				           
        if( getIntent().getBooleanExtra("Exit me", false)){
	 finish();
	 return;
	 }
	 
	f_name=(EditText)findViewById(R.id.editText);
        
	
	submit=(Button)findViewById(R.id.button);

	submit.setOnClickListener(new View.OnClickListener() {
	   @Override
        public void onClick(View v) 
	{
	String fname  = f_name.getText().toString();
        obj_sp.setFname(fname);
	}

      Intent in=new Intent(getApplicationContext(),display.class);
      startActivity(in);

   }


 ** Display.java : **

     public class Display extends Activity {

      EditText firstname;
      SharedPref_activity obj_sp;

      public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
	setContentView(R.layout.display);

       firstname=(EditText)findViewById(R.id.editText4);

       obj_sp=new SharedPref_activity(getApplicationContext());
	         
		         
       firstname.setText(obj_sp.getFname());

        }


 **Result : **

     In the shared preference I created object for shared preference.
     By using that object we can store and access those data into application.
     In the Main activity the person's firstname would be get from the user.
     That name would be stored and it would be displayed in the Display page.




















