# JavaProject3
Java课程作业第三次实验

## 计G201 张丽蓉 2020322068

## 一、实验目的
1. 通过实例化对象调用方法的过程，再次学习理解子类继承父类的原理与实现
2. 通过构造方法的重载以及实例化多个不同参数变量的对象，学习理解子类继承父类的原理与实现
3. 在实例化对象时，通过使用super()方法，理解super()调用父类有参构造方法的作用
4. 在输出结果信息时，学会使用Object父类的toString()方法
## 二、实验要求
1. 拥有一个具有共同属性的实体父类SchoolPerson,分别具有各自属性和方法的子类Student类和Teacher类
2. 编写Course实体类以及模拟系统操作的主类Test类
3. 主类通过实例化Student、Teacher、Course类的实体，完成学生选课并输出信息、学生退课并输出信息的模拟操作
## 三、实验过程
#### 1. 创建父类SchoolPerson并满足以下要求：
- 具有（姓名）name、（编号）num、（性别）gender、（电话）tel、（民族）nation属性
- 重载构造方法SchoolPerson，参数列表为全部属性
- 重写toString（）方法，输出属性信息
#### 2. 创建子类Student类并满足以下要求：
- 具有从父类继承来的（姓名）name、（编号）num、（性别）gender、（电话）tel、（民族）nation属性，以及新属性（课程）scourse、（成绩）grade
- 编写setter、getter方法
- 拥有super()方法调用父类有参数的构造方法
- 重写toString（）方法，输出属性信息
#### 3. 创建子类Teacher类并满足以下要求：
- 具有从父类继承来的（姓名）name、（编号）num、（性别）gender、（电话）tel、（民族）nation属性，以及新属性（课程）tcourse、（职称）competent
- 拥有super()方法调用父类有参数的构造方法
- 编写setter、getter方法
- 重写toString（）方法，输出属性信息
#### 4. 创建Course类并满足以下要求：
- 具有（课程名称）name、（课程编号）num、（上课地点）location、（授课教师）teacher、（上课时间）time、（学分）credit属性
- 分别拥有无参和有参的构造方法
- 编写setter、getter方法
- 重写toString（）方法，输出属性信息
#### 5. 创建Test主类并满足以下要求：
- 在main（）方法中实例化Teacher、Student、Course实体类，并赋值
- 分别拥有无参和有参的构造方法
- 编写setter、getter方法
- 重写toString（）方法，输出属性信息

## 四、核心代码与注释

#### 1. 方法一
父类SchoolPerson
```
	//父类SchoolPerson有参的构造方法
	SchoolPeople(String name,int num,String gender,int tel,String nation){	
		this.name=name;
		this.num=num;
		this.gender=gender;
		this.tel=tel;
		this.nation=nation;
	}
	//父类SchoolPerson的输出方法toString（）
	public String toString(){
		return "|姓名："+name+
				"| |编号："+num+
				"| |性别："+gender+
				"|	|联系方式："+tel+"||民族："+nation+"|";		
	}
```
#### 2. 方法二
子类Student
```
//重载父类构造方法
	Student(String name,int num,String gender,int tel,String nation){
		super(name,num,gender,tel,nation);
	}
	//输出学生信息
	public String toString(){
		return "学生信息："+"\r\n"+super.toString()+"\r\n";
	}
```
#### 3. 方法三
子类Teacher
```
//重载父类构造方法
	Teacher(String name,int num,String gender,int tel,String nation){
		super(name,num,gender,tel,nation);
	}
//子类单独定义属性
	Course tcourse;
	String competent;
//子类输出教师信息
	public String toString(){
		return "\r\n"+"授课教师信息："+"\r\n"+super.toString()+"|职称："+competent+"|";
	}
```
#### 4. 方法四
Course类

```
//Course（）无参构造方法
	Course(){}
	//Course（）有参构造方法
	Course(String name,int num,String location,String teacher,String time,double credit)
	{
		this.name=name;
		this.num=num;
		this.location=location;
		this.teacher=teacher;
		this.time=time;
		this.credit=credit;
	}
	//输出课程信息
	public String toString()
	{ 
		return "所选课程信息："+"\r\n"+"|课程名："+name+
				"| |课程编号："+num+"| |上课地点："
				+teacher+"| |授课教师："+location+
				"| |上课时间："+time+"| |学分："+credit+"|";		
	}
```
#### 5. 方法五
主类Test

```
//实例化各个类的对象
		Student stu1=new Student("莉莉",2020322,"女",1393939399,"汉");
		Course cour1=new Course("大学物理",001,"李老师","图306","周一06节",3.0);
		Course nocourse=new Course();
		Teacher tch=new Teacher("李老师",0202333,"女",1306893522,"蒙族");                  
```
#### 6. 方法六
```
//通过逻辑判断学生的选课状态
		if (stu1.getScourse().num==0){
			System.out.println("该学生未选课或已退课！");
			System.out.println(stu1);
			System.out.println("无选课信息");
	
		}else{
			System.out.println("该学生已选课！");
			System.out.println(stu1);
			System.out.println(cour1);
			System.out.println(tch);
		}
```
## 五、实验结果运行截图

##### 学生选课成功，输出打印学生信息、所选课程信息、老师信息

![图片文件](http://note.youdao.com/yws/public/resource/1a6540318fbcd87bfdb94a92233d55cd/xmlnote/WEBRESOURCEcae05bb7889ab735a67d71724f5f3ad9/22)

##### 学生选课失败，输出打印学生信息

![图片文件](http://note.youdao.com/yws/public/resource/0310ad631bfd36a3baed93ed5fd3447a/xmlnote/WEBRESOURCE78cf137c40ae2a01c82c33b99d4e7470/16)
## 六、实验感想
通过简单分析需求，我决定使用逻辑判断Student类的scourse属性值，选择输出打印的内容，模拟学生选课退课的操作。此次实验将SchoolPerson设为主类抽取共同属性，子类Student和Teacher分别用super（）方法体现了继承的特性，以及通过使用Object类的toString（）方法输出打印信息，实验过程中遇到无法正确输出信息问题，发现是因为对象调用set方法时出现错误。通过本次实验，我加深了对子类继承父类内容的理解，同时重新复习了构造方法和重载的概念，基本完成本次实验任务。
