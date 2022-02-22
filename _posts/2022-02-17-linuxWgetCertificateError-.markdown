---

layout: post
title: '[centOS]Linux wget 사용시 증명서(certificate)에러'
subtitle: '[centOS]Linux wget 사용시 증명서(certificate)에러'
categories: devlog
tags: --- centOS
comments: true

---

# wget 사용시 증명서 문제

![image](https://user-images.githubusercontent.com/60701130/154402575-62c9fb8e-c1ba-4ffb-ac86-7213d01d9d71.png)

해결법
``` [root@lx /]# echo "check_certificate = off" >> ~/.wgetrc ```


wget 다시 실행
![image](https://user-images.githubusercontent.com/60701130/154402810-ee9d9121-4534-42bf-9463-796587ea6ffc.png)
