---
title: 시작하기
type: guide
order: 2
---

## Vue 가 무엇인가요?

Vue(/vjuː/ 로 발음, **view** 와 발음이 같습니다.)는 사용자 인터페이스를 만들기 위한 **미래형 프레임워크** 입니다. 다른 단일형 컴포넌트 프레임워크들과는 다르게, 마치 어린이들의 장난감 레고처럼 하나 둘 씩 확장시켜 나아가 마지막으로는 아주 멋진 앱이 만들어 질 수 있도록 설계되었습니다.

Vue의 코어는 사용자의 인터페이스만 집중합니다. 때문에 다른 자바스크립트 라이브러리를 사용한다거나, 기존에 있던 프로젝트에 Vue를 사용하려고 할 때도 아무런 제약이 없습니다.

또, Vue를 사용하여 개발할 때 공식 [도구](single-file-components.html) 또는 [라이브러리](https://github.com/vuejs/awesome-vue#libraries--plugins) 를 함께 사용한다면, 좀 더 쉽고 편하게 개발할 수 있습니다.

많은 자바스크립트 라이브러리와 프레임워크를 경험해보셨다면, Vue의 성능이 궁금하실 겁니다. 지금 바로 [비교 결과](comparison.html)를 확인하세요.

## Vue 세계에 오신 것을 환영합니다.

<p class="tip">
  **프론트엔드는 처음이신가요?**
</p>

HTML 과 CSS 그리고 자바스크립트를 유연하게 다룰 수 없다면, 가이드를 따라가기 어려울 수 있습니다.

Vue는 정말 쉽지만, 가이드를 천천히 따라가다 이해하기 어렵다면 먼저 웹 개발의 기본을 익히신 후에 진행해보세요. 그럼 Vue의 매력에 빠져 헤어나올 수 없을 거라고 확신합니다!

<p class="tip">
  Vue의 세계에 접속하기 전에, 간접 체험을 해보고 싶으신가요? [JSFiddle Hello World 예제](https://jsfiddle.net/chrisvfritz/50wL7mdz/)
</p>

예제에 접속하는 순간.. 이미 Vue의 매력에 빠져있을 겁니다.

## 설치

프론트엔드 개발 도구에 익숙하지 않으신가요? 그렇다면, html 파일에서 Vue를 바로 사용하세요.

``` html
<script src="https://unpkg.com/vue/dist/vue.js"></script>
```

<p class="tip">
  Node.js 의 패키지 매니저를 사용하실 줄 안다면, 정말 간단하게 Vue 세계에 [접속](installation.html)할 수 있습니다.
</p>

## 선언적 렌더링

Vue 의 핵심은 정말 간단한 템플릿 구문으로 데이터를 렌더링할 수 있다는 것입니다.

``` html
<div id="app">
  {{ message }}
</div>
```
``` js
var app = new Vue({
  el: '#app',
  data: {
    message: '인간보다는 기계가 더 믿을만 하죠. - 토니 스타크 (아이언 맨)'
  }
})
```
{% raw %}
<div id="app" class="demo">
  {{ message }}
</div>
<script>
var app = new Vue({
  el: '#app',
  data: {
    message: '인간보다는 기계가 더 믿을만 하죠. - 토니 스타크 (아이언 맨)'
  }
})
</script>
{% endraw %}

축하합니다! 첫 Vue 앱을 만들었습니다.
단순히 문자열을 렌더링하는 것과 비슷하지만, Vue 는 더 많은 일을 합니다.

<p class="tip">
  엘리먼트를 Vue 에 등록하는 순간, 마법이 펼쳐집니다.
</p>

마법을 경험하셨나요? 위처럼 엘리먼트를 Vue 에 등록하게 되면, 해당 엘리먼트는 Vue 의 세계를 관리하는 DOM 에 연결되어 모든 일이 **반응형**이 됩니다.

에이~.. 이렇게 간단한 문법으로 어떻게 어떻게 반응형이 되냐구요? 그렇다면 브라우저 자바스크립트 콘솔을 열고 `app.message = 원하는 값` 을(를) 통해 message 를 다른 값으로 설정해보세요! 다시 한 번 마법이 펼쳐집니다.

<p class="tip">
  Vue 세계에서는 단순히 문자열 렌더링 이외에도 많은 일을 할 수 있습니다.
</p>

``` html
<div id="app-2">
  <span v-bind:title="message">
    마우스를 올려보세요. Vue가 title을 감시할 겁니다.
  </span>
</div>
```
``` js
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: '내가 만든 일생 최고의 작품은, 너란다. - 하워드 스타크 (아이언 맨)'
  }
})
```
{% raw %}
<div id="app-2" class="demo">
  <span v-bind:title="message">
    마우스를 올려보세요. Vue가 title을 감시할 겁니다.
  </span>
</div>
<script>
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: '내가 만든 일생 최고의 작품은, 너란다. - 하워드 스타크 (아이언 맨)'
  }
})
</script>
{% endraw %}

여기서 Vue 가 당신을 또 한 번 매료시켰습니다.

<p class="tip">
  `v-bind` 어트리뷰트는 **지시문** 이라고 부릅니다.
</p>

지시문은 `v-` 접두어를 가지고 있는 **특수 속성**입니다. 특수 속성은 Vue 세계를 관리하는 DOM 에게 명령을 내릴 수 있게 도와줍니다.

우리는 방금 DOM 에게 title 어트리뷰트를 Vue 세계 인스턴스 `message` 를 사용해 항상 최신 상태로 유지하라고 명령을 내렸습니다.

다시 한 번 명령을 내리고 싶으시다면, 자바스크립트 콘솔을 다시 열고 `app2.message = 원하는 값` 을 입력해보세요. DOM 이 title 을 최신 상태로 유지시켜줄 겁니다.

## 조건문과 반복문

Vue 의 세계에서 엘리먼트를 조작하는 것은 정말 간단합니다.

``` html
<div id="app-3">
  <p v-if="seen">잠시 길을 잃었다고 해서, 영원히 길을 잃은 것은 아니다. - 찰스 자비에 (엑스맨)</p>
</div>
```

``` js
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
```

{% raw %}
<div id="app-3" class="demo">
  <span v-if="seen">잠시 길을 잃었다고 해서, 영원히 길을 잃은 것은 아니다. - 찰스 자비에 (엑스맨)</span>
</div>
<script>
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
</script>
{% endraw %}

또 한 번 자바스크립트 콘솔을 열고 `app3.seen = false` 를 입력해보세요. 눈 깜짝할 사이에 신비한 일이 벌어질 겁니다.

방금 벌인 일을 통해, DOM 에게 단순히 텍스트와 어트리뷰트 뿐만 아니라 DOM 의 **구조**에도 지시 명령을 내릴 수 있다는 것을 알았습니다.

<p class="tip">
**어떤가요?**

당신은 Vue 의 세계에서 매우 특별한 사람입니다.
</p>

지시문은 각각 고유한 기능을 가지고 있습니다. 그리고 이곳에서 DOM 을 조작할 수 있는 몇 가지 지시문을 알려드리겠습니다.

`v-for` 지시문은 배열의 데이터를 사용해 엘리먼트를 표시할 수 있습니다.

``` html
<div id="app-4">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
```
``` js
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: '한 사람만 노력해도 세상은 달라지기 마련이야 - 스파이더 맨' },
      { text: '가장 어려운 일부터 해라. 그건 바로 자신을 용서하는 일이야 - 스파이더 맨' }
    ]
  }
})
```
{% raw %}
<div id="app-4" class="demo">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
<script>
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: '한 사람만 노력해도 세상은 달라지기 마련이야 - 스파이더 맨' },
      { text: '가장 어려운 일부터 해라. 그건 바로 자신을 용서하는 일이야 - 스파이더 맨' }
    ]
  }
})
</script>
{% endraw %}

자바스크립트 콘솔에서 `app4.todos.push({ text: 원하는 값 })` 을 입력해보세요. li 엘리먼트가 새롭게 추가될 겁니다.

## 이벤트 제어

`v-on` 지시문은 앱의 사용자가 Vue 세계와 상호 작용할 수 있게 만들어줍니다.
여기서는 `v-on` 지시문을 사용하여, Vue 세계에 이벤트를 제어하는 메소드를 추가해보겠습니다.

``` html
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">메시지 뒤집기</button>
</div>
```
``` js
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: '아들아. 내 인생 일대 최고의 최고 발명품은 바로 너란다. - 아이언 맨'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
```
{% raw %}
<div id="app-5" class="demo">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">메시지 뒤집기</button>
</div>
<script>
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: '아들아. 내 인생 일대 최고의 최고 발명품은 바로 너란다. - 아이언 맨'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
</script>
{% endraw %}

`v-model` 지시문은 사용자와 Vue 세계를 양방향 바인딩할 수 있게 도와줍니다.

``` html
<div id="app-6">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
```
``` js
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Vue 세계에 오신 것을 환영합니다.'
  }
})
```
{% raw %}
<div id="app-6" class="demo">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
<script>
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Vue 세계에 오신 것을 환영합니다.'
  }
})
</script>
{% endraw %}

## 선언적 컴포넌트를 만드는 방법

콤포넌트는 Vue 세계를 만드는 아주 중요한 역할을 합니다. 이것은 마치 현실 세계의 `사물`과 같습니다.

콤포넌트는 재사용할 수 있으며, 콤포넌트는 하나 하나 블럭처럼 이어붙여 대규모 앱을 구축할 수 있게 만들어줍니다.

![컴포넌트 트리](/images/components.png)

Vue 세계에서 콤포넌트를 만들고 사용하는 것은 정말 간단합니다.

``` js
// todo-item 이름을 가진 컴포넌트를 정의합니다
Vue.component('todo-item', {
  template: '<li>할일입니다.</li>'
})
```

이제 Vue 세계에서 todo-item 콤포넌트를 사용할 수 있게 됐습니다!

``` html
<ol>
  <!-- todo-item 컴포넌트의 인스턴스 만들기 -->
  <todo-item></todo-item>
</ol>
```

하지만 위의 예제에서 만든 콤포넌트는 모든 상황에서 같은 성질을 가지고 있습니다.
콤포넌트마다 각각 다른 성질을 가지게 하려면, 상위 HTML 엘리먼트의 데이터를 전달받을 수 있도록 만들어야 합니다.

Vue 세계는 [props](components.html#Props)을 통해 데이터를 전달받을 수 있습니다. 하지만 `props`를 사용하기 위해선 콤포넌트에서 props 프로퍼티를 정의해야 합니다.

``` js
Vue.component('todo-item', {
  // 이제 todo-item 컴포넌트는 사용자 정의 속성과 같은
  // "prop"를 허용합니다. 이 prop는 todo라고 합니다.
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
```

축하합니다!
이제 `v-bind`를 사용하여 콤포넌트에 데이터를 전달할 수 있습니다.

``` html
<div id="app-7">
  <ol>
    <!-- 각 todo-item 에 todo 객체를 제공합니다. -->
    <!-- 그것의 컨텐츠는 동적입니다. -->
    <todo-item v-bind:todo="text" v-for="text in textList"></todo-item>
  </ol>
</div>
```
``` js
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})

var app7 = new Vue({
  el: '#app-7',
  data: {
    textList: [
      { text: '한 사람만 노력해도 세상은 달라지기 마련이야 - 스파이더 맨' },
      { text: '가장 어려운 일부터 해라. 그건 바로 자신을 용서하는 일이야 - 스파이더 맨' }
    ]
  }
})
```
{% raw %}
<div id="app-7" class="demo">
  <ol>
    <todo-item v-for="item in textList" v-bind:todo="item"></todo-item>
  </ol>
</div>
<script>
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
var app7 = new Vue({
  el: '#app-7',
  data: {
    textList: [
      { text: '한 사람만 노력해도 세상은 달라지기 마련이야 - 스파이더 맨' },
      { text: '가장 어려운 일부터 해라. 그건 바로 자신을 용서하는 일이야 - 스파이더 맨' }
    ]
  }
})
</script>
{% endraw %}

부모 엘리먼트에 영향을 주지 않으면서, 우리가 원하는 `todo-item` 역할을 아주 잘 수행하였습니다.
이렇게 콤포넌트를 사용하면, 대규모 앱에서 Vue 세계를 좀 더 쉽게 관리할 수 있습니다.

<p class="tip">
  Vue 세계의 콤포넌트에 대해서 더 궁금하신 것이 있으신가요?

  [이곳에서](components.html) 더 많은 이야기를 하겠습니다.
</p>

또 한 가지의 예제를 통해 이해를 도와 드리겠습니다.

``` html
<div id="app">
  <app-nav></app-nav>
  <app-view>
    <app-sidebar></app-sidebar>
    <app-content></app-content>
  </app-view>
</div>
```

### 사용자 정의 엘리먼트와의 관계

Vue 컴포넌트는 [Web Components Spec](http://www.w3.org/wiki/WebComponents/)의 일부인 **사용자 지정 엘리먼트** 와 매우 유사하다는 것을 눈치 챘을 수 있습니다. Vue의 컴포넌트 구문은 스펙 이후 느슨하게 모델링 되었기 때문입니다. 예를 들어 Vue 컴포넌트는 [Slot API](https://github.com/w3c/webcomponents/blob/gh-pages/proposals/Slots-Proposal.md)와 `is` 특수 속성을 구현합니다. 그러나 몇가지 중요한 차이가 있습니다.

1. Web Components Spec은 여전히 초안이며 모든 브라우저에서 기본적으로 구현되지 않습니다. 이에 비해 Vue 컴포넌트는 지원되는 모든 브라우저 (IE 9 이상)에서 폴리필을 필요로 하지 않으며 일관되게 작동합니다. 필요한 경우 Vue 컴포넌트는 기본 사용자 정의 엘리먼트 내에 래핑할 수 있습니다.

2. Vue 컴포넌트는 일반 사용자 정의 엘리먼트에서 사용할 수 없는 중요한 기능을 제공합니다. 특히 컴포넌트 데이터 흐름, 사용자 지정 이벤트 통신 및 빌드 도구 통합이 중요합니다.

## 더 해야 할 것은 무엇인가요?

어떠신가요. Vue 세계를 조작하는 것은 재미있었나요?

앞으로 더 흥미진진한 이야기를 할 터이니, 가이드를 천천히 읽어나가면 이곳에서 설명하지 못한 Vue 세계의 나머지 부분 그리고 고급 기능에 대해서 알 수 있게 될 것입니다.

<p class="tip">
  **축하합니다.**

  이제 어엿한 Vue 세계의 창조주가 되었습니다.
</p>
