### **前置条件**

要求：jdk1.8及以上

变量名：JAVA_HOME
变量值：电脑上JDK安装的绝对路径

变量名：CLASSPATH
起始位置添加
变量值：.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;

变量名：PATH

%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;
win10新建两条路径：
%JAVA_HOME%\bin
%JAVA_HOME%\jre\bin

### **添加一个接口**

新建一个测试计划，右击添加-线程-线程组

右击添加-取样器-HTTP请求，在其中配置对应的接口

- 协议：http

- 服务名称或IP：httpbin.org

- HTTP请求：GET

- 路径：/get

- 添加变量：

  - 名称：user

  - 值：zsj或是${变量名}

查询执行结果需要右击添加-监听器-察看结果树

若果接口的部分协议或ip相同，可以在测试计划页面添加变量，或者是右击测试计划添加-配置元件-HTTP默认请求中进行配置

### 如何进行接口测试

1. 接口需求分析;
2. 测试计划编写;
3. 测试用例设计;
4. 测试脚本开发;
5. 测试执行;
6. 发布测试结果。

### 请求体

| Content-Type     | 提交数据方式        |
| ---------------- | ------------------- |
| application/json | 序列化 Json数据提交 |
| text/xml         | XML数据提交         |

### 断言

- 包括：响应内容包括需要匹配的内容即代表响应成功，支持正则表达式
- 匹配：响应内容要**完全匹配**需要匹配的内容即代表响应成功，不区分大小写，支持正则表达式
- Equals：响应内容要完全等于需要匹配的内容才代表成功，区分大小写，需要匹配的内容是字符串正则表达式
- Substring：返回结果包含指定结果的字串，但是 subString不支持正则字符串
- 否：不进行匹配

### 变量

Jmeter支持以下类型变量：

#### 一、用户自定义变量

右击添加-前置处理器-用户参数，定义变量和值，使用${变量名}调用，引用时需要加上引号

#### 二、函数生成变量

菜单栏中选择工具-函数助手对话框

#### 三、BeanShell变量

- 什么是Bean Shell?

  BeanShell是一种完全符合Java语法规范的脚本语言,并且又拥有自己的一些语法和方法;

  BeanShell是一种松散类型的脚本语言(这点和JS类似);

  BeanShell是用Java 写成的,一个小型的、免费的、嵌入式的Java

  源代码解释器具有对象脚本语言特性非常精简。

  BeanShell执行标准Java语句和表达式另外包括一些脚本命令和语法。

1. 定时器：BeanShell Timer

2. 前置处理器：BeanShell PreProcessor

   右击-添加-前置处理器-BeanShell PreProcessor，生成BeanShell 预处理程序

   定义变量user

   ```java
   // 定义Jmeter变量
   vars.put("user","yzp");
   //日志输出
   log.info("1024!");
   ```

   导入包，再定义变量orderDate、delivery

   ```java
   import java.text.SimpleDateFormat;
   import java.util.Calendar;
   import java.util.Date;
   
   Date date = new Date();
   SimpleDateFormat sf = new SimpleDateFormat("yyyy-MM-dd");
   String nowDate = sf.format(date);
   Calendar cal = Calendar.getInstance();
   cal.setTime(sf.parse(nowDate));
   cal.add(Calendar.DAY_OF_YEAR, +3);
   String chanceDate = sf.format(cal.getTime());
   cal.add(Calendar.DAY_OF_YEAR, +7);
   String planFinishDate = sf.format(cal.getTime());
   vars.put("orderDate",chanceDate);
   vars.put("delivery",planFinishDate);
   ```

   

3. 采样器：BeanShell Sampler

4. 后置处理器：BeanShell PostProcessor

5. 断言：BeanShell断言

6. 监听器：BeanShell Listener

#### 四、数据文件变量

右键添加-配置元件-CSV Data Set Config，生成CSV 数据文件设置，注：用户参数优先级高于CSV 数据文件设置

```CSV
XLN,123
YZP,456
XZ,789
```

- 文件名:C:/Users/zsj/Desktop/data.csv
- 文件编码:UTF-8
- 变量名称(西文逗号间隔):username,password
- 忽略首行(只在设置了变量名称后才生效):False
- 分隔符(用'\t'代替制表符):,
- 是否允许带引号?:False
- 遇到文件结束符再次循环?:False
- 遇到文件结束符停止线程?:True
- 线程共享模式:所有现场

