# preg_quote
(PHP 4, PHP 5, PHP 7)
preg_quote — Quote regular expression characters
![](/img/Webp.png)

## ตัวอย่างการใช้งาน
```
preg_quote ( string $str , string|null $delimiter = null ) : string
```

preg_quote () คือ การเพิ่มเครื่องหมาย backslashes หน้าอักขระพิเศษ (characters) เช่น \ + * ? [ ^ ] $ ( ) { } = ! < > | : - ด้วยฟังก์ชั่น

ตัวอย่างการใช้งานที่ 1 preg_quote()
```
<?php
$keywords = '$40 for a g3/400';
$keywords = preg_quote($keywords, '/');
echo $keywords; // returns \$40 for a g3\/400
?>
```

ตัวอย่างการใช้งานที่ 2 Italicizing a word within some text
```
<?php
// In this example, preg_quote($word) is used to keep the
// asterisks from having special meaning to the regular
// expression.

$textbody = "This book is *very* difficult to find.";
$word = "*very*";
$textbody = preg_replace ("/" . preg_quote($word, '/') . "/",
                          "<i>" . $word . "</i>",
                          $textbody);
?>
```

# Notes
```
Note: This function is binary-safe.
```


## เพิ่มเติม
- [PCRE Patterns](https://www.php.net/manual/en/pcre.pattern.php)
- [escapeshellcmd() - Escape shell metacharacters](https://www.php.net/manual/en/function.escapeshellcmd.php)
