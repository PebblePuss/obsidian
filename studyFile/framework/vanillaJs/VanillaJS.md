> [!tip] This Post exists for vanillaJS #vanilla_JS 
> 우리는 주로 React 프레임워크를 활용하여 개발을 수행하지만, 웹 개발에는 React 이외에도 다양한 프레임워크와 라이브러리가 존재합니다. 게다가, JavaScript만을 사용하여도 웹 컴포넌트를 구현할 수 있으며, 내장 상태 관리까지 가능합니다. 그럼에도 불구하고, 이러한 정보는 여전히 많은 사람들에게 잘 알려지지 않은 실정입니다. 이번 기회를 통해 VanillaJS(순수 JavaScript)를 조금 더 정리하고 이해하려고 합니다.

<br/>

# What is Vanilla JS?

- - - 
클래스 형태를 지닌 어떠한 framework없이 순수히 javaScript만으로 만드는 웹을 말한다.
VanillaJS로 만드는 이유는 framework를 위한 라이브러리의 자원 소모가 없어 빠르게 실행될 수 있으며, 무엇보다 변화가 없는 개발 방식임.
또한, VanillaJS는 웹 라이브러리 개발에도 사용된다.

HTMLElement 혹은 LitElement 혹은 직접 만들어서, 제작할 수 있다.

## 1. HTML-Element
- - - 
```js
	class exampleHTMLElement extends HTMLElement {
		constructor() {
			super();
			this.attachShadow({ mode : "open" }).append(this.template);
		}

		template() {
			return ``;
		}
		
		connectedCallback() {
			console.log("Component ON");
		}
		disconnectedCallback() {
			console.log("Component OFF");
		}

		static get observedAttributes() {
			return ['state'];
		}
		attributeChangeCallback(name, oldValue, newValue) {
			console.log('name에서 Value 변경되었습니다.')
		}
	}
```

먼저 해당 Component의 기본적인 부분을 설정하는 부분인 Constructor에 대해서 보자.

### Constructor

```js
	constructor() {
		super();
		this.attachShadow({ mode : "open" }).append();
	}
```

Super[^1] 는 클래스의 속성에 접근하여 슈퍼 클래스의 생성자를 호출하는 데에 사용된다.

Custom Component를 예시로 설명을 들도록 하겠다. 
extends 대상이 되는 SuperClass인 Component의 모습은 이러하다.

```js
import { observable, observe } from "./Observer.js";

export default class Component {
    state; props; $target;
    constructor($target, props) {
        this.$target = $target;
        this.props = props;
        this.setUp();
    }
    
    setUp() {
        this.state = observable(this.initState());
        observe(() => {
            this.render();
            this.setEvent();
            this.mounted();
        });
    }

    render() { this.$target.innerHTML = this.template(); }
    template() { return ``; }
    initState() { return {}; }
    setEvent() { }
    mounted() { }
}
```

하지만 자식Class에서 이 Component를 extends하고 constructor()에 무언가 추가하고 싶다면,

```js
import { Component } from "../core/component.js";

export default class ExampleComponent extends Component {
	constructor(target, props) {
		super(target, props);
		this.attachShadow({ mode : "open" }).append();
	}
}
```

이런 식으로 활용이 가능하다.

즉, Constructor의 활용 방법은
1. HTMLElement를 사용할 때에는 super()가 필수이다.
2. 각종 기본적인 설정을 할 때에 사용된다.

### ConnectedCallback()

Component가 DOM tree에 등장할 때에 작동된다.
해당 함수가 실행될 때에 updateStyle(Element)가 같이 실행되나, updateStyle는 추천하지 않음.

대체적으로는 이벤트의 선언을 넣는 곳임.
```js
	connectedCallback() {
        this.printCoinValue.innerHTML = `${this.CurrentCoin}`;

        this.addCoinBtn.addEventListener("click", () => {

            this.CurrentCoin += Number.parseInt(this.addCoinBtn.value) * (this.upgradeCount + 1);

            this.printCoinValue.innerHTML = `${this.CurrentCoin}`;

        });

        this.upgradeCoinBtn.addEventListener("click", () => {
            if (this.CurrentCoin >= (this.upgradeCount+1) * this.upgradeCoinBtn.value) {
                if (this.upgradeCount < 5) {
                    this.upgradeCount += 1;
                    this.CurrentCoin -= this.upgradeCount * this.upgradeCoinBtn.value;
                } else {
                    this.printNotice.innerHTML="<p>This is already the best upgrade.</p>";
                }
                
                this.printCoinValue.innerHTML = `${this.CurrentCoin}`;
            }
            else {
                this.printNotice.innerHTML = "<p>It's not enough. the number of coins</p>";
            }
        });

        this.saveCoinBtn.addEventListener("click", () => {
            if(localStorage) {
                let coinKey = "CurrentCoin";
                let coinVal = this.CurrentCoin;
                localStorage.setItem(coinKey, coinVal);

                let upgradeKey = "Upgrade";
                let upgradevVal = this.upgradeCount;
                localStorage.setItem(upgradeKey, upgradevVal);
            }
        });
    }
```

### disconnectedCallback()

ConnectedCallback과 반대로 DOM tree에서 제거될 때에 혹은 다른 페이지로 이동했을 때에 작동되는 함수이다.



### attributeChangeCallback()

observerAttribute에서 지정한 자원의 변화가 일어날 경우 발생하는 함수

```js
	static get observerAttributes() { return ['c', 'l']; }
```

해당 변화 감지를 위한 자원은 해당 Component의 속성에 있을 경우 감지가 된다. 예시의 'c'와 'l'이 어떠한 Tag의 Attribute로 들어가 있을 경우 감지의 대상이 된다.

```js
attributeChangedCallback(name, oldValue, newValue) {
  console.log('Custom square element attributes changed.');
  this.render();
}
```

해당 함수는 속성의 변화가 일어날 경우 Component를 리랜더하는 함수이다.

이 외에도 매우 많은 속성들이 존재함. 이 외는 특수한 경우에 사용되는 경우이니 직접 해당 홈페이지 접속하여 알아볼 것.
[MDN - CustomElement](https://developer.mozilla.org/ko/docs/Web/API/HTMLElement)

### HTMLElement LifeCycle

![[Pasted image 20230923140815.png]]

## 2. Lit - Element
- - -
```js
import { LitElement, css, html } from 'lit-element';

class MyElement extends LitElement {
	@eventOptions({passive: true})
	private _handleTouchStart() { ... }
	
	static get properties() {
	  return {
	    greeting: {type: String},	
	    data: {attribute: false},	
	    items: {}	
	  };	
	}

  static get styles() {
    return css`
      div { color: red; }
    `;
  }

    render() {
    return html`<button @click="${this._handleClick}">click</button>`;
  }
  
  _handleClick(e) {
    console.log(this.prop);
  }
}
```

React의 class방식과 살짝 유사한 방식을 가진 CustomElement이다.

LitElement는 VanillaJS에도 포함이 되긴 하지만, 라이브러리 설치와 React에 비견하는 용량으로 추천하지 않는 CustomElement이다.

사용법은 HTMLElement와 유사하나, 조금의 내장 함수가 다르며, 이벤트 작동 방식 또한 다르다.

자세한 사용 방법은 해당 홈페이지를 이용하여 알아보자
[Lit-Element](https://lit.dev/docs/v1/components/events/)

대부분의 함수는 HTMLElement와 유사하다.
( connectedCallback, disconnectedCallback, 등... )

### Template

```js
import { LitElement, html } from 'lit-element';

class MyElement extends LitElement {
  render() {
    return html`<p>template content</p>`;
  }
}

import {LitElement, html, eventOptions} from 'lit-element';

=> Event의 다른 버젼
class MyElement extends LitElement {
	@eventOptions({passive: true})
	private _handleTouchStart() { ... }
	
	render() {
	  return html`
	    <div @touchstart=${this._handleTouchStart}><div>
	  `;
	}
}
```


## 3. Custom-Component
- - -
```js
import { observable, observe } from "./Observer.js";

export default class Component {
    state; props; $target;
    constructor($target, props) {
        this.$target = $target;
        this.props = props;
        this.setUp();
    }

    setUp() {
        this.state = observable(this.initState());
        observe(() => {
            this.render();
            this.setEvent();
            this.mounted();
        });
    }

    render() { this.$target.innerHTML = this.template(); }
    template() { return ``; }
    initState() { return {}; }
    setEvent() { }
    mounted() { }
}
```

어떠한 라이브러리 필요 없이 모든 것을 구성할 수 있으며, 구현할 수 있다면, 직접 구현이 가능하다.
하지만, 기본적으로 모두 구현되어있는 HTMLElement를 생각한다면 구지? 이렇게까지 구현해야 되나 싶다.

## 추가적인 Tip
- - -

#### 1. customElements.define("tag-name", class-name)
```js
customElements.define("popup-temp", CustomPopup);
```
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
        <script defer src="../js/test14_quiz01.js"></script>
    </head>

    <body>
        <opener-temp></opener-temp>
        <template id="quiz14_01_opener">
            <div class="openerPop">
                <h1>OPENER</h1>
                <button type="button" id="openPopBtn">Open PopUp</button>
                <br>
                
                전달할 값 >>
                <input type="text" name="inputSentData" id="sendDataInput">
                <button type="button" id="sendDataBtn">Send</button>
                
                <br>
                전달받은 값 >>
                <input type="text" name="inputGetData" id="getDataInput">
                <button type="button" id="getDataBtn">Get</button>
            </div>
        </template>

        <template id="quiz14_01_popup">
            <div class="popUp">
                <h1>POPUP</h1>
                전달받은 값 >>
                <input type="text" name="inputGetData" id="getDataInput">
                <br>

                전달할 값 >>
                <input type="text" name="inputSentData" id="sendDataInput">
                <br>

                <button type="button" id="closePopBtn">Close This PopUp</button>
            </div>
        </template>
    </body>
</html>
```

해당 customElements.define을 이용한다면 클래스의 내용에 따라 내부의 Component를 Tag에 적용 시킬 수 있음.

추가적으로 React 처럼 Props도 넣을 수 있다.
```html
<body>
	<opener-temp name="example" />
</body>
```
```js
let example = $elem.getAttribute("name");
```

만약 기존에 존재하는 Tag를 기반으로 Custom Component를 넣고 싶다면 해당하는 방법을 사용하면 된다.

```html
<ul is="example-ls">
	...
</ul>

<example-ls></example-ls>
```
```js
customeElements.define("example-ls", ClassName, { extends : "ul" });
```


#### 2. template
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
        <script defer src="../js/test14_quiz01.js"></script>
    </head>

    <body>
        <opener-temp></opener-temp>
        
        <template id="quiz14_01_opener">
            <div class="openerPop">
                <h1>OPENER</h1>
                <button type="button" id="openPopBtn">Open PopUp</button>
                <br>
                
                전달할 값 >>
                <input type="text" name="inputSentData" id="sendDataInput">
                <button type="button" id="sendDataBtn">Send</button>
                
                <br>
                전달받은 값 >>
                <input type="text" name="inputGetData" id="getDataInput">
                <button type="button" id="getDataBtn">Get</button>
            </div>
        </template>

        <template id="quiz14_01_popup">
            <div class="popUp">
                <h1>POPUP</h1>
                전달받은 값 >>
                <input type="text" name="inputGetData" id="getDataInput">
                <br>

                전달할 값 >>
                <input type="text" name="inputSentData" id="sendDataInput">
                <br>

                <button type="button" id="closePopBtn">Close This PopUp</button>
            </div>
        </template>
    </body>
</html>
```
```js
import {stateQuiz} from "./test14_quiz01.js"

class CustomPopup extends HTMLElement {
    constructor() {
        super();
        this.attachShadow({ mode: "open" }).append(
            quiz14_01_popup.content.cloneNode(true)
        );

        this.getDataInput = this.shadowRoot.querySelector("#getDataInput");
        this.sendDataInput = this.shadowRoot.querySelector("#sendDataInput");
        this.closePopBtn = this.shadowRoot.querySelector("#closePopBtn");
        this.openState = {};
    }

    connectedCallback() {
        this.sendDataInput.addEventListener("input", (e) => {
            this.openState["popup"] = e.target.value ? e.target.value : "There is no Data.";
            stateQuiz.setState(this.openState);
        });

        this.closePopBtn.addEventListener("click", () => {
            console.log();
        });
    }
}

customElements.define("popup-temp", CustomPopup);
```

html에서 template Tag를 이용하여, 해당 Component의 구조를 설정하고, Component JS 단계에서 attachShadow를 통해서 ShadowDOM을 적용 및 이벤트를 가져올 수 있다.


그러면 ShadowDOM은 대체 무엇인가?
#### 3. ShadowDOM

쉽게 설명하면 캡슐화이며, 마크업 구조와 스타일 동작을 숨기고 다른 페이지의 다른 코드로부터 분리하여 각기 다른 부분이 충돌하지 않도록 막는 구조임

![[Pasted image 20230923172133.png]]

즉, 해당 shadowDOM은 타 컴포넌트와 겹치는 부분이 없으며, 자원을 공유하고 있지 않은 경우에 활용하면 좋다.

```js
exampleElement.attachShadow({ mode : "open" }); //ShadowDOM on
exampleElement.attachShadow({ mode : "close" }); //shadowDOM off
```


```js
constructor() {
	super();
	this.attachShadow({ mode: "open" }).append(
		quiz14_01_popup.content.cloneNode(true)
	);

	this.getDataInput = this.shadowRoot.querySelector("#getDataInput");
	this.sendDataInput = this.shadowRoot.querySelector("#sendDataInput");
	this.closePopBtn = this.shadowRoot.querySelector("#closePopBtn");
	this.openState = {};
}
```

해당 shadowDOM의 생성 문장의 해석은 `quiz14_01_popup이라는 template의 Component Content의 노드를 복제하여 shadowDOM에 붙여 넣는다.` 라는 의미임.


#### 4. Slot
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    <body>
        <custom-elem>
            <span slot="username">OST</span>
            <span slot="birthday">0228</span>
            <div slot="subdiv">
                <ul>
                    <li>Text01</li>
                    <li>Text02</li>
                    <li>Text03</li>
                </ul>
            </div>
        </custom-elem>

        <template id="temp1">
            <h1>Name : <slot name ="username"></slot></h1>
            <h3>Birthday : <slot name ="birthday"></slot></h3>
            <div><slot name="subdiv"></slot></div>
        </template>
        
        <script>
            class CustomElem extends HTMLElement {
                connectedCallback() {
                    this.attachShadow({mode : "open"});
                    this.shadowRoot.append(temp1.content.cloneNode(true));
                }
            }
            customElements.define("custom-elem", CustomElem);
        </script>
    </body>
</html>
```

해당 예제를 보면 이해가 될 수도 있지만, 이해가 안될 가능성도 높다.
slot은 shadow DOM에서 일반적인 DOM의 변화에 따라 자동으로 변환될 수 있도록 지원하는 Element이다.

즉, 접근이 불가능한 ShadowDOM에서 외부의 변화에 따라 동적으로 핸들링이 가능하도록 하는 기능을 제공한다.

대신 외부 일반 DOM의 slot이름과 template 내부의 slot Tag의 name과 같아야 한다.


#### 5. 중앙 자원 관리 시스템 ( Redux, Pinia )

![[projectFile/myMiniProject/vanilla/Store_vanillaJS/README|README]]


[^1]: 객체 리터럴 또는 클래스의 Prototype 속성에 접근하거나 슈퍼 클래스의 생성자를 호출하는 데에 사용된다.