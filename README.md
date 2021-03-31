# Vue.js 공부하기!
Vue.js 공식문서   
: __https://kr.vuejs.org/v2/guide/__


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

---

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

---

### #03 데이터 바인딩 (Data Binding)
__v-bind:__   
HTML 태그 속성에도 데이터 값을 넣어줄 수 있다.   
또한, 함수를 넣는 것도 가능하다.   

__Ex.__
```
<div id="app">
  <input v-bind:type="type">
  <input :type="type">

  <!-- v-bind:를 생략하고 : 만 작성해도 상관없다. -->

  <a :href="getLink('kenta5293')"> 이동하기 </a>
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

---

### #04 이벤트 (Events)
__v-on:__   
이벤트 앞에 v-on을 작성하는 것으로 이벤트를 생성할 수 있다.   
또, 데이터 바인딩과 같이 v-on을 @ 으로 대체할 수 있다.    

__Ex.__
```
<div id="app>
  <form v-on:submit.prevent="submit">
    <input type="text">
    <button>Submit</button>
  </form>
</div>

<script>
  new Vue({
    el: '#app',
    data: {
    },
    methods: {
      submit() {
        alert('Hello')
        console.log('Hello')
      }
    }
  });
</script>
```

Submit 버튼을 누르면 methods에 작성된 submit() 함수가 실행되며,   
.prevent는 수식어로, Vue.js 에는 수식어가 존재한다.   
.prevent는 자바스크립트 기본 문법의 event.preventDefault()를 호출하는 것이다.   
외에도 다양한 수식어가 있으니 Vue.js 공식 사이트를 참고하면 좋을 듯 하다.   
__https://kr.vuejs.org/v2/api/index.html#v-on__

---

### #05 데이터 양방향 바인딩 (Data Two Way Binding)
__v-model__   
v-model="데이터"를 작성하는 것으로 데이터 양방향 바인딩이 가능하다.   
__데이터 → 뷰__ 의 형태로 데이터의 값을 뷰로 업데이트하여 보여주는 것을 __단방향 바인딩__ 이라고 한다.   
한 방향으로 흐르는 것과 다르게 __데이터 ⇄ 뷰__ 형태로 바인딩하여 양 방향으로 흐르게 해주는 것을 __양방향 바인딩__ 이라고 한다.   
즉, 데이터에 있는 값이 뷰에 나타나고, 이 뷰의 값이 바뀌면 데이터의 값도 바뀌는 것이다.

__Ex.__
```
<div id="app">
  <form v-on:submit.prevent="submit">
    <input type="text" v-model="text" ><br>
    {{ text }}<br>
  </form>
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      text: 'text'
    },
  });
</script>
```

---

### #06 Computed 속성
__Computed__   
간단한 연산의 경우 {{ }} 안에 넣어도 괜찮으나, 많은 연산이 들어갈 경우 코드가 비대해지고, 유지보수가 어렵다고 한다.   
이를 해결하기 위해 사용해야하는 것이 바로 __computed 속성__ 이다.   

__Ex.__
```
<div id="app">
  {{ reversedMessage }}
  <!-- '안녕하세요'의 역순인 '요세하년안'이 출력된다. -->
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      message: '안녕하세요'
    },
    methods: {

    },
    computed: {
      reversedMessage() {
        return this.message.split('').reverse().join('');
      }
    }
  });
</script>
```

Computed 속성은 computed 라는 오브젝트 안에 작성하는 것으로, 템플릿 안에는 {{ reversedMessage }} 와 같이 작성한다.   
메소드와의 차이점으로는 메소드는 템플릿에 () 소괄호를 꼭 작성해야하지만 Computed에 정의된 경우에는 소괄호를 작성하지 않는다!   

다른 차이점으로 Computed는 캐싱을 하고, 메소드는 캐싱을 하지 않는다는 점이다!   
Computed는 처음 한번만 연산하여 __저장(캐싱)__ 을 하여 값을 가지고 있고, 종속 대상이 바뀔 때에만 함수를 다시 실행한다.   
즉, 몇 번을 요청해도 처음 계산했던 결과를 즉시 반환해주는 것이다.   
메소드의 경우에는 요청될 때마다 data에서 가져와 여러번 연산을 하고 return을 해주는 것이다.   

---

### #07 Watch 속성
__Watch__   
Watch 속성은 가끔 Computed 속성을 쓸 수 없는 상황일 때 사용하면 된다. Computed 속성으로 구현 가능한 것이면 Computed 속성을 사용하면 된다.   
Watch 속성은 감시하고 있는 데이터가 바뀌면 작동을 한다.

__Ex.__
```
<div id="app">
  {{ message }}<br>
  <button @click="changeMessage">Click</button><br>
  {{ updated }}
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      message: '안녕하세요',
      updated: '안녕못해요'
    },
    methods: {
      changeMessage() {
        this.message = "Hello"
      }
    },
    watch: {
      message(newVal, oldVal) {
        console.log(newVal, oldVal);
        this.updated = "NO Hello!";
      }
    }
  });
</script>
```

Watch속성을 사용할 때에는 감시하고 싶은 데이터를 함수 형식으로 작성하면 된다. 위의 예제에선 "message"를 감시하고 있으므로 watch 안에 "message"라는 함수를 만든 것이다.   
또 매개변수로 __newValue__ 와 __oldValue__ 를 받는데, 업데이트 된 값이 첫번째(newValue)에 들어오고, 기존의 값이 두번째(oldValue)에 들어오게 된다.

---

### #08 클래스 & 스타일 바인딩
클래스와 스타일 바인딩도 데이터 바인딩을 했던 것과 같이 v-bind: 혹은 : 문자로 할 수 있다.   
밑의 예시를 보면서 알아보도록 하자.   

__Ex.__
css
```
.red {
  color: red;
}
.bold-text {
  font-weight: bold;
}
```

template & js
```
<div id="app">
  <!-- 클래스 바인딩 -->
  <div :class="{ red: isRed, 'bold-text': isBold }">Hello</div>

  <!-- 스타일 바인딩 -->
  <div :style="{ color: red, fontSize: size}">He
  <button @click="update">Click</button>
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      isRed: false,
      isBold: false,
      red: 'red',
      size: '30px'
    },
    methods: {
      update() {
        this.isRed = !this.isRed;
        this.isBold = !this.isBold;
      }
    }
  });
</script>
```

> 먼저 클래스 바인딩에 대해 알아보면, 스타일의 이름이 앞에 나오고 :(콜론) 뒤에 그 값이 true 혹은 false의 값을 가진 데이터가 나와있다.   
위 코드에선 버튼을 클릭하면 update라는 메소드의 실행으로 원래 false 였던 isRed와 isBold의 값을 true로 바꾸면서 첫번째 div태그에 클래스를 적용하게 된다.   
또한, 두개의 class를 적용하고 싶다면 ,를 이용하면 되고, class 이름에 "-"가 존재한다면, String으로 묶어주어야 한다.

> 다음으로 스타일 바인딩에 알아보면 :style로 작성하며 {} 안에는 자바스크립트로 작성하기 때문에 css의 속성으로 적는 것이 아닌 자바스크립트 형태로 속성을 작성해야 한다. 그 뒤에는 data의 값을 넣어주면 적용된다.

---

### #09 v-if & v-show
#### v-if
v-if는 vue.js의 조건문으로 조건을 작성하여 값이 만약 true라면 그 요소를 렌더링 해준다.   
v-else를 이용하여 false일 경우의 값을 출력할 수도 있다. 또한, v-else-if 도 존재하여 다른 경우에 대한 요소도 여러 번 연결하여 렌더링 가능하다.   

__Ex.__
```
<div id="app">
  <template v-if="number === 1">
    <div>1</div>
    <div>2</div>
    <div>3</div>
  </template>
  <div v-else-if="number === 3">It is 3</div>
  <div v-else>No</div>
  <button @click="increaseNumber">Up</button> {{ number }}
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      number: 1,
    },
    methods: {
      increaseNumber() {
        this.number++;
      }
    }
  });
</script>
```
위는 number의 값이 1일 경우 123을 출력하고, 버튼을 눌러 number의 값이 커져 3이 될 경우 "It is 3"을 출력하는 예제이다. 또, 그 외의 값은 else 를 통해 No를 출력한다.   
그리고 위에서는 < templeate /> 라는 태그를 이용하여 두개 이상의 요소 즉 123을 묶어서 보이게 할 수 있다.


#### v-show
v-show 또한 v-if와 매우 비슷하다. v-show는 v-if와 다르게 < template /> 태그를 사용할 수 없으며, v-else와 같은 기능을 하는 속성이 존재하지 않다. 가장 큰 차이점은 v-if는 렌더링을 아예 하지 않지만, v-show는 렌더링을 하고 css의 속성 중 하나인 "display: none"을 toggle 을 한다.   

__Ex.__
```
  <div id="app">
    <div v-show="show">Yes</div>
    <button @click="toggle">Show</button>
  </div>

  <script>
    new Vue({
      el: '#app',
      data: {
        show: false
      },
      methods: {
        toggle() {
          this.show = !this.show;
        }
      }
    });
  </script>
```

위의 예제를 보면 알 수 있듯이, v-show는 v-if에 비해 매우 간단하다. 공식문서에서는 v-show는 자주 토글해야할 때 즉 없어지거나 렌더링되어야 할 때 사용하고 그 외에는 v-if를 사용하는 것을 권장한다.

---

### #10 v-for & 리스트 렌더링
v-for는 배열을 기반으로 리스트를 렌더링 할 수 있다. v-for는 "item in items" 라는 특별한 문법으로 작성되며, 여기서 items는 원본 배열의 이름이며, item은 별칭이다. 밑의 예제를 확인해보자.

__Ex.__
```
<div id="app">
  <div>
    {{ people[0].name }} / {{ people[0].age }}
  </div>
  <div>
    {{ people[1].name }} / {{ people[1].age }}
  </div>
  <div>
    {{ people[2].name }} / {{ people[2].age }}
  </div>
  <div>
    {{ people[3].name }} / {{ people[3].age }}
  </div>

  <hr>

  <!-- v-for 이용 -->
  <div v-for="(person, index) in people" :key="person.id">
    {{ person.name }} / {{ person.age }} / {{ index }}
  </div>
</div>


<script>
  new Vue({
    el: '#app',
    data: {
      people: [
        { id: 1, name: "a", age: 20 },
        { id: 2, name: "b", age: 21 },
        { id: 3, name: "c", age: 22 },
        { id: 4, name: "d", age: 23 },
        { id: 5, name: "e", age: 24 },
        { id: 6, name: "e", age: 25 },
      ]
    }
  });
</script>
```

예제에서 확인 할 수 있듯이, people이라는 기존의 배열명과 person이라는 별칭이 사용되었다. 또, index는 v-for에서 제공하는 두번째 인자로 배열의 index값(번지값)을 제공해준다.   
그리고 __item in items__ 에서 __in__ 대신 __of__ 를 구분자로 사용할 수 있다. __( item of items )__    
 v-for를 작성할 때의 이점으로는 배열이 추가될 때마다 일일히 div 태그를 추가해주지 않아도 되어 유지보수에도 도움이 된다.

 v-for를 사용하면 객체의 속성도 반복할 수 있다고 한다.
 __https://kr.vuejs.org/v2/guide/list.html#v-for%EC%99%80-%EA%B0%9D%EC%B2%B4__

 ---

 ### #11 여러개의 Vue 인스턴스 사용하기
 __Ex.__
```
<div id="app">
  {{ name }}
  <button @click="changeText">Click</button>
</div>
<div id="app-1">
  {{ name }}
  <button @click="changeText">Click</button>
</div>


<script>
  const app = new Vue({
    el: '#app',
    data: {
      name: "kenta"
    },
    methods: {
      changeText() {
        app01.name = "update kenta";
      }
    }
  });

  const app01 = new Vue({
    el: '#app-1',
    data: {
      name: "kenta01"
    },
    methods: {
      changeText() {
        app.name = "update kenta01";
      }
    }
  });
</script>
```

여러 개의 Vue 인스턴스를 사용하는 방법은 새로운 Vue 인스턴스를 생성하고 el 값 안에 새로 사용할 아이디(클래스) 이름을 넣으면 된다.   

또, 새로 만든 Vue인스턴스에서 다른 인스턴스의 데이터에 접근하고 싶을 때에는 Vue 인스턴스를 __변수 안에 담으면 된다.__   

위의 예제에서 app과 app01 이라는 변수에 각각의 Vue 인스턴스를 담았고, changeText()라는 메소드가 있을 것이다. 이 메소드는 실행하면 서로의 name을 바꾸는 기능을 가지고 있다.   

각 메소드는 Vue 인스턴스가 담긴 변수를 활용하여 서로의 값을 바꿀 수 있는 것이다.

· this는 new Vue를 가르키는데, new Vue를 const 변수에 담음으로써 this 대신에 변수명을 사용할 수 있다.