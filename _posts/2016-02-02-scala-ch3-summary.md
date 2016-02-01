---
layout: post
title: "scala ch3 summary"
description: ""
category: 
tags: [scala]
---
{% include JB/setup %}

# 3장

## 배열타입에 파라미터를 지정하자.

* 파라미터화라는 말은 인스턴스 생성시 설정한다는 의미이다.


* 예제코드


		val greetStrings = new Array[String](3)  
		val greetStrings: Array[String] = new Array[String](3)
		
		greetStrings(0) // okay~!
		greetStrings[0] // Error~!
		
> 객체가 Val일 경우
> greetStrings 에는 다른 변수를 넣을 수 없지만 배열 자체는 변경 가능하다.
> 

		for ( i <- 0 to 2 ) // == for ( i <- (0).to(2) ) 와 동일
			print(greetStrings(i))
> 스칼라는 연산자 오버로드를 제공 안함.
> +,-,*,/ 등을 메소드명으로 사용이 가능함.
> 

	

## 리스트를 사용해보자

변경 불가능한 시퀀스를 위해서는 리스트!
리스트 변경하는 것 같은 메소드는 **변경안하고 새 값 갖는 리스트를 생성해서 리턴**한다.  

두 리스트를 잇기  
':::' (이름모름)  

리스트 맨 앞에 추가해 새 리스트를 반환하기  
'::': 콘즈(cons)  

리스트 뒤에 추가해 새 리스트 반환하기  
':+' (이름없음)





## 튜플을 사용해보자
변경은 불가능!
다른 타입의 원소를 넣을 수 있다!

val pair = (99, "수학점수")
println(pair._1)
println(pair._2)

튜플은 인덱스가 1부터 시작한다.(swift는 0부터)
멀티 리턴값을 만들 수 있다.





## 집합과 맵을 사용해보자

## 함수형 스타일을 인식하는 법을 배우자

## 파일의 내용을 줄 단위로 읽자


	


 
 	

  
  
  
  
