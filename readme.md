## Config ➡️ Middleware ➡️ isAuthenticated.js
 * Form of middleware that is used to validate code to assure that user is logged into the application. If so, the validation data is exported and retrieved into [html-routes.js](../../routes/html-routes.js) file, where it is then passed as a parameter to validate that user is logged in; form of try and catch error method. 
 If the user is not logged in when attempting to access site, then the user is redirected to the home page.
 ![example_gif_1](./Assets/example_validate.gif)
 * As shown above, there error that is thrown when an already existing user attempts to login is caused by this middleware. However, when a new user logs in with a new, unique email, then the error is not thrown.
 ![isAuthenticated](./Assets/isAuthenticated.png)

 ## Config ➡️ config.json
* Object that creates connection from application to the database, where it outlines three directories: Development, Test, and Production, where each compartment within is able to connection by disclosing the username, password, database, host and dialect.
![example_png](./Assets/example_connection.png)
![example_png](./Assets/example_successConnect.png)
![example_png](./Assets/example_connectDB.png)
When the server is ran, if the connection is successful, then in the terminal it will print copy after execution of creating columns within the table, and will show an empty table with null values in the database. 

 ## Config ➡️ passport.js
 * Imports the object library passport, which is authentication middleware for Node.js that is extremely flexible, modular, and works hand-in-hand with express. Used primarily on backend for user validation through OAuth with over 500+ websites, such as Facebook, Twitter, Instagram, GitHub, and many more. [Read More](http://www.passportjs.org/#:~:text=Passport%20is%20authentication%20middleware%20for,500%2B%20Strategies%20Now!) Through importing passport, the child object of LocalStrategy is important as well through the passport-local library, a subsidiary of passport. All files within the models folder is also imported as *var db*.
 * Passport is then called by using its subsidiary library of ***Local Strategy*** that signs in via email, and then makes connection to database (*var db*) to connect to the User modal. 
    - *The User modal, which will be described in depth later, is a piece of middleware that connects to the database and inserts in succinct formation how data will be inserted into table. By doing so, all data is validated and authenticated to assure that database cannot be breached with malinformation.*
    - *Essentially, all models are linked one way or another the ***passport.js*** either directly, or indirectly, which allows for the application to filter users from non-users.*  
    - *In this instance, the modals folder contains **users.js** and **index.js**, which filters into the subject file.*
    ![example_png](./Assets/modals.gif)

   ## Models ➡️ index.js
   * Nuclei of database connection that filters data within file, assures that data is in javascript formation, non-duplicated, and then pushes and sequelizes into work bench to store.
   * File is executed in 5 main steps.
     - 1) Require necessary libraries and documents to link to filesystem, database, and server when deployed.
     - 2) Conditional statement to set variable of sequelize to process the URL presented directly, based off if one is presented or not
     - 3) Filter data model presented in **user.js** file, where it assures that data is in JavaScript formation, associated with the database, and is non repetative.
     - 4) When data is pushed into database on on file, it is in object notation. So this function uses an array function to grab each model name of the database and its associations.
     - 5) Once the values are grabbed, then they are synced into the database via **server.js**
         
   ## Models ➡️ user.js
   * The document that acts as a template for the database and is used to pivot all data from extraction point of routes, to authentication point in index.js, to be sent to server.js to then export to database. 
   * Main hub for sequelize, where this is where the template itself is held, and all needed authentication and validation keys are necessary before sending data on.
      - **There are pro's and con's to added the various plugins for the model**
      - ***PRO:*** 👓  
         - Able to import third party libraries to increase security in hashes with stored data.
            - ***bcryptjs*** is an instance for this application that grabs the users password and hashes into a crypt and stores the, then, crypt password in the database, which it is able to retrieve and transverse back into the original password upon retrieval.
            - ***simplecrpyt*** is another alternative to bcrypt that is ery database and user friendly. 
         - Able to dictate the columns to be created within the data base.
         - Able to insert validators and constraints into form to assure data inserted meets certain criteria to secure the database. [Read More](https://sequelize.org/master/manual/validations-and-constraints.html)
         ![alt-text](./Assets/formats.png)
      - ***CON:*** 🔥
         - Easily can complicated, or contradict, code that is inserted into the database by overlapping filters or inserting libraries that may have contradicting elements.
         - Can easily be replicated through front end filters to prevent duplication.
   * Uses sequelize library to make automatic and javascript version of mySql in back end of application to create defined tables and to set parameters to store data automatically.
      - The connection requires an object model to send data to server, which is done so by using key as the column headed, and the filter be data received from the front end that is verified and validated in the back end and filtered through the values components.
      - Different types of filters include binary null parameters, data type inputs, email, website URL, or any other tertiary parameter. 
      - **If** the forced parameter in the ***server.js*** file is set to true, then the developer can augment the number, type, and parameter values of the object to change details of the database. However, if not, then an error will be thrown because the attempted connection to the database will not be coherent and refuse to connect.
   ![example_png](./Assets/example_user.png)
      - When the data is processed, the ***bcrpyt*** plug-in hashes the information and sends to back end, which then allows for complete privacy, as only the algorithm itself is able to decode the hash and validate credentials.[Read More](https://www.npmjs.com/package/bcrypt)
      - An important plug-in for **all** databases as it assures the highest form of security for the clients and the company.
   ## Public 
   ![example_png](./Assets/front_end.gif)
      * The public folder houses all front-end technologies, which is intended solely for UI and linkage to backend database for maximum effectiveness. 
      * As shown, because the **html-routes** on the back end is connected to the **server** that runs the application, when a specific link or action is executed, then the html-route verifies the link and redirects the user to the proper form based off the action.
      * As mentioned earlier, there are front end functions as well that can be used to filter data and assure the passwords math, passwords are of valid length, email is authenticated, etc. to be executed upon submission to assure filtered and valid data **only** is stored into the database.

   ## Routes 
   * Sending and receiving data have two forms communications: 
      - (1) Method:
         * ![example_png](./Assets/crud.png)
            - **POST**
               * **C**reates routes for data to be inputted into database.
            - **GET**
               * **R**eads data by receiving data from database to view and analyze.
            - **PUT** / **PATCH**
               * **U**pdates data by finding values of certain fields and replacing through new data inserted.
            - **DELETE**
               * **D**eleted based off value.
      - (2) Route:   
         * Routes are arbitrary routes created by programmer where the front and back end of the application communicate to actually send and retrieve data. The data can come in many forms, but is primarily connoted with API-routes and HTML-routes. Nonetheless, all that routes do are navigate the user based off requests send sending and receiving the method and routes by means of how data is going to get transported by.
            d.

            ##  ➡️  api-routes.js 
            * Data is fully received from front end, connection is made to **user.js** to link to database, and the data is either sent or received, based off the method and links routes to fluently execution operations.
      
            ##  ➡️ html-routes.js 
            * Server redirects which HTML files to present based off users demands to redirect and send files based off the request given.
   ## Server.js
   ![example_gif](./Assets/server.gif)
   - The actual server script itself that feeds in all data exported from other back-end files to execute all commands given. It is where the dependencies are called and executed to enhance the application, along with where the developer denotes how the data will be sent and received when be transported from the front end to the back end, and vica versa. 
   - The main file that must be ran when using a website. Hosts the server and port required for UI.
   
   