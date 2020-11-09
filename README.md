# JavaProject3
Java课程作业第三次实验

## 计G201 张丽蓉 2020322068

## 一、实验目的
1. 通过书写接口，体会接口在编写程序中呈现出来的抽出共有属性和方法等作用
2. 通过实体类实现接口的过程，了解实现接口时需要重写抽象方法等细节，体会理解实现接口与继承父类的不同
3. 体会abstract关键字的作用和意义，学习在继承、实现、重写等过程中abstract的限制和作用，了解抽象类和接口的不同
4. 实例化对象时使用scaaner类进行交互式输入，学习不同类型输入时scanner调用的不同方法
5. 学习抛出捕获异常的代码语句，try catch方法的实现，编写自定义异常类实现更具体的输入判断
## 二、实验要求
1. 拥有若干接口，必须拥有教师属性接口和学生属性接口，并在接口中抽象出相关方法
2. 编写实体类Doctor实现多个接口并重写接口内抽象方法，同时实体类需要自定义特有方法，计算所缴税金额
3. 主类通过实例化Doctor类的实体，sccner类交互输入为Doctor类实例化对象赋值，并调用对象的方法，根据不同工资梯度计算缴税金额
4. 在主类中通过捕获异常做输入项判断处理，并输出异常捕获后输出语句
## 三、实验过程
#### 1. 创建接口Tax并满足以下要求：
- 具有默认被static、final修饰的属性int MONTH=12;int TERM=2;int ST = 5000;int ST1 = 8000;int ST2 = 17000;double RATE=0.03;double RATE1=0.1;
#### 2. 创建接口Teacher并满足以下要求：
- 具有inSalary(double ins)与searchSalary(String n)两个管理抽象方法
#### 3. 创建接口Student并满足以下要求：
- 具有payTuition(double pt)和searchTuition(String n)两个管理抽象方法
#### 4. 创建Doctor类并满足以下要求：
- 定义自有属性String name;int num;int age;double tuitionOfTerm;double tuitionOfYear;double salaryOfYear;double salaryOfMonth;double tax;
- 实现接口Tax、接口Teacher、接口Student，并重写接口中的抽象方法
- 分别拥有无参和有参的构造方法
- 编写setter、getter方法，方便sccner得到数据后传值
- 定义double doTax(double salaryOfYear, double tuitionOfYear)方法，用于计算不同工资梯度对应应缴税额
#### 6. 创建自定义异常类MyException继承Exception父类并满足以下要求：
- 定义捕获到异常后执行的操作
#### 5. 创建Test主类并满足以下要求：
- 定义抛出自定义异常类的方法checkNum(int c)和checkTuition(float c)，设定判断输入年龄需要大于20且小于30，判断输入月薪不可以为0
- 在main（）方法中实例化Doctor实体类，除tax属性外，其他属性通过scanner交互输入赋值
- 在main（）方法中set到月薪和学期学费后计算年薪和每年的学费
- 在main（）方法中调用doTax方法计算应缴税额并输出
- 在捕获到异常后用冒号跳转和while循环设置重新输入
## 四、核心代码与注释

#### 1. 接口
Tax接口
```
	interface Tax {
		int MONTH=12;
		int TERM=2;
		int ST = 5000;
		int ST1 = 8000;
		int ST2 = 17000;
		double RATE=0.03;
		double RATE1=0.1;
	}
```
Teacher和Student接口
```
	interface Teacher {
		void inSalary(double ins);
		void searchSalary(String n);
	}
	interface Student {
		void payTuition(double pt);
		void searchTuition(String n);
}

```
#### 2. doTax方法
Doctor实体类 计算税额方法
```
public double doTax(double salaryOfYear, double tuitionOfYear) {
		double i = salaryOfYear - tuitionOfYear;
		if (i <= ST * MONTH) {
			tax = 0;
			System.out.println("提示：您今年无需缴纳税费");
		} else if (i >= ST * MONTH && i <= ST1 * MONTH) {
			tax = i * RATE;
		} else if (i >= ST1 * MONTH && i <= ST2 * MONTH) {
			tax = i * RATE;
		}
		return tax;

	}
```
#### 3. 自定义异常类
```
class MyException extends Exception {
	String message;

	public MyException(int m) {
		message = "您输入的  "+ m + " 不符合系统规则，请重新输入";
	}

	public String warnness() {
		return message;
	}
}
```
#### 4. 抛出自定义异常类
```
public class Text {

	public static void checkNum(int c) throws MyException {
		if (c >= 20 &&c <= 30) {
			throw new MyException(c);
		}
	}

	public static void checkTuition(float c) throws MyException {
		if (c == 0) {
			throw new MyException((int) c);
		}
	}
```
#### 5. 主类中scanner交互输入并赋值计算方法
```
input:
		while(true){
		try {
			Scanner scanner = new Scanner(System.in);
			System.out.print("请输入姓名：");
			String str = scanner.nextLine();
			doctorOne.setName(str);
			System.out.print("请输入年龄：");
			int age = scanner.nextInt();
			checkNum(age);
			doctorOne.setAge(age);
			System.out.print("请输入工号：");
			int num = scanner.nextInt();
			doctorOne.setNum(num);
			System.out.print("请登记月薪：");
			float salary = scanner.nextFloat();
			checkTuition(salary);
			doctorOne.inSalary(salary);
			System.out.print("请登记每学期的学费：");
			float tuition = scanner.nextFloat();
			doctorOne.payTuition(tuition);
			double totalSalaryOfYear = doctorOne.totalSalaryOfYear(doctorOne.salaryOfMonth);
			double totalTuitionOfYear = doctorOne.totalTuitionOfYear(doctorOne.tuitionOfTerm);
			double tax = doctorOne.doTax(totalSalaryOfYear, totalTuitionOfYear);
			System.out.println("用户:" + doctorOne.name + " 您本年该交的税费共计为：" + tax
					+ "元/年");
			break;
		}catch(InputMismatchException ime){
			System.out.print("输入数据类型错误！\n");
			continue input; 
			
		}catch (MyException e) {
			System.out.println(e.warnness());
		}
	}                
```

## 五、实验结果运行截图

##### 输入每一项数据无误，成功输出对应税额

![图片文件](http://note.youdao.com/yws/public/resource/253bd04b7be5f80431825916d9afbaa8/xmlnote/WEBRESOURCE842a9d2208a055cc9d028a6671fe38ab/26)

##### 输入年龄小于20岁，打印输出异常信息

![图片文件](http://note.youdao.com/yws/public/resource/253bd04b7be5f80431825916d9afbaa8/xmlnote/WEBRESOURCE492b266291cfaa0cc0ea030a1cee4d77/29)
##### 输入工号非int型数据，打印输出异常信息

![图片文件](http://note.youdao.com/yws/public/resource/253bd04b7be5f80431825916d9afbaa8/xmlnote/WEBRESOURCEd5e69a7e349e32401b9ef414ab320a3c/31)
## 六、实验感想
此次实验通过设计了三个不同的接口，抽象出了实体类需要使用的共同属性和方法，方便后期修改和维护，实验过程中我遇到了无法捕获抛出异常的问题，发现是因为try语句块没有正确的包含，第二个问题是抛出异常信息后无法重新输入，通过上网查找资料，发现可以使用冒号跳转的方法。通过本次实验，我对接口和抽象类、抽象方法的概念和作用基本有了大体的理解，尤其通过对书写、修改、使用异常类的代码，理解了使用异常类在代码运行过程中的优缺点，基本完成本次实验任务。
