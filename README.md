# Các phương pháp kiểm thử
- Kiểm thử hộp đen [1-100]
- Xét 3 vùng: < 1, 1 - 100, > 100
-  **Phân vùng tương đương:** -1; 50; 102
- **Phân tích giá trị biên**
	- Tại biên (1; 100)
	- Cận biên (+-1 đơn vị của giá trị biên)
- **Bảng quyết định **(Áp dụng với từ 2 field dữ liệu trở lên)
	- Tài khoản: 1, 1, 0, 0
	- Mật khẩu: 1, 0, 1, 0
- **Đoán lỗi**
	- Trống
	- Trùng
	- Kí tự đặc biệt
	- Nhập số (đoán nhập chữ),...

# Exception
| Tên  | Định nghĩa  |
| ------------ | ------------ |
| AssertionError  | Khẳng định thất bại  |
|  NullPointerException | Khi null được dùng trong method không truyền vào null  |
| IllegalArgumentException | Khi đối số truyền vào phương thức không hợp lệ |
| IndexOutOfBoundException | Chỉ mục không hợp lệ trong mảng, danh sách hoặc chuỗi |
| TimeoutException | Khi phương thức vượt quá thời gian quy định |
| Exception | Ngoại lệ |
| ArithmeticException | Lỗi toán học |

# Tạo project
- Generators: JakartaEE
- Template: Web Application
## Dependencies
- Junit
- Selenium
### Tạo lớp (Class)
- Tạo trong package main.java
Ví dụ:
```java
public class Calculator {
	public int add (int a, int b) {
		return a+b;
	}
	
	public double divide (int a, int b) {
		if (b == 0) {
			throw new ArithmeticException(" Khong chia cho 0");
		}
		return (double) a/b;
	}
}
```
- Lớp test (CalculatorTest) (test.java.CalculatorTest)
```java
public class CalculatorTest {
	Calculator calc = new Calculator();
	
	@Test
	public void testAdd() {
		//Ket qua mong muon
		int exp = 7;
		//Ket qua thuc te
		int act = calc.add(4, 3);
		//So sanh
		Assertions.assertEquals(exp, act);
	}
	
	@Test
	public void testDivide() {
		double exp = 1.5;
		double act = calc.divide(3, 2);
		Assertions.assertEquals(exp, act);
	}
	
	@Test
	public void testDivideByZero() {
		Assestions.assertThrows(ArithmeticException.class, ()->calc.divide(3, 0));
	}
}
```

- xepLoaiHocLuc.java
```java
public class xepLoaiHocLuc {
	public String xepLoaiHocLuc (double diemTB) {
		if(diemTB < 0 || diemTB > 10) {
			throw new IllegalArgumentException("Diem khong hop le");
		} else if (diemTB >= 9.0) {
			return "Xuat sac";
		} else if (diemTB >= 7.0) {
			return "Gioi";
		} else if (diemTB >= 5.0) {
			return "Trung Binh";
		} else {
			return "yeu";
		}
	}
}
```

- xepLoaiHocLucTest.java
```java
public class XepLoaiHocLucTest {
	XepLoaiHocLuc hocLuc = new XepLoaiHocLuc();
	
	@Test
	public void testHLPhanVung_95() {
		String exp = "Xuat sac";
		String act = hocLuc.xepLoaiHocLuc(9.5);
		Assertions.assertEqual(exp, act);
	}
	
	//tiep tuc paste ra:)
	
	@Test
	public void testHLEx_min() {
		Assertions.assertThrows(IllegalAccessError.class, ()-> hocLuc.xepLoaihocLuc(-5));
	}
	
	@Test
	public void testHLEx_max() {
		Assertions.assertThrows(IllegalAccessError.class, ()-> hocLuc.xepLoaihocLuc(15));
	}
	
	//Test tai bien cac kieu... Ctrl C -> Ctrl V, de co may bien thi dien nay test cay vao
}
```

- Arrayutils
```java
public class ArrayUtils {
	public int findMax(int[] arrNumber) {
		if(arrNumber == null || arrNumber.length == 0) {
			throw new IllegalArgumentException("Mang khong đuoc trong");
		}
		
		Arrays.sort(arrNumber);
		int max = arrNumber[arrNumber.length-1];
		int index = arrNumber.length-1;
		System.out.println("Gia tri lon nhat la" + max + "va tai vi tri thu: " + index);
		return max;
	}
}
```

- ArrayutilsTest
```java
public class ArrayUtilsTest {
	ArrayUtils arrayUtils = new ArrayList();
	@Test
	public void testFindMax() {
		int exp = 9;
		int act = ArrayUtils.findMax(new int[]{2, 4, 6, 8, 9});
		Assertions.assertEquals(exp, act);
	}
	
	@Test
	public void testFindMaxEX() {
		Assertions.assertThrows(ArrayIndexOutOfBoundsException.class, () -> arrayUtils.findMax(new int[]{}));
	}
	
	@Test
	public void testFindMaxEX2() {
		Assertions.assertThrows(ArrayIndexOutOfBoundsException.class, () -> arrayUtils.findMax(null);
	}
}
```
