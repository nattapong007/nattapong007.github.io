![](145.png)
# ctype_alnum()

**ctype_alnum()** เป็นฟังก์ชันที่ใช้ในการตรวจสอบอักขระที่เป็นตัวเลขและตัวอักษรเท่านั้น ในที่นี้หมายถึงตัวเลข **0-9 และ A/a-Z/z** <br>
มีค่าเป็น **bool** เท่านั้นเช่น ถ้าพบว่าใน string มีเพียงตัวเลขและตัวอักษรจะส่งค่ากลับมาเป็น **true** ในทางกลับกันหากพบว่ามีตัวอักระอื่นๆเช่น <br>
สัญลักษณ์ต่างๆเข้ามาแทรกส่วนใดส่วนหนึ่งหรือทั้งหมดของ string จะส่งค่ากลับมาเป็น **false**

### ตัวอย่างการใช้งาน
```
ctype_alnum ( string $text ) : bool
```

### ตัวอย่างการใช้งานฟังก์ชันที่ถูกต้อง
```
<?php
$strings = array('AbCd1zyZ9', 'foo!#$bar');
foreach ($strings as $testcase) {
    if (ctype_alnum($testcase)) {
        echo "The string $testcase consists of all letters or digits.\n";
    } else {
        echo "The string $testcase does not consist of all letters or digits.\n";
    }
}
?>
```
### ผลลัพธ์
```
The string AbCd1zyZ9 consists of all letters or digits.
The string foo!#$bar does not consist of all letters or digits.
```
ซึ่งแน่นอนว่าฟังก์ชันนี้ นักพัฒนานำมาใช้ประกอบในการตรวจสอบข้อมูลของการตั้ง **username** ของผู้ใช้ ในกรณีไม่ต้องการมีตัวอักขระอื่นเช่นสัญลักษณ์ต่างๆมาปะปนด้วย เพื่อให้ได้ข้อมูลเพียงแค่ตัวอักษรและตัวเลขเท่านั้น

### Reference
[PHP ctype_alnum](https://www.php.net/manual/en/function.ctype-alnum.php)<br>
[WebDesign Tuutorialz](https://www.webdesigntutorialz.com/2020/11/php-ctypealnum-function.html)
