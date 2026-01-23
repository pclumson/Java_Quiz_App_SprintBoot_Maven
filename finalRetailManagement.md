# Module 4: Java Development with Databases
&lt;table border&#x3D;&quot;1&quot;&gt;
&lt;thead&gt;
&lt;tr&gt;
&lt;th&gt;Package/
Method&lt;/th&gt;
&lt;th&gt;Description&lt;/th&gt;
&lt;th&gt;Code Example&lt;/th&gt;
&lt;/tr&gt;
&lt;/thead&gt;
&lt;tbody&gt;
&lt;tr&gt;
&lt;td&gt;Creating a table in a database&lt;/td&gt;
&lt;td&gt;To create a table for storing book information, use the CREATE command.This creates a table named &#x27;Books&#x27; with four columns: BookID, Title, Author, and Price. The PRIMARY KEY ensures that each book has a unique ID, and NOT NULL means the Title column cannot be empty. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;CREATE TABLE Books (
    BookID INT PRIMARY KEY,
    Title VARCHAR(100) NOT NULL,
    Author VARCHAR(100),
    Price DECIMAL(10, 2)
);
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Add a new column to the table&lt;/td&gt;
&lt;td&gt;You can use the ALTER command to edit the books table.The &#x27;ADD&#x27; command followed by the column name and data type adds the column to the table. In this code, we are adding an integer column called &#x27;PublicationYear&#x27; to the &#x27;Books&#x27; table.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;ALTER TABLE Books
ADD PublicationYear INT;
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Remove a table&lt;/td&gt;
&lt;td&gt;
Use the DROP TABLE command to remove the table entirely. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt; DROP TABLE Books; &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Add a new record&lt;/td&gt;
&lt;td&gt;To add a new book, use the INSERT command and specify values for the BookID, Title, Author, and Price. This adds a new row to the &#x27;Books&#x27; table.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;INSERT INTO Books (BookID, Title, Author, Price)
VALUES (1, &#x27;The Art of SQL&#x27;, &#x27;Stephane Faroult&#x27;, 39.99);
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Update a record&lt;/td&gt;
&lt;td&gt;If the price of a book changes, update it using the UPDATE command and use SET to specify the new price. The WHERE clause ensures that only the book with BookID 1 is updated.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;UPDATE Books
SET Price &#x3D; 29.99
WHERE BookID &#x3D; 1;
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Delete a record&lt;/td&gt;
&lt;td&gt;To delete a book, use the DELETE command and use the WHERE clause to specify the BookID. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;DELETE FROM Books
WHERE BookID &#x3D; 1;
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Retrieve records through filtering&lt;/td&gt;
&lt;td&gt; To retrieve all books written by a specific author, use the SELECT command with the WHERE clause acting as a filter to specify the name of the author. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;SELECT * FROM Books
WHERE Author &#x3D; &#x27;Stephane Faroult&#x27;;
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Create a simple procedure&lt;/td&gt;
&lt;td&gt;To create a simple procedure to calculate the total price of all books in the Books table, use the CREATE PROCEDURE command.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;CREATE PROCEDURE CalculateTotalPrice()
BEGIN
    SELECT SUM(Price) AS TotalPrice
    FROM Books;
END;
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Call a procedure&lt;/td&gt;
&lt;td&gt;Call a procedure whenever you need it by using the CALL statement.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;CALL CalculateTotalPrice();
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Include a driver for a MySQL database&lt;/td&gt;
&lt;td&gt;To include the driver for a MySQL database, add the &#x27;MySQL Connector/J&#x27; dependency to your project.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;&lt;dependency&gt;
&lt;groupId&gt;mysql&lt;/groupId&gt;
&lt;artifactId&gt;mysql-connector-java&lt;/artifactId&gt;
&lt;version&gt;8.0.33&lt;/version&gt;
&lt;/dependency&gt; &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Establish a connection to a MySQL database&lt;/td&gt;
&lt;td&gt; In this code, the &#x27;DriverManager.getConnection()&#x27; part establishes the connection using the database URL, username, and password. The &#x27;try&#x27; command is part of the &#x27;try-with-resources&#x27; statement which automatically closes the connection to prevent any resource leaks. When the &#x27;try&#x27; block completes (successfully or due to an exception), the &#x27;close()&#x27; method is automatically called on all resources declared in the parentheses. The &#x27;catch&#x27; command is part of the &#x27;try-catch&#x27; statement that handles exceptions and prevents abnormal termination of the program, making debugging easier.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt; import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
public class DatabaseConnection {
    public static void main(String[] args) {
        String url &#x3D; &quot;jdbc:mysql://localhost:3306/bookstore&quot;;
        String user &#x3D; &quot;root&quot;;
        String password &#x3D; &quot;password&quot;;
        try (Connection connection &#x3D; DriverManager.getConnection(url, user, password)) {
            if (connection !&#x3D; null) {
                System.out.println(&quot;Connected to the database!&quot;);
            }
        } catch (SQLException e) {
            System.out.println(&quot;Error connecting to the database&quot;);
            e.printStackTrace();
        }
    }
}&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Add a dependency code to create a connection pool&lt;/td&gt;
&lt;td&gt;Use Apache Commons Database Connection Pooling (or DBCP to create a basic connection pool. Add a dependency code section to your pom.xml file.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;&lt;dependency&gt;
    &lt;groupId&gt;org.apache.commons&lt;/groupId&gt;
    &lt;artifactId&gt;commons-dbcp2&lt;/artifactId&gt;
    &lt;version&gt;2.9.0&lt;/version&gt;
&lt;/dependency&gt;
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Java code needed to implement the connection pool&lt;/td&gt;
&lt;td&gt;In this code, the &#x27;BasicDataSource&#x27; part manages the connection pool. The &#x27;setInitialSize()&#x27; part specifies the number of connections in the pool. The &#x27;getConnection()&#x27; part retrieves a connection from the pool. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;import org.apache.commons.dbcp2.BasicDataSource;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;
public class ConnectionPoolExample {
    public static void main(String[] args) {
        // Create a connection pool
        BasicDataSource dataSource &#x3D; new BasicDataSource();
        dataSource.setUrl(&quot;jdbc:mysql://localhost:3306/bookstore&quot;);
        dataSource.setUsername(&quot;root&quot;);
        dataSource.setPassword(&quot;password&quot;);
        dataSource.setInitialSize(5); // Number of initial connections in the pool
        try (Connection connection &#x3D; dataSource.getConnection();
             Statement statement &#x3D; connection.createStatement();
             ResultSet resultSet &#x3D; statement.executeQuery(&quot;SELECT * FROM Books&quot;)) {
            while (resultSet.next()) {
                System.out.println(&quot;Book Title: &quot; + resultSet.getString(&quot;Title&quot;));
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Use a PreparedStatement object to insert data&lt;/td&gt;
&lt;td&gt;This code inserts a new book into the table with the title &quot;New Book&quot;, the author &quot;Author X&quot;, and price of &quot;25.99.&quot; The SQL query includes placeholders (using a question mark) for values that are later replaced with actual data using the &#x27;setString()&#x27; and &#x27;setDouble()&#x27; methods. The &#x27;executeUpdate()&#x27; method executes the INSERT command and returns the number of rows affected. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;PreparedStatement preparedStatement &#x3D; connection.prepareStatement(
  &quot;INSERT INTO Books (Title, Author, Price) VALUES (?, ?, ?)&quot;);
preparedStatement.setString(1, &quot;New Book&quot;);
preparedStatement.setString(2, &quot;Author X&quot;);
preparedStatement.setDouble(3, 25.99);
int rowsAffected &#x3D; preparedStatement.executeUpdate();
System.out.println(&quot;Rows inserted: &quot; + rowsAffected);&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Use a PreparedStatement object to update data&lt;/td&gt;
&lt;td&gt; This code updates the book&#x27;s price to &quot;30.99.&quot; UPDATE modifies rows based on the condition in the WHERE clause. Reusing the same query structure for different parameter values improves efficiency. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;PreparedStatement preparedStatement &#x3D; connection.prepareStatement(
  &quot;UPDATE Books SET Price &#x3D; ? WHERE Title &#x3D; ?&quot;);
preparedStatement.setDouble(1, 30.99);
preparedStatement.setString(2, &quot;New Book&quot;);
int rowsAffected &#x3D; preparedStatement.executeUpdate();
System.out.println(&quot;Rows updated: &quot; + rowsAffected);
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Use a PreparedStatement object to query existing data&lt;/td&gt;
&lt;td&gt;
The SELECT query retrieves the data, and the parameters make the query dynamic. Iterating over the ResultSet allows you to process each row returned.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;PreparedStatement preparedStatement &#x3D; connection.prepareStatement(
  &quot;SELECT * FROM Books WHERE Author &#x3D; ?&quot;);
preparedStatement.setString(1, &quot;Author X&quot;);
ResultSet resultSet &#x3D; preparedStatement.executeQuery();
while (resultSet.next()) {
  System.out.println(&quot;Title: &quot; + resultSet.getString(&quot;Title&quot;));
  System.out.println(&quot;Price: &quot; + resultSet.getDouble(&quot;Price&quot;));
}
END;
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Use a Callable Statement object using an input parameter&lt;/td&gt;
&lt;td&gt; This is an example of using a CallableStatement object to call a stored procedure by using an input parameter. In this code, the procedure &#x27;GetBooksByAuthor&#x27; takes an input parameter &#x27;(authorName)&#x27; and retrieves books written by that author. The setString(1, &quot;Author X&quot;) method sets the value of input parameter 1, which is &#x27;authorName&#x27; in the stored procedure, to &quot;Author X&quot;. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt; CREATE PROCEDURE GetBooksByAuthor(IN authorName VARCHAR(255))
BEGIN
  SELECT Title, Price FROM Books WHERE Author &#x3D; authorName;
END;
CallableStatement callableStatement &#x3D; connection.prepareCall(&quot;{CALL GetBooksByAuthor(?)}&quot;);
callableStatement.setString(1, &quot;Author X&quot;);
ResultSet resultSet &#x3D; callableStatement.executeQuery();
while (resultSet.next()) {
  System.out.println(&quot;Title: &quot; + resultSet.getString(&quot;Title&quot;));
  System.out.println(&quot;Price: &quot; + resultSet.getDouble(&quot;Price&quot;));
} &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Use a Callable Statement object using input and output parameters&lt;/td&gt;
&lt;td&gt;This is an example of using a CallableStatement object to call a stored procedure by using input and output parameters. In this code, the output parameters allow the stored procedure to return values to the Java application. The &#x27;registerOutParameter()&#x27; method specifies the type of the output parameter, which in this example is java.sql.Types.DOUBLE. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;CREATE PROCEDURE GetTotalSales(OUT totalSales DOUBLE)
BEGIN
  SELECT SUM(Price) INTO totalSales FROM Books;
END;
CallableStatement callableStatement &#x3D; connection.prepareCall(&quot;{CALL GetTotalSales(?)}&quot;);
callableStatement.registerOutParameter(1, java.sql.Types.DOUBLE);
callableStatement.execute();
double totalSales &#x3D; callableStatement.getDouble(1);
System.out.println(&quot;Total Sales: &quot; + totalSales); &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Use a PreparedStatement object to insert data and retrieve a generated key&lt;/td&gt;
&lt;td&gt;In this code, the auto-generated keys are returned using &#x27;getGeneratedKeys()&#x27;, which is useful for tracking newly inserted records. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;PreparedStatement preparedStatement &#x3D; connection.prepareStatement(
  &quot;INSERT INTO Books (Title, Author, Price) VALUES (?, ?, ?)&quot;,
  Statement.RETURN_GENERATED_KEYS);
preparedStatement.setString(1, &quot;Generated Key Book&quot;);
preparedStatement.setString(2, &quot;Author Y&quot;);
preparedStatement.setDouble(3, 30.00);
preparedStatement.executeUpdate();
ResultSet generatedKeys &#x3D; preparedStatement.getGeneratedKeys();
if (generatedKeys.next()) {
  int newBookID &#x3D; generatedKeys.getInt(1);
  System.out.println(&quot;Generated Book ID: &quot; + newBookID);
}  &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Handle SQL exceptions&lt;/td&gt;
&lt;td&gt;In this code, the &#x27;try&#x27; and &#x27;catch&#x27; statements catch any exceptions that happen during the &#x27;try&#x27; block when creating the PreparedStatement and executing the query. If anything fails for any reason the exception is passed to the &#x27;catch&#x27; block and a message appears on screen enabling the developer to troubleshoot and fix the issue. Catching exceptions ensures your application can gracefully handle errors such as invalid queries or missing tables. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;try {
  PreparedStatement preparedStatement &#x3D; connection.prepareStatement(
    &quot;SELECT * FROM NonExistentTable&quot;);
  preparedStatement.executeQuery();
} catch (SQLException e) {
  System.err.println(&quot;SQL Error: &quot; + e.getMessage());
  e.printStackTrace();
}&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Connect to database before performing CRUD operations&lt;/td&gt;
&lt;td&gt;In this code, we use several &#x27;String&#x27; connection parameters, the first being the &#x27;url,&#x27; which specifies the bookstore database&#x27;s location,then &#x27;user&#x27; and &#x27;password&#x27; strings, which are used to authenticate the user, establishing the database connection. Then, the &#x27;getConnection&#x27; method of the DriverManager class is used to create the connection and store it in a variable called &#x27;connection&#x27; for future use. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;Connection connection &#x3D; null;
try {
  String url &#x3D; &quot;jdbc:mysql://localhost:3306/bookstore&quot;;
  String user &#x3D; &quot;root&quot;;
  String password &#x3D; &quot;password&quot;;
  connection &#x3D; DriverManager.getConnection(url, user, password);
  System.out.println(&quot;Connected to the database successfully!&quot;);
} catch (SQLException e) {
  System.err.println(&quot;Connection failed: &quot; + e.getMessage());
  e.printStackTrace();
} &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Add a book to the inventory&lt;/td&gt;
&lt;td&gt;This is an example of adding a new book to the inventory by providing information about the book&#x27;s title, author, price, genre, publication date, and publisher. It uses a simple Statement object, which is easier to understand, but it&#x27;s vulnerable to SQL injection. In this code, the &#x27;try&#x27; block creates a simple statement. Then, the query is executed to insert a book into the Books table, with the specified values for the table columns. Further, &#x27;execute Update&#x27; inserts the new row into the database. The number of rows affected is then printed out and as usual, any exception that occurs is passed into the &#x27;catch&#x27; block. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;try (Statement statement &#x3D; connection.createStatement()) {
  String insertSQL &#x3D; &quot;INSERT INTO Books (Title, Author, Price, Genre, PublicationDate, PublisherID) &quot; +
            &quot;VALUES (&#x27;Advanced Java&#x27;, &#x27;Jane Doe&#x27;, 45.99, &#x27;Programming&#x27;, &#x27;2023-01-10&#x27;, 1)&quot;;
  int rowsAffected &#x3D; statement.executeUpdate(insertSQL);
  System.out.println(&quot;Rows inserted: &quot; + rowsAffected);
} catch (SQLException e) {
  System.err.println(&quot;Error inserting data: &quot; + e.getMessage());
  e.printStackTrace();
} &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Add a book to the inventory using a PreparedStatement object&lt;/td&gt;
&lt;td&gt; In this code, the &#x27;try&#x27; block creates a PreparedStatement object, using the &#x27;connection dot prepare Statement&#x27; method.Then, the query is executed to insert a book into the Books table, using parameters as dynamic values instead of hard-coded specific values. These parameters are set using the set String, set Double, set Date, and set Int methods. Then, the &#x27;execute Update&#x27; method on the &#x27;preparedStatement&#x27; object, inserts the new row into the database. The number of rows affected is then printed out, and any exception that occurs is passed into the &#x27;catch&#x27; block.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;try (PreparedStatement preparedStatement &#x3D; connection.prepareStatement(
  &quot;INSERT INTO Books (Title, Author, Price, Genre, PublicationDate, PublisherID) VALUES (?, ?, ?, ?, ?, ?)&quot;)) {
  preparedStatement.setString(1, &quot;Advanced Java&quot;);
  preparedStatement.setString(2, &quot;Jane Doe&quot;);
  preparedStatement.setDouble(3, 45.99);
  preparedStatement.setString(4, &quot;Programming&quot;);
  preparedStatement.setDate(5, java.sql.Date.valueOf(&quot;2023-01-10&quot;));
  preparedStatement.setInt(6, 1);
  int rowsAffected &#x3D; preparedStatement.executeUpdate();
  System.out.println(&quot;Rows inserted: &quot; + rowsAffected);
} catch (SQLException e) {
  System.err.println(&quot;Error inserting data: &quot; + e.getMessage());
  e.printStackTrace();
} &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Add new book using a stored procedure and a CallableStatement object&lt;/td&gt;
&lt;td&gt;In this code, the &#x27;try&#x27; block creates a CallableStatement object, using the &#x27;connection dot prepare Call&#x27; method. Then, the query is executed to insert a book into the Books table, using parameters as dynamic values instead of hard-coded specific values. These parameters are set using the set String, set Double, set Date, and set Int methods. Then, the &#x27;execute Update&#x27; method on the &#x27;callableStatement&#x27; object, inserts the new row into the database. Any exception that occurs is passed into the &#x27;catch&#x27; block. You can see that this CallableStatement is very similar to the PreparedStatement. The key difference is that CallableStatement is specifically designed to execute stored procedures, whereas PreparedStatement is used for executing parameterized SQL queries directly.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;CREATE PROCEDURE AddBook(
  IN bookTitle VARCHAR(255),
  IN bookAuthor VARCHAR(255),
  IN bookPrice DOUBLE,
  IN bookGenre VARCHAR(100),
  IN publicationDate DATE,
  IN publisherID INT
)
BEGIN
  INSERT INTO Books (Title, Author, Price, Genre, PublicationDate, PublisherID)
  VALUES (bookTitle, bookAuthor, bookPrice, bookGenre, publicationDate, publisherID);
END;
try (CallableStatement callableStatement &#x3D; connection.prepareCall(&quot;{CALL AddBook(?, ?, ?, ?, ?, ?)}&quot;)) {
  callableStatement.setString(1, &quot;Advanced Java&quot;);
  callableStatement.setString(2, &quot;Jane Doe&quot;);
  callableStatement.setDouble(3, 45.99);
  callableStatement.setString(4, &quot;Programming&quot;);
  callableStatement.setDate(5, java.sql.Date.valueOf(&quot;2023-01-10&quot;));
  callableStatement.setInt(6, 1);
  callableStatement.execute();
  System.out.println(&quot;Book added successfully using stored procedure.&quot;);
} catch (SQLException e) {
  System.err.println(&quot;Error calling stored procedure: &quot; + e.getMessage());
  e.printStackTrace();
} &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Retrieve all books using a simple Statement&lt;/td&gt;
&lt;td&gt;In this code, the statement query is executed using &#x27;SELECT asterisk FROM Books&#x27;, and the results are traversed and printed out. As before a &#x27;catch&#x27; block captures any exceptions that occur. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;try (Statement statement &#x3D; connection.createStatement();
   ResultSet resultSet &#x3D; statement.executeQuery(&quot;SELECT * FROM Books&quot;)) {
  while (resultSet.next()) {
    System.out.println(&quot;Book ID: &quot; + resultSet.getInt(&quot;BookID&quot;));
    System.out.println(&quot;Title: &quot; + resultSet.getString(&quot;Title&quot;));
    System.out.println(&quot;Author: &quot; + resultSet.getString(&quot;Author&quot;));
    System.out.println(&quot;Price: &quot; + resultSet.getDouble(&quot;Price&quot;));
  }
} catch (SQLException e) {
  System.err.println(&quot;Error retrieving data: &quot; + e.getMessage());
  e.printStackTrace();
} &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Retrieve all books of a specific genre using PreparedStatement&lt;/td&gt;
&lt;td&gt;This code creates and uses a PreparedStatement object using the &#x27;connection dot prepare Statement&#x27; method, and it retrieves all books from the &#x27;Programming&#x27; genre, by using &#x27;SELECT asterisk FROM Books&#x27; with the &#x27;WHERE Genre equals question mark&#x27; clause. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;try (PreparedStatement preparedStatement &#x3D; connection.prepareStatement(
  &quot;SELECT * FROM Books WHERE Genre &#x3D; ?&quot;)) {
  preparedStatement.setString(1, &quot;Programming&quot;);
  ResultSet resultSet &#x3D; preparedStatement.executeQuery();
  while (resultSet.next()) {
    System.out.println(&quot;Title: &quot; + resultSet.getString(&quot;Title&quot;));
    System.out.println(&quot;Price: &quot; + resultSet.getDouble(&quot;Price&quot;));
  }
} catch (SQLException e) {
  System.err.println(&quot;Error retrieving data: &quot; + e.getMessage());
  e.printStackTrace();
} &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Pagination example using PreparedStatement &lt;/td&gt;
&lt;td&gt;The query used in this code is &#x27;SELECT asterisk FROM Books&#x27; but it also specifies &#x27;ORDER BY Price&#x27; and in descending order with a maximum limit of only the top 5 most expensive books.It prints out the results and uses &#x27;try&#x27; and &#x27;catch&#x27; blocks for SQL exceptions. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;try (PreparedStatement preparedStatement &#x3D; connection.prepareStatement(
  &quot;SELECT * FROM Books ORDER BY Price DESC LIMIT 5 OFFSET 0&quot;)) {
  ResultSet resultSet &#x3D; preparedStatement.executeQuery();
  while (resultSet.next()) {
    System.out.println(&quot;Title: &quot; + resultSet.getString(&quot;Title&quot;));
    System.out.println(&quot;Price: &quot; + resultSet.getDouble(&quot;Price&quot;));
  }
} catch (SQLException e) {
  System.err.println(&quot;Error with pagination: &quot; + e.getMessage());
  e.printStackTrace();
}&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Change the price of a book using PreparedStatement&lt;/td&gt;
&lt;td&gt; In this code, the UPDATE command sets the new price and uses the WHERE clause to filter on the title. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;try (PreparedStatement preparedStatement &#x3D; connection.prepareStatement(
  &quot;UPDATE Books SET Price &#x3D; ? WHERE Title &#x3D; ?&quot;)) {
  preparedStatement.setDouble(1, 49.99);
  preparedStatement.setString(2, &quot;Advanced Java&quot;);
 int rowsUpdated &#x3D; preparedStatement.executeUpdate();
  System.out.println(&quot;Rows updated: &quot; + rowsUpdated);
} catch (SQLException e) {
  System.err.println(&quot;Error updating data: &quot; + e.getMessage());
  e.printStackTrace();
} &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Remove all books of a specific genre using PreparedStatement &lt;/td&gt;
&lt;td&gt;In this code, the DELETE command removes all the books of the &#x27;Programming&#x27; genre from the Books table by using the &#x27;WHERE Genre equals question mark&#x27; clause to filter on the genre and specifying the &#x27;Programming&#x27; genre with a set String method.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;try (PreparedStatement preparedStatement &#x3D; connection.prepareStatement(
  &quot;DELETE FROM Books WHERE Genre &#x3D; ?&quot;)) {
  preparedStatement.setString(1, &quot;Programming&quot;);
  int rowsDeleted &#x3D; preparedStatement.executeUpdate();
  System.out.println(&quot;Rows deleted: &quot; + rowsDeleted);
} catch (SQLException e) {
  System.err.println(&quot;Error deleting data: &quot; + e.getMessage());
  e.printStackTrace();
} &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Add the MySQL JDBC dependency to the pom.xml file&lt;/td&gt;
&lt;td&gt;
        The mysql-connector-java dependency is added to the pom.xml file with a scope of runtime. This dependency provides the Java API that enables Java applications to interact with MySQL databases using JDBC.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;
		&lt;dependencies&gt;
  &lt;!- - MySQL JDBC Driver --&gt;
  &lt;dependency&gt;
    &lt;groupId&gt;mysql&lt;/groupId&gt;
	&lt;artifactId&gt;mysql-connector-java&lt;/artifactId&gt;
    &lt;scope&gt;runtime&lt;/scope&gt;
  &lt;/dependency&gt;
&lt;/dependencies&gt; &#x60;
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Define the database connection properties &lt;/td&gt;
&lt;td&gt;
        Define the database connection properties in the application.properties file located in src/main/resources.



The application.properties file centralizes your application configuration.

spring.datasource.url specifies the database URL.

spring.datasource.username and spring.datasource.password define the credentials for database access.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;# Database connection properties only

spring.datasource.url&#x3D;jdbc&amp;colon;mysql://localhost:3306/bookstore

spring.datasource.username&#x3D;root

spring.datasource.password&#x3D;password

spring.datasource.driver-class-name&#x3D;com.mysql.cj.jdbc.Driver
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Customize and activate profiles for different environments&lt;/td&gt;
&lt;td&gt;
        Spring Boot supports multiple environment profiles (dev, prod, etc.) through application-{profile}.properties.

The spring.profiles.active setting determines which profile is currently in use, allowing different database configurations based on the execution environment.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;# application-dev.properties

spring.datasource.url&#x3D;jdbc&amp;colon;mysql://localhost:3306/bookstore_dev

#_application-prod.properties

spring.datasource.url&#x3D;jdbc&amp;colon;mysql://prod-server:3306/bookstore

#_Profile activation 

spring.profiles.active&#x3D;dev&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Set up logging&lt;/td&gt;
&lt;td&gt;
        Spring Boot logging is configured using logging.level properties. Log files can be stored using logging.file.name.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;logging.level.org.springframework&#x3D;INFO

logging.level.com.yourapp&#x3D;DEBUG

logging.file.name&#x3D;logs/app.log
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Securing sensitive data&lt;/td&gt;
&lt;td&gt;
        To secure credentials, environment variables (DB_USERNAME, DB_PASSWORD) should be used instead of hardcoding values in the application.properties file.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;spring.datasource.username&#x3D;${DB_USERNAME}

spring.datasource.password&#x3D;${DB_PASSWORD}

export DB_USERNAME&#x3D;root

export DB_PASSWORD&#x3D;securepassword
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Initialize the schema&lt;/td&gt;
&lt;td&gt;The schema.sql file defines the structure of tables in the database. When Spring Boot starts, it executes this script to create tables if they do not exist. The CREATE TABLE statement defines column names, data types, and constraints.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;CREATE TABLE Books (

id INT AUTO_INCREMENT PRIMARY KEY,

title VARCHAR(255),

author VARCHAR(255),

price DOUBLE

);
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Seed the database with initial data&lt;/td&gt;
&lt;td&gt; data.sql seeds the database with initial data. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;INSERT INTO Books (title, author, price) VALUES (&#x27;Spring Boot Essentials&#x27;, &#x27;Jane Doe&#x27;, 29.99);

Add some more values

INSERT INTO Books (title, author, price) VALUES

(&#x27;Mastering Hibernate&#x27;, &#x27;John Smith&#x27;, 39.99),

(&#x27;Java Persistence API Guide&#x27;, &#x27;Emily Davis&#x27;, 25.50);
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;List the databases&lt;/td&gt;
&lt;td&gt;The code creates a statement with an existing connection to a database. The statement is then used to execute the query &quot;Show databases&quot;. The result is stored in resultSet and then printed out to the console using a while loop. This is a simple way to ensure the code can connect to the database.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;try (Statement statement &#x3D; connection.createStatement();

   ResultSet resultSet &#x3D; statement.executeQuery(&quot;SHOW DATABASES&quot;)) {

  System.out.println(&quot;Available Databases:&quot;);

  while (resultSet.next()) {

    System.out.println(resultSet.getString(1));

  }

} catch (SQLException e) {

  System.err.println(\&quot;Error retrieving databases: \&quot; + e.getMessage());

  e.printStackTrace();

}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Connect to the database and list the tables&lt;/td&gt;
&lt;td&gt;
To list the tables, first create a connection to the database using the database URL, username, and password. The credentials should be stored securely and not hardcoded as shown here. We are doing this for simplicity&#x27;s sake. The code creates a statement with the query &quot;show tables&quot; and the result is stored in the variable resultSet. A while statement then loops over it and prints the tables to the console.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;try (Connection connection &#x3D; DriverManager.getConnection(

    &quot;jdbc&amp;colon;mysql://localhost:3306/bookstore&quot;, &quot;root&quot;, &quot;password&quot;);

   Statement statement &#x3D; connection.createStatement();

   ResultSet resultSet &#x3D; statement.executeQuery(&quot;SHOW TABLES&quot;)) {


  System.out.println(&quot;Tables in the database:&quot;);

  while (resultSet.next()) {

    System.out.println(resultSet.getString(1));

  }

} catch (SQLException e) {

  System.err.println(&quot;Error: &quot; + e.getMessage());

  e.printStackTrace();

}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Data health checks: Add the Spring Actuator dependency to your pom.xml.&lt;/td&gt;
&lt;td&gt;
        Adding the spring-boot-starter-actuator dependency enables application monitoring, including database health checks.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;&lt;dependency&gt;  

   &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;  

   &lt;artifactId&gt;spring-boot-starter-actuator&lt;/artifactId&gt;  

&lt;/dependency&gt;&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Data health check: Enable the database health endpoint&lt;/td&gt;
&lt;td&gt; The management.health.db.enabled setting allows Spring Boot&#x27;s Actuator to check the status of the database connection via a REST endpoint (/actuator/health/db).&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt; management.endpoint.health.show-details&#x3D;always

management.health.db.enabled&#x3D;true



 Output:



&quot;status&quot;: &quot;UP&quot;,

  &quot;components&quot;: {

    &quot;db&quot;: {

      &quot;status&quot;: &quot;UP&quot;,
      &quot;details&quot;: {

        &quot;database&quot;: &quot;MySQL&quot;,

        &quot;validationQuery&quot;: &quot;isValid()&quot;

      }

    }

  }

}

&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Setting up JPA in Spring Boot: Add dependencies to enable JPA in SpringBoot&lt;/td&gt;
&lt;td&gt;
      The spring-boot-starter-data-jpa dependency enables JPA (Java Persistence API), allowing ORM (Object-Relational Mapping) with MySQL databases.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;&lt;dependencies&gt;

    &lt;!-- Spring Boot Starter for JPA --&gt;

    &lt;dependency&gt;

        &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;

        &lt;artifactId&gt;spring-boot-starter-data-jpa&lt;/artifactId&gt;

    &lt;/dependency&gt;
    &lt;!-- MySQL JDBC Driver --&gt;

    &lt;dependency&gt;
        &lt;groupId&gt;mysql&lt;/groupId&gt;

        &lt;artifactId&gt;mysql-connector-java&lt;/artifactId&gt;

        &lt;scope&gt;runtime&lt;/scope&gt;

    &lt;/dependency&gt;

&lt;/dependencies&gt;
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Setting up JPA in Spring Boot: Configure application.properties&lt;/td&gt;
&lt;td&gt;
        Set the database and JPA configuration in src/main/resources/application.properties.

spring.jpa.hibernate. ddl-auto automatically manages the database schema, and the update part updates the schema based on your JPA entities.

So, if your database is missing some tables but your JPA has the right classes, those missing tables will be auto-created.

Other options for this setting would be create, validate, or none. 

spring.jpa.show-sql logs the generated SQL queries for debugging purposes.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;spring.datasource.url&#x3D;jdbc:mysql://localhost:3306/bookstore

spring.datasource.username&#x3D;root

spring.datasource.password&#x3D;password

spring.jpa.hibernate.ddl-auto&#x3D;update

spring.jpa.show-sql&#x3D;true&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Setting up JPA in Spring Boot: Define an entity&lt;/td&gt;
&lt;td&gt;An entity is a Java class mapped to a database table.

In this code, @Entity is an annotation that marks the class as a JPA entity mapped to a database table. 

@Id is an annotation that denotes the primary key of the entity.

@GeneratedValue is an annotation that specifies how the primary key is generated, such as AUTO or IDENTITY. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;@Entity

public class Book {

    @Id

    @GeneratedValue(strategy &#x3D; GenerationType.IDENTITY)  

    private Long id;

    private String title;

    private String author;

    private double price;


    // Getters and Setters

} &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Setting up JPA in Spring Boot: Create a repository&lt;/td&gt;
&lt;td&gt; In this code, JpaRepository is a built-in Spring Data JPA interface that provides methods like save, findAll, and deleteById.

Book,Long specifies the entity type, Book, and the type of its primary key, Long&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;@Repository public interface BookRepository extends (2) JpaRepository (3) &lt;Book,Long&gt;
		{
		}&lt;/pre&gt;
	&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Using JPA: Bookstore application example&lt;/td&gt;
&lt;td&gt;
In this code snippet, the &#x27;setTitle&#x27; method on the &#x27;book&#x27; object sets the title,
Similarly, the &#x27;setAuthor&#x27; method sets the author, and the &#x27;setPrice&#x27; method sets the price.

The \&#x27;save\&#x27; method of the bookRepository object saves the Book object to the database.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;@Component  

public class BookApp implements CommandLineRunner {  

    @Autowired  

    private BookRepository bookRepository;  


    @Override  

    public void run(String... args) {  

        Book book &#x3D; new Book();  

        book.setTitle(&quot;Spring Boot Essentials&quot;);  

        book.setAuthor(&quot;Jane Doe&quot;);  

        book.setPrice(19.99);  

        bookRepository.save(book);  


        System.out.println(&quot;Book saved successfully!&quot;);  

    }  

}  
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Apply Java core annotations to a JPA entity&lt;/td&gt;
&lt;td&gt; The NotNull annotation on the title ensures the title cannot be null. The same applies to the author attribute. The Size annotation restricts the title to a length between 2 and 100 characters. The Min annotation ensures the price is at least 1.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt; @Entity  

  public class Book {  


  @Id  

 private Long id;  


  @NotNull  

  @Size(min &#x3D; 2, max &#x3D; 100)  

  private String title;  


  @NotNull  

  private String author;  

  @Min(1)  

  private double price;  

  // Getters and Setters  

} &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Spring-specific validation options: Example&lt;/td&gt;
&lt;td&gt;First, import the required packages
The validator class is the core of Spring&#x27;s validation framework. It allows us to implement custom validation logic for any object.

The errors class is used to store and retrieve validation errors during validation processing.

The ValidationUtils class is used to automatically check for empty fields and adds errors if a field is blank or null.

The Implements Validator class implements the Validator interface, which requires defining two methods: supports and validate.

The Supports method takes in a class type as an input parameter and returns \&quot;true\&quot; only if the given class is Book.class.

The Validate method contains the validation rules. It first converts the target object into a Book and then checks if the price is less than 1. If true, it returns an error message stating that the price has to be greater than zero

The ValidationUtils class is used to check if the title is empty or contains only spaces. This ensures the caller does not send an empty title or blank string. 
		&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;import org.springframework.validation.Errors;
import org.springframework.validation.ValidationUtils;
import org.springframework.validation.Validator;
  public class BookValidator implements Validator {
  @Override
  public boolean supports(Class&amp;lt;?&amp;gt; clazz) {
    return Book.class.equals(clazz); // Ensures this validator applies only to Book objects.
  }
  @Override
  public void validate(Object target, Errors errors) {
    Book book &#x3D; (Book) target;
    // Ensures the price is greater than 0
    if (book.getPrice() &amp;lt; 1) {
      errors.rejectValue(&quot;price&quot;, &quot;price.invalid&quot;, &quot;Price must be greater than 0&quot;);
    }
    // Ensures the title is not empty
    ValidationUtils.rejectIfEmptyOrWhitespace(errors, &quot;title&quot;, &quot;title.empty&quot;, &quot;Title cannot be empty&quot;);
  }
}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Use the Validator in Spring Controllers: Validate user input dynamically&lt;/td&gt;
&lt;td&gt;The Validator interface can be integrated into Spring controllers to validate user input dynamically.

The Controller annotation marks this class as a Spring MVC controller, allowing it to handle HTTP requests.

The bookValidator object created previously manually validates Book objects before processing them. It calls the validate method from BookValidator to check if the Book object meets the defined constraints.

This controller ensures that any book added through the addBook endpoint is validated before processing, preventing invalid data from being stored or processed.

result.hasErrors checks if validation errors exist. If true, it returns \&quot;errorPage\&quot;, indicating validation failed. If false, it proceeds with normal processing and returns \&quot;successPage\&quot;.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;@Controller
public class BookController {
  private final BookValidator bookValidator &#x3D; new BookValidator();  

  @PostMapping(&quot;/addBook&quot;)

  public String addBook(@ModelAttribute Book book, BindingResult result) {

    bookValidator.validate(book, result); // Validate the book object.

    if (result.hasErrors()) {

      return &quot;errorPage&quot;; // Return an error page if validation fails.

    }

    // Process the book object if validation passes.

    return &quot;successPage&quot;;

  }

}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;The DataBinder class&lt;/td&gt;
&lt;td&gt;New DataBinder creates a DataBinder instance for the book object.

dataBinder.setValidator attaches the custom BookValidator to the DataBinder. This is the validator you created previously.

dataBinder.bind simulates binding input data, such as input from an HTTP request, to the book object.

dataBinder.validate executes runs the validation logic defined in the BookValidator.

BindingResult.getAllErrors retrieves all validation errors for further processing.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;Book book &#x3D; new Book(); // The target object.

DataBinder dataBinder &#x3D; new DataBinder(book);

// Set the custom validator.  

dataBinder.setValidator(new BookValidator());  

// Simulate binding input data.  

dataBinder.bind(new MutablePropertyValues(Map.of(&quot;title&quot;, &quot;&quot;, &quot;price&quot;, 0)));

// Validate the object.  

dataBinder.validate();  


// Retrieve validation errors.  

BindingResult result &#x3D; dataBinder.getBindingResult();  

if (result.hasErrors()) {  

  result.getAllErrors().forEach(System.out::println);  

} &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Handle validation in REST API: Global exception handler &lt;/td&gt;
&lt;td&gt;The ControllerAdvice annotation designates the class as a centralized exception handler.  

The ExceptionHandler annotation captures specific exceptions. In this case, it captures MethodArgumentNotValidException.  

MethodArgumentNotValidException is thrown when a request body fails validation. Whenever validation fails, this method gets called.  

The getFieldErrors method retrieves all validation errors from the exception.

The forEach statement loops through each validation error, extracts the field name and the error message, and adds them to the errors map.  

HttpStatus.BAD_REQUEST returns a 400 Bad Request status code for invalid requests.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;@ControllerAdvice  

public class GlobalExceptionHandler {  

  @ExceptionHandler(MethodArgumentNotValidException.class)  

  public ResponseEntity&lt;Map&lt;String, String&gt;&gt; handleValidationExceptions(MethodArgumentNotValidException ex) {  

    Map&lt;String, String&gt; errors &#x3D; new HashMap&lt;&gt;();  

    ex.getBindingResult().getFieldErrors().forEach(error -&gt;  

      errors.put(error.getField(), error.getDefaultMessage())  

    );

    return new ResponseEntity&lt;&gt;(errors, HttpStatus.BAD_REQUEST);  

  }

} &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Standardize API responses&lt;/td&gt;
&lt;td&gt;The ApiResponse class includes three key fields. The status field indicates whether the request was successful. The message field provides a short description of the outcome. The data field contains the actual response payload.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;public class ApiResponse&lt;T&gt; {  

    private String status;  

    private String message;  

    private T data;

    public ApiResponse(String status, String message, T data) {  

        this.status &#x3D; status;  

        this.message &#x3D; message;  

        this.data &#x3D; data;  

    } &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Modify the controller methods to use this structured response&lt;/td&gt;
&lt;td&gt;The controller method modifies API responses to follow this structure. If a book is found, the API returns a successful response. If not, it returns a structured error response. This approach ensures consistency and improves front-end handling.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;@GetMapping(&quot;/{id}&quot;)  

public ResponseEntity&lt;ApiResponse&lt;Book&gt;&gt; getBookById(@PathVariable Long id) {  

    return bookRepository.findById(id)  

            .map(book -&gt; ResponseEntity.ok(new ApiResponse&lt;&gt;(&quot;success&quot;, &quot;Book found&quot;, book)))  

            .orElseGet(() -&gt; ResponseEntity.status(HttpStatus.NOT_FOUND)  

                    .body(new ApiResponse&lt;&gt;(&quot;error&quot;, &quot;Book not found&quot;, null)));  

} &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Return proper status codes&lt;/td&gt;
&lt;td&gt;This example shows how to return a 201 status when adding a new book.

The ResponseEntity.status(HttpStatus.CREATED) method sets the status code, and the ApiResponse object structures the response.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;@PostMapping  

public ResponseEntity&lt;ApiResponse&lt;Book&gt;&gt; createBook(@Valid @RequestBody Book book) {  

    Book savedBook &#x3D; bookRepository.save(book);  

    return ResponseEntity.status(HttpStatus.CREATED)  

            .body(new ApiResponse&lt;&gt;(&quot;success&quot;, &quot;Book created successfully&quot;, savedBook));  

} &lt;/pre&gt;
		&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Retrieve all books using a simple Statement&lt;/td&gt;
&lt;td&gt;In this code, the statement query is executed using &#x27;SELECT asterisk FROM Books&#x27;, and the results are traversed and printed out. As before a &#x27;catch&#x27; block captures any exceptions that occur.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;try (Statement statement &#x3D; connection.createStatement();
   ResultSet resultSet &#x3D; statement.executeQuery(&quot;SELECT * FROM Books&quot;)) {
  while (resultSet.next()) {
    System.out.println(&quot;Book ID: &quot; + resultSet.getInt(&quot;BookID&quot;));
    System.out.println(&quot;Title: &quot; + resultSet.getString(&quot;Title&quot;));
    System.out.println(&quot;Author: &quot; + resultSet.getString(&quot;Author&quot;));
    System.out.println(&quot;Price: &quot; + resultSet.getDouble(&quot;Price&quot;));
  }
} catch (SQLException e) {
  System.err.println(&quot;Error retrieving data: &quot; + e.getMessage());
  e.printStackTrace();
}&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Implement Pagination for Large Datasets&lt;/td&gt;
&lt;td&gt;Use pagination to limit the number of records in API responses.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;@GetMapping(&quot;/paged&quot;)  

public Page&lt;Book&gt; getPagedBooks(Pageable pageable) {  

    return bookRepository.findAll(pageable);  

} &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Pagination query example&lt;/td&gt;
&lt;td&gt;In this code snippet, the endpoint is &#x27;forward slash paged&#x27;.

When somebody makes a call to this endpoint, they can pass in certain parameters. In this example, we are passing in page zero, which is the first page, we are passing in a size of 5, so we only want 5 books returned in the response, and we want the results sorted by title in ascending order.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;GET /books/paged?page&#x3D;0&amp;size&#x3D;5&amp;sort&#x3D;title,asc &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Enable SQL query logging&lt;/td&gt;
&lt;td&gt; To see SQL queries executed by JPA, add this to application.properties.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;spring.jpa.show-sql&#x3D;true &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Add logging in controllers&lt;/td&gt;
&lt;td&gt;In this code snippet, the import command imports the logger, the &#x27;Logger factory&#x27; class is used with &#x27;get Logger&#x27; to create the logger instance, and &#x27;logger.info&#x27; is used to log the fetched information.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;import org.slf4j.Logger;  

import org.slf4j.LoggerFactory;  

@RestController  

@RequestMapping(&quot;/books&quot;)  

public class BookController {  

    private static final Logger logger &#x3D; LoggerFactory.getLogger(BookController.class);  


    @GetMapping  

    public List&lt;Book&gt; getAllBooks() {  

        logger.info(&quot;Fetching all books from database.&quot;);  

        return bookRepository.findAll();  

    }

} &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Curl command: POST request&lt;/td&gt;
&lt;td&gt;In this code snippet, curl is using the POST method, the \&#x27;dash H\&#x27; flag sets the header, the content type is specified, the dash d flag is used to pass the data, and the URL is the endpoint that is being created.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;curl -X POST -H &quot;Content-Type: application/json&quot; -d &#x27;{  

    &quot;title&quot;: &quot;Spring Boot Guide&quot;,  

    &quot;author&quot;: &quot;John Doe&quot;,  

    &quot;price&quot;: 20.99,  

    &quot;genre&quot;: &quot;Programming&quot;,  

    &quot;publicationDate&quot;: &quot;2025-03-15&quot;  

}&#x27; http://localhost:8080/books &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Curl command: GET request&lt;/td&gt;
&lt;td&gt;The code fetches all books from the database. A GET request is used to retrieve all books from the database. The API returns a list of books in JSON format.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;curl -X GET http://localhost:8080/books   &lt;/pre&gt;
&lt;/td&gt;
    &lt;tr&gt;
&lt;td&gt;Hibernate annotations&lt;/td&gt;
&lt;td&gt;This is a basic Hibernate entity class for a Book. The annotations define how this Java class maps to a database table.

The @Entity annotation marks this class as a Hibernate entity, meaning it is mapped to a database table. The @Table(name &#x3D; \&quot;books\&quot;) annotation specifies the exact table name used in the database.

The @Id annotation marks the id field as the primary key.

The @GeneratedValue(strategy &#x3D; GenerationType.IDENTITY) annotation configures Hibernate to generate a unique ID automatically.

The @Column annotation maps Java fields to database columns. The title column has constraints such as nullable &#x3D; false, ensuring it cannot be empty, and length &#x3D; 100, which limits the character length. The price column is also set to nullable &#x3D; false to prevent missing values.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;import jakarta.persistence.*;

@Entity
@Table(name &#x3D; &quot;books&quot;)
public class Book {
  @Id
  @GeneratedValue(strategy &#x3D; GenerationType.IDENTITY)
  private Long id;

  @Column(name &#x3D; &quot;title&quot;, nullable &#x3D; false, length &#x3D; 100)
  private String title;

  @Column(name &#x3D; &quot;price&quot;, nullable &#x3D; false)
  private double price;

  // Getters and setters
}&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;@Transient annotation in Hibernate&lt;/td&gt;
&lt;td&gt;The @Transient annotation prevents a field from being persisted in the database. It&#x27;s useful for calculated fields or fields used only in business logic. The @Transient field, discountedPrice, is excluded from the database schema, even though it exists in the entity class.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;@Entity
public class Product {
  @Id
  @GeneratedValue(strategy &#x3D; GenerationType.IDENTITY)
  private Long id;

  private String name;

  @Transient
  private double discountedPrice; // This will not be stored in the database.

  // Getters and setters
}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;@Enumerate annotation in Hibernate&lt;/td&gt;
&lt;td&gt;The @Enumerated annotation maps Java enum types to database values.

The at Enumerated (EnumType dot STRING) part maps the enum as strings such as AVAILABLE or OUT_OF_STOCK. 
 &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt; public enum ProductStatus {
  AVAILABLE, OUT_OF_STOCK, DISCONTINUED
}

@Entity
public class Product {
  @Id
  @GeneratedValue(strategy &#x3D; GenerationType.IDENTITY)
  private Long id;

  @Enumerated(EnumType.STRING)
  private ProductStatus status;

  // Getters and setters
}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;@Lob annotation in Hibernate&lt;/td&gt;
&lt;td&gt;The @Lob annotation indicates that a field should be stored as a large object, such as a Character Large Object (CLOB) or a Binary Large Object (or BLOB).&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;@Entity
public class Article {
  @Id
  @GeneratedValue(strategy &#x3D; GenerationType.IDENTITY)
  private Long id;

  @Lob
  private String content; // Stores large text data.

  // Getters and setters
}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;@Temporal annotation in Hibernate&lt;/td&gt;
&lt;td&gt;
The @ Temporal annotation maps date and time values to corresponding column types in the database. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;@Temporal(TemporalType.TIMESTAMP)
  private Date eventDate;

  // Getters and setters
}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;One-to-one relationship&lt;/td&gt;
&lt;td&gt;A one-to-one relationship maps one entity to another single entity. For example, a User can have a single associated Profile.

@Entity marks the class as a Hibernate entity.

@OneToOne defines the one-to-one relationship.

@JoinColumn specifies the foreign key in the User table that references the Profile table.

CascadeType.ALL propagates operations (such as save and delete) on a User entity to a Profile entity.
&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;public class User {
  @Id
  @GeneratedValue(strategy &#x3D; GenerationType.IDENTITY)
  private Long id;

  @OneToOne(cascade &#x3D; CascadeType.ALL)
  @JoinColumn(name &#x3D; &quot;profile_id&quot;, referencedColumnName &#x3D; &quot;id&quot;)
  private Profile profile;

  // Getters and setters
}

@Entity
public class Profile {
  @Id
  @GeneratedValue(strategy &#x3D; GenerationType.IDENTITY)
  private Long id;

  private String address;
  private String phoneNumber;

  // Getters and setters
}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;One-to-many and many-to-one relationships&lt;/td&gt;
&lt;td&gt; A One-to-Many relationship links one entity to multiple other entities, and a many-to-One relationship does the reverse.

For example, a customer can have many Orders, as seen in this code snippet.

The at OneToMany(mappedBy &#x3D; \&quot;customer\&quot;) part links the Customer entity to its associated Order entities.

CascadeType.ALL saves or deletes Orders when the parent Customer is saved or deleted.

FetchType.LAZY Orders are fetched only when explicitly accessed.

@ManyToOne specifies the reverse relationship from Order to Customer.

@OneToMany(mappedBy &#x3D; \&quot;customer\&quot;) is placed in the Customer class to represent that one customer has many orders.

@ManyToOne in the Order class tells Hibernate that each order belongs to one customer.
 &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;@Entity
public class Customer {
  @Id
  @GeneratedValue(strategy &#x3D; GenerationType.IDENTITY)
  private Long id;

  @OneToMany(mappedBy &#x3D; &quot;customer&quot;, cascade &#x3D; CascadeType.ALL, fetch &#x3D; FetchType.LAZY)
  private List &lt;Order&gt; orders;

  // Getters and setters
}

@Entity
public class Order {
  @Id
  @GeneratedValue(strategy &#x3D; GenerationType.IDENTITY)
  private Long id;

  @ManyToOne
  @JoinColumn(name &#x3D; &quot;customer_id&quot;, nullable &#x3D; false)
  private Customer customer;

  private String product;
  private double price;

  // Getters and setters
}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Many-to-many relationship&lt;/td&gt;
&lt;td&gt;A many-to-many relationship allows multiple entities to map to multiple other entities.

For example, a student can enroll in multiple Courses, and each Course can have multiple Students.

@ManyToMany establishes a many-to-many relationship between Student and Course.

@JoinTable specifies the join table student_course for the relationship.

joinColumns and inverseJoinColumns: define foreign keys for Student and Course tables.

Lastly, mappedBy indicates that Student owns the relationship.
&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;@Entity
public class Student {
  @Id
  @GeneratedValue(strategy &#x3D; GenerationType.IDENTITY)
  private Long id;

  @ManyToMany
  @JoinTable(
    name &#x3D; &quot;student_course&quot;,
    joinColumns &#x3D; @JoinColumn(name &#x3D; &quot;student_id&quot;),
    inverseJoinColumns &#x3D; @JoinColumn(name &#x3D; &quot;course_id&quot;)
  )
  private List&lt;Course&gt; courses;

  // Getters and setters
}

@Entity
public class Course {
  @Id
  @GeneratedValue(strategy &#x3D; GenerationType.IDENTITY)
  private Long id;

  @ManyToMany(mappedBy &#x3D; &quot;courses&quot;)
  private List&lt;Student&gt; students;

  // Getters and setters
}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Cascading&lt;/td&gt;
&lt;td&gt;Operations on the Library parent entity would propagate down to the child &#x27;Book&#x27; entity.

When you call entityManager.persist(library), it automatically persists all associated books. Without this, you&#x27;d have to manually persist() each book before saving the library.
&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;@Entity
public class Library {
  @Id
  @GeneratedValue(strategy &#x3D; GenerationType.IDENTITY)
  private Long id;

  @OneToMany(cascade &#x3D; CascadeType.PERSIST)
  private List&lt;Book&gt; books;

  // Getters and setters
}

@Entity
public class Book {
  @Id
  @GeneratedValue(strategy &#x3D; GenerationType.IDENTITY)
  private Long id;

  private String title;

  // Getters and setters
}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Fetch strategy: Lazy loading&lt;/td&gt;
&lt;td&gt;FetchType.LAZY part ensures performance by loading orders only when accessed explicitly.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;@OneToMany(mappedBy &#x3D; &quot;customer&quot;, fetch &#x3D; FetchType.LAZY)
private List&lt;Order&gt; orders;
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Fetch strategy: Eager loading&lt;/td&gt;
&lt;td&gt; @OneToMany specifies a one-to-many relationship. mappedBy &#x3D; &#x27;customer&#x27; indicates that the customer field in the Order entity owns the relationship. Finally, fetch &#x3D; FetchType.EAGER configures JPA to load the associated Order entities immediately whenever a Customer entity is fetched.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt; @OneToMany(mappedBy &#x3D; &quot;customer&quot;, fetch &#x3D; FetchType.EAGER)
private List&lt;Order&gt; orders;
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Run native SQL queries in Hibernate&lt;/td&gt;
&lt;td&gt;In this example code snippet, the @PersistenceContext annotation injects an instance of the Entity Manager.

Hibernate allows native SQL queries to run inside a Spring Boot application using the Entity Manager.

 The createNativeQuery method is used to run a raw SQL statement directly in Hibernate.

The setParameter method prevents SQL injection by setting a parameterized value instead of directly embedding variables into the query. 

The getResultList method retrieves the results from the query processing as a list of objects.
&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;@PersistenceContext
private EntityManager entityManager;

public List&lt;Object[]&gt; getBooksByPrice(double price) {
  String sql &#x3D; &quot;SELECT title, price FROM books WHERE price &gt; ?&quot;;
  Query query &#x3D; entityManager.createNativeQuery(sql);
  query.setParameter(1, price);
  return query.getResultList();
}

&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Basic HQL query&lt;/td&gt;
&lt;td&gt;In this code, the FROM Book clause instructs Hibernate to retrieve data from the Book entity instead of directly querying the database table.

The b.price condition filters books where the price is greater than the specified value.

The setParameter method prevents SQL injection by ensuring safe input handling.

And the getResultList method retrieves the results as a list of Java objects rather than raw database records.
&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;@PersistenceContext
private EntityManager entityManager;

public List&lt;Book&gt; getBooksAbovePrice(double price) {
  String hql &#x3D; &quot;FROM Book b WHERE b.price &gt; :price&quot;;
  Query query &#x3D; entityManager.createQuery(hql, Book.class);
  query.setParameter(&quot;price&quot;, price);
  return query.getResultList();
}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Using HQL in a Spring Boot application&lt;/td&gt;
&lt;td&gt;In this code example, the @Repository annotation marks this as a Spring Data repository, allowing automatic running of queries.

The @Query(&quot;FROM Book b WHERE b.price &gt; :price&quot;) annotation defines an HQL query to fetch expensive books.

And the @Param price annotation maps the method argument to the query parameter dynamically.
&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;@Repository
public interface BookRepository extends JpaRepository&lt;Book, Long&gt; {
  @Query(&quot;FROM Book b WHERE b.price &gt; :price&quot;)
  List&lt;Book&gt; findExpensiveBooks(@Param(&quot;price&quot;) double price);
}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Example data structure in MongoDB&lt;/td&gt;
&lt;td&gt; Each product can have different fields, making the database highly adaptable. Developers can add fields to this document on an ad-hoc basis as there is no strict schema to restrict that.

Unlike SQL, there\&#x27;s no strict schema definition that forces every document in a collection to have the same fields. It is great for dynamic or evolving applications like product catalogs or content management systems.
&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;{
  &quot;product_id&quot;: &quot;A123&quot;,
  &quot;name&quot;: &quot;Wireless Mouse&quot;,
  &quot;category&quot;: &quot;Electronics&quot;,
  &quot;price&quot;: 29.99,
  &quot;stock&quot;: 100,
  &quot;specs&quot;: {
    &quot;brand&quot;: &quot;Logitech&quot;,
    &quot;connectivity&quot;: &quot;Bluetooth&quot;,
    &quot;battery_life&quot;: &quot;12 months&quot;
  }
}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;MongoDB CRUD operations: Insert data into a collection&lt;/td&gt;
&lt;td&gt;This code adds a new document or record to the products collection by using the &quot;insertOne&quot; method on the products collection.

Here, products is a collection that holds product documents.

If products does not already exist, MongoDB automatically creates it when the first document is inserted.

Each document in the collection represents an individual product, with fields such as product_id, name, price, and so on.
&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;db.products.insertOne({
  &quot;product_id&quot;: &quot;A123&quot;,
  &quot;name&quot;: &quot;Wireless Mouse&quot;,
  &quot;category&quot;: &quot;Electronics&quot;,
  &quot;price&quot;: 29.99,
  &quot;stock&quot;: 100
})
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;MongoDB CRUD operations: Retrieve all the documents in a collection&lt;/td&gt;
&lt;td&gt;This code retrieves all the documents from the products collection using the find method.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt; db.products.find({})&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;MongoDB CRUD operations: Retrieve a specific product by product_id&lt;/td&gt;
&lt;td&gt;findOne retrieves only one document representing a specific product with the specified product Id. The findOne method returns the first matching document.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;db.products.findOne({ &quot;product_id&quot;: &quot;A123&quot; })
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;MongoDB CRUD operations: Update data in a collection&lt;/td&gt;
&lt;td&gt;This code updates the stock value for a specific product.

The code modifies an existing document in the products collection using the updateOne method.

The first parameter, \&quot;product_id\&quot; specifies which document to update.

The second parameter, dollar-set, updates the stock field to 75. The dollar-set method ensures that only the specified field is modified without affecting the rest of the document.
&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;db.products.updateOne(
  { &quot;product_id&quot;: &quot;A123&quot; }, 
  { $set: { &quot;stock&quot;: 75 } } 
)
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;MongoDB CRUD operations: Delete a product&lt;/td&gt;
&lt;td&gt;Let&#x27;s say you want to delete one product by product ID. deleteOne deletes only one record where product_id is equal to A123.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;db.products.deleteOne({ &quot;product_id&quot;: &quot;A123&quot; }) &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;MongoDB CRUD operations: Delete all product&lt;/td&gt;
&lt;td&gt;To delete all the products in a category, use the deleteMany method.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;db.products.deleteMany({ &quot;category&quot;: &quot;Electronics&quot; })  &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;InfluxDB example data structure&lt;/td&gt;
&lt;td&gt;Here is an example data structure in InfluxDB, which is a time series database. Each data point has a timestamp. It records when the data was collected, making it easy to track historical changes and retrieve time-based trends. The time format used in this time series database entry follows the ISO 8601 standard for timestamps.

 InfluxDB organizes data into measurements, tags, and fields.

In this case, the measurement is temperature.

The tags include location and sensor_id, which help categorize data.

The field value holds the temperature reading.
 &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;{
  &quot;measurement&quot;: &quot;temperature&quot;,
  &quot;tags&quot;: {
    &quot;location&quot;: &quot;New York&quot;,
    &quot;sensor_id&quot;: &quot;sensor-001&quot;
  },
  &quot;fields&quot;: {
    &quot;value&quot;: 23.5
  },
  &quot;timestamp&quot;: &quot;2025-03-10T10:00:00Z&quot;
}
 &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;InfluxDB CRUD operations: Insert a data point&lt;/td&gt;
&lt;td&gt; This query inserts a new temperature into the database.

INSERT temperature specifies the measurement, similar to a table in SQL.
location is a tag indicating the location of the temperature sensor. Tags are indexed for fast querying.

sensor_id is another tag identifying the specific sensor that recorded the data.
Value is the field storing the actual recorded temperature.

If no timestamp is provided, InfluxDB automatically assigns the current time.
&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;INSERT temperature,location&#x3D;NYC sensor_id&#x3D;&quot;sensor-001&quot; value&#x3D;23.5  &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;InfluxDB CRUD operations: Delete old data&lt;/td&gt;
&lt;td&gt;This query retrieves all temperature readings from the past hour.

SELECT with the asterisks retrieves all fields and tags from the temperature measurement.

FROM temperature specifies the measurement similar to a table in relational databases.

The WHERE condition filters data to return only records from the last 1 hour.

And \&quot;now\&quot; represents the current timestamp.
&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;SELECT * FROM temperature WHERE time &gt; now(): 1h&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;InfluxDB CRUD operations: Retrieve data from a time range&lt;/td&gt;
&lt;td&gt;This query deletes all records older than 30 days.

DELETE FROM temperature deletes records from the temperature measurement.

The WHERE condition deletes only records older than 30 days.

And \&quot;now\&quot; represents the timestamp of 30 days ago.
&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;DELETE FROM temperature WHERE time &lt; now(): 30d  &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Neo4J graph data structure&lt;/td&gt;
&lt;td&gt;This example represents a social media network where a user follows another user and likes a post.

User-name-Alice and user-name-Bob are nodes representing users called Alice and Bob.

FOLLOWS is an edge or relationship showing that Alice follows Bob.

LIKES represents Alice liking a Post.
&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;(:User {name: &quot;Alice&quot;})-[:FOLLOWS]-&gt;(:User {name: &quot;Bob&quot;})
(:User {name: &quot;Alice&quot;})-[:LIKES]-&gt;(:Post {title: &quot;Graph Databases are awesome!&quot;})
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Cypher syntax &lt;/td&gt;
&lt;td&gt;Cypher uses ASCII-art-like syntax to visually represent relationships.

Nodes are enclosed in parentheses. For example, \&quot;a colon user\&quot; in parentheses represents a user node.

Relationships are enclosed in brackets. For example, \&quot;colon FOLLOWS\&quot; in brackets represents a FOLLOWS relationship.

Arrows indicate direction in relationships.
&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;MATCH (a:User)-[:FOLLOWS]-&gt;(b:User)
RETURN a, b
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Neo4j CRUD operations: Create nodes and relationships&lt;/td&gt;
&lt;td&gt; This code creates users and defines a FOLLOWS relationship.

The CREATE command creates two User nodes with property names equal to \&quot;Alice\&quot; and \&quot;Bob.\&quot;

Further, it establishes a FOLLOWS relationship between Alice and Bob.
&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;CREATE (a:User {name: &quot;Alice&quot;})
CREATE (b:User {name: &quot;Bob&quot;})
CREATE (a)-[:FOLLOWS]-&gt;(b)
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Neo4j CRUD operations: Retrieve data &lt;/td&gt;
&lt;td&gt;This code helps find all users that Alice follows.

The RETURN command retrieves the names of those users.
&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;MATCH (a:User {name: &quot;Alice&quot;})-[:FOLLOWS]-&gt;(b)
RETURN b.name
 &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Neo4j CRUD operations: Updates the data&lt;/td&gt;
&lt;td&gt;This code updates the data by adding new relationships.

It adds a LIKES relationship between Alice and a post.

The MATCH command finds the user Alice and the post.

Then, the CREATE command adds the LIKES relationship

&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;MATCH (a:User {name: &quot;Alice&quot;}), (p:Post {title: &quot;Graph Databases are awesome!&quot;})
CREATE (a)-[:LIKES]-&gt;(p)
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Neo4j CRUD operations: Delete the data&lt;/td&gt;
&lt;td&gt;This code removes the FOLLOWS relationship.

The MATCH command finds the FOLLOWS relationship.

The DELETE command removes it.
&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;MATCH (a:User {name: &quot;Alice&quot;})-[r:FOLLOWS]-&gt;(b:User {name: &quot;Bob&quot;})
DELETE r
 &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Configure MongoDB in Spring Boot&lt;/td&gt;
&lt;td&gt;To connect a Spring Boot application with MongoDB, we need to define the database connection properties in the application.properties file.

This configuration sets the database name to \&quot;ecommerce\&quot; and connects to a locally running MongoDB instance.
&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;spring.data.mongodb.uri&#x3D;mongodb://localhost:27017/ecommerce
spring.data.mongodb.database&#x3D;ecommerce
 &lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;MongoDB: Defining the entity class&lt;/td&gt;
&lt;td&gt;This code defines a Product entity representing an e-commerce product.

Note that MongoDB stores data as documents in collections. The Document annotation marks this class as a MongoDB collection. The Id annotation designates id as the primary key. The other fields define the product attributes.
&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;import org.springframework.data.annotation.Id;
import org.springframework.data.mongodb.core.mapping.Document;

@Document(collection &#x3D; &quot;products&quot;)
public class Product {
 @Id
 private String id;
 private String name;
 private String category;
 private double price;
 private int stock;

 // Constructors, Getters, and Setters
}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;MongoDB repository setup&lt;/td&gt;
&lt;td&gt;By extending MongoRepository, ProductRepository automatically inherits a set of pre-built methods for interacting with the MongoDB database.

The findBy prefix tells Spring Data MongoDB that this method should perform a query. Category is the property of the Product class that will be used in the query. Spring Data MongoDB will parse the method name and look for a field named category inside of the Product document. The same methods are also made available for the other attributes like findByName and findByPrice.

&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;import org.springframework.data.mongodb.repository.MongoRepository;
import java.util.List;

public interface ProductRepository extends MongoRepository&lt;Product, String&gt; {
 List&lt;Product&gt; findByCategory(String category);
}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;MongoDB CRUD operations: Create a new product&lt;/td&gt;
&lt;td&gt;This code creates a new product with the name, &quot;Wireless Mouse,&quot; category of electronics, price of 29.99 and stock of 100. The save method saves the product into the database. &lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;Product product &#x3D; new Product(&quot;Wireless Mouse&quot;, &quot;Electronics&quot;, 29.99, 100);
productRepository.save(product);
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;MongoDB CRUD operations: Reads products by category&lt;/td&gt;
&lt;td&gt;This code reads products by category. The findByCategory method automatically searches for the text &quot;Electronics&quot; in the category attribute of the mongodb document.&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;List&lt;Product&gt; electronics &#x3D; productRepository.findByCategory(\&quot;Electronics&quot;);
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;MongoDB CRUD operations: Updates the product price&lt;/td&gt;
&lt;td&gt;This code updates the product price. The setPrice method sets the price of the product to the given value. Other examples are example setCategory and setStock can be used to set the category and stock of the product.

The save method is then used to update the product in the database.
&lt;/td&gt;
&lt;td&gt;
&lt;pre&gt;product.setPrice(24.99);
productRepository.save(product);
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;MongoDB CRUD operations: Deletes the product&lt;/td&gt;
&lt;td&gt;This code deletes a product. The deleteById method takes the id of the product as input and deletes that product from the collection.
&lt;/td&gt;
&lt;td&gt;&lt;pre&gt;productRepository.deleteById(product.getId());
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Configure InfluxDB in Spring Boot&lt;/td&gt;
&lt;td&gt;To configure InfluxDB in Spring Boot, InfluxDB connection details are defined in application.properties.

The Spring.influx.url property defines the URL of your InfluxDB instance.

The Spring.influx.token is your InfluxDB authentication token.

The spring.influx.org specifies the InfluxDB organization you want to connect to.

The Spring.influx.bucket property defines the InfluxDB bucket, where your application will write and read data.
&lt;/td&gt;
&lt;td&gt;&lt;pre&gt;spring.influx.url&#x3D;http://localhost:8086
spring.influx.token&#x3D;your-token
spring.influx.org&#x3D;your-org
spring.influx.bucket&#x3D;sensor_data
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;InfluxDB: Define the entity&lt;/td&gt;
&lt;td&gt;This code defines the SensorData entity.

This import has an InfluxMeasurement annotation. This annotation is used at the class level to specify the name of the InfluxDB measurement, like a table that the Java class represents.
&lt;/td&gt;
&lt;td&gt;&lt;pre&gt;import org.springframework.data.annotation.Id;
import org.springframework.data.influxdb.mapping.InfluxMeasurement;

@InfluxMeasurement(name &#x3D; &quot;sensor_data&quot;)
public class SensorData {
 @Id
 private String id;
 private String sensorId;
 private double temperature;
 private long timestamp;

 // Constructors, Getters, and Setters
}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;InfluxDB repository setup&lt;/td&gt;
&lt;td&gt;This code creates an InfluxDBClient instance using the provided URL and token. This client is used to interact with the InfluxDB server. The token is converted to a character array as required by the library.
&lt;/td&gt;
&lt;td&gt;&lt;pre&gt;import com.influxdb.client.InfluxDBClient;
import com.influxdb.client.InfluxDBClientFactory;
import com.influxdb.client.WriteApi;

public class InfluxDBService {

 private InfluxDBClient client &#x3D; InfluxDBClientFactory.create(url, token.toCharArray());
}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;InfluxDB CRUD operations: Insert a data point&lt;/td&gt;
&lt;td&gt;The code creates a new record of SensorData. The saveSensorData method is used to save this data point into the InfluxDB database.
&lt;/td&gt;
&lt;td&gt;&lt;pre&gt;SensorData sensorData &#x3D; new SensorData(&quot;sensor-001&quot;, 22.5, System.currentTimeMillis());
influxDBService.saveSensorData(sensorData);
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;InfluxDB CRUD operations: Query data from the last 1 hour&lt;/td&gt;
&lt;td&gt;This query simply selects data from the last hour from the database
&lt;/td&gt;
&lt;td&gt;&lt;pre&gt;SELECT * FROM sensor_data WHERE time &gt; now() - 1h 
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;InfluxDB CRUD operations: Delete old data&lt;/td&gt;
&lt;td&gt;This code deletes old data, in this case, data older than 30 days.

Now - 30d is 30 days before today. The query removes all data previous to 30 days. 
&lt;/td&gt;
&lt;td&gt;&lt;pre&gt;DELETE FROM sensor_data WHERE time &lt; now() - 30d
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Configure Neo4j in Spring Boot&lt;/td&gt;
&lt;td&gt;Neo4j connection details go into application.properties.

Uri is the unique URL for the database. Username is the username of an authorized user. The password is the password for this particular user.
&lt;/td&gt;
&lt;td&gt;&lt;pre&gt;spring.neo4j.uri&#x3D;bolt://localhost:7687
spring.neo4j.authentication.username&#x3D;neo4j
spring.neo4j.authentication.password&#x3D;yourpassword
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Neo4j: Define the user entity&lt;/td&gt;
&lt;td&gt;The Node annotation represents a Neo4j node. A user is denoted as a node. The Relationship annotation models user relationships between nodes. The OUTGOING direction means the current user has friends. The list of friends is captured in the &#x27;friends&#x27; variable.
&lt;/td&gt;
&lt;td&gt;&lt;pre&gt;import org.springframework.data.neo4j.core.schema.*;

@Node
public class User {
 @Id @GeneratedValue
 private Long id;
 private String name;

 @Relationship(type &#x3D; &quot;FRIENDS_WITH&quot;, direction &#x3D; Relationship.Direction.OUTGOING)
 private List&lt;User&gt; friends;

 // Constructors, Getters, and Setters
}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Neo4j repository setup&lt;/td&gt;
&lt;td&gt;This code defines a UserRepository interface, which provides a way to interact with user entities stored in a Neo4j graph database. It extends Spring Data Neo4j&#x27;s Neo4jRepository, inheriting standard database operations like saving, retrieving, and deleting users. Finally, it adds a custom method, findByName, which enables searching for users by their name.
&lt;/td&gt;
&lt;td&gt;&lt;pre&gt;import org.springframework.data.neo4j.repository.Neo4jRepository; public interface UserRepository extends Neo4jRepository&lt;User, Long&gt; {
 User findByName(String name);
}
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Neo4j CRUD operations: Create a user node&lt;/td&gt;
&lt;td&gt;This code creates a new User and saves it to the database.
&lt;/td&gt;
&lt;td&gt;&lt;pre&gt;User alice &#x3D; new User(&quot;Alice&quot;);
userRepository.save(alice);
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Neo4j CRUD operations: Retrieve a user by name&lt;/td&gt;
&lt;td&gt;The code simply searches the data for users called &quot;Alice&quot;.
&lt;/td&gt;
&lt;td&gt;&lt;pre&gt;User user &#x3D; userRepository.findByName(&quot;Alice&quot;);
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;Neo4j CRUD operations: Establish a relationship&lt;/td&gt;
&lt;td&gt;This code creates a new user called &quot;Bob&quot;. It then adds Bob as a friend to Alice and saves this relationship to the database.
&lt;/td&gt;
&lt;td&gt;&lt;pre&gt;User bob &#x3D; new User(&quot;Bob&quot;);
alice.getFriends().add(bob);
userRepository.save(alice);
&lt;/pre&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;/tbody&gt;
&lt;/table&gt;

&lt;br&gt;
