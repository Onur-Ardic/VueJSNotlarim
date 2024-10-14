## VueJS Notlarım

- Merhabalar, çalıştığım firmadan dolayı biraz VueJS tarafına yöneldim. VueJS öğrenirken almış olduğum notları VueJS öğrenmek isteyen dostlarım için bir dokümantasyon haline getirmeye çalıştım. Umarım sizlere faydalı olur.

- Şimdiden iyi çalışmalar.

---

#OptionsAPİ ve CompositionAPI arasında ki farklar nedir?

- VueJS bizlere iki farklı syntax yapısı sunuyor. OptionsAPI biraz daha geleneksel bir yöntemken VUE3 ten sonra bir çok proje CompositionAPI ile yazılmaya başlandı.

\*Aşağıda ki örnekte arasında ki farkalara göz atalım

- Options API

```bash
export default {
  // Properties returned from data() become reactive state
  data() {
    return {
      count: 0
    }
  },

  // Methods are functions that mutate state and trigger updates.
  // They can be bound as event handlers in templates.
  methods: {
    increment() {
      this.count++
    }
  },

  // Lifecycle hooks are called at different stages
  // of a component's lifecycle.
  // This function will be called when the component is mounted.
  mounted() {
    console.log(`The initial count is ${this.count}.`)
  }
}
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>
```

    Yukarda da görüldüğü üzere OptionsAPI kullanırken method, fonksiyon ve lifecycle metodları bu şekilde yapılıyor. Bu durum CompositionAPI tarafında biraz daha farklı. Şimdi gelin onu da inceleyeleim.

- CompositionAPI

```bash
<script setup>
import { ref, onMounted } from 'vue'

// reactive state
const count = ref(0)

// functions that mutate state and trigger updates
function increment() {
  count.value++
}

// lifecycle hooks
onMounted(() => {
  console.log(`The initial count is ${count.value}.`)
})
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>
```

|| Gördüğünüz gibi aralarında ufak tefek farklar var. Bu durumlar kodun anlamlı olmasını ve fonksiyonelliği bana göre biraz daha arttırıyor. Ancak sizler bu konunun değerlendirmesini kendi içinizde yapabilirsiniz.

## Kurulum

- VueJS i tıpkı Bootstrap import eder gibi head içine koyacağımız bir link ile import edebiliyoruz. Ancak bu çok tavsiye edilmeyen bir yöntem olduğu için VueJS CLİ veya NPM ile kurulum yapabilirsiniz ben npm ile kuracağım. sizler merak ederseniz diğer kurulum yöntemini kullanabilirsiniz.

        OptionsAPI kullanmak için CLI ile kurulum yapılırken CompositionAPI ile kurmak için
        NPM ile kurulum yapılır.

- Bir klasör oluşturarak terminali açalım ve şunu yazalım.

       npm create vue@latest

| Bu işlemi yaptıktan sonra karşınıza bir kaç soru gelecek

Benim cevaplarım aşağıda ki şekilde;

    √ TypeScript Eklensin mi? ... Hayır

    √ JSX Desteği Eklensin mi? ... Hayır

    √ Tek Sayfa Uygulama geliştirilmesi için Vue Router eklensin mi? ... / Evet

    √ Durum yönetimi için Pinia eklensin mi? ... / Evet

    √ Birim Testi için Vitest eklensin mi? ... / Evet

    √ Uçtan Uca Test Çözümü Eklensin mi? » Hayır

    √ Kod kalitesi için ESLint eklensin mi? ... / Evet

    √ Kod formatlama için Prettier eklensin mi? ... / Evet

    √ Hata ayıklama için Vue DevTools 7 eklentisi eklensin mi? (deneysel) ...
    / Evet

| Kurulum bittikten sonra dosya içine giderek npm i yazalım ve sonrasında "npm run dev" diyerek projeyi başlatalım.

| Bu işlemlerden sonra sizleri hazır bir template karşılayacak ancak ben kendime göre şekil vermek için bu templateyi temizliyorum. Bunun için ana dizin olan app.vue içini şu şekilde temizleyebilirsiniz.

```bash
<script setup>
</script>

<template>
  <header>
    <div class="wrapper">
      <h1>hellow word</h1>
    </div>
  </header>

</template>

<style scoped></style>

```

||

| Kodun hata vermemesi için router dosyasına giderek routerları yorum satırına alalım sonrasında ihtiyacımız olduğu takdirde bu kısımları kodlayacağız

```bash
import { createRouter, createWebHistory } from 'vue-router'

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    // {
    //   path: '/',
    //   name: 'home',
    //   component: HomeView
    // },
    // {
    //   path: '/about',
    //   name: 'about',
    //   component: () => import('../views/AboutView.vue')
    // }
  ]
})

export default router
```

| Diğer bileşenlere dokunmadan VueJS de temel konulara başlayalım.

---

## Data Binding ve Property Tanımlamaları

```bash
#app.vue
<script setup>
import { ref } from 'vue'

const firstMessage = ref('firstMessage')
const changeValue = () => {
  firstMessage.value = 'updated message'
}
</script>

<template>
  <header>
    <div class="wrapper">
      <h1>{{ firstMessage }}</h1>
      <button @click="changeValue">Change Message</button>
    </div>
  </header>
</template>

<style scoped></style>

```

|| Yukarda firtsMessage şeklinde bir property tanımladım ve butona tıkladığımda firstMessage değerini değiştirdim bu tanımlayama bir nevi reactte ki state tanımlamasının farklı bir hali diyebiliriz. Ek olarak constant bir değişkeni güncellemek için let kullanmamız lazım ancak bunu yaptığımız zaman fonksiyon çalışmayacaktır. Bunun için burada ref kullanıyoruz.

! Peki neden ref kullanıyoruz gelin anlatayım.

- Vue 3'te script setup içinde let ile tanımlanan değişkenler reaktif değildir. Yani, Vue'nun reaktif sistemine dahil olmadıkları için DOM'da yapılan değişiklikler güncellenmez. Reaktif bir değişken tanımlamak için ref veya reactive kullanmamız gerekiyor. Yani compositionAPI ile gelen bir durum diyebiliriz.

#v-bind kullanımı

| a tagları gibi href özellikleri içeren taglarda bir data bind işlemi yapmak için v - bind özelliğini kullanıyoruz.

örnek olarak vermek gerekirse;

```bash
<script setup>
import { ref } from 'vue'

const firstMessage = ref('firstMessage')
const links = "google.com"
const changeValue = () => {
  firstMessage.value = 'updated message'
}
</script>

<template>
  <header>
    <div class="wrapper">
      <h1>{{ firstMessage }}</h1>
      <a v-bind:ref="links">Google</a> // href özelliği v-bind ile verdik
      <button @click="changeValue">Change Message</button>
    </div>
  </header>
</template>

<style scoped></style>


```

## Input Event

| inputlardan değerleri almak için JS'ten bildiğimiz change gibi eventlar ı kullanırız gelin VueJS tarafında input eventlar nasıl kullanılıyor bakalım.

```bash
<script setup>
import { ref } from 'vue'

const firstMessage = ref('firstMessage')
const links = 'google.com'
const newValue = ref('')

const changeValue = () => {
  firstMessage.value = 'updated message'
}

const setValue = (e) => {
  newValue.value = e.target.value
}
</script>

<template>
  <header>
    <div class="wrapper">
      <h1>{{ firstMessage }}</h1>
      <h1>{{ newValue }}</h1>
      <a v-bind:href="links">Google</a>
      <input type="text" placeholder="değer giriniz" @input="setValue" />
      <button @click="changeValue">Change Message</button>
    </div>
  </header>
</template>

<style scoped></style>
```

---

## Two Way Data Binding v-model

| Bu property ile uzun uzun eventlarla uğraşmak yerine tek bir property ile input içerisinden value değerini alıyoruz.

```bash
<script setup>
import { ref } from 'vue'

const firstMessage = ref('firstMessage')
const links = 'google.com'
const newValue = ref('')

const changeValue = () => {
  firstMessage.value = 'updated message'
}
</script>

<template>
  <header>
    <div class="wrapper">
      <h1>{{ firstMessage }}</h1>
      <h1>{{ newValue }}</h1>
      <a v-bind:ref="links">Google</a>
      <input v-model="newValue" /> // v-model ile inputtan valueyi alıp değişkene atadık.
      <button @click="changeValue">Change Message</button>
    </div>
  </header>
</template>

<style scoped></style>
```

## Computed

| VueJS de bir property'nin özelliği değiştiğinde tüm component yeniden render edilir ancak bu durum optimizasyon açısından projeye zarar verebilir bu gibi durumları engellemek için computed kullanıyoruz

Örnek;

```bash
<script setup>
import { reactive, computed } from 'vue'

const author = reactive({
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
})

// a computed ref
const publishedBooksMessage = computed(() => {
  return author.books.length > 0 ? 'Yes' : 'No'
})
</script>

<template>
  <p>Has published books:</p>
  <span>{{ publishedBooksMessage }}</span>
</template>
```

---

## Dinamik CSS Kullanımı

- Dinamik inlineCSS Kullanımı

* Değişken durumlarına göre stile inline olarak aşağıda ki gibi müdahale edebiliriz.

```bash
<script setup>
import { ref } from 'vue'

const firstBox = ref(false)
const secondBox = ref(false)
const chooseBoxStyle = (number) => {
  console.log(number)
  if (number === '1') {
    firstBox.value = !firstBox.value
  } else if (number === '2') {
    secondBox.value = !secondBox.value
  }
}
</script>

<template>
  <header>
    <div class="wrapper">
      <div
        class="box"
        @click="chooseBoxStyle('1')"
        :style="{ borderColor: firstBox ? 'darkmagenta' : 'gray' }"
      ></div>
      <div
        class="box"
        @click="chooseBoxStyle('2')"
        :style="{ borderColor: secondBox ? 'darkmagenta' : 'gray' }"
      ></div>
    </div>
  </header>
</template>

<style scoped>
.box {
  width: 200px;
  height: 200px;
  transition: background-color 0.5s;
  margin: 10px;
  border: dashed;
}
</style>
```

- Dinamik Class

Değişken durumlarına göre class bilgisine aşağıda ki gibi müdahale edebiliriz.

```bash

<script setup>
import { ref } from 'vue'

const firstBox = ref(false)
const secondBox = ref(false)
const chooseBoxStyle = (number) => {
  console.log(number)
  if (number === '1') {
    firstBox.value = !firstBox.value
  } else if (number === '2') {
    secondBox.value = !secondBox.value
  }
}
</script>

<template>
  <header>
    <div class="wrapper">
      <div class="box" :class="{ selected: firstBox }" @click="chooseBoxStyle('1')"></div>
      <div
        class="box"
        @click="chooseBoxStyle('2')"
        :style="{ borderColor: secondBox ? 'darkmagenta' : 'gray' }"
      ></div>
    </div>
  </header>
</template>

<style scoped>
.box {
  width: 200px;
  height: 200px;
  transition: background-color 0.5s;
  margin: 10px;
  border: dashed;
}

.selected {
  border-color: darkmagenta;
}
</style>
```

---

## VueJS ' de koşullu durumlar

- VueJS de koşullu durumları açıklamak için klasik TODO örneği yapalım

```bash
<script setup>
import { ref } from 'vue'

const todos = ref([])
const newTodo = ref('')

const addTodo = () => {
  if (newTodo.value) {
    todos.value.push({ text: newTodo.value, completed: false })
  }
}
</script>

<template>
  <header>
    <h3>TODO</h3>
    <input type="text" v-model="newTodo" placeholder="Enter a new TODO" />
    <button @click="addTodo(newTodo)">Add</button>

    <p v-if="todos.length == 0">Todo Bulunmamaktadır</p>
    <p v-else>TODO LİST</p>

    <ul class="todos">
      <li v-for="todo in todos" :key="todo.text">
        {{ todo.text }}
      </li>
    </ul>
  </header>
</template>

<style scoped></style>

```

     VueJS de gördüğünüz gibi koşullu durum kullanımları oldukça basit. VueJS yapısı itibari

     ile React ve Angular'ın karışıımı gibidir ikisinden de bazı özellikler alarak bunu kendi ,

     syntax yapısına göre adapte eder. Eğer daha önce Angular ile çalıştıysanız bu

     kullanımlar size yabancı gelmez

## VueJS İleri Seviye konulara

---

## VueJS de Component Oluşturma ve Entegrasyonu(OptionsAPI) ve Props Geçişleri

| Eğer daha önce ReactJS kullandıysanız VueJS de component mantığı neredeyse ReactJS ile aynı. Bu yüzden eminim yabancı gelmeyecektir. Components

| Ufak bir örnekle açıklayalım.

Öncelikle klasör yapımızın düzeni açısından src klasörü altında bulunan components klasörüne bir Home klasörü açarak indexte kullanacağımız komponentleri burada açalım.

TodoList.vue adında bir dosya açarak şunları yazalım.

```bash


<script>
export default {
  name: 'todoList' // componenti export ile dışarıya açtık
}
</script>

<template>
  <div>
    <li v-for="todo in todos" :key="todo.text">
      {{ todo.text }}
    </li>
  </div>
</template>



```

| App.vue ya gelerek import edelim.

```bash
<script setup>
import { ref } from 'vue'
import TodoList from './components/Home/TodoList.vue' // componenti import ettik

export default{
  components: {
    TodoList // Componenti burada tanımlamamız gerekiyor
  },
  data() {
    props:{
    todos,
    }
    return {
      todos,
      newTodo
    }
  },
  methods: {
    addTodo
  }
}

</script>

<template>
  <header>
    <h3>TODO</h3>
    <input type="text" v-model="newTodo" placeholder="Enter a new TODO" />
    <button @click="addTodo">Add</button>

    <p v-if="todos.length == 0">Todo Bulunmamaktadır</p>
    <p v-else>TODO LİST</p>

    <ul class="todos">
      <TodoList :todos = todos />
      // componenti çağırdık
    </ul>
  </header>
</template>

<style scoped></style>

```

      ! Uyarı !
      Ben compositionAPI kullandığım için bu kod bende hata verecektir.
      Eğer OptionsAPI kullanıyorsanız yukarda ki gibi import etmeniz gerekiyor.

## VueJS de Component Oluşturma ve Entegrasyonu(CompositionAPI) ve Props Geçişleri

| CompositionAPI kullanımında biraz daha işler farklı ancak biraz daha kolay bir kullanımı var.

```bash
#TodoList.vue
<script setup>
const { todos } = defineProps({
  todos: {
    type: Array,
    required: true
  }
})
// Propsları bu componente geçirdik
</script>

<template>
  <div>
    <li v-for="(todo, index) in todos" :key="index">
      {{ todo.text }}
    </li>
  </div>
</template>

<style scoped></style>

```

````bash
## App.vue
<script setup>
import { ref } from 'vue'
import TodoList from './components/Home/TodoList.vue' // componenti import

const todos = ref([])
const newTodo = ref('')

const addTodo = () => {
  if (newTodo.value) {
    todos.value.push({ text: newTodo.value, completed: false })
  }
}
</script>

<template>
  <header>
    <h3>TODO</h3>
    <input type="text" v-model="newTodo" placeholder="Enter a new TODO" />
    <button @click="addTodo">Add</button>

    <p v-if="todos.length == 0">Todo Bulunmamaktadır</p>
    <p v-else>TODO LİST</p>

    <ul class="todos">
      <TodoList :todos="todos" />
      <!-- Componenti Çağırdık -->
    </ul>
  </header>
</template>

<style scoped></style>

```

````
