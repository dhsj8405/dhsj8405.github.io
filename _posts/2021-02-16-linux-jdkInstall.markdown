---

layout: post
title: 'Linux java 설치/ 환경 설정'
subtitle: 'Linux java 설치/환경 설정'
categories: devlog
tags: linux
comments: true

---

# 자바설치
## 1. JDK 다운
```linux
[root@localhost ~]# wget http://download.oracle.com/otn-pub/java/jdk/8u72-b15/jdk-8u72-linux-x64.tar.gz
```

# tar.gz 압축 해제 에러
```linux
tar -xvfz jdk-8u72-linux-x64.tar.gz
```

에러메세지
```
gzip: stdin: not in gzip format  
tar: Child returned status 1  
tar: Error is not recoverable: exiting now 
```

```깨진 파일을 받으면 뜬다함```

해결방법 : 리눅스용 jdk zip 파일 구해서 윈도우에 다운 후 리눅스로 옮기기

# 윈도우와 리눅스 사이 파일 이동 시키기 (SFTP)

사용자 계정 : ex_desktop_01

```[C:\~]$ sftp ex_desktop_01@xxx.xxx.xxx.xxx```  
```sftp:/home/ex_desktop_01> put 파일이 설치된경로/파일명```  

- 설치된경로에 한글이 있어서그런지 에러뜸

 	로컬C에 옮겨놓고 ```put C:\파일명``` 하니까 됨

ssh 클라이언트 다시 켜서 확인하면됨

## 2. 리눅스에 이동 된거 확인하고 /usr/local에 옮기고 압축 풀기

확인하기  
```[root@localhost ~]# cd /home/desktop_01/```

압축하려고하는 폴더로 이동하기  
```[root@localhost local]# mv jdk-8u291-linux-x64.tar.gz /usr/local/douzone```  

```[root@localhost local]# gzip -d jdk-8u291-linux-x64.tar.gz ```  

```[root@localhost local]# tar -xvf jdk-8u291-linux-x64.tar ``` 

링크해주기  
(자바 버전 바꿔도 환경설정 바꿀 필요 없어짐 : 환경설정에선 링크이름으로 해놓으면됨 )

```[root@localhost douzone]# ln -s 파일명 링크할이름 ```  
- 파일명  : jdk1.8.0_291  
링크할 이름 : java

링크 확인하기
ls -l

링크파일 지우는것  
rm -fr jdk1.8.0_291  

## 3. 환경 설정하기

```[root@localhost ~]# vi /etc/profile```

1. 설정하기
	```
	#java
	export JAVA_HOME=/usr/local/douzone/java
	export PATH=$PATH:$JAVA_HOME/bin
	export CLASSPATH=.:$JAVA_HOME/lib/tools.jar

	```
	-	$PATH: 앞에거 받아줘야함(앞에 설정들무시하면안됨)  
		export : 환경변수설정할때 자식에게 변수 세팅해주는것 = 자바실행시 클래스들 찾는것

2. 설정 적용하기  
```[root@localhost ~]# source /etc/profile```


## 4. 설치 됐는지 확인하기
자바 버전 확인하기  
```[desktop_01@localhost douzone]$ java -version```  
```[desktop_01@localhost douzone]$ javac -version```


다른 확인방법  
```[root@localhost src]# cd /usr/local/douzone/jdk1.8.0_291/bin```

```[desktop_01@localhost bin]$ ./java -version```

결과

![image](https://user-images.githubusercontent.com/60701130/154252886-ea87fcc6-747d-4bbb-aca3-93969d47207d.png)


## 5. 최종 자바 컴파일 후 확인해보기

/root에서  
```[root@localhost /]# mkdir dowork```
```[root@localhost /]# vi HelloWorld.java ```  

```
public class HelloWorld {
        public static void main(String[] args) {
                System.out.println("자바 설치완료");
        }
}
```

컴파일  
```[root@localhost dowork]# javac HelloWorld.java```

실행  
```[root@localhost dowork]# java HelloWorld```

결과  
![image](https://user-images.githubusercontent.com/60701130/154255580-d4938aa4-bfbd-4083-96c8-95508ad9196a.png)
