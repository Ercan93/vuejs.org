---
title: The Vue Instance
type: guide
order: 3
---

## Vue Instance(Vue Örneği) oluşturma

Her Vue uygulaması, `Vue` fonksiyonu ile yeni bir **Vue instance** oluşturarak başlar: 

```js
var vm = new Vue({
  // belirtimler
})
```

Vue, [MVVM modelini](https://en.wikipedia.org/wiki/Model_View_ViewModel) tam olarak uygulamamasına rağmen, çerçeve mimarisi büyük ölçüde ondan ilham alıyor. ondan ilham alıyor. Bu nedenle, Vue örneğimizi(instance) belirtmek için genellikle `vm` değişkenini (ViewModel kısaltması) kullanırız.

Bir Vue örneği oluşturduğunuzda, bir **options object**(seçenek nesnesi) geçersiniz. Bu kılavuzun çoğu, istediğiniz davranışı elde etmek için bu seçenekleri nasıl kullanabileceğinizi açıklamaya yöneliktir. Referans olarak, [API referansındaki](../api/#Options-Data) seçeneklerin tam listesine göz atabilirsiniz.

Vue uygulaması, `new Vue` ile  bir **root Vue instance**(kök Vue örneği) oluşturur, isteğe bağlı olarak, iç içe geçmiş, yeniden kullanılabilir bileşenlerden oluşan bir ağaç halinde düzenlenmiştir. Örneğin, bir Todo uygulaması için bileşen ağacı şöyle görünür:

```
Kök örneği
└─ TodoList
   ├─ TodoItem
   │  ├─ DeleteTodoButton
   │  └─ EditTodoButton
   └─ TodoListFooter
      ├─ ClearTodosButton
      └─ TodoListStatistics
```

[Component sistemini](components.html) daha sonra ayrıntılı olarak açıklayacağız. Şimdilik, tüm Vue componentlerinin esasen Vue instance'ları olduğunu bilmeniz gerekir(root'a özgü bir kaç özellik hariç).

## Veri(Data) ve Yöntemler(Methods)

Bir Vue instance oluşturulduğunda, kendi `data` nesnesinin tüm özelliklerini **reaktif sisteme** ekler. Bu özelliklerin değerleri değiştiğinde görünüm “tepki verecek” ve yeni değerlerle eşleşecek şekilde güncellenecektir.

```js
// Veri nesnesi
var data = { a: 1 }

// Nesneye bir Vue instance eklendi
var vm = new Vue({
  data: data
})

// Instance'tan özellikleri aldığımızda
// orijinal verilerden döndürür
vm.a == data.a // => true

// Instance'da özelliklerin değiştirlmesi
// orijinal verileri de etkiler
vm.a = 2
data.a // => 2

// ... ve tam tersi
data.a = 3
vm.a // => 3
```

Değerler değiştiğinde görünüm(the view) yeniden oluşturulur. `data` Özelliği yalnızca instance oluşturulduğunda(created) mevcutsa **reaktif** olur. Başka bir deyişle, yeni bir özellik eklerseniz:

```js
vm.b = 'merhaba'
```

`b` değiştirildiğinde yenileme yapmaz.  Özelliğe daha sonra ihtiyacınız olacağını biliyorsanız, boş olsun veya olmasın başlangıç ​​değerini ayarlayabilirsiniz. Örneğin:

```js
data: {
  newTodoText: '',
  visitCount: 0,
  hideCompletedTodos: false,
  todos: [],
  error: null
}
```

Buradaki tek istisna, Object.freeze() kullandığınız zamandır. Bu, mevcut sistemlerin değiştirilemeyeceği ve reaktif sistemin değişiklikleri _takip_ edemediği anlamına gelir.

```js
var obj = {
  foo: 'bar'
}

Object.freeze(obj)

new Vue({
  el: '#app',
  data: obj
})
```

```html
<div id="app">
  <p>{{ foo }}</p>
  <!-- buradaki `foo` güncellenmeyecek! -->
  <button v-on:click="foo = 'baz'">Değiştir</button>
</div>
```

Data özelliklerine(properties) ek olarak, Vue instance'ları bir dizi yardımcı özellik ve instance yöntemleri sağlar. Diğer kullanıcı tanımlı özniteliklerden ayırt etmek için önüne `$` eklenmiştir. Örneğin:

```js
var data = { a: 1 }
var vm = new Vue({
  el: '#example',
  data: data
})

vm.$data === data // => true
vm.$el === document.getElementById('example') // => true

// $watch bir instance methodudur
vm.$watch('a', function (newValue, oldValue) {
  // Bu callback `vm.a` değiştiğinde çağrılır.
})
```

Gelecekte, bir instance properties ve yöntemleri listesi için [API referansına](../api/#Instance-Properties) başvurabilirsiniz.

## Instance Lifecycle Hooks

Each Vue instance goes through a series of initialization steps when it's created - for example, it needs to set up data observation, compile the template, mount the instance to the DOM, and update the DOM when data changes. Along the way, it also runs functions called **lifecycle hooks**, giving users the opportunity to add their own code at specific stages.

For example, the [`created`](../api/#created) hook can be used to run code after an instance is created:

```js
new Vue({
  data: {
    a: 1
  },
  created: function () {
    // `this` points to the vm instance
    console.log('a is: ' + this.a)
  }
})
// => "a is: 1"
```

There are also other hooks which will be called at different stages of the instance's lifecycle, such as [`mounted`](../api/#mounted), [`updated`](../api/#updated), and [`destroyed`](../api/#destroyed). All lifecycle hooks are called with their `this` context pointing to the Vue instance invoking it.

<p class="tip">Don't use [arrow functions](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions) on an options property or callback, such as `created: () => console.log(this.a)` or `vm.$watch('a', newValue => this.myMethod())`. Since arrow functions are bound to the parent context, `this` will not be the Vue instance as you'd expect, often resulting in errors such as `Uncaught TypeError: Cannot read property of undefined` or `Uncaught TypeError: this.myMethod is not a function`.</p>

## Lifecycle Diagram

Below is a diagram for the instance lifecycle. You don't need to fully understand everything going on right now, but as you learn and build more, it will be a useful reference.

![The Vue Instance Lifecycle](/images/lifecycle.png)
