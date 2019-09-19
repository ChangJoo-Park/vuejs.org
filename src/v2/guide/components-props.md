---
title: props
type: guide
order: 102
---

> 이 페이지는 여러분이 이미 [컴포넌트 기초](components.html)를 읽었다고 가정하고 쓴 내용입니다. 컴포넌트가 처음이라면 기초 문서를 먼저 읽으시기 바랍니다.
> (역자 주: 아래 문서는 컴포넌트의 옵션 중 하나인 `props`를 다루고 있습니다. 해당 옵션은 'props'로 표기하고 property는 속성으로, prop은 때에 따라 props의 요소 혹은 속성으로 번역했습니다.)

## props의 표기법 (카멜표기법 vs 케밥표기법)

HTML 인자의 이름들은 대소문자를 가리지 않습니다. 브라우저가 모든 대문자를 소문자로 변환하기 때문입니다. 'in-DOM 템플릿'을 사용할 때 카멜표기법 방식의 props의 표기를 케밥표기법(하이픈으로 단어를 구분하는 표기법)으로 바꿔야 하는 이유입니다.

```js
Vue.component("blog-post", {
  // 자바스크립트에서는 카멜표기법(postTitle) 사용
  props: ["postTitle"],
  template: "<h3>{{ postTitle }}</h3>"
});
```

```html
<!-- HTML에서는 케밥표기법(post-title) 사용 -->
<blog-post post-title="hello!"></blog-post>
```

하지만 문자 템플릿을 사용한다면 이 제한이 적용되지 않습니다.

## props의 타입

이제까지는 아래와 같이 주로 문자 배열로 된 props를 살펴봤습니다.

```js
props: ["title", "likes", "isPublished", "commentIds", "author"];
```

보통은 props의 각 요소 별로 특정한 타입이 필요합니다. 그럴 경우에는 props 각 요소의 이름과 타입을 함께 저장하는 객체 방식을 사용할 수 있습니다.

```js
props: {
  title: String,
  likes: Number,
  isPublished: Boolean,
  commentIds: Array,
  author: Object,
  callback: Function,
  contactsPromise: Promise // 다른 생성자 사용 가능
}
```

이를 통해 컴포넌트를 문서화할 뿐만 아니라 브라우저의 자바스크립트 콘솔 사용자들이 잘못된 타입을 사용했을 때 경고를 줄 수 있습니다. [타입 확인과 다른 props 검증](#props-검증)에 대해서는 아래쪽에서 더 다룰 것입니다.

## 고정된 props와 가변적인 props를 전달하는 방법

이제까지는 아래와 같이 고정된 값을 props로 넘기는 사례들을 살펴봤습니다.

```html
<blog-post title="My journey with Vue"></blog-post>
```

하지만 아래와 같이 `v-bind`를 이용해서 가변적으로 props를 정하는 것도 가능합니다.

```html
<!-- 변수값을 가변적으로 배정합니다 -->
<blog-post v-bind:title="post.title"></blog-post>

<!-- 복잡한 표현식을 통해 가변적으로 데이터를 배정합니다 -->
<blog-post v-bind:title="post.title + ' by ' + post.author.name"></blog-post>
```

위의 두 사례에서는 문자를 이용했지만 _어떤_ 타입의 값도 props에 사용할 수 있습니다.

### 숫자 이용하기

```html
<!-- `42`는 고정된 값이지만 v-bind를 사용하면 Vue에 이것이 문자가 -->
<!-- 아니고 자바스크립트 표현식이라는 것을 알려줄 수 있습니다      -->
<blog-post v-bind:likes="42"></blog-post>

<!-- 변수값을 가변적으로 배정합니다 -->
<blog-post v-bind:likes="post.likes"></blog-post>
```

### 불리언 이용하기

```html
<!-- 아무 속성 값이 없으면 `true`를 뜻합니다 -->
<blog-post is-published></blog-post>

<!-- `false`는 고정된 값이지만 v-bind를 사용하면 Vue에 이것이 문자가 -->
<!-- 아니고 자바스크립트 표현식이라는 것을 알려줄 수 있습니다      -->
<blog-post v-bind:is-published="false"></blog-post>

<!-- 변수값을 가변적으로 배정합니다 -->
<blog-post v-bind:is-published="post.isPublished"></blog-post>
```

### 배열 이용하기

```html
<!-- 아래의 배열이 고정된 값이지만 v-bind를 사용하면 Vue에 이것이 -->
<!-- 문자가 아니고 자바스크립트 표현식이라는 것을 알려줄 수 있습니다 -->
<blog-post v-bind:comment-ids="[234, 266, 273]"></blog-post>

<!-- 변수값을 가변적으로 배정합니다 -->
<blog-post v-bind:comment-ids="post.commentIds"></blog-post>
```

### 객체 이용하기

```html
<!-- 아래의 객체는 고정된 값이지만 v-bind를 사용하면 Vue에 이것이 -->
<!-- 문자가 아니고 자바스크립트 표현식이라는 것을 알려줄 수 있습니다 -->
<blog-post
  v-bind:author="{
    name: 'Veronica',
    company: 'Veridian Dynamics'
  }"
></blog-post>

<!-- 변수값을 가변적으로 배정합니다 -->
<blog-post v-bind:author="post.author"></blog-post>
```

### 객체의 구성요소 이용하기

객체의 모든 구성요소(property)들을 props로 전달하려면 인수가 없는 `v-bind`(즉 `v-bind:prop-name` 대신 `v-bind`)를 이용할 수 있습니다. `post` 객체의 예를 살펴봅시다.

```js
post: {
  id: 1,
  title: 'My Journey with Vue'
}
```

템플릿이 아래와 같으면

```html
<blog-post v-bind="post"></blog-post>
```

아래와 같은 결과가 나옵니다.

```html
<blog-post v-bind:id="post.id" v-bind:title="post.title"></blog-post>
```

## 단방향 데이터 흐름

모든 props의 데이터들은 자식 컴포넌트의 속성과 부모 컴포넌트의 속성 사이에서 **단방향 바인딩**을 형성합니다. 부모 컴포넌트의 속성이 업데이트되면 하위로 흐르게 되지만 그 반대는 안됩니다. 이렇게하면 자식 컴포넌트가 실수로 부모 컴포넌트의 상태를 변경하여 앱의 데이터 흐름을 이해하기 어렵게 만드는 것을 방지할 수 있습니다.

그리고 부모 컴포넌트가 업데이트 될 떄마다 자식 컴포넌트의 모든 속성들이 최신값으로 갱신됩니다. 즉 자식 컴포넌트의 속성들을 굳이 변경시킬 필요가 **없는** 겁니다. 만약 사용자가 그렇게 하면 Vue에서 콘솔을 통해 경고를 줄 것입니다.

일반적으로 (역자 주: 상위 컴포넌트의 속성이 바뀌었을 때 하위) 컴포넌트의 속성을 변경시켜야 하는가 싶을 때가 두 가지 있습니다.

1. **그 속성이 초기값을 전달할 때 사용되며 자식 컴포넌트는 이를 받아서 로컬 데이터 속성으로 이용하는 경우.** 이 경우에는 자식 컴포넌트에 로컬 데이터 속성을 따로 정의하고 전달받는 속성은 초기값으로만 쓰는 것이 좋습니다.(역자 주: 즉 이후에 전달받은 속성을 따로 업데이트할 필요 없습니다.)

```js
props: ['initialCounter'],
data: function () {
  return {
    counter: this.initialCounter
  }
}
```

2. **전달된 속성을 그대로 쓰는 것이 아니라 적절하게 가공해서 사용할 떄.** 이 경우에는 전달된 속성의 값을 이용해서 computed 속성을 정의해놓는 것이 좋습니다.(역자 주: 즉 알아서 업데이트 되니까 신경쓰지 않아도 됩니다.)

```js
props: ['size'],
computed: {
  normalizedSize: function () {
    return this.size.trim().toLowerCase()
  }
}
```

<p class="tip">자바스크립트의 객체와 배열은 참조로 전달되므로 전달되는 속성이 배열이나 객체인 경우 자식 컴포넌트의 객체 또는 배열 자체를 변경하면 부모 컴포넌트의 데이터에 **영향을 줍니다**.</p>

## props 검증

컴포넌트가 props에 대해서 앞에서 봤던 타입 등 구체적인 조건을 지정할 수도 있습니다. 조건이 맞지 않으면 Vue에서 브라우저의 자바스크립트 콘솔을 통해 사용자에게 경고를 보낼 것입니다. 이 기능은 다양한 사람들이 사용할 컴포넌트를 만들 때 특히 유용합니다.

props에 대한 검증 조건을 구체화하기 위해 각 props의 값에 대한 검증 조건을 객체 형태로 제시할 수 있습니다. 아래의 예를 살펴봅시다.

```js
Vue.component("my-component", {
  props: {
    // 기본적인 타입 확인 (`null`, `undefined`는 어떤 타입 검증도 통과합니다.)
    propA: Number,
    // 복수의 타입이 가능한 경우
    propB: [String, Number],
    // 문자 타입이며 필수값
    propC: {
      type: String,
      required: true
    },
    // 기본값이 있는 숫자 타입
    propD: {
      type: Number,
      default: 100
    },
    // 기본값이 있는 객체 타입
    propE: {
      type: Object,
      // 객체나 배열의 기본값은 반드시 팩토리 함수로 표현되어야 합니다.
      default: function() {
        return { message: "hello" };
      }
    },
    // 검증 함수를 만들 수도 있습니다.
    propF: {
      validator: function(value) {
        // value가 반드시 아래의 문자 중 하나여야 합니다.
        return ["success", "warning", "danger"].indexOf(value) !== -1;
      }
    }
  }
});
```

props에 대한 검증이 실패하면 Vue가 콘솔에 경고를 날립니다.(물론 개발 모드일 때요.)

<p class="tip">props에 대한 검증은 컴포넌트 인스턴스를 만들기 **전에** 진행한다는 점을 주의하세요. 인스턴스의 속성들(`data`, `computed` 등)은 그래서 `기본값`이나 `검증 함수`에 쓸 수 없습니다.</p>

### 타입 확인

`type`은 다음의 자바스크립트 고유 생성자들 중 하나일 수 있습니다.

- String(문자)
- Number(숫자)
- Boolean(불리언)
- Array(배열)
- Object(객체)
- Date(날짜)
- Function(함수)
- Symbol(심벌)

아니면 `type`이 다른 커스텀 생성자 함수일 수도 있고 `instanceof` 를 이용해서 나중에 확인할 수도 있습니다. 아래의 예에서 생성자 함수를 봅시다.

```js
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}
```

이렇게 이용할 수 있겠죠.

```js
Vue.component("blog-post", {
  props: {
    author: Person
  }
});
```

`author` 속성의 값은 `new Person`을 통해서 만들어진 값입니다.

## 속성이 아닌 인자들

속성이 아닌 인자란 컴포넌트로 넘겨지는 인자이긴 하지만 해당하는 정의된 속성은 없는 것을 의미합니다.

자식 컴포넌트로 정보를 넘길 때 명시적으로 정의된 속성이 더 선호된 것은 사실이지만 컴포넌트 라이브러리를 만드는 사람들이 컴포넌트가 사용될 상황을 항상 예측할 수는 없습니다. 그래서 컴포넌트에서 컴포넌트의 루트 요소에 임의적인 인자를 추가할 수 있게 만들어 뒀습니다.

예를 들어 `bootstrap-date-input`라는 서드파티 컴포넌트를 쓰고 있다고 생각해봅시다. 이 컴포넌트는 `input`에 `data-date-picker` 인수를 필요로 합니다. 아래와 같이 컴포넌트 인스턴스에 이 인수를 추가할 수 있죠.

```html
<bootstrap-date-input data-date-picker="activated"></bootstrap-date-input>
```

`data-date-picker="activated"` 인수는 자동으로 `bootstrap-date-input` 컴포넌트의 루트 요소에 추가됩니다.

### 기존 인수를 대체하거나 기존 인수에 합치기

`bootstrap-date-input`의 템플릿을 생각해봅시다.

```html
<input type="date" class="form-control" />
```

날짜를 고르는 플러그인에 쓸 테마를 만들기 위해 특정한 클래스를 아래와 같이 추가할 수 있습니다.

```html
<bootstrap-date-input
  data-date-picker="activated"
  class="date-picker-theme-dark"
></bootstrap-date-input>
```

이 경우에 `class`에 대한 두 가지 값이 정의됩니다.

- `form-control`, 템플릿에 있는 컴포넌트에 의해서 정해진 값
- `date-picker-theme-dark`, 부모 컴포넌트에서 전달된 값

대부분의 인수들은 컴포넌트로 전달된 값이 컴포넌트에서 정해진 값을 대체합니다. 예를 들어 `type="text"`가 전달되면 `type="date"`를 대체하고 에러가 나는 거죠. 다행히도 `class`, `style` 인수는 조금 더 똑똑해서 두 값을 `form-control date-picker-theme-dark`로 합칩니다.

### 인수 상속 금지

만약 컴포넌트의 루트 요소가 인수를 상속받는 걸 **금지**하고 싶다면 컴포넌트의 옵션에서 `ingeritAttrs: false`를 지정할 수 있습니다. 아래의 예를 봅시다.

```js
Vue.component("my-component", {
  inheritAttrs: false
  // ...
});
```

`$attrs` 인스턴스 속성과 함께 쓰면 특히 유용합니다. `$attrs` 인스턴스 속성에는 속성의 이름과 컴포넌트로 넘기는 값이 들어 있습니다. 아래의 예를 봅시다.

```js
{
  required: true,
  placeholder: 'Enter your username'
}
```

`inheritAttrs: false`와 `$attrs`를 사용하면 어느 요소를 어떻게 할 지를 따로 정할 수 있습니다. [베이스 컴포넌트](../style-guide/#베이스-컴포넌트-이름-매우-추천함)에 적합한 방식입니다.

```js
Vue.component("base-input", {
  inheritAttrs: false,
  props: ["label", "value"],
  template: `
    <label>
      {{ label }}
      <input
        v-bind="$attrs"
        v-bind:value="value"
        v-on:input="$emit('input', $event.target.value)"
      >
    </label>
  `
});
```

<p class="tip">`inheritAttrs: false` 옵션은 `style`, `class` 요소를 통한 통합에는 영향을 미칠 수 **없습니다**.</p>

이 패턴을 통해 어느 요소가 실제로 어느 루트 요소에 있는지를 신경쓰지 않고 베이스 컴포넌트를 HTML 요소처럼 쓸 수도 있습니다.

```html
<base-input
  v-model="username"
  required
  placeholder="Enter your username"
></base-input>
```
