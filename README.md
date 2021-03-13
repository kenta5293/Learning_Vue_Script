# Vue.js 공부하기!
### #01 Vue 인스턴스 생성하기

```
<div id="app">
  {{ name }}
</div>

<script>
  new Vue({
    el: '#app',
    data: {
     name: 'kenta'
    }
  }
</script>
```
Vue.js에서 데이터를 쓸 때에는 중괄호 2개 안에 쓴다.   


### #02 메소드(Methods) 사용하기
```
new Vue({
  el: '#app',
  data: {
    person: {
      name: 'kenta',
      age: 19
    }
  },
  methods: {
    nextYear(greeting) {
      return `${greeting}! ${thperson.name}는(은) ${(thperson.age + 1)}살 입니다.`;
    },
    otherMethod: function() {
      this.nextYear();
    }
  }
});
```
함수를 사용할 때에는 인스턴스에 methods에 함수를 추가하여 사용하고, 함수 안에 함수를 넣는 것도 가능하다.   
그리고 함수는 "함수이름: fucntion() { }" 이런식으로 작성해도 되지만, function을 생략하고 작성해도 무관하다.   
__Ex.__
```
nextYear: function(greeting) { }

nextYear(greeting) { }
// 둘이 동일하다.
```

매개변수를 사용할 때에는 {{ nextYear(매개변수) }} 이렇게 넣어주면 된다.   
__Ex.__
```
{{nextYear('안녕하세요')}}
```


### #03 데이터 바인딩 (Data Binding)
__v-bind:__   
HTML 태그 속성에도 데이터 값을 넣어줄 수 있다.   
또한, 함수를 넣는 것도 가능하다.   

__Ex.__
```
<div id="app">
  <input v-bind:type: "type">
  <input :type: "type">

  <!-- v-bind:를 생략하고 : 만 작성해도 상관없다. -->

  <a :href: "getLink('kenta5293')"> 이동하기 </a>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    type: 'text',
    link: 'https://github.com/'
  },
  methods: {
    getLink(nickname) {
      return this.link + nickname
    }
  }
})
</script>
```