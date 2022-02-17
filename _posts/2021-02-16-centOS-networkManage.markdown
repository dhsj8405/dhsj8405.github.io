---

layout: post
title: '[centOS]Linux 네트워크 관리 및 설정(고정IP설정)'
subtitle: '[centOS]Linux 네트워크 관리 및 설정(고정IP설정)'
categories: devlog
tags: server
comments: true

---

# 리눅스 네트워크관리 및 설정

## 네트워크 관리 기본 명령어

ping : 
ping 명령을 이용하면 다름 시스템의 네트워크가 현재 동작 중인지 알 수가 있다.

- 사용법  
	```ping [옵션] 호스트```

	옵션  
	-s : 패킷 사이즈를 지정한다.  
	-q : 종합 결과만 보여준다.  
	-i  : 지연시간을 설정한다.  
	-c : 보낼 패킷 수를 지정해 준다.  

	옵션 없이 사용하면 계속 패킷 보냄  
	Ctrl + C 로 중지

	<span style = "color:red">ping 명령어는 상대 호스트 또는 자신이 정상적으로 네트워크 작동을 하는 지 확인하는 데 아주 유용하게 쓰인다.</span>  
	하지만 과도하게 사용하면 서버에 부담을 줄 수 있다.

	ping 응답을 막는 설정  
	```#vi /etc/sysctl.conf```
	```
	# For more information, see sysctl.conf(5) and sysctl.d(5).

	net.ipv4.icmp_echo_ignore_all=1

	```
	확인  
	![image](https://user-images.githubusercontent.com/60701130/154268007-0c598484-1db4-47e1-b1d0-bc3c93faeb01.png)


nslookup : 
nslookup은 도메인 네임서버에 질의를 할 수 있는 명령어 이다. 도메인 이름의 호스트의 IP주소를 검색할 수 있고 네임서버가 올바르게 작동하는 지 확인 할 수도 있다.

- 사용법  
	```nslookup [도메인]```

	도메인을 입력하지 않으면 대화형으로 프로그램이 작동한다.

hostname : 
호스트네임을 화면에 출력하고, 호스트네임을 변경할 수 있다.

- 사용법  
```hostname```  

	결과
	![image](https://user-images.githubusercontent.com/60701130/154268606-4646e1fb-a3e8-4711-8298-1175304068e8.png)



	호스트 명 변경  
	```vi /etc/hostname ```
	```
	lx.kickscar.com
	```

	결과(반영하기 위해서 재부팅)  
	![image](https://user-images.githubusercontent.com/60701130/154268683-2dfaac0d-d512-429b-a44d-1b682fec9273.png)
	
	centos ssh서버 아예 껐다 켜야함


netstat : 
네트워크 연결, 라우팅 테이블, 네트워크 장치의 통계정보 등 네트워크에 관련된 여러가지 정보를 확인할 수 있다.

- 사용법  
	netstat [옵션]

	옵션  
	-a : 연결된 모든 소켓을 출력한다.  
	-n : 호스트, 포트등의 정보를 이름대신 숫자로 표시한다.  
	-p : 소켓을 열고 있는 프로세스의 아이디(PID) 를 출력한다.  
	-r  : 라우팅 테이블을 출력한다.  
	-t  : TCP 연결에 대한 소켓을 출력한다.  
	-u : UDP 연결에 대한 소켓을 출력한다.  

ifconfig : 
네트워크 인터페이스를 설정하고, 현재 네트워크 인터페이스의 정보를 알아보는 명령어이다.
대부분 네트워크 서정을 확인하는 명령어로 많이 사용된다.

- 사용법  
```ifconfig [옵션]```

## 네트워크 설정하기 (고정 아이피 설정)
ifconfig 에서 설정된 IP 주소는 시스템이 재 시작하게 되면 반영이 되지 못한다. 따라서 시스템의 네트워크를 설정에서 영구적으로 반영 되도록 해야 한다. 

### 1. 설정하기 전에 알아두어 야 할 것  
- IP Address  
		```ifconfig```로 확인 가능  
- Subnet Mask  
		```ifconfig```로 확인 가능  
- Gateway IP Address  
		IP Address에서 마지막 자리만 1로 바꿔주면됨  
		
		ex)    
		IP Address : 192.168.10.24  
		Gateway IP Address : 192.168.10.1

- DNS Server IP Address  
		cmd(window + r 키)에서 확인가능  
		![image](https://user-images.githubusercontent.com/60701130/154276733-03e0d2dc-f1da-4b68-a9d1-1a0aae876f51.png)  
		(Address : DNS Server IP Address)



### 2. 현재 설정 확인하기

```[사용자@lx ~]$ cat /etc/sysconfig/network-scripts/ifcfg-인터페이스네임```
- 인터페이스네임: ifconfig로 확인가능 (enp0s3)

### 3. 설정하기

```
BOOTPPROTO= "dhcp"
```
- dynamic 하게 dhcp 서버로 부터 IP 주소와 게이웨이 IP 주소 Subnet Mask, DNS 서버 IP 정보를 받아와 세팅하게 된다.

이렇게 바꾸기
![image](https://user-images.githubusercontent.com/60701130/154280979-49cdf51c-0d8d-4789-9b5d-ca2a79a6d95c.png)


### 4. 적용하기

네트워크 다시 시작  
```[root@lx network-scripts]# systemctl restart network.service```

### 5. 확인하기
```ifconfig```