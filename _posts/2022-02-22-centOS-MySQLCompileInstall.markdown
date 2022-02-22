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

11. 설정파일 위치 변경  
`cp -R /usr/local/douzone/mariadb/etc/my.cnf.d /etc`

12. 기본(관리) 데이터베이스(mysql) 생성  
`/usr/local/douzone/mariadb/scripts/mysql_install_db --user=mysql --basedir=/usr/local/douzone/mariadb --defaults-file=/usr/local/douzone/mariadb/etc/my.cnf --datadir=/usr/local/douzone/mariadb/data`

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

