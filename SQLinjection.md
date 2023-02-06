這是示範如何在 PHP 中防止 SQL injection 的五種方法：



1.過濾輸入數據: 在將用戶輸入的數據插入數據庫前，應過濾該數據，以防止特殊字符（如引號）造成的 SQL 注入攻擊。


bash  
Copy code  
$username = strip_tags($_POST['username']);  
$username = mysqli_real_escape_string($conn, $username);  


2.使用 Prepared Statements: 使用預編譯的 SQL 語句防止 SQL 注入攻擊。


bash  
Copy code  
$stmt = $conn->prepare("INSERT INTO users (username, email) VALUES (?, ?)");  
$stmt->bind_param("ss", $username, $email);  
$stmt->execute();  


3.使用 ORM（物件關係映射）框架：使用 ORM 框架，例如 Doctrine 或 Eloquent，可以防止 SQL 注入攻擊，因為它們自動將數據值過濾，並在數據庫中生成預編譯的 SQL 語句。


php  
Copy code  
$user = new User;  
$user->username = $username;  
$user->email = $email;  
$user->save();  


4.使用 Input Sanitization 函數: 將輸入數據的驗證與過濾與代碼中分開。


php  
Copy code   
$username = sanitize_input($_POST['username']);  
$email = sanitize_input($_POST['email']);  



$conn->query("INSERT INTO users (username, email) VALUES ('$username', '$email')"); 

function sanitize_input($data) {  
  $data = trim($data);  
  $data = stripslashes($data);  
  $data = htmlspecialchars($data);  
  return $data;  
} 


5.使用 LIMIT 子句限制輸出: 限制從數據庫中返回的數據行數，以防止被惡意code利用。  