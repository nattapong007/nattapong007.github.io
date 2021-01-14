![](.png)
# memset and memset_s

**memset** และ **memset_s** เป็นการกำหนดจำนวนค่าหรือสมาชิกที่เก็บไว้ในตัวแปร โดยมีประโยชน์คือ ทำให้สามารถกำหนดค่าสมาชิกได้ตามที่ต้องการ<br>
ซึ่งไม่ต้องเขียนคำสั่งควบคุมการทำงานซ้า ทำให้สะดวกและลดบรรทัดของการเขียนชุดคำสั่ง <br>
แต่ฟังก์ชัน memset_s ถึงจะทำงานคล้ายกัน memset แต่ข้อแตกต่างที่สำคัญคือไม่สามารถจะปรับแต่งอะไรได้ เพราะหน่วยความจำจะถูกเขียนทับทุกกรณีจึงเหมาะกับการใช้งานกับ Sensitive Data

### ตัวอย่างการใช้งานที่ไม่ควรใช้ memset
**"memset" should not be used to delete sensitive data**

### ### รูปแบบการใช้งานที่ไม่ปลอดภัย
```
void f(char *password, size_t bufferSize) {
  char localToken[256];
  init(localToken, password);
  memset(password, ' ', strlen(password)); // Noncompliant, password is about to be freed
  memset(localToken, ' ', strlen(localBuffer)); // Noncompliant, localToken is about to go out of scope
  free(password);
}

```

### ตัวอย่างการใช้งานฟังก์ชันที่ถูกต้อง
```
void f(char *password, size_t bufferSize) {
  char localToken[256];
  init(localToken, password);
  memset_s(password, bufferSize, ' ', strlen(password));
  memset_s(localToken, sizeof(localToken), ' ', strlen(localBuffer));
  free(password);
}
```
### Reference
[SonarSource](https://rules.sonarsource.com/cpp/type/Vulnerability/RSPEC-5798)
