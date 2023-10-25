# 1.What is Obsidian? #obsidian_define
- - -


	1-1. obsidian
		- Markdown 언어를 활용하여서 문서를 관리하거나 연결 할 수 있는 프로그램

	1-2. obsidian의 장-단점
		1. 제텔카스텐을 구현하기 좋음
			1-2. 백링크로 쉽게 확장하고 연결된다
			1-3. 그래프 뷰를 통한 확장을 확인 할 수 있으며 열람이 매우 쉬움
		2. "무료"임
			2-1. 웹 퍼블리싱은 유료임 => 하지만 플러그인으로 유사하게 지원이 가능
		3. 매우 빠른 속도와 안정적인 보안성 그리고 다양한 플랫폼과 동기화가 가능함



# 2. How to use Obsidian #obsidian_use 
- - -

- 기본적으로 Markdown 언어를 따라간다. 자세한 마크 다운 언어를 모른다면, 
	정의 : [[markDown#1. What is MarkDown? markdown_define]]
	사용법 : [[markDown#2. How to use MarkDown markdown_use]]
<br/>
- 글쓰기의 방법은 제텔카스텐의 방법을 따라가면 좋을 듯 하다.
	사용법 : [[zettelkasten#1. 형식 zettelkasten_use]]
<br />

- #### 추가적인 정보

	1. 체크 박스
		- " - [ ]"를 통하여 체크 박스를 만들 수 있음.
```
- [ ] title1
- [ ] title2
- [ ] title3
- [ ] title4
- [ ] title5
```
<br />

- #### 그래프 뷰

	1. 로컬 그래프 뷰
		- 해당 작성중인 문서의 연결된 링크들을 연결되어서 간단하게 보여주는 것이다. 
		- 모든 파일을 보여주지 않는 다는 점이 특징임.
		- 이미 있는 링크를 연결하는 방법 "[[]]" 이렇게 감싸면 된다.


	2. 전체 그래프 뷰
		- 해당 root의 문서 하위 모든 md파일을 모아 그래프로 만든다.
		- 모든 파일을 보여준다는 점이 특징이며, 설정에 따라서 더 많은 파일들을 보여줄 때도 있다.


	3. 이용 방법
		- filter를 이용한 파일을 구분할 수 있음,
		- group기능을 이용해서 관련되어있는 파일들의 색을 지정할 수 있음.
<br/>

- #### 링크 연결

1. 일반적인 링크 연결
```
[[exampleFileName]]
```


2. 파일 내의 링크 연결
```
[[exampleFileName#TagName]]
```

3. 문단 단위의 링크 연결
```
[[exampleFileName^TitleText]]
```

4. 메모 링크
```
![[exampleMemoName]]
```
<br />

- #### 주석
```
Obsidian[^id]

- - -
[^id] : example
```
<br />

- 이미지 조정
```
![[exampleFileName|width]]
```
<br />

- #### 표 만들기
```
|언어|C|C++|Java|JavaScript|
|----|----|----|----|----|
|달성도|50|30|20|50|
```
<br />

- 이중 인용
```
>> 응애
```