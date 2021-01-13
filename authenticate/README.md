![](xxx.png)
# authenticate()

authenticate — การยืนยันตัวตน เป็นการบอกว่าคนที่กำลังเข้ามาในระบบคือใคร และเป็นคนๆนั้นจริงหรือเปล่า


### รูปแบบการใช้งานที่ไม่ปลอดภัย
```
function authenticate() {
  if( isset( $_POST[ 'Connect' ] ) ) {
    $login = $_POST[ 'login' ];
    $pass = $_POST[ 'pass' ];

    $query = "SELECT * FROM users WHERE login = '" . $login . "' AND pass = '" . $pass . "'"; // Unsafe

    // If the special value "foo' OR 1=1 --" is passed as either the user or pass, authentication is bypassed
    // Indeed, if it is passed as a user, the query becomes:
    // SELECT * FROM users WHERE user = 'foo' OR 1=1 --' AND pass = '...'
    // As '--' is the comment till end of line syntax in SQL, this is equivalent to:
    // SELECT * FROM users WHERE user = 'foo' OR 1=1
    // which is equivalent to:
    // SELECT * FROM users WHERE 1=1
    // which is equivalent to:
    // SELECT * FROM users

    $con = getDatabaseConnection();
    $result = mysqli_query($con, $query);

    $authenticated = false;
    if ( $row = mysqli_fetch_row( $result ) ) {
      $authenticated = true;
    }
    mysqli_free_result( $result );
    return $authenticated;
  }
}
```


### ตัวอย่างการใช้งานฟังก์ชันที่ถูกต้อง
```
function authenticate() {
  if( isset( $_POST[ 'Connect' ] ) ) {
    $login = $_POST[ 'login' ];
    $pass = $_POST[ 'pass' ];

    $query = "SELECT * FROM users WHERE login = ? AND pass = ?"; // Safe even if authenticate() method is still vulnerable to brute-force attack in this specific case

    $stmt = $pdo->prepare($query);

    $stmt->execute(array($login, $pass));

    $authenticated = false;
    if ( $stmt->rowCount() == 1 ) {
      $authenticated = true;
    }

    return $authenticated;
  }
}
```

### Reference
>https://rules.sonarsource.com/php/type/Vulnerability/RSPEC-3649 <br>
>OWASP SQL Injection Prevention [Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)<br>
>[OWASP Top 10 2017 Category A1](https://owasp.org/www-project-top-ten/2017/A1_2017-Injection.html) - Injection<br>
>[MITRE, CWE-89](https://cwe.mitre.org/data/definitions/89) - Improper Neutralization of Special Elements used in an SQL Command<br>
>[MITRE, CWE-20](https://cwe.mitre.org/data/definitions/20.html) - Improper Input Validation<br>
>[MITRE, CWE-943](https://cwe.mitre.org/data/definitions/943.html) - Improper Neutralization of Special Elements in Data Query Logic<br>
>[CERT, IDS00-J.](https://wiki.sei.cmu.edu/confluence/x/ITdGBQ) - Prevent SQL injection<br>
>[SANS Top 25](https://www.sans.org/top25-software-errors/#cat1) - Insecure Interaction Between Components<br>

