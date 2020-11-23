# JavaProject4
Java第四次实验
## 计G201 张丽蓉 2020322068

## 一、实验目的
1. 复习String类型对象的使用，学习stringbuffer类型对象的方法
2. 学习了解文件读取输入的方法和具体细节问题
3. 再次复习异常处理的知识
## 二、实验要求
1. 学生实体类并通过交互式输入实例化学生类
2. 将学生类信息写入文件
3. 读取另一文件内容并进行格式操作
4. 将操作好的String内容写入学生信息的文件
5. 具有查询某汉字在文本中出现次数的方法
## 三、实验过程
#### 1. 创建学生类并满足以下要求：
- 具有基本属性和get、set方法
#### 2. 创建Test主类并满足以下要求：
- 创建学生类对象，通过scanner获取输入学生信息并存入文件“Student.txt”
- 设计判断汉字出现次数的方法
- 设计将学生信息存入文件的方法
- 设计读取source文件的方法
- 使用for循环将文本内容插入标点符号，并将整理过后的内容存入文件“Student.txt”
## 四、核心代码与注释

#### 1. 获取学生信息并捕获异常
将学生类对象封装成ArrayList
```
ArrayList<Student> studentArray = new ArrayList<Student>();
try {
			Student one = new Student();
			Scanner scanner = new Scanner(System.in);
			System.out.println("请输入您要在文档中查询的汉字或词语：");
			wordForSearch=scanner.nextLine();
			System.out.print("请输入学生姓名：");
			String str = scanner.nextLine();
			one.setName(str);
			System.out.print("请输入性别：");
			String gender = scanner.nextLine();
			one.setGender(gender);
			System.out.print("请输入年龄：");
			int age = scanner.nextInt();
			one.setAge(age);
			System.out.print("请输入学号：");
			int num = scanner.nextInt();
			one.setNum(num);
			studentArray.add(one);
			System.out.println("该学生个人信息已成功提交至作业文档！");
		}catch(InputMismatchException ime){
			System.out.print("输入数据类型错误！\n");
		}
```

#### 2. 存入学生信息方法
创建student.txt文件并存入学生信息
```
 File destPath = new File("Student.txt");
	        BufferedWriter bw = new BufferedWriter(new FileWriter(destPath));  
	        bw.write("学生姓名\t");
	        bw.write("性别\t");
	        bw.write("年龄\t");
	        bw.write("学号\t");
	        bw.newLine();
	        bw.flush();
	        for (Student one : studentArray) {
	            String name = one.getName();
	            String gender = one.getGender();
	            int age = one.getAge();
	            int num = one.getNum();
	            bw.write(name + "\t");
	            bw.write(gender + "\t");
	            bw.write(age + "\t");
	            bw.write(num + "\t");
	            bw.newLine();
	            bw.flush();
	        }
	        bw.write("作业内容：");
	        bw.newLine();
	       
	        bw.close();
	        
```
#### 3. 读取文件
读取source.txt文件，并将文件文本定义为字符串
```
          InputStreamReader ir =new InputStreamReader(new FileInputStream("source.txt"), "UTF-8");
	       BufferedReader bf = new BufferedReader(ir);
	       String poem=bf.readLine();
```
#### 4. 文本格式整理方法
利用stringbuffer类整理格式并写入student.txt文件
```
StringBuffer sb=new StringBuffer();
	       sb.append(poem);  
	       	int i;
			int j=0; 
			for(i=7;i<=sb.length();i+=8){
					if(i==7){
						sb.insert(i, ",");
					}else if((i-j)%7==0&&(i-j)%14!=0){
						sb.insert(i,",");
					} else if((i-j)%14==0){
						sb.insert(i,"。");
	    		}
	    	 j=j+1;
	    } 
      
       bw.append(sb.toString());
```
#### 5.GetCount方法
 查找某汉字在文本中出现次数方法
```
        static int GetCount(String source,String wordForSearch){
	   	   int i, j, count = 0;
	   	   int len1 = source.length(); 
	   	   int len2 = wordForSearch.length(); 
	   	   for(i=0; i<len1-len2; i++){
	   	   for(j=0; j<len2; j++){ 
	   		   if(wordForSearch.charAt(j) != source.charAt(j + i)){
	   			   break;
	   		   		}
	   	   		}
	   	   		if(j>=wordForSearch.length()){
	   	   			count++;
	   	   			}
	   	   		}
	   	   return count;
	  }
    
        InputStreamReader ir2 =new InputStreamReader(new FileInputStream("source.txt"), "UTF-8");
		    BufferedReader bf2 = new BufferedReader(ir2);
		    String poemForSearch=bf2.readLine();
		    int count = GetCount(poemForSearch, wordForSearch);
		    System.out.println(wordForSearch + "：这个汉字或词语在作业里出现了" + count+"次");          
```

## 五、实验结果运行截图

##### 控制台显示成功接收学生信息并存入

![图片文件](http://note.youdao.com/yws/public/resource/18fc0d14ac63f42e810afc6657b99d74/xmlnote/WEBRESOURCE5c2960b7de86d64d62259c0727d1b615/34)

##### 信息与文本成功写入student.txt文件

![图片文件](http://note.youdao.com/yws/public/resource/859da5035b4f5208532d47e221dd4dd6/xmlnote/WEBRESOURCE8b8e3c2a54bbbb4ba6e696b9d5d55a70/44)
##### 打印输出异常信息

![图片文件](http://note.youdao.com/yws/public/resource/18fc0d14ac63f42e810afc6657b99d74/xmlnote/WEBRESOURCEbc708e1fb490b7ae4718aed18ece756c/41)
## 六、实验感想
此次实验通过利用以前实现过的学生类，交互式输入了学生的信息，并保存在了文件中，其次，我使用了InputStreamReader方法读取了文本源文件，并通过添加UTF-8解决中文乱码问题，将读取到的文本封装成stringbuffer对象，使用stringbuffer类的insert方法，循环下标并添加了正确的标点符号，最后把已经整理好格式的文本内容写入了存放学生信息的文件中，基本完成本次实验的内容。我在实验中遇到的问题，一，stringbuffer类的长度随时变化更新，使用for循环判断下标时长度随时会变，所以我添加了整型变量j来保证标点符号的添加位置正确无误；二，在设计书写判断某个汉字在文本中出现次数的代码时，无法获取到输入的需要判断的汉字或词语，后来发现是因为String变量放在了主方法里，修改变量位置后，代码成功运行并输出。
