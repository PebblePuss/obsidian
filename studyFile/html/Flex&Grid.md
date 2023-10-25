> **CSS의 Flex와 Grid를 이해하기 위한 글임.**
>이 프로젝트는 flex와 grid에 대해서 이해하고, 어느 상황에서 flex grid를 사용해야되는지 알아보고 적절한 상황에 맞는 display를 부여할 수 있도록 하며, 뿐만 아니라 구조적 이해를 하기 위한 글이다.

<br/>

# Flex란 무엇일까?


![[Pasted image 20230910154155.png]]
레이아웃을 조금 더 편리하게 배치하기 위한 기능이며, 수직 형태의 블록 배치 방식보다 조금 더 유연한 배치를 지원하기 위해 고안된 배치 방식임.
<br/>

![[Pasted image 20230910155700.png]]
- Flex와 Float의 차이점은 높이가 다른 요소와 맞춰진다는 점이 차이점임.

## Flex의 구성 요소

![[Pasted image 20230910154315.png]]
- 각 위치에 따라서 적용되는 CSS의 속성이 다름.

- - -
### 1. Flex Container
가장 외부를 감싸고 있는 부모 Tag
Ex) justify-content, align-content(place-content), align-items
Ex) flex-direction[^1], flex-wrap[^2]

#### - Option

| 속성        | 설명                                 |
| ----------- | ------------------------------------ |
| flex        | 지정한 크기만큼 x축과 y축으로 이동함 |
| inline-flex | 지정한 크기만큼 x축으로 이동함       |

#### **Flex-direction과 flex-wrap을 같이 처리하기엔 귀찮다**
이때 사용할 수 있는 것이 flex-flow임.

```
flex-flow : <flex-direction> <flex-wrap>;
```

![[Pasted image 20230910160057.png]]


#### - justify-content Option

![[Pasted image 20230910161634.png]]

| 속성          | 설명                                                |
| ------------- | --------------------------------------------------- |
| flex-start    | 좌에서 우로 배치                                    |
| flex-end      | 우에서 좌로 배치                                    |
| center        | 중앙에 배치                                         |
| space-between | item들 사이의 균일한 간격을 만들어 가운데 배치      |
| space-around  | item 둘레와 균일한 간격을 만들어 배치               |
| space-evenly  | 아이템을 사이와 양 끝에 균일한 간격을 만들어서 배치 |

- space-between과 space-around, space-evenly의 차이를 보여주는 이미지

![[Pasted image 20230910161907.png]]

#### - align-items Option

![[Pasted image 20230910162710.png]]

| 속성       | 설명                                |
| ---------- | ----------------------------------- |
| stretch    | 기존 배치                           |
| flex-start | 위를 기준으로 배치                  |
| flex-end   | 아래를 기준으로 배치                |
| center     | 부모 Tag의 중앙을 기준으로 배치     |
| baseline   | content를 기준선을 잡아서 배치한다. |

- 부모 기준선의 중앙에 넣는 법
```
justify-content: center;
align-items : center;
```


#### - align-content Option

![[Pasted image 20230910163316.png]]

| 속성          | 설명                                                |
| ------------- | --------------------------------------------------- |
| stretch       | 기존 배치                                           |
| flex-start    | 위를 기준으로 배치                                  |
| flex-end      | 아래를 기준으로 배치                                |
| center        | 부모 Tag의 중앙을 기준으로 배치                     |
| space-between | 위 아래로 item들 사이에 균일한 간격을 만들어 배치   |
| space-around  | item들의 둘레에 균일한 간격을 만들어서 배치         |
| space-evenly  | item들의 사이와 양 끝에 균일한 간격을 만들어서 배치 |

- - -
### 2. Flex Item
Container의 안쪽을 담당하는 자식 Tag
Ex) align-self
Ex) flex-grow[^3], flex-shrink[^4], flex-basis[^5]

#### **Flex-grow와 flex-shrink, flex-basis을 같이 처리하기엔 귀찮다**
이때 사용 가능 한 것이 flex이다.
Ex) flex : (flex-grow) | (flex-shrink) | (flex-basis)

#### - align-items Option
Order : 아이템의 배치 순서를 바꾼다. ( 권장하지 않음 )
각 item에 숫자를 지정하면 숫자가 클수록 순서가 뒤로감.
```
.container {
	display : flex;
}

.item:nth-child(1) {
	order : 1;
}
```
![[Pasted image 20230910170751.png]]


- - -

# Grid란 무엇일까

격자 모양의 레이아웃을 표현하기 위해 사용하는 기능
Flex는 한방향의 레이아웃을 지원하지만 Grid는 가로, 세로 양방향의 레이아웃을 지원할 경우 사용함. 즉, 페이지의 전체 구조를 잡는 데에 사용함.


## Grid 용어를 먼저 알아보고 가자

![[Pasted image 20230910171012.png]]

| 용어           | 설명                                                      |
| -------------- | --------------------------------------------------------- |
| Grid Container | display : grid를 적용하는 Grid의 전체 영역                |
| Grid Item      | Grid Container의 item 자식 요소들                         |
| Grid Track     | Grid의 Row 또는 Column                                    |
| Grid Cell     | Grid의 한 칸을 의미함 item 자식 요소가 아님               |
| Grid Line      | Grid Shell을 구분하는 선                                  |
| Grid Number    | Grid Line의 각 번호                                       |
| Grid Gap       | Grid Shell 사이의 간격                                    |
| Grid Area      | Grid Line으로 둘러 쌓인 사각형 영역으로 Grid Shell의 집합 |

- - -
## 1. Grid Container

  ### 1-1. grid-template-rows & columns
- 가로 세로 Item의 크기를 정의하는 옵션

```
grid-template-colums : 100px 300px 200px;
grid-template-rows : 200px 200px 100px;
```

![[Pasted image 20230910180046.png]]

  - fr : Grid에서는 고정적인 크기가 아닌 비율로 트랙을 나눌 때에 fr단위를 사용한다.

```
grid-template-columns : 1fr 1fr 1fr
```

![[Pasted image 20230910180219.png]]

```
grid-template-columns : 1fr 2fr 1fr
```

![[Pasted image 20230910180248.png]]

  - auto : 만약 auto가 들어간 셀이 있다면, 해당 셀은 다른 셀이 차지하고 있는 크기를 제외한 나머지 크기를 차지한다.
```
grid-template-colums : 70px auto
```

![[Pasted image 20230910180423.png]]

  - 우리는 반복되는 것이 매우 귀찮다.
```
grid-template-columns : 1fr 1fr 1fr
=> grid-template-columns : repeat(3, 1fr)
```

즉 repeat은 (반복되는 횟수, 반복되는 값)이 들어간다.


  - 반응형 적인 웹에서는 너무 최소적으로 줄어들면 이상하게 보여지는 경우도 있다.
```
minmax(최소값, 최대값)
grid-template-columns : minmax(100px, 200px) 200px 200px;

당연히 repeat에도 들어갈 수 있다.
grid-template-columns : repeat(3, minmax(100px, 200px));
```
![[Pasted image 20230910180735.png]]
  - repeat에는 minmax가 아닌 다른 다양한 옵션도 들어갈 수 있다.
  - auto-fill, auto-fit
	  - repeat 함수와 같이 사용되는 옵션 함수임. 반복함수에 이 함수가 사용되며, 컨테이너의 크기가 아이템들을 수용하기 충분하지 않을 경우 item을 자동으로 줄 바꿈 처리하며 그에 맞게 암시적인 행과 열을 수정한다.
	  - auto-fill은 남는 공간을 그대로 유지함.
	  - auto-fit는 남는 공간을 축소함.

```
grid-template-columns : repeat(auto-fill, minmax(120px, 1fr));
```
![[Pasted image 20230910181035.png]]

```
grid-template-columns : repeat(auto-fit, minmax(120px, 1fr));
```

![[Pasted image 20230910181112.png]]

  ### 1-1. row-gap, column-gap, gap
  - row-gap : 가로 줄 간격을 설정함
  - column-gap : 세로 줄 간격을 설정함
  - gap : 둘 다 동시에 설정함


## 2. Grid 영역 지정 Option

| 속성              | 설명                                |
| ----------------- | ----------------------------------- |
| grid-column-start | Cell이 시작하는 열 시작 라인 번호  |
| grid-column-end   | Cell이 끝나는 열 시작 라인 번호    |
| grid-column       | grid-column-start + grid-column-end |
| grid-row-start    | Cell이 시작하는 행 라인 번호       |
| grid-row-end      | Cell이 끝나는 행 라인 번호         |
| grid-row          | grid-row-start + grid-row-end       |
| grid-area         | grid-column + grid-row              |

```{css}
.item:nth-child(1) {
	grid-column-start : 1;
	grid-colums-end : 3;
	grid-row-start : 1;
	grid-row-end : 2;
}

=> .item:nth-child(1) {
	grid-column : 1 / 3;
	grid-row : 1 / 2;
}
```

![[Pasted image 20230910181804.png]]

- 만약 몇 개의 Cell을 차지할 예정이라면 그 크기를 알기 힘들기 때문에 span 값을 사용할 수 있다.
```{css}
.item:nth-child(1) {
	grid-column : 1 / span 2;
	grid-row : 1 / span 3;
}
```

  - grid-column 배치를 하면 grid-auto-columns와 grid-template-colums의 통제를 받지 않음.
```{css}
.container {
	grid-template-columns : 50px;
	grid-auto-columns : 1fr 2fr;
}

.item:nth-child(1) { grid-column : 2; }
.item:nth-child(2) { grid-column : 3; }
.item:nth-child(3) { grid-column : 4; }
.item:nth-child(4) { grid-column : 5; }
.item:nth-child(5) { grid-column : 6; }
.item:nth-child(6) { grid-column : 7; }
```

  - grid-template-areas는 각 영역에 이름을 붙이고 그 이름을 통해 배치하는 방식임.
  - 페이지 구성에서 사용함
```
.grid_container {
	display: grid;
	gap: 1rem;
	grid-template-columns: 1fr 3fr 1fr;
	grid-template-areas:
		'.....  header'
		'sidebar-a main sidebar-b'
		'footer footer footer';
}

.header { grid-area: header; }
.sidebar-a { grid-area: sidebar-a; }
.sidebar-b { grid-area: sidebar-b; }
.main { grid-area: main; }
.footer { grid-area: footer; }
```

![[Pasted image 20230910182431.png]]

  - grid-auto-flow
	  - 배치되지 않은 item을 어떤 방식의 자동 배치 알고리즘으로 처리할지 정의함.

| 속성              | 설명                                           |
| ----------------- | ---------------------------------------------- |
| row               | 각 행 축을 따라 차례로 배치                    |
| column            | 각 열 축을 따라 차례로 배치                    |
| row dense(dense) | 각 행 축을 따라 차례로 배치, 단 빈 영역은 메움 |
| column dense      | 각 열 축을 따라 차례로 배치, 단 빈 영역은 메움 |

[ExampleGridAutoFlow](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-auto-flow)


## 2. Grid 정렬 Option

- 세로 방향 정렬 : align-items
- 가로 방향 정렬 : justify-items

| 속성   | 설명                            |
| ------ | ------------------------------- |
| strech | 세로 확장 / 가로 확장 (default) |
| start  | 위로 배치 / 왼쪽으로 배치       |
| center | 중앙에 배치                     |
| end    | 아래 배치 / 오른쪽 배치         |

![[Pasted image 20230910183400.png]]

#### **justify-items와 align-items을 같이 처리하기엔 귀찮다**
이때 사용할 수 있는 것이 place-items 옵션
```
.item:nth:child(1) {
	place-items : center;
	=> justify-items, align-items : center
	
	place-items : center start;
	=> align-items: center, justify-items : start;
}
```

- 아이템 그룹 세로 정렬 : align-content ( 단, item 높이를 모두 합한 값이 Grid Container보다 작아야 함. )
- 아이템 그룹 가로 정렬 : justify-content ( 단, item 너비를 모두 합한 값이 Grid Container 보다 작아야 함. )
- 귀찮다면 : space-content : align-content + justify-content

![[Pasted image 20230910183803.png]]

| 속성          | 설명                                                |
| ------------- | --------------------------------------------------- |
| stretch       | 기존 배치                                           |
| start    | 위를 기준으로 배치                                  |
| end      | 아래를 기준으로 배치                                |
| center        | 부모 Tag의 중앙을 기준으로 배치                     |
| space-between | 위 아래로 item들 사이에 균일한 간격을 만들어 배치   |
| space-around  | item들의 둘레에 균일한 간격을 만들어서 배치         |
| space-evenly  | item들의 사이와 양 끝에 균일한 간격을 만들어서 배치 |

- 개별 아이템 세로 정렬 : align-self
- 개별 아이템 가로 정렬 : justify-self
-  귀찮다면 : place-self

![[Pasted image 20230910184051.png]]

## 그 외 옵션

1. Order ( 권장하지 않음 )
	- 배치 순서를 정하는 옵션임, 숫자 값이 들어가며, 작은 숫자일 수록 먼저 배치됨.
```
.item:nth-child(1) { order : 3; }
.item:nth-child(2) { order : 1; }
.item:nth-child(3) { order : 2; }
```
![[Pasted image 20230910184240.png]]

1. Z-index
	- 기존의 z-index와 동일함
```
.item:nth-child(5) {
	z-index : 1;
	transform: scale(2)
}
```

![[Pasted image 20230910184425.png]]



[^1]: flex안의 item을 수평 혹은 수직으로 둘 것인지 역방향 혹은 정방향으로 둘 것인지 알아보는 CSS 기능 (속성 : row, row-reverse, column, column-reverse)

[^2]: flex안의 item을 한줄로 나열할 것인지 item의 갯수에 따라서 배치를 달리 할 것인지 알아보는 CSS 기능 (속성 : nowrap, wrap, wrap-reverse)

[^3]:  ![[Pasted image 20230910170317.png]] <br/>item마다 개별적으로 기준점의 비율을 설정하는 CSS기능임. (input num)

[^4]: ![[Pasted image 20230910170408.png]] <br/>item에 width가 부여되었을 경우 부모의 width 보다 큰 경우에 input에 따라서 축소하는 비율을 맞춘다. (input num)

[^5]: item의 초기 크기를 지정한다. (속성 : auto, 0, 200px, content, max-content, fill 등 )
