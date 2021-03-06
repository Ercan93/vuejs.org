---
title: Introduction
type: guide
order: 2
---

## Vue.js nedir?

Vue (telaffuzu /viuvː/, **view** gibi) kullanıcı arayüzleri oluşturmak için **ilerici bir çerçevedir**. Diğer monolitik(tekparça) çerçevelerin aksine, Vue, aşamalı olarak benimsenecek şekilde sıfırdan tasarlanmıştır. Çekirdek kütüphanesi yalnızca görünüm katmanına odaklanmıştır, ve diğer kütüphaneler ya da mevcut projelerle birleştirilmesi ve entegre edilmesi kolaydır. Diğer yandan, Vue [modern araçlar](single-file-components.html) ve [destekleyici kütüphaneler](https://github.com/vuejs/awesome-vue#components--libraries) ile birlikte kullanıldığında sofistike(çok gelişmiş) Tek Sayfalı Uygulamalara(SPA) mükemmel bir şekilde güç verir.

Başlamadan önce Vue hakkında daha fazla bilgi edinmek isterseniz, temel ilkeler ve örnek proje üzerinden ilerleyen bir <a id="modal-player"  href="#">video hazıladık.</a>

Eğer deneyimli bir fronted geliştiricisi iseniz ve Vue'nun diğer kütüphanelerle/çerçevelerle(frameworklerle) nasıl karşılaştırıldığını bilmek istiyorsanız, [Diğer Çerçevelerle Karşılaştırma](comparison.html) bölümüne bakın.

<div class="vue-mastery"><a href="https://www.vuemastery.com/courses/intro-to-vue-js/vue-instance/" target="_blank" rel="noopener" title="Free Vue.js Course">Vue Mastery'da ücretsiz bir video kursu izleyin</a></div>

## Başlarken

<p class="tip">Resmi kılavuz, orta düzeyde HTML, CSS ve JavaScript bilginiz olduğunu varsayar. Eğer frontend geliştirmede tamamen yeni iseniz, ilk adım olarak bir çerçeveyi(framework) direk öğrenmeye başlamak iyi bir fikir olmayabilir - temelleri kavrayıp geri gelin! Diğer çerçevelerle ilgili deneyim yardımcı olur, ancak gerekli değildir.</p>

Vue.js'i denemenin en kolay yolu [JSFiddle Hello World örneğini](https://jsfiddle.net/ErcanUzunsakal/aby6u2ds) kullanmaktır. Başka bir sekme açmaktan çekinmeyin ve bazı temel örnekleri incelerken takip edin. Ya da, bir<a href="https://gist.githubusercontent.com/Ercan93/ef377da0e2ab4ce39677ba027692a935/raw/fc360b3e808af7a6fc252f6340375316cbb67e54/index.html" target="_blank" download="index.html" rel="noopener noreferrer"> <code>index.html</code> dosyası oluşturabilir  </a> ve Vue'yu şununla dahil edebilirsiniz :

``` html
<!-- geliştirme sürümü, yararlı konsol uyarıları içerir -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

or:

``` html
<!-- üretim sürümü, boyut ve hız için optimize edilmiş -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

[Kurulum](installation.html) sayfası, Vue kurulumu için daha fazla seçenek sunar. Not: Yeni başlayanların `vue-cli` ile başlamalarını **önermiyoruz**, özellikle de Node.js tabanlı derleme araçlarını henüz bilmiyorsanız.

Daha etkileşimli bir şey tercih etmek isterseniz, [Scrimba'daki bu öğretici videolara ](https://scrimba.com/playlist/pXKqta) bakabilirsiniz, Burası(Scrimba), istediğiniz zaman duraklatabileceğiniz ve oynatabileceğiniz bir ekran kaydı ve kod yazım alanı sunar.

## Beyan(Tanımlayıcı) Oluşturma

<div class="scrimba"><a href="https://scrimba.com/p/pXKqta/cQ3QVcr" target="_blank" rel="noopener noreferrer">Scrimba'daki bu dersi dene</a></div>

Vue.js'nin özünde, basit bir şablon sözdizimini kullanarak bildirimsel olarak DOM'a veri oluşturmamızı sağlayan bir sistemdir:

``` html
<div id="app">
  {{ mesaj }}
</div>
```
``` js
var app = new Vue({
  el: '#app',
  data: {
    mesaj: 'Merhaba Vue!'
  }
})
```
{% raw %}
<div id="app" class="demo">
  {{ mesaj }}
</div>
<script>
var app = new Vue({
  el: '#app',
  data: {
    mesaj: 'Merhaba Vue!'
  }
})
</script>
{% endraw %}

İlk Vue uygulamamızı şimdiden oluşturduk! Bu, bir dize(string) şablonu oluşturmaya oldukça benziyor, ancak Vue, arka planda çok iş yaptı. Veri ve DOM şimdi bağlandı, ve şimdi herşey **reaktif**. Nasıl emin olabiliriz? Tarayıcınızın JavaScript konsolunu açın (şu anda bu sayfada) ve `app.mesaj` öğesini farklı bir değere ayarlayın. Yukarıda işlenen örneği güncellemeye göre görmelisiniz.

Metin eklemesine ek olarak, aşağıdaki gibi element özelliklerini de bağlayabiliriz:

``` html
<div id="app-2">
  <span v-bind:title="mesaj">
    Dinamik olarak, bağlı başlığımı görmek için
    farenizi birkaç saniye üzerime getirin!
  </span>
</div>
```
``` js
var app2 = new Vue({
  el: '#app-2',
  data: {
    mesaj: 'Bu sayfayı şu tarihte yüklendiniz: ' + new Date().toLocaleString()
  }
})
```
{% raw %}
<div id="app-2" class="demo">
  <span v-bind:title="mesaj">
    Dinamik olarak, bağlı başlığımı görmek için
    farenizi birkaç saniye üzerime getirin!
  </span>
</div>
<script>
var app2 = new Vue({
  el: '#app-2',
  data: {
    mesaj: 'Bu sayfayı şu tarihte yüklendiniz: ' + new Date().toLocaleString()
  }
})
</script>
{% endraw %}

Burada yeni bir şey ile karşılaşıyoruz. Gördüğünüz `v-bind` özniteliği(attribute),   **yönerge(directive)** olarak adlandırılır. Yönergeler(directives), Vue tarafından sağlanan özel öznitelik(attribute) olduklarını belirtmek için önüne `v-` eklenmiştir, ve tahmin edebileceğiniz gibi, işlenen DOM'a özel reaktif davranışlar uygularlar. Burada temel olarak "bu öğenin `title` özniteliğini(attribute) Vue instance'daki `mesaj` özelliği(property) ile güncel tutun" diyor.

Javascript konsolunuzu tekrar açıp `app2.mesaj = 'yeni bir mesaj'` yasarsanız, bir kez daha ilişkili HTML'in - bu durumda `title` attribute'unun - güncellendiğini göreceksiniz.

## Koşul ve Döngüler

<div class="scrimba"><a href="https://scrimba.com/p/pXKqta/cEQe4SJ" target="_blank" rel="noopener noreferrer">Scrimba'daki dersi deneyin</a></div>

Bir öğenin varlığını değiştirmek çok kolaydır:

``` html
<div id="app-3">
  <span v-if="gorunum">Şuan beni görüyorsun</span>
</div>
```

``` js
var app3 = new Vue({
  el: '#app-3',
  data: {
    gorunum: true
  }
})
```

{% raw %}
<div id="app-3" class="demo">
  <span v-if="gorunum">Şuan beni görüyorsun</span>
</div>
<script>
var app3 = new Vue({
  el: '#app-3',
  data: {
    gorunum: true
  }
})
</script>
{% endraw %}

Devam edin ve konsola `app3.gorunum = false` yazın. Mesajın kaybolduğunu görmelisin.

Bu örnek, verileri yalnızca metin ve attribute'lara değil aynı zamanda DOM **yapısı**na da bağlayabildiğimizi göstermektedir. Vue ayrıca, öğeler Vue tarafından eklendiğinde/güncellendiğinde/kaldırıldığında geçiş efeklerini otomatik olarak uygulayan güçlü bir [geçiş efekt](transitions.html) sistemi sağlar.
Her biri kendi özel işlevselliğine sahip olan oldukça az sayıda başka directive var. Örneğin, `v-for` directive'i, bir Dizideki verileri kullanarak bir öğe listesini görüntülemek için kullanılabilir:

``` html
<div id="app-4">
  <ol>
    <li v-for="gorev in gorevler">
      {{ gorevler.metin }}
    </li>
  </ol>
</div>
```
``` js
var app4 = new Vue({
  el: '#app-4',
  data: {
    gorevler: [
      { metin: 'JavaScript öğrenilecek' },
      { metin: 'Vue öğrenilecek' },
      { metin: 'Harika bir şey yap' }
    ]
  }
})
```
{% raw %}
<div id="app-4" class="demo">
  <ol>
    <li v-for="gorev in gorevler">
      {{ gorevler.metin }}
    </li>
  </ol>
</div>
<script>
var app4 = new Vue({
  el: '#app-4',
  data: {
    gorevler: [
      { metin: 'JavaScript öğrenilecek' },
      { metin: 'Vue öğrenilecek' },
      { metin: 'Harika bir şey yap' }
    ]
  }
})
</script>
{% endraw %}

Konsola `app4.Gorevler.push({ metin: 'Yeni öğe' })` yazın, listeye yeni bir öğe eklendiğini göreceksiniz.

## Kullanıcı Girişlerinin Kullanımı

<div class="scrimba"><a href="https://scrimba.com/p/pXKqta/czPNaUr" target="_blank" rel="noopener noreferrer">Scrimba'daki bu dersi dene</a></div>

Kullanıcıların uygulamanızla etkileşimde bulunmasına izin vermek için, Vue instances'taki yöntemleri çağıran olay dinleyicileri eklemek için `v-on` directive'ini kullanabiliriz:

``` html
<div id="app-5">
  <p>{{ mesaj }}</p>
  <button v-on:click="mesajiTersCevir">Mesajı ters çevir</button>
</div>
```
``` js
var app5 = new Vue({
  el: '#app-5',
  data: {
    mesaj: 'Merhaba Vue.js!'
  },
  methods: {
    mesajiTersCevir: function () {
      this.mesaj = this.mesaj.split('').reverse().join('')
    }
  }
})
```
{% raw %}
<div id="app-5" class="demo">
  <p>{{ mesaj }}</p>
  <button v-on:click="mesajiTersCevir">Mesajı ters çevir</button>
</div>
<script>
var app5 = new Vue({
  el: '#app-5',
  data: {
    mesaj: 'Merhaba Vue.js!'
  },
  methods: {
    mesajiTersCevir: function () {
      this.mesaj = this.mesaj.split('').reverse().join('')
    }
  }
})
</script>
{% endraw %}

Bu yöntemde, DOM'a dokunmadan uygulamamızın durumunu güncellediğimizi unutmayın - tüm DOM manipülasyonları Vue tarafından yapılır ve Vue'nun, yazdığınız kodun temel mantığa odaklandığını unutmayın.

Vue, form girişi ve uygulama durumu arasında iki yönlü bağlama yapan `v-model` directive'i sağlar:
``` html
<div id="app-6">
  <p>{{ mesaj }}</p>
  <input v-model="mesaj">
</div>
```
``` js
var app6 = new Vue({
  el: '#app-6',
  data: {
    mesaj: 'Merhaba Vue!'
  }
})
```
{% raw %}
<div id="app-6" class="demo">
  <p>{{ mesaj }}</p>
  <input v-model="mesaj">
</div>
<script>
var app6 = new Vue({
  el: '#app-6',
  data: {
    mesaj: 'Merhaba Vue!'
  }
})
</script>
{% endraw %}

## Bileşen(component) Yapılandırma

<div class="scrimba"><a href="https://scrimba.com/p/pXKqta/cEQVkA3" target="_blank" rel="noopener noreferrer">Scrimba'daki bu dersi dene</a></div>

Bileşen sistemi Vue.js'deki bir başka önemli soyutlamadır. "Küçün kendi kendine yeten, sıklıkla yeniden kullanılabilir componentleri" birleştirerek, büyük ölçekli uygulamalar oluşturabilirsiniz. Bir düşünün, uygulama arayüzleri göz önüne alındığında, hemen hemen her türlü arayüz component ağacından  soyulanabilir.

![Component Tree](/images/components.png)

Vue'da, bir “bileşen(component)” aslında önceden tanımlanmış seçeneklere sahip bir Vue örneğidir. Vue kullanarak bir componenti kaydetmek kolaydır:

``` js
// todo-item adlı yeni bir bileşen(component) tanımla
Vue.component('todo-item', {
  template: '<li>Bu bir todo öğesi</li>'
})
```

Şimdi bu componenti diğer componentlerin şablonlarında(template) kullanabilirsiniz.

``` html
<ol>
  <!-- todo-item bileşenin bir örneğini oluşturduk -->
  <todo-item></todo-item>
</ol>
```

Ancak bu, yapılacak her öğe için aynı metni gösterecektir; bu çok kullanışlı değil. Verileri üst kapsamdan alt bileşene aktarabilmemiz gerekir. Component'in tanımını değiştirelim ki bir [prop](components.html#Props)(özellik) kabul etsin.

``` js
Vue.component('todo-item', {
  // todo-item bileşeni artık özel bir nitelik(attribute)
  // gibi olan bir "prop"u kabul ediyor.
  // Bu prop todo diye çağırılır.
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
```

Şimdi `v-bind` kullanarak todo'yu tekrarlanan her component'e geçirebiliriz:

``` html
<div id="app-7">
  <ol>
    <!--
      Şimdi her todo-item'a, temsil ettiği todo nesnesini 
      sağladık, böylece içeriği dinamik olabilir.
      Ayrıca her bileşene bir "anahtar" sağlamamız gerekiyor,
      bu daha sonra açıklanacak.
    -->
    <todo-item
      v-for="item in alınacaklarListesi"
      v-bind:todo="item"
      v-bind:key="item.id"
    ></todo-item>
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
    alınacaklarListesi: [
      { id: 0, text: 'Sebzeler' },
      { id: 1, text: 'Zile Pekmezi' },
      { id: 2, text: 'İnsanın yiyebildiği ne varsa' }
    ]
  }
})
```
{% raw %}
<div id="app-7" class="demo">
  <ol>
    <todo-item v-for="item in alınacaklarListesi" v-bind:todo="item" :key="item.id"></todo-item>
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
    alınacaklarListesi: [
      { id: 0, text: 'Sebzeler' },
      { id: 1, text: 'Zile Pekmezi' },
      { id: 2, text: 'İnsanın yiyebildiği ne varsa' }
    ]
  }
})
</script>
{% endraw %}

Bu sadece kasıtlı bir tasarım örneği olmasına rağmen, uygulamayı iki küçük birime ayırmayı başardık. Alt birim(child), props arayüzü vasıtasıyla ana bileşenden(parent) iyi bir şekilde ayrılmaktadır. Gelecekte, ana uygulamanızı etkilemeden `<todo-item>` componentlerinizi daha karmaşık şablonlar ve mantıklarla daha da geliştirebileceksiniz.

Büyük bir uygulamada, gelişimi yönetilebilir hale getirmek için tüm uygulamayı componentlere bölmek gerekir. Bir [sonraki kılavuzda](components.html), bileşenler hakkında daha fazla konuşacağız, ancak bir uygulamanın template'inin componentlere nasıl görünebileceğinin (kurgusal) bir örneği:

``` html
<div id="app">
  <app-nav></app-nav>
  <app-view>
    <app-sidebar></app-sidebar>
    <app-content></app-content>
  </app-view>
</div>
```

### Özel Öğelerle(Custom Elements) İlişki

Vue componentlerinin, [Web Componentleri Spesifikasyonunun](https://www.w3.org/wiki/WebComponents/) bir parçası olan **Custom Elements'lere** çok benzer olduğunu fark etmiş olabilirsiniz.  Bunun nedeni Vue'nun bileşen sözdiziminin belirtimden sonra gevşek bir şekilde modellenmesidir. Örneğin, Vue componentleri [Slot API](https://github.com/w3c/webcomponents/blob/gh-pages/proposals/Slots-Proposal.md) ve `is` özel attribute'unu(nitelik) uygular. Ancak bir kaç özemli fark vardır:

1. Web Bileşenleri Spesifikasyonu tamamlandı, ancak tüm tarayıcılar tarafından yerel olarak uygulanmıyor. Safari 10.1+, Chrome 54+ ve Firefox 63+ yerel olarak Web Componentleri destekler. Buna karşılık, Vue bileşeni herhangi bir polyfill gerektirmez ve desteklenen tüm tarayıcılarda (IE9 ve üstü) aynı şekilde çalışır. Gerekirse, Vue bileşenleri native custom element(yerel özel öğeler) içine sarılabilir.


2. Vue bileşenleri, düz custom elementlerde bulunmayan, özellikle de cross-component(çapraz bileşen) veri akışı, custom event (özel olay) iletişimi ve araç entegrasyonları gibi önemli özellikler sunar.

## Daha fazlası için Hazır mısın?

Vue.js çekirdeğinin en temel özelliklerini kısaca açıkladık - bu kılavuzun geri kalanı, temel özellikler ve daha gelişmiş ayrıntılara sahip diğer gelişmiş özellikleri ayrıntılı olarak ele alacaktır, bu nedenle dokümanın hepsini okuduğunuzdan emin olun!

<div id="video-modal" class="modal"><div class="video-space" style="padding: 56.25% 0 0 0; position: relative;"><iframe src="https://player.vimeo.com/video/247494684" style="height: 100%; left: 0; position: absolute; top: 0; width: 100%; margin: 0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div><script src="https://player.vimeo.com/api/player.js"></script><p class="modal-text">Video by <a href="https://www.vuemastery.com" target="_blank" rel="noopener" title="Vue.js Courses on Vue Mastery">Vue Mastery</a>. Vue Mastery'de ücretsiz izle <a href="https://www.vuemastery.com/courses/intro-to-vue-js/vue-instance/" target="_blank" rel="noopener" title="Vue.js Courses on Vue Mastery">Vue kursuna giriş</a>.</div>
