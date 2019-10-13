# flutter_app_http_response

A new Flutter application.

## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://flutter.dev/docs/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://flutter.dev/docs/cookbook)

For help getting started with Flutter, view our
[online documentation](https://flutter.dev/docs), which offers tutorials,
samples, guidance on mobile development, and a full API reference.


## App modified to fetch data from MySQL.

A separate PHP page or equivalent is reuired that returns the JSON kind of response

For example:

{"id":"0","post_header":"Flutter","post_body":"Flutter helps create beautiful apps for Android as well as iOS"}

Please note the first column id is marked as String.

The flutter app then displays the column "post_body"

PHP Page is given below for your reference.

**************************************************

<?php
$servername = "localhost";
$username = "root";
$password = "";
$dbname = "id8813320_flutter";

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);
// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

$sql = "SELECT id, post_header, post_body FROM posts";
// trial to check if we can directly get JSON from MySQL - it did not work though
//$sql = "SELECT json_object('id', id, 'post_header', post_header, 'post_body', post_body) from posts";

$result = $conn->query($sql);

//Initialize array variable
  $dbdata = array();
//$dbdata = $result->fetch_assoc();

//Fetch into associative array
  while ( $row = $result->fetch_assoc())  {
	$dbdata[]=$row;
  }

//Print array in JSON format
echo trim(json_encode($dbdata), '[]');

$conn->close();
?>


**************************************************

MySQL database details are not shown here; however it can be created as follows:

Database Name: id8813320_flutter

Table Name: posts

No of rows = 1
(currently only one row is being handled on flutter side)

Columns:

id
post_header
post_body

(while id can be integer - it is treated as String on flutter side due to json_encode of PHP changing it as a String)
