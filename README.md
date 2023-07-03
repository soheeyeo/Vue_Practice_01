# Vue_Practice_01

#### Vue 설치
```
npm install -g @vue/cli
```
- vue/cli : vue 프로젝트 빠르게 생성해주는 라이브러리

#### Vue 서버 실행
```
npm run serve
```

### Vue 데이터바인딩
Vue 인스턴스가 생성될 때 `data` 객체의 모든 속성이 실시간으로 반영됨. <br>
자주 변경될 수 있는 데이터들은 `data` 객체에 보관하여 사용. 

```jsx
<template>
  <div>
    <h1 :style="txtColor">{{ title }}</h1>
  </div>
</template>

<script>
export default {
  name : 'App',
  data(){
    return {
      title : 'Hello world',
      txtColor : 'color:pink',
    }
  },
}
</script>
```

<br>

### Vue 반복문 v-for
`v-for`을 사용하여 객체의 속성을 반복.

```jsx
<template>
  <nav class="menu">
    <a v-for="i in menu" :key="i">{{ i }}</a>
  </nav>
</template>

<script>
export default {
  name : 'App',
  data(){
    return {
      menu :['Home', 'About', 'Contact'],
    }
  },
}
</script>
```
<br>

### Vue 이벤트 핸들링 v-on
`v-on`을 사용하여 이벤트 처리. `v-on` 대신 `@` 사용 가능. <br>
이벤트 발생 시 실행될 함수를 메소드에 담아 호출. 

```jsx
<template>
  <button v-on:click="increase">클릭</button>
  <span>클릭수: {{ counter }}</span>
</template>

<script>
export default {
  name : 'App',
  data(){
    return {
      counter : 0,
    }
  },
  methods: {
    increase(){
      this.counter += 1;
    }
  },
}
</script>
```

<br>

### Vue 조건부 렌더링 v-if
`v-if`의 조건식이 true일 때만 렌더링.<br>

```jsx
<template>
  <button @click="open">열기</button>
  <div v-if="isOpen">
    <p>안녕하세요</p>
  </div>
</template>

<script>
export default {
  name : 'App',
  data(){
    return {
      isOpen : false,
    }
  },
  methods: {
    open(){
      this.isOpen = !this.isOpen;
    }
  },
}

</script>
```
<br>

### Vue Component
HTML이 복잡해지면 컴포넌트 만들어 사용. <br>
컴포넌트 파일 생성 후 App.vue 파일에서 import, 등록하여 사용. <br>
`props`로 부모 데이터 전달하기.

```jsx
<template>
  <div>
    <p>모달창입니다.</p>
    <a v-for="i in items" :key="i">{{ i }}</a>
    <button>닫기</button>
  </div>
</template>

<script>
export default {
  name : 'ModalComponent',
  props : {
    items : Array,
  }
}
</script>
```

```jsx
<template>
  <div>
    <Modal :items="items"/>
  </div>
</template>

<script>
import Modal from './ModalComponent.vue';

export default {
  name : 'App',
  data(){
    return {
      items :['Vue', 'React', 'TypeScript'],
    }
  },
  components: {
    Modal
  },
}
</script>
```
<br>

### Custom event
부모의 데이터를 변경하고 싶으면 `custom event`를 사용. <br>
자식에서 이벤트를 발생시고 싶을 때 `$emit`을 사용하여 부모에게 메세지를 보냄.

```jsx
<template>
  <div>
    <p>모달창입니다.</p>
    <button @click="$emit('closeModal')">닫기</button>
  </div>
</template>
```

```jsx
<template>
  <div>
    <Modal @closeModal="isOpenModal = false" />
  </div>
</template>
```
<br>

### 데이터 감시 Watcher
`watch`를 사용하여 데이터 변경을 감시. <br>
데이터 변경에 대한 응답으로 비동기식 작업 수행. 

```jsx
<template>
  <div>
    <input v-model="message">
    <p>메세지 : {{ message }}</p>
  </div>
</template>

<script>
export default {
  watch : {
    message(value){
      console.log(value);
    }
  },
}
</script>
```
<br>