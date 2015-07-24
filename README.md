# Android-Code-Style-Conventions

## การแยก package
``` java
package.root.model
package.root.view
package.root.activity
package.root.fragment
package.root.service
package.root.adapter
package.root.util
```

## การตั้งชื่อ
- Class มีประเภทต่อท้าย เช่น Main**Activity**, Settings**Fragment**, Currency**DialogFragment**, Country**Adapter**
- Non-public, non-static นำหน้าด้วย m
- Static นำหน้าด้วย s
- Public static final (constants) ตัวใหญ่หมดคั่นด้วยขีดล่าง ALL_CAPS_WITH_UNDERSCORES.

``` java
public class MyClass {
    public static final int SOME_CONSTANT = 42;
    public int publicField;
    private static MyClass sSingleton;
    int mPackagePrivate;
    private int mPrivate;
    protected int mProtected;
}
```

- xml ตั้ง id นำหน้าด้วยตัวย่อ 2 หลักของประเภท View นั้น ตามด้วยหน้าที่ของ View นั้น เช่น lvCurrency คือ ListView ที่แสดงค่าเงิน tvName คือ TextView ที่แสดงชื่อ svImage คือ HorizontalScrollView ที่แสดงรูปภาพ

- ใน xml เอา id ไว้บนสุดเสมอ ต่อด้วย width และ height
``` xml
<Button
  android:id="@+id/btSend"
  android:layout_width="wrap_content"
  android:layout_height="wrap_content"
  android:text="@string/send"/>
```

- ใน string.xml ใช้อักษรตัวเล็กหมด
``` xml
<string name="send">Send</string>
```

- ต้องตั้งชื่อตัวแปรของ View เป็นชื่อ id ของ View นั้นๆ
``` java
private Button btSend;
```

## อื่นๆ

- ประกาศตัวแปรก่อน method ใดๆ ห้ามวางประกาศตัวแปรไว้กลาง class เด็ดขาด

- เว้นวรรค 1 ครั้งหลังประกาศ method หรือ if

- limit scope ของตัวแปรให้มากที่สุด
``` java
void doSomething() {
  if (…) {
    double d = someCalculation(…);
    doSomethingWith(d);
  }
}
```

- ใส่ private เป็น default หากจำเป็นจึงจะแก้เป็น protected หรือ public

- ห้าม import foo.* ให้ import full name foo.Bar

- ห้ามทิ้ง catch exception ว่างไว้ ถ้าไม่ throw อย่างน้อยก็ต้อง logcat ออกมา
``` java
try {
        serverPort = Integer.parseInt(value);
    } catch (NumberFormatException e) { }
```

- ทุก if ต้องมีปีกกา {}
``` java
if (condition) {
  body();
}
```
ห้ามเขียนแบบนี้
``` java
if (condition)
  body();
```
เด็ดขาด เพราะเวลา debug ชอบมา Log ล่าง if แล้วลืม

- ใน Activity หรือ Fragment มี method setup() ที่เรียกครั้งดเียว และ update() ที่ไว้เรียกหลายครั้ง

- method ไม่ควรเกิน 50 บรรทัด

- ไม่ตั้งชื่อตัวย่อด้วยตัวใหญ่หมด
XmlHttpRequest = ดี
XMLHTTPRequest = ไม่ดี

## UX
- ทุกๆ network operation ต้องมี progress bar บางอันให้ user cancel ได้ บางอันห้าม cancel

## Programming
- ยิง Error และ Exception ทุกอย่างขึ้น Crashlytics

## Development process
- Rebase ทุกครั้งที่มี develop นำหน้า

## Database
- ทุกครั้งที่รับสมัคร email หรือ username หรือค่าต่างๆที่จะทำให้ search ได้ ให้ทำเป็น lowercase ก่อน save และ lowercase ก่อน login ทุกครั้ง
