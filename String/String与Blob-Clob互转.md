[String与Blob-Clob互转.md](https://www.cnblogs.com/alex-blog/articles/2793424.html)
```java
package gov.test;
import java.sql.Blob;
import java.sql.Clob;
import javax.sql.rowset.serial.SerialBlob;
import javax.sql.rowset.serial.SerialClob;

public class SplitTest {
	public static void main(String[] args) {
		String str = "hewgdbwt36tHBGBGvgBbg不会把动不动就方便大家!@#$%";
			try {
				Clob c = new SerialClob(str.toCharArray());
				Blob b = new SerialBlob(str.getBytes());
				System.err.println(c+"-----------"+b);
				String clobString = c.getSubString(1, (int) c.length());
				String blobString = new String(b.getBytes(1, (int) b.length()));
				System.out.println(clobString+"------------"+blobString);
			} catch (Exception e) {
				e.printStackTrace();
			}
	}
}
/*
	 * 结果如下:
	 * 转为Clob/Blob:   javax.sql.rowset.serial.SerialClob@f62373-----------javax.sql.rowset.serial.SerialBlob@19189e1
	 * 转为String:      hewgdbwt36tHBGBGvgBbg不会把动不动就方便大家!@#$%------------hewgdbwt36tHBGBGvgBbg不会把动不动就方便大家!@#$%
	 */
```
