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

파라미터화라는 말은 인스턴스 생성시 **설정을** 한다는 의미이다.  
파라미터화할 때는 아래 형식으로 지정한다.

~~~
클래스명[타입](값) 
~~~
		
Array[String]은 영어로 array of string 이라서 어순과 코드순서가 동일하다.  

예제코드(추천하는 방식은 아니다)   

~~~
val greetStrings = new Array[String](3)  
greetStrings(0) = "Hello"
greetStrings(1) = ", "
greetStrings(2) = "world!\n"
~~~

~~~		
		for ( i <- 0 to 2)
			print(greetStrings(i))
~~~			
			
배열은 아래같이 추론엇이 명시적 타입을 지정이 가능하다.   
~~~
		val greetStrings: Array[String] = new Array[String](3)
~~~		
스칼라는 ()를 넣어서 배열 원소를 접근한다. 자바,C처럼 각괄호([])를 사용하지 않는다.  
~~~
		greetStrings(0) // okay~!
		greetStrings[0] // Error~!
~~~	
		
객체가 Val일 경우 greetStrings 에는 다른 변수를 넣을 수 없지만 배열 자체는 변경 가능하다.  

~~~
		for ( i <- 0 to 2 )
				print(greetStrings(i))
~~~

메소드의 파라미터가 1개일 경우는 점(.)과 괄호없이 호출이 가능하고 내부적으로 아래처럼 사용된다.
~~~
	for ( i<- (0).to(2) )
~~~	
	
스칼라는 연산자 오버로드를 제공하지 않고, 연사자라는 것이 없다.   
대신 +,-,*,/ 등을 메소드명으로 사용이 가능하다.
~~~
		1 + 2는 (1).+(2)처럼 +라는 메소드를 2를 인자로 호출한 것이다.
~~~		
### 왜 배열을 괄호로 사용해 접근하는가?
스칼라는 배열뒤 ()를 싸서 호출하면 apply라는 메소드를 호출하는 것으로 바꾼다.  
~~~
		greetStrings(i) 
~~~		
는 다음과 같이 변환한다.
~~~
		greeetStrings.apply(i)
~~~
할당하는 표현식도 마찬가지다.
~~~
		greetStrings(0) = "Hello"
~~~	
는 아래와 동일하다.	
~~~
		greetStrings.upate(0, "Hello")	
~~~
배열도 마찬가지다.
~~~
		val numNames = Array("Zero", "one", "two")
~~~
		
는 아래와 동일하다.
~~~
		val numNames = Array.apply("Zero", "one", "two")
~~~


	

## 리스트를 사용해보자

변경 불가능한 시퀀스를 위해서는 리스트!
리스트 변경하는 것 같은 메소드는 **변경안하고 새 값 갖는 리스트를 생성해서 리턴**한다.  

두 리스트를 잇기  

		':::'

리스트 맨 앞에 추가해 새 리스트를 반환하기  

		'::': 콘즈(cons)  

리스트 뒤에 추가해 새 리스트 반환하기  

		':+' 


빈 리스트 만들기 또는 ::로 초기화하기

		val oneTwoThree = 1 :: 2 :: 3 :: Nil
		
> ::로 초기화 시는 반드시 Nil를 반드시 넣어야한다. 컴파일에러
 


## 튜플을 사용해보자
변경은 불가능!  
다른 타입의 원소를 넣을 수 있다!

~~~
val pair = (99, "수학점수")
println(pair._1)
println(pair._2)
~~~

튜플은 인덱스가 1부터 시작한다.(swift는 0부터)  
멀티 리턴값을 위해 새로운 클래스를 만들어 넘길 필요가 없다.



## 집합과 맵을 사용해보자
변경 가능한 것과 변경 불가능한 것 모두 제공한다.
집합, 맵 모두 디폴트가 변경 불가능한 것

### 집합(Set)

#### immutable Set
~~~
var jetSet = Set("Boeing", "Airbus")
jetSet += "Lear"
~~~

jetSet += "Lear"는 jetSet = jetSet + "Lear"의 축약 코드이다.  
"Lear"라는 새 원소가 들어 있는 새로운 Set를 재할당하는 방식으로 처리한다.

#### mutable Set
변경 가능한 집합을 쓰려면 아래 import 문을 사용한다.  
import scala.collection.mutable.Set

~~~
val movieSet = Set("Hitch", "Poltergeist")
movieSet += "Shrek"
~~~

movieSet += "Shrek"은 새 Set를 재할당한 것이 아니라 movieSet.+=("Shrek")의 축약된 코드이다.


### 맵

#### mutable map

~~~
import scala.colleciton.mutable.Map

val treasureMap = Map[Int, String]()
treasureMap += (1 -> "Go to island")
~~~

1 -> "Go to island"는 (1).->("Go to island")와 같다.  
> 1이라는 정소에 들어잇는 ->라는 메소드를 "Go to island"를 인자로 호출하는 것이다.


#### immutable map

~~~
val romanNumeral = Map ( 1 -> "I", 2 -> "II" )

~~~

## 함수형 스타일을 인식하는 법을 배우자

~~~
def printArgs(args: Array[String]): Unit = {
    var i = 0
    while (i < args.length) {
      println(args(i))
      i += 1
    }
  }
~~~

간단하게 만들자

~~~
 def printArgs(args: Array[String]): Unit = {
    for (arg <- args)
      println(arg)
  }
~~~
또는,
~~~
def printArgs(args: Array[String]): Unit = {
    args.foreach(println)
  }
~~~

> 코드가 더 명확하고 간결하다
> 오류 가능성이 낮다.

* 수정해야할 점
    * 표준 출력 스트림에 글자를 찍는 side effect가 있다.

* 부수효과(side effect) 존재 여부를 아는 지표

~~~
    결과 타입이 Unit인가하는 점이다.  
    어떤 함수가 관심의 대상이 될 만한 값을 리턴하지 않는다면 주변에 영향을 미칠 수 있는 방법은 side effect밖에 없다.
~~~


#### 부수 효과가 없는 함수를 만들자
~~~
   def formatArgs(args: Array[String]) = args.mkString("\n")
~~~

##### mkString?
* 이터러블(배열, 리스트, 집합, 맵 등)에 호출 가능하다.  
* toString을 각 원소에 호출해 얻은 문자열에 인자를 추가한 문자열을 반환한다.

~~~
  println(formatArgs(args))
~~~

부수효과없는 새로운 함수의 이점은 **프로그램을 테스트하기가 쉽다**는 것이다.

~~~
  val res = formatArgs(Array("zero", "one", "two"))
  assert(res == "zero\none\ntwo")
~~~



## 파일의 내용을 줄 단위로 읽자
~~~
import scala.io.Source
  
    if (args.length > 0) {
  
      for (line <- Source.fromFile(args(0)).getLines)
        print(line.length +" "+ line)
    }
    else
      Console.err.println("Please enter filename")
~~~

getLines 메소드는 Iterator[String]을 반환한다.


모든 줄의 문자 개수를 형식에 맞게 출력하기

~~~
    import scala.io.Source
  
    def widthOfLength(s: String) = s.length.toString.length
  
    if (args.length > 0) {
  
      val lines = Source.fromFile(args(0)).getLines.toList // toList Iterator말고 List가 필요해서
  
      val longestLine = lines.reduceLeft(
        (a, b) => if (a.length > b.length) a else b 
      ) 
      val maxWidth = widthOfLength(longestLine)
  
      for (line <- lines) {
        val numSpaces = maxWidth - widthOfLength(line)
        val padding = " " * numSpaces
        print(padding + line.length +" | "+ line)
      }
    }
    else
      Console.err.println("Please enter filename")
~~~


끝.