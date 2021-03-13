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