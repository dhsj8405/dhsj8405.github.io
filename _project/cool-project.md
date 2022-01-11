---
layout: project_single
encoding: utf-8
title:  "0906 �ڹ� ����ȯ�� ���� �� �� Ǫ�� (+ maven ��Ƽ������Ʈ����)"
slug: "cool-project"
---
**# 1.����**
# �˰������� ���ϰ� ������
��������Ʈ ������ �ҹ��� (�߿��� ���� !)
����Ű�� ����: �ҹ��� (ȸ�� �̸��� �Ųٷ�)(com.douzone.������Ʈ����)
��javac���� ��ġ
C:\Program Files\Java\jdk1.8.0_301\bin

# �ڹ� �������
 ## 1. jar
src (.java����)�� �������ϸ� class  �װ� ��Ű¡�ϸ� jar
scr(java, ��Ű��)   scr������ �������� ���
 = ���� (build)

 ## 2. war 
web �� class���� war�� ������� (jar���� Ŭ������ html,css �� �߰�)

# build tool ����
ant
maven * ���� �� ���� 
gradle

# java perspective ��õ
1. ���Ҷ� javaee
2. �ܼ� java
# ���̺귯�� �����
project�� property - java build path - library�� ���
# Native project
 ## 1. ��Ŭ���� Native project
  ### ����
/helloworld[Eclipse Native Project]
	---- src 
	---- bin
	---- .project
	---- .classpath
	---- /.settings

�������ϸ� src�� com/douzone�� bin �������� ����鼭 H.class ������ 4:42
����꿡 ���� bin, .project, .classpath, /.settings�� �ø��� �ȵ�
( �ذ�� : build tool�� �ذ� 
   = maven������Ʈ�� .gitignore����
   = ���� ������� ����� 3������ )
build tool�� Native intellij�� eclipsed�� ȣȯ�� ��������

#  �� ���� ���
push
���÷������丮���� ����꿡 �ø��°�
pull
����꿡�� �������°� ( ���� �귣ġ�� �ڵ����� ����)
fetch
����꿡�� �������°� ( ���� �귣ġ�� �ڵ� ���� x)

 ## 2. Intellij Native project
  ### ����
/helloworld[Intellij Native Project]	����Ƽ�� ��Ŭ���� ���丮�� ȣȯ�� �ȵ�
	---- /.idea	
	---- src
	---- traget

maven���� ����
src/main/java
src/text/java
src/main/resource
pom.xml
maven�� ��Ŭ������ ���ڸ����̿�  ����Ʈ�ϸ� ȣȯ��


**# 2.����**



# ����ȯ�汸��
# 1.ȯ�溯�� ����
�� ��ǻ�� - �ý��ۼӼ� - ��� �ý��� ���� - ȯ�溯�� - �ý��� ������ path ���� - ���θ���� - jdk������ bin���� ��� �ֱ�
# 2.��Ŭ���� ��� �ؾ��ϴ� ����
1. window - preferences - encoding �˻� - content Types - text�ȿ� java properties file ���� ���� ������ defalut encoding �� UTF-8������Ʈ���ֱ� 
2. window - preferences - encoding- general - workspace �ǹؿ� other - utf-8 ����(Text file encoding)
3. window - preferences - encoding�� web,xml ������ files�� ���ڵ���� utf-8�ιٲٱ�
4. window - preferences - spelling �˻��ؼ� spelling ���� üũ ���ֱ� (Enable spell checking)
5. window - preferences - java - installed JREs  add �ؼ� jdk �츮�ɷιٲ��ֱ� 


# maven ��Ƽ ��� ������Ʈ ����¹�
 ## 1. maven ������Ʈ �θ����
/parent(������Ʈ)
	---- child1(���)	��Ⱓ ���̺귯�� ������ ������
	---- child2


 ## 2. ����
file -new - project - maven - maven prject - create a simple project(üũ) - next
ex)
group id : com.douzone
artifact id : javastudy
packaging�� pom üũ (�θ� ���� �ž��ϱ� ����)
* �θ�� src ���� ��� �� (�����ϱ�)


 ## 3. maven ������Ʈ ���
maven�� �ٲٰ��� update maven project ������� (����Ű : Alt F5)

 ## 4. maven ������ ���̺귯�� �����ϴ� ���
���ۿ� maven mariadb jdbc ġ�� �ҽ� �����ؼ� pom�� dependencies �±� ���̿� �ٿ��ֱ� 
  ### ������Ʈ �� �ٿ�ε�� ���̺귯����ġ
C:/�����/user/.m2/repository


## 5. maven���� ������Ʈ�����ϱ� (�����ϴ°�)
pom.xml�����ʹ�ư - run as - maven build 



 ## 6. �ڽ� ��� ����� ���
�ڽ��� ������Ʈ �߰� ���̺� ������
��Ƽ ����� ���� ������Ʈ ��Ŭ�� - new -project- Maven - MavenProject
create a simple project üũ -������ (ex:project1) next
ex)
group id : com.douzone

# ���� ������� ����� 
 ## 1. GitHub ����Ҹ� ���� ����ҷ� ���

git init
git add -A
git commit -m "first commit"
git branch -M main
git remote add origin github.com/dhsj8405
git push -u origin main

������Ʈ ������ Ŭ�� team - share project ���� Use or create repository in parent folder of project, (Create Repository ������ )���� ���� üũ
 ## 2. git ������ġ Ȯ�ο� git perspective �����ϱ�(git repository)
window - show view - other - git - git repositories ����
* local �������丮 = .git ���丮 

��������Ҹ����
�� repository�� javastudy ���� Remotes ������ Ŭ�� create remote - ok - change - �� ��ũ �ּ� �ְ� Authentication�� ���� ������̸�, ��й�ȣ �Է�

 ## 3. gitignore ���� (���� ����ҿ� �������� ���ƾߵǴ� ���� �������ִ� ��)
�׺�����Ϳ� javastudy(maven������Ʈ) ������Ŭ�� ���ϻ��� �����̸� .gitignore 
���Ͼȿ� ** �� ��� ���丮��� ��


 ## 4. Ŀ��,Ǫ���ϴ¹��1 (���� �ð��� �ȵż� 2�� ������� ����)

javastudy �ֻ��� ���丮 ������Ŭ�� team -commit
- Unstaged changes ��� ���� �����ؼ� staged changes�� �ٿ��ְ�
commit message�� �ֿ� Ű���� �� , �������� ����
- commit and push

* Ǫ���� �� �α��� ���� ���� �߻�
  ### �ذ��� 1 ���� ( cmd���� ��������� �����ϰ� ���� �ο�)
cmdâ���� javastudy �������� �̵���
git add -A ��ɾ� ġ��
git branch -M main
git remote add origin http~~~
git push -u origin main
ġ���� sign in with your browser ������
autorize �����ϱ�
(�� ��ɾ�� repository ó�� �������� �� ���ο� ��������)
  ### �ذ��� 2 ����
�� ��ġ
cmd���� 
git
git config --global user.name "dhsj8405"
git config --global user.email dhsj8405@naver.com
������� �������ֱ�


 ## 5. Ŀ��,Ǫ���ϴ� ���2(��Ŭ���� �͹̳η� �� Ǫ���ϱ�)
C:\douzone2021\eclipse-workspace\javastudy ��η� �ű��
git add -A
git commit -m '..'           (..�� �ֿ� Ű���� �� , �������� ����)
git push