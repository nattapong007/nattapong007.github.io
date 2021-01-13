![](createimage.png)

# PHP | imagestring() Function

(PHP 4, PHP 5, PHP 7)<br>
**imagestring - การเขียนข้อความลงในภาพ**

### รูปแบบการใช้งาน
```
imagestring ( resource $image , int $font , int $x , int $y , string $string , int $color ) : bool
```

**$image** คือ resource ซี่งอาจได้จากการสร้างโดย [imagecreatetruecolor()](https://www.php.net/manual/en/function.imagecreatetruecolor.php)<br>
**$font** คือ ขนาดของตัวอักษรที่ต้องการ ซึ่งอาจได้จากการสร้างโดย [Imageloadfont()](https://www.php.net/manual/en/function.imageloadfont.php)<br>
**$x** และ **$y** คือ ตำแหน่งเริ่มต้นวาดตามแนวแกน x และ y ของรูปภาพ<br>
**$string** คือ ข้อความที่ต้องการวาด ในรูป UTF-8 และตัวอักษรในรูป &#3585; (รองรับภาษาอื่นๆ รวมทั้งภาษาไทย)<br>
**$color** คือ resource ของสีของตัวอักษรที่ต้องการ อาจได้มาจากการสร้างโดย [imagecolorallocate()](https://www.php.net/manual/en/function.imagecolorallocate.php)
```
ตัวอย่างสี ขาว ดำ แดง เขียว และน้ำเงิน
$white = ImageColorAllocate ($im, 255, 255, 255);
$black = ImageColorAllocate ($im, 0, 0, 0);
$red = ImageColorAllocate ($im, 255, 0, 0);
$green = ImageColorAllocate ($im, 0, 255, 0);
$blue = ImageColorAllocate ($im, 0, 0, 255);
```

### การใช้งานตัวอย่างที่ 1
```
<?php 
   
// Create the size of image or blank image 
$image = imagecreate(500, 300); 
   
// Set the background color of image 
$background_color = imagecolorallocate($image, 0, 153, 0); 
   
// Set the text color of image 
$text_color = imagecolorallocate($image, 255, 255, 255); 
   
// Function to create image which contains string. 
imagestring($image, 5, 180, 100,  "GeeksforGeeks", $text_color); 
imagestring($image, 3, 160, 120,  "A computer science portal", $text_color); 
   
header("Content-Type: image/png"); 
   
imagepng($image); 
imagedestroy($image); 
?> 
```

### การใช้งานตัวอย่างที่ 2
```
<?php
// Create a 100*30 image
$im = imagecreate(100, 30);

// White background and blue text
$bg = imagecolorallocate($im, 255, 255, 255);
$textcolor = imagecolorallocate($im, 0, 0, 255);

// Write the string at the top left
imagestring($im, 5, 0, 0, 'Hello world!', $textcolor);

// Output the image
header('Content-type: image/png');

imagepng($im);
imagedestroy($im);
?>
```

### การใช้งานตัวอย่างที่ 3
```
<?php
header ("Content-type: image/png");
$im=@imagecreatetruecolor(120, 20)
      or die("Cannot Initialize new GD image stream");
$text_color=imagecolorallocate($im, 233, 14, 91);
imagestring($im, 1, 5, 5, "A Simple Text String", $text_color);
imagepng($im);
imagedestroy($im);
?>
```
### Reference
https://www.php.net/manual/en/function.imagestring.php
https://www.geeksforgeeks.org/php-imagestring-function/
