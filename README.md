# PHP-Store-Data-To-sql-Database.github

This PHP script handles form data submission and stores it in a MySQL database. It establishes a connection to the database using PDO (PHP Data Objects) and securely inserts the form data into the specified table. The script begins by defining database connection parameters such as server name, username, password, and database name. Then, it retrieves form data using the $_POST superglobal and assigns it to variables. 

```php
// Database connection parameters
$servername = "localhost"; // Replace with your database server name
$username = "username"; // Replace with your database username
$password = "password"; // Replace with your database password
$database = "database_name"; // Replace with your database name

// Form data
$name = $_POST["name"];
$email = $_POST["email"];
$message = $_POST["message"];
```

A PDO instance is created to establish a connection to the database with error handling to ensure graceful error reporting. The script prepares an SQL statement to insert the form data into the specified table using named placeholders and binds the variables to prevent SQL injection attacks. Finally, it executes the prepared statement, echoes a success message if the insertion is successful, and catches and displays any errors that occur during execution.

```php
try {
    // Create a new PDO instance
    $conn = new PDO("mysql:host=$servername;dbname=$database", $username, $password);

    // Set the PDO error mode to exception
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

    // Prepare SQL statement
    $sql = "INSERT INTO your_table_name (name, email, message) VALUES (:name, :email, :message)";
    $stmt = $conn->prepare($sql);

    // Bind parameters
    $stmt->bindParam(':name', $name);
    $stmt->bindParam(':email', $email);
    $stmt->bindParam(':message', $message);

    // Execute the prepared statement
    $stmt->execute();

    echo "Data stored successfully!";
} catch(PDOException $e) {
    echo "Error: " . $e->getMessage();
}
```

Finally, the database connection is closed.

```php
// Close connection
$conn = null;
```

This script serves as a foundational example for building a secure form submission and database storage system.
