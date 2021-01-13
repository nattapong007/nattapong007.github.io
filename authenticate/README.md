![](xxx.png)
# exec
(PHP 4, PHP 5, PHP 7)

exec — เป็นฟังก์ชันที่ให้ PHP ไปเรียกใช้คำสั่ง Command line และจะคืนค่ากลับ (return)มาเป็น string บรรทัดสุดท้ายที่ได้จากการรันคำสั่ง $command

### รูปแบบการใช้งาน
```
exec ( string $command , array &$output = null , int &$result_code = null ) : string|false
```


### ตัวอย่างการใช้งานฟังก์ชัน exec()
```
<?php
// outputs the username that owns the running php/httpd process
// (on a system with the "whoami" executable in the path)
$output=null;
$retval=null;
exec('whoami', $output, $retval);
echo "Returned with status $retval and output:\n";
print_r($output);
?>
```

