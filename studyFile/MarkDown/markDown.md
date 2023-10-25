# 1. What is MarkDown? #markdown_define
-----------------------

	1-1. markdown
	- Markdown은 텍스트 기반의 마크업 언어로 쉽게 쓰고 읽을 수 있으며, html로 변환이 가능하다. 특수 기호와 문자를 이용한 매우 간단한 구조의 문법을 사용하여 웹에서도 보다 빠르게 컨텐츠를 작성할 수 있으며, 보다 직관적으로 인식할 수 있다. 마크 다운 언어를 통해서 설치 방법, 소스코드에 대한 설명과 이슈 등을 간단하게 설명하고 가독성을 올릴 수 있다는 강점이 부각된다.


	1-2. 마크 다운의 장-단점
		1. 별도의 도구 없이 사용이 가능한 편의성과 간결함을 가지고 있음.
		2. 다양한 형태로 변환이 가능함. (Ex. html)
		3. 텍스트로 저장되기 때문에 용량이 적어 보관이 용이함.
		4. 텍스트 파일이기 때문에 용량이 매우 적음, 보관이 매우 용이
		5. 텍스트 파일이므로 버전 관리 시스템을 이용하여 변경 이력을 관리할 수 있음.
		6. 지원하는 프로그램과 플랫폼이 다양함 (Ex. obsidian)


# 2. How to use MarkDown #markdown_use
--------------------------------------------------------

2-1. 글자 강조
---------

- 큰 제목 : 문서의 제목
```
this is Title of Doc
====================
```

- 작은 제목 : 문서의 부 제목
```
this is Sub Title of Doc
------------------------
```

- 글머리 : 글자 크기와 관련한 다른 형식
==주의 점 : "#" 이후 띄어쓰기가 반드시 있어야 함.==
```
# this is H1
## this is H2
### this is H3
#### this is H4
##### this is H5
###### this is H6
```

2-2. BlockQuote 
------------------

- 블럭 인용 문자인 ">"를 사용한다.
```
> this is a first blockqute.
> 	> this is a second blockqute.
> 	> 	> this is a third blockqute.
```


- 해당 인용문 안에서는 다른 마크 다운 요소를 포함 할 수 있다.
```
> this is a first blockqute.
>  - List
> 	 ```
> 	 code
> 	 ```
```

2-3. List
----------

#### 2-3-1. 순서가 있는 목록 ( number )
- 순서가 있는 목록은 숫자와 점을 사용한다.
- 순서를 섞어도 내림차순으로 정의된다.
```
1. first
2. second
3. third
```


#### 2-3-2. 순서가 없는 목록 ( ```*``` , ```+``` , ```-```  )

- 구체 형의 목록
```
- this is circle List
- one
- two
- three
```

- 다른 형식의 목록
```
+ this is circle List
* this is circle List too
```

2-4. Code
----------

- 4개의 공백 또는 하나의 탭으로 들여쓰기를 만나면 변환되기 시작하며, 들여 쓰지 않은 행을 만날 때까지 변환이 지속됨.

#### 2-4-1. 들여쓰기

	this is a nomal paragraph:
		this is a code block
	end code block.

#### 2-4-2. 코드 블럭

- 코드 블럭은 ```<pre><code>{example}</code></pre>``` 방식으로 이용이 가능함.

<pre>
<code>
	public class BootSpringBootApplication {
		public static void main(String[] args) {
			System.out.println("Hello, this is springBoot");
		}
	}
</code>
</pre>

- 다른 방식으로 ```"``````"``` 이것을 이용하여 감쌀 수 있다.

```
public class BootSpringBootApplication {
		public static void main(String[] args) {
			System.out.println("Hello, this is springBoot");
		}
	}
```



2.5 수평선 ```<hr />```
--------------

- 아래 예시는 모두 수평선을 만들 수 있는 형식이다.

```
* * *
***
*****
- - -
------------------------------------------------
```

2.6 링크
----------

- 참조 링크
```
[link keyword][id]

[id] : URL "Optional Title here"

//code
Link : [Google][googleLink]

[googleLink] : https://google.com "Go google"
```

- 외부 링크
```
[title](link | url)

Example : [go google](https://google.com)
```

- 자동 연결
```
<https://google.com>
<example@example.com>
```

- 옵시디언에서의 링크
```
[["LinkName"]]
```

2.7 강조
-----------

```
1. iteric font
	*single asterisks* 
	_single asterisks_
	
2. big font
	**double asterisks**
	__double asterisks__

3. font center line
	~~cancelline~~
```

2.8 이미지
--------

```
![Alt text](/path/to/img.jpg)
![Alt text](/path/to/img.jpg "Optional Title")
```

- 만약 사이즈 조절이 필요한 이미지라면 다음의 예시를 사용하면 된다
```
<img src="/path/to/img.jpg" width="450px" height="300px" />
<img src="/path/to/img.jpg" width="450px" height="300px" alt="Optional Title" />
```

Tstory