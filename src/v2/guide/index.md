---
title: 시작하기
type: guide
order: 2
---

## Vue 가 무엇인가요?

Vue(/vjuː/ 로 발음, **view** 와 발음이 같습니다.)는 사용자 인터페이스를 만들기 위한 **미래형 프레임워크** 입니다. 다른 단일형 컴포넌트 프레임워크들과는 다르게, 마치 어린이들의 장난감 레고처럼 하나 둘 씩 확장시켜 나아가 마지막으로는 아주 멋진 앱이 만들어 질 수 있도록 설계되었습니다.  
Vue의 코어는 사용자의 인터페이스만 집중합니다. 때문에 다른 자바스크립트 라이브러리를 사용한다거나, 기존에 있던 프로젝트에 Vue를 사용하려고 할 때 아무런 제약이 없습니다.  
또, Vue를 사용하여 개발할 때 공식 [도구](single-file-components.html) 또는 [라이브러리](https://github.com/vuejs/awesome-vue#libraries--plugins) 를 함께 사용한다면, 좀 더 쉽고 편하게 개발할 수 있습니다.

많은 자바스크립트 라이브러리와 프레임워크를 경험해보셨다면, Vue의 성능이 궁금하실 겁니다. 지금 바로 [비교 결과](comparison.html)를 확인하세요.

## Vue 세계에 오신 것을 환영합니다.

<p class="tip">
  **프론트엔드는 처음이신가요?**

  HTML 과 CSS 그리고 자바스크립트를 유연하게 다룰 수 없다면, 가이드를 따라가기 어려울 수 있습니다.

  Vue는 정말 쉽지만, 가이드를 천천히 따라가다 이해하기 어렵다면 먼저 웹 개발의 기본을 익히신 후에 진행해보세요. 그럼 Vue의 매력에 빠져 헤어나올 수 없을 거라고 확신합니다!
</p>

Vue의 세계에 접속하기 전에, 간접 체험을 해보고 싶으신가요? [JSFiddle Hello World 예제](https://jsfiddle.net/chrisvfritz/50wL7mdz/)

<p class="tip">
  예제에 접속하는 순간.. 이미 Vue의 매력에 빠져있을 겁니다.
</p>

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
    message: '인간보다는 기계가 더 믿을만 하죠. - 토니 스타크'
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
    message: '인간보다는 기계가 더 믿을만 하죠. - 토니 스타크'
  }
})
</script>
{% endraw %}

<p class="tip">
  축하합니다! 첫 Vue 앱을 만들었습니다.
</p>

단순히 문자열을 렌더링하는 것과 비슷하지만, Vue 는 더 많은 일을 합니다.

<p class="tip">
  엘리먼트를 Vue 에 등록하는 순간, 마법이 펼쳐집니다.
</p>

마법을 경험하셨나요? 위처럼 엘리먼트를 Vue 에 등록하게 되면, 해당 엘리먼트는 **Vue 콤포넌트** 가 됩니다. 모든 콤포넌트는 Vue의 세계를 관리하는 DOM에 연결되어, 모든 일이 **반응형**이 됩니다.

에이~.. 이렇게 간단한 문법으로 어떻게 어떻게 반응형이 되냐구요? 그렇다면 브라우저 자바스크립트 콘솔을 열고 `app 콤포넌트의 message` 를 다른 값으로 설정해보세요! 다시 한 번 마법이 펼쳐집니다.

<p class="tip">
  Vue 세계에서는 단순히 문자열 렌더링 이외에도 많은 일을 할 수 있습니다.
</p>

``` html
<div id="app-2">
  <span v-bind:title="message">
    내 위에 마우스를 올리면 동적으로 바인딩 된 title을 볼 수 있습니다!
  </span>
</div>
```
``` js
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: '이 페이지는 ' + new Date() + ' 에 로드 되었습니다'
  }
})
```
{% raw %}
<div id="app-2" class="demo">
  <span v-bind:title="message">
    내 위에 마우스를 올리면 동적으로 바인딩 된 title을 볼 수 있습니다!
  </span>
</div>
<script>
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: '이 페이지는 ' + new Date() + '에 로드 되었습니다'
  }
})
</script>
{% endraw %}

여기서 우리는 새로운 곳에 다다랐습니다. `v-bind` 속성은 **지시문**이라고 부릅니다. 지시문은 Vue에서 제공하는 특수 속성임을 나타내는 `v-` 접두어가 붙어있으며 사용자가 짐작할 수 있듯 렌더링 된 DOM에 특수한 반응형 동작을 합니다. 기본적으로 "이 요소의 `title` 속성을 Vue 인스턴스의 `message` 속성으로 최신 상태를 유지 합니다."

JavaScript 콘솔을 다시 열고 `app2.message = '새로운 메시지'`라고 입력하면 HTML(이 경우에 `title` 속성)이 업데이트되었음을 다시 한번 확인할 수 있습니다.

## 조건문과 반복문

엘리먼트의 존재 여부를 토글하는 것은 아주 간단합니다.

``` html
<div id="app-3">
  <p v-if="seen">이제 나를 볼 수 있어요</p>
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
  <span v-if="seen">이제 나를 볼 수 있어요</span>
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

계속해서, `app3.seen = false` 를 콘솔에 입력하세요. 메시지가 사라지는 것을 확인해야 합니다.

이 예제는 텍스트와 속성뿐 아니라 DOM의 **구조**에도 데이터를 바인딩 할 수 있음을 보여줍니다. 또한 Vue 엘리먼트가 Vue에 삽입/갱신/제거될 때 자동으로 [전환 효과](transitions.html)를 적용할 수 있는 강력한 시스템을 제공합니다.

몇가지 지시문이 있습니다. 지시문마다 고유한 기능이 있습니다. 예를 들어 `v-for` 지시문은 배열의 데이터를 사용해 항목 목록을 표시하는 데 사용할 수 있습니다.

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
      { text: 'JavaScript 배우기' },
      { text: 'Vue 배우기' },
      { text: '무언가 멋진 것을 만들기' }
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
      { text: 'JavaScript 배우기' },
      { text: 'Vue 배우기' },
      { text: '무언가 멋진 것을 만들기' }
    ]
  }
})
</script>
{% endraw %}

콘솔에서, `app4.todos.push({ text: 'New item' })`을 입력하십시오. 목록에 새 항목이 추가되어야 합니다.

## 사용자 입력 핸들링

사용자가 앱과 상호 작용할 수 있게 하려면 `v-on` 지시문을 사용하여 Vue 인스턴스에 메소드를 호출하는 이벤트 리스너를 추가 할 수 있습니다.

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
    message: '안녕하세요! Vue.js!'
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
    message: '안녕하세요! Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
</script>
{% endraw %}

이 메소드에서 우리는 단순히 DOM을 건드리지 않고 앱의 상태를 업데이트 합니다. 모든 DOM 조작은 Vue에 의해 처리되며 작성한 코드는 기본 로직에만 초점을 맞춥니다.

Vue는 또한 양식에 대한 입력과 앱 상태를 양방향으로 바인딩하는 `v-model` 지시문을 제공합니다.

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
    message: '안녕하세요 Vue!'
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
    message: '안녕하세요 Vue!'
  }
})
</script>
{% endraw %}

## 컴포넌트를 사용한 작성방법

컴포넌트 시스템은 Vue의 또 다른 중요한 개념입니다. 이는 작고 그 자체로 제 기능을 하며 재사용할 수 있는 컴포넌트로 구성된 대규모 응용 프로그램을 구축할 수 있게 해주는 추상적 개념입니다. 생각해보면 거의 모든 유형의 응용 프로그램 인터페이스를 컴포넌트 트리로 추상화할 수 있습니다.

![컴포넌트 트리](/images/components.png)

Vue에서, 컴포넌트는 본질적으로 미리 정의된 옵션을 가진 Vue 인스턴스 입니다. Vue에 컴포넌트를 등록하는 것은 간단합니다.

``` js
// todo-item 이름을 가진 컴포넌트를 정의합니다
Vue.component('todo-item', {
  template: '<li>할일입니다.</li>'
})
```

이제 다른 컴포넌트의 템플릿에서 사용할 수 있습니다.

``` html
<ol>
  <!-- todo-item 컴포넌트의 인스턴스 만들기 -->
  <todo-item></todo-item>
</ol>
```

그러나 이는 모든 할 일에 대해 같은 인스턴스를 렌더링 합니다. 부모 범위의 데이터를 하위 컴포넌트로 전달할 수 있어야 합니다. [prop](components.html#Props)을 허용하도록 컴포넌트 정의를 수정 해 보겠습니다.

``` js
Vue.component('todo-item', {
  // 이제 todo-item 컴포넌트는 사용자 정의 속성과 같은
  // "prop"를 허용합니다. 이 prop는 todo라고 합니다.
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
```

이제 todo를 `v-bind`를 사용하여 반복된 각 컴포넌트에 전달할 수 있습니다.

``` html
<div id="app-7">
  <ol>
    <!-- 각 todo-item 에 todo 객체를 제공합니다. -->
    <!-- 그것의 컨텐츠는 동적입니다. -->
    <todo-item v-for="item in groceryList" v-bind:todo="item"></todo-item>
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
    groceryList: [
      { text: '채소' },
      { text: '치즈' },
      { text: '사람이 먹을 수 있는 무엇이든' }
    ]
  }
})
```
{% raw %}
<div id="app-7" class="demo">
  <ol>
    <todo-item v-for="item in groceryList" v-bind:todo="item"></todo-item>
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
    groceryList: [
      { text: '채소' },
      { text: '치즈' },
      { text: '사람이 먹을 수 있는 무엇이든' }
    ]
  }
})
</script>
{% endraw %}

이것은 예시를 위한 예제 입니다. 하지만 우리는 앱을 두개의 더 작은 단위로 나눌 수 있었고 자식은 부모로부터 prop 인터페이스를 통해 합리적으로 잘 분리하였습니다. 부모 앱에 영향을 주지 않으면서 더 복잡한 템플릿과 로직으로 `<todo-item>` 컴포넌트를 더욱 향상시킬 수 있습니다.

대규모 응용 프로그램에서는 개발을 쉽게 관리할 수 있도록 전체 앱을 컴포넌트로 나누어야 합니다. [나중에 이 가이드](components.html)에서 컴포넌트에 대해 더 많은 이야기를 나누겠습니다. 하지만 여기서는 컴포넌트로 앱의 템플릿이 어떻게 표시되는지에 대한 예를 보겠습니다.

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

## 더 해야할 것은 무엇인가요?

우리는 Vue.js 코어의 가장 기본적인 기능을 간략하게 소개했습니다. 이 가이드의 나머지 부분에서 더 자세한 세부 내용이 포함된 다른 고급 기능에 대해 다룰 예정이므로 꼭 읽어보시기 바랍니다.
