> [!tip] This Post exists for #Jest 
> TDD 방식 개발 방법론이 유행하기 시작하면서 테스팅 기법에 대한 관심도가 올라가기 시작했는데, 우리는 이러한 흐름에 맞춰서 테스팅 기법이 무엇인지, 프론트엔드에서 어떤 방식으로 TDD가 이뤄지는지 알아보도록 하겠다.

<br/>

# TDD

- - - 

TDD[^1]는 소프트웨어를 개발하는 여러 방법론 중 하나, 제품이 오류 없이 작동하는 지에 대한 여부와 프로그래머가 코드를 작성한 이후 테스팅을 통해 안정적으로 서비스를 유통하기 위한 목적임. 즉, 안정적인 서비스의 개발과 테스팅을 통한 버그가 없는 코드를 만들고자 할 때에 사용할 수 있다.

하지만, 단점으로는 사용자가 무조건 개발자가 원하는 방향으로 흘러가지 않는다는 점과, 테스트가 명확하게 설계되지 않으면, 개발에서 많은 어려움을 겪을 수 있다.

그렇다면, 우리는 안정적인 서비스의 제공과 코드를 만들기 위해 TDD 방법론을 위한 언어가 있을까?

다양한 테스팅 언어가 있지만, 프론트 엔드에서 가장 많이 사용하는 프레임워크인 react에서 정식으로 사용하고 있는 테스팅 언어인 jest에 대해서 알아보도록 하겠다.


## Jest
- - -
Jest는 기본적으로 테스팅 프레임 워크이며, 자스민 위에서 동작한다.
대체적으로 같이 사용하는 프로젝트는 Babel, TypeScript, Node.js, React, Angular, Vue.js, Svelte에서 사용된다.

react에서는 기본적인 설정이 되어있으나, 만약 WebPack에 없다면,
```
[npm]
npm install jest --save-dev

[yarn]
yarn add --dev jest

[pnpm]
pnpm add --save-dev jest
```
위의 명령어를 통해서 설치가 가능하다.

jest의 TestingFile Setting엔 유의해야 될 점이 있다.
```fileName
[FileName].test.js
```
로 파일명을 지정하거나, `__test__`의 directory에 있는 파일들은 모두 테스트 파일로 인식이 된다.

이제 기본적인 세팅의 설명은 모두 끝났다. 이제 Jest를 활용해서 어떤 문법을 사용할 수 있으며, 어떻게 테스팅이 작동되는 지에 대해 알아보도록 하겠다.

Jest에는 기본적으로 알아야 되는 문법이 존재한다.

| 명령어   | Excep                                                                                                          | 사용법                                        |
| -------- | -------------------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| Describe | 여러 테스트를 묶어서 그룹화를 시키고 해당 그룹에 명칭을 지정할 때에 사용 (필수는 아니지만, 구분을 위해 필요함) | describe("구분 내용",() => { function })      |
| Test     | 테스트 한 개에 대한 명칭을 지정할 때에 사용 (필수)                                                             | test("test이름",() => { function })           |
| Expect   | 특정 값에 대한 테스트를 진행할 경우 사용됨, 다만 단독으로 사용되는 일은 없음. (matcher와 같이 사용됨)          | expect(`[Test 내용]`)`[.modifiers]`.matcher() |
| Modifier | expect와 matcher사이에 들어가는 수식어 (필수는 아님)                                                           | -                                             |
| Matcher  | expect의 값에 대응되는 조건을 매칭 시킬 경우, 사용되는 메서드 Matcher의 함수는 매우 많음                       | -                                             |

이렇게 구성 되어 있는데, 전체적인 예시 안을 이용해서 설명하면 밑과 같다.

```jest
describe("exampleGroup", () => {
	test("exampleTest01", () => {
		expect(func.1).matcher(4);
	});

	test("exampleTest02", () => {
		expect(func.2).matcher(5);
	})
})
```

그렇다면 우리가 비교를 위한 Matcher는 어떤 종류가 있고 사용 방법은 어떻게 되는지 알아보도록 하겠다.

## Matcher

### 동등 비교 Matcher

| Method Name           | Excep                                                               |
| --------------------- | ------------------------------------------------------------------- |
| .tobe(value)          | 기본 값을 비교하거나 개체 인스턴스의 참조 ID를 확인하는 데에 사용됨 |
| .toEqual(value)       | 개체 인스턴스의 모든 속성을 재귀적으로 비교하는 데에 사용한다.      |
| .toStrictEqual(value) | .toEqual과 기능은 비슷하지만, 정의되지 않는 속성이 있는 키와 항목이 확인된다는 점과, 배열 희소성과 객체 유형이 확인된다는 점에서 차이점이 존재한다.                                                               |

정확한 예시를 통해서 보여주겠다.

```jest
[1] 정의되지 않는 속성이 있는 키가 확인됨.
{ a : undefined, b : 2 } != { b : 2 }

[2] 정의되지 않는 항목 고려됨.
[2] != [2, undefined]

[3] 배열 희소성이 확인됨
[, 1] != [undefined, 1]

[4] 객체 유형이 확인된다.
new instance( a : 111, b : 222 ) != { a : 111, b : 222 }
```

이를 작동한 예제를 본다면,
```javaScript
const fn = {

    funcA : a => a + 10,

    funcB : (a, b) => ({a, b}),

    funcC : (a, b) => ({a, b, c:undefined})

}

module.exports = fn;
```

```jest
const fn = require('./code121_test');

describe('isSame Num? Test', () => {

    test("[input 1] FuncA result: 1", () => {
        expect(fn.funcA(1)).toBe(11);
    });

    test("[input 2, 3] FuncB result: {a:2, b:3}", () => {
        expect(fn.funcB(2, 3)).toEqual({a:2, b:3});
    });

    test("[input 2, 3] FuncB result: {a:2, b:3}", () => {
        expect(fn.funcC(2, 3)).toEqual({a:2, b:3});
    });

    test("[input 2, 3] FuncB result: {a:2, b:3, c:undefined}", () => {
        expect(fn.funcC(2, 3)).toStrictEqual({a:2, b:3, c:undefined});
    });

});
```


### 참, 거짓 Matcher

| Method Name   | Excep                                         |
| ------------- | --------------------------------------------- |
| toBeNull      | Null 값이 아닌 경우 에러                      |
| toBeUndefined | Undefined가 아닌 경우 에러                    |
| toBeDefined   | toBeUndefined의 반대                          |
| toBeTruthy    | True 혹은 true에 준하는 값이 아닌 경우 에러   |
| toBeFalsy     | False 혹은 false에 준하는 값이 아닌 경우 에러 |

이렇게 함수가 존재하는 데, 이것을 활용한 예시는 이렇게 존재한다.

```jest
test("null", () => {
    const n = null;

    expect(n).toBeNull();           // n === null
    expect(n).toBeUndefined();      // n === undefined
    expect(n).toBeDefined();         // n !== undefined
    expect(n).toBeTruthy();         // !!(n) == true
    expect(n).toBeFalsy();          // !!(n) == false
    //one test only have one case
});
```

이 외에도 Number와 String, Array, Exception 체크를 위한 함수가 존재한다 이것은
[[2.matcher.pdf]] 이 파일을 참고하면 된다.

우리는 계산 식을 프론트에서 해결하는 경우도 있지만, 대다수의 프론트가 할 일은 백엔드와의 통신을 통해 얻은 자원들이나, 정보를 이용해서 화면에 표출하거나, 값을 도출하는 일이다.

그렇다면 비동기적으로 작동 되어야 되는 통신 관련은 어떻게 찾아야될까?

## CallBack 함수 Testing

매우 간단하다. 우리가 JavaScript에서 어떻게 비동기적으로 받아왔는가?

```javaScript
const func () => {
	return new Promise(res => {
		...작동
	})
}
```

`func.then()`을 이용해서 func이 끝날 경우 then 안이 작동되는 방식으로 사용이 된다. 이와 매우 유사하다.

```jest
test("Name", () => {
	import.func().then(value => {
		expect(value).matcher();
	})
})
```
이렇게 활용이 가능하다. 만약 resolves나 rejects를 활용한다면, 다음과 같이 사용이 가능하다
```jest
test("Name1", () => {
	return expect(import.func()).resolves.matcher();
});

test("Name2", () => {
	return expect(import.func()).rejects.matcher();
});
```

만약 resolves와 rejects가 모르겠다 하면,,, Promise()을 조금 더 공부를 하고 와보자.

_"Promise에서 성공 될 경우, resolves가 작동이 되고, 실패 된 경우 rejects가 작동된다."_

만약 return을 필수적으로 사용해야 되는 Promise가 매우 불편한 경우, async / await를 사용할 수 있다.
사용법은 javascript와 비슷하다.

```jest
test("Name", async () => {
	const result = await import.func();
	expect(result).matcher(20);
});
```

서버와의 통신을 테스팅 할 수 있는 방법도 있다. Mock Server가 있는데 해당 경우는 Mock Server에 대한 정보를 찾아보도록 하자.

지금까지 우리는 JS에서 함수를 만들고 그에 대한 결과를 이용해서 Testing을 하는 방법에 대해서 알아봤다.

하지만, 가만히 생각해보면 안 써도 무방하지 않나? 싶을 정도다.
_"console.log를 통한 값 확인이 되지 않나?"_
게다가 우리에겐 화면에 값이 표출되는 게 중요하지 "값이 통신에서 잘 받아 왔는가?"는 백엔드에서 확인해줘야 되는 문제인 것 같다.

그런 당신을 위한 React에서 화면 결과를 이용한 Test 기법에 대해서 알려주겠다.

```jest
import { render, screen } from "@testing-library/react";
import App from "./App";

test("renderTest", () => {
	render(<App/>);

	const h1El = screen.getByText(/Hello/i); //정규식
	expect(h1El).toBeInTheDocument();
})
```

이 방법을 활용한다면, 화면에 표출 된 것이 정확히 표출이 되었는지 확인이 가능하다.
_"정규식을 공부해야 되는 이유가 늘어난다."_

이 외의 상세한 내용은 [Getting Started · Jest (jestjs.io)](https://jestjs.io/docs/getting-started) 여기에서 상세하게 알아보도록 하자....


[^1]: TDD: Test-Driven Development의 약자 테스트 주도 개발 론이다.
