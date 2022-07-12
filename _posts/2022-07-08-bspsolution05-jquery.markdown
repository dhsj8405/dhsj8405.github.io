---

layout: post
title: 'bspsolution05 - jquery'
subtitle: 'bspsolution05 - jquery'
categories: devlog
tags: bspsolution
comments: true

---
# jquery

## DataTable column 간격 조절하기
$("#foo-table").DataTable({
	// 스크롤바 설정
	scrollX: true,
	scrollY: 200,

	// 열 넓이 설정
	columnDefs: [
		// 2번째 항목 넓이를 100px로 설정
		{ targets: 1, width: 100 }
	]
});