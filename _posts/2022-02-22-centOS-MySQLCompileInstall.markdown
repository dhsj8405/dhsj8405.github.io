---

layout: post
title: '[centOS]Linux에 MySQL 컴파일설치'
subtitle: '[centOS]Linux에 MySQL 컴파일설치'
categories: devlog
tags: centOS
comments: true

---


# 컴파일 설치

1. 유저 생성(계정 생성)


	Root는 모든 권한이 있기 때문에 Root 계정으로 MySQL을 실행하는 것은 보안상 좋지않음


	`groupadd mysql`  	// mysql 그룹 생성  
	`useradd -M -g mysql mysql`  //mysql 그룹에 속하며 홈 디렉터리가 없는 mysql 계정을 생성  
	`cat /etc/passwd`  		//유저 생성 여부 확인  

	mysql 그룹을 생성한 뒤, mysql 그룹에 속하며 홈 디렉터리가 없는 mysql 계정을 생성합니다.

	그리고 /etc/passwd 파일을 출력하여 유저가 생성되었는지 확인합니다.

2. 의존성 설치  
`yum install -y gcc`  
`yum install -y gcc-c++`  
`yum install -y gcc-c++`  
`yum install -y gdbm-devel`  
`yum install -y zlib*`  
`yum install -y libxml*`  
`yum install -y freetype*`  
`yum install -y libpng*`  
`yum install -y flex`  
`yum install -y gmp`  
`yum install -y ncurses-devel`  
`yum install -y cmake.x86_64`  
`yum install -y libaio `  

3. 소스 다운로드  
`wget https://downloads.mariadb.org/interstitial/mariadb-10.1.48/source/mariadb-10.1.48.tar.gz`  

4. 압축 풀기  
`tar xvfz mariadb-10.1.48.tar.gz`

5. 폴더 이동
`mv mariadb-10.1.48.tar.gz /usr/local/douzone`

6. 링크 하기  
`ln -s mariadb-10.1.48 mariadb`

7. 빌드 환경 설정
`cmake -DCMAKE_INSTALL_PREFIX=/usr/local/douzone/mariadb -DMYSQL_USER=mysql -DMYSQL_TCP_PORT=3307 -DMYSQL_DATADIR=/usr/local/douzone/mariadb/data -DMYSQL_UNIX_ADDR=/usr/local/douzone/mariadb/tmp/mariadb.sock -DINSTALL_SYSCONFDIR=/usr/local/douzone/mariadb/etc -DINSTALL_SYSCONF2DIR=/usr/local/douzone/mariadb/etc/my.cnf.d -DDEFAULT_CHARSET=utf8 -DDEFAULT_COLLATION=utf8_general_ci -DWITH_EXTRA_CHARSETS=all -DWITH_ARIA_STORAGE_ENGINE=1 -DWITH_XTRADB_STORAGE_ENGINE=1 -DWITH_ARCHIVE_STORAGE_ENGINE=1 -DWITH_INNOBASE_STORAGE_ENGINE=1 -DWITH_PARTITION_STORAGE_ENGINE=1 -DWITH_BLACKHOLE_STORAGE_ENGINE=1 -DWITH_FEDERATEDX_STORAGE_ENGINE=1 -DWITH_PERFSCHEMA_STORAGE_ENGINE=1 -DWITH_READLINE=1 -DWITH_SSL=bundled -DWITH_ZLIB=system`

8. 빌드  (꽤 오래걸림)  
`make`  

9. 설치  
`make install`  

10. 인스톨 디렉토리 /mariadb 소유자 변경  
`chown -R mysql:mysql /usr/local/douzone/mariadb`

- mysql 데몬을 뛰우기 전에 소켓 만드는 것을 root가 하기 때문에 tmp 디렉터리의 group 소유권은 root로 변경합니다.  
`chown mysql:root /usr/local/douzone/mariadb/tmp`
	
- 변경확인
	ls -l /usr/local/douzone/



11. 설정파일 위치 변경  
`cp -R /usr/local/douzone/mariadb/etc/my.cnf.d /etc`

12. 기본(관리) 데이터베이스(mysql) 생성  
`/usr/local/douzone/mariadb/scripts/mysql_install_db --user=mysql --basedir=/usr/local/douzone/mariadb --defaults-file=/usr/local/douzone/mariadb/etc/my.cnf --datadir=/usr/local/douzone/mariadb/data`

- mysql 환경설정  
	`vi /etc/my.cnf`
	```
	# Example MySQL config file for large systems.
	#
	# This is for a large system with memory = 512M where the system runs mainly
	# MySQL.
	#
	# MySQL programs look for option files in a set of
	# locations which depend on the deployment platform.
	# You can copy this option file to one of those
	# locations. For information about these locations, see:
	# http://dev.mysql.com/doc/mysql/en/option-files.html
	#
	# In this file, you can use all long options that a program supports.
	# If you want to know which options a program supports, run the program
	# with the "--help" option.

	# The following options will be passed to all MySQL clients
	[client]
	port            = 3306
	socket         = /usr/local/douzone/mariadb/tmp/mysql.sock
	character-set   = utf8

	# Here follows entries for some specific programs

	# The MySQL server
	[mysqld]
	port            = 3306
	socket         = /usr/local/douzone/mariadb/tmp/mysql.sock
	key_buffer_size = 256M
	max_allowed_packet = 1M
	table_open_cache = 256
	sort_buffer_size = 1M
	read_buffer_size = 1M
	read_rnd_buffer_size = 4M
	myisam_sort_buffer_size = 64M
	thread_cache_size = 8
	query_cache_size= 16M
	# Try number of CPU's*2 for thread_concurrency
	thread_concurrency = 8

	character-set-server=utf8
	collation-server=utf8_general_ci

	init_connect=SET collation_connection=utf8_general_ci
	init_connect=SET NAMES utf8

	[mysqldump]
	quick
	max_allowed_packet = 16M

	[mysql]
	no-auto-rehash
	default-character-set = utf8
	# Remove the next comment character if you are not familiar with SQL
	#safe-updates

	[myisamchk]
	key_buffer_size = 128M
	sort_buffer_size = 128M
	read_buffer = 2M
	write_buffer = 2M

	[mysqlhotcopy]
	interactive-timeout
	```
13. 서버 구동   
서비스 등록안하면 매번 입력해야함(실행시 아무것도 입력안되기도함 서비스등록하는거 추천)  
`/usr/local/douzone/mariadb/bin/mysqld_safe &`

14. root 패스워드 설정
`/usr/local/douzone/mariadb/bin/mysqladmin -u root password`

15. 데이터베이스 접속 테스트
`/usr/local/douzone/mariadb/bin/mysql -u root -p`

16. path 설정(/etc/profile)  
`vi /etc/profile`  
맨밑에 추가하기  
	```
	# mysql
	export PATH=$PATH:/usr/local/douzone/mariadb/bin
	```

17. 서비스등록  
1) 켜져있는 mariadb 서버 죽이기  
 	ps -ef |grep mysql 로 PID 확인하기
	
	![image](https://user-images.githubusercontent.com/60701130/155153637-3f07e336-4968-41c1-a4cd-5852dbc4e5cb.png)
	mysql의 pid번호가 4자리씩 두개인데 뒤에 번호를 먼저 kill하고 앞의 pid번호를 kill해야 서버가 죽음    
	앞에 pid번호를 먼저 kill 해봤는데 새로운 pid번호가 다시 생성됨  
	`kill -9 1480`  
	`kill -9 1660`  

2) 서비스 등록하기    
	`vi /usr/lib/systemd/system/mysql.service`  
	
	```
	[Unit]  
	Description=MySQL Community Server  
	After=network.target  
	After=syslog.target  

	[Install]  
	WantedBy=multi-user.target  
	Alias=mysql.service  

	[Service]  
	User=mysql  
	Group=mysql  

	# Execute pre and post scripts as root
	PermissionsStartOnly=true

	# Needed to create system tables etc.
	#ExecStartPre=

	# Start main service
	ExecStart=/usr/local/douzone/mariadb/bin/mysqld_safe

	# Don't signal startup success before a ping works
	#ExecStartPost=

	# Give up if ping don't get an answer
	TimeoutSec=300

	Restart=always
	PrivateTmp=false
	```

3) 등록 확인  
	(1) mysql 서버 구동  
	`systemctl enable mysql.service`  
	`systemctl start mysql.service`  
	`ps -ef | grep mysql`    

	(2) mysql 끄고 리부트했을 때 켜지는지 확인  
	`systemctl stop mysql.service`  
	`reboot`  
	`ps -ef | grep mysql`  


# 리눅스에서 mysql 접속하기  
`mysql -p`
