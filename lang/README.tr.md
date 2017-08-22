Angular 4 - Notları
====================

Bu kod deposu benim angular 4 notlarımın bir derlemesidir. Angular 2'yi deneyememiştim. Fakat şimdi Angular 4'e bir göz atmaya ve bir ders hazırlamaya karar verdim. Öğrendiğim her şeyi yazacağım, belki bu kod deposu sizin için de rehber olabilir.

[Maximilian Schwarzmuller](https://www.udemy.com/the-complete-guide-to-angular-2)'e bu harika rehber için teşekkürler.


İçindekiler
----------------

- [Kurulum](#installation)
- [Bir proje yaratmak](#creating-project)
- [Projeyi çalıştırmak](#serving-project)
- [Çalıştırılmış Projeyi İncelemek](#investigating-created-project)
- [Yeni bir komponent oluşturmak](#creating-a-new-component)
- [Komut satırı ile bir komponent oluşturmak](#create-component-with-cli)
- [Projeye bootstrap css eklemek](#including-bootstrap-css-to-project)
- [Databinding](#databinding)
- [Direktifler](#directives)
  - [ngIf](#ngif)
  - [ngFor](#ngfor)
  - [ngStyle](#ngstyle)
  - [ngClass](#ngclass)
  - [ngSwitch](#ngswitch)
- [Input](#input)
- [Output](#output)
- [View Encapsulation](#view-encapsulation)
- [Yerel Referanslar](#local-reference)
- [ng-content](#ng-content)
- [Komponentlerin Yaşam Döngüsü](#life-cycle-of-components)
- [Yeni bir direktif oluşturmak](#creating-a-new-directive)
  - [HostListener](#hostlistener)
  - [HostBinding](#hostbinding)
- [Servisler ve Bağlılıkların Zerki](#services-and-dependency-injection)
  - [Bir servisi bir başka servise zerk etmek](#injecting-a-service-into-another-service)
  - [Olay yayınlama servisi](#event-emitting-service)
- [Router](#router)
  - [Links](#links)
  - [Active Router](#active-route)
  - [Kod içinden yönlendirme](#navigating-from-code)
  - [Route Parameters](#parameters-of-routes)
  - [Nested Routes](#nested-routes)
  - [Yönlendirme](#redirecting)

### Kurulum

Uygulama geliştirmek için ilk önce node.js kurmamız gerekiyor. Eğer node.js nedir bilmiyorsanız Angular 4'ten önce lütfen ona bir göz atın. Biz angular komut satırı eklentisini kullanacağız, bu eklenti bize projelerimizi yaratırken yardımcı olacak. Oldukça kullanışlı bir araç.

```
npm i @angular/cli -g
```

Angular komut satırı paketini `@angular/cli` global parametresiyle yüklemeliyiz. Bu parametre proje lokaline değil global node_modules klasörüne kurulum sağlayacaktır. 

Artık terminalde `ng` komutunu kullanabiliyor olmamız gerek.

### Proje yaratmak

Proje yaratmak için `ng` komutunu kullanacağız. Eğer terminale `ng` yazdığınızda bir hata alıyorsanız `Kurulum` adımında bir hata yapmışsınız demektir, lütfen o adıma gidip işlemleri doğru şekilde tamamladığınızdan emin olun. 

`ng` komutu birden fazla opsiyonel parametreye sahiptir. O konuya da geleceğiz ancak öncelikle bir proje yaratmak için `new` parametresini kullanmalıyız.

Bu parametre güncel dizinimizde yeni bir proje yapısı oluşturacaktır. Ancak işlem sırasında bir proje ismi vermeliyiz. Ben proje ismi olarak ilk uygulamam anlamına gelen "my-first-app" ismini seçtim.

```
ng new my-first-app
```

Bu komutu kullandıktan sonra terminalimiz `ng` tarafından bazı dosyalar oluşturacak. Ardından gerekli npm paketlerini yükleyecek, işlemler tamamlanana kadar bekleyin.

### Projeyi çalıştırmak

Az önce yeni bir proje oluşturduk. `my-first-app` klasörüne girip `ng` nin `serve` komutunu kullanırsak yüklenen paketler bir http sunucusu oluşturup yayına başlayacaktır.

```
cd my-first-app
ng serve
```

Terminal çıktımızda bir url adresi olmalı. İsterseniz seçiminize bağlı olarak `--port xx` parametresiyle uygulamanın istediğiniz herhangi bir porttan yayınlanmasını sağlayabilirsiniz.

```
ng serve --port 8080
```

Typescript javascript'e çevrildi ve Webpack uygulamanızı paketledi.
Artık localhost:8080 adresnden uygulamaya erişebilirsiniz.


### Çalıştırılmış Projeyi İncelemek

> Daha fazla derinlere inmeden önce projeyi bir IDE ile açtığınızdan emin olun. Ben Visual Studio Code ya da WebStorm tavsiye ediyorum.

Proje dizininde `e2e` klasörünü, `src` klasörünü ve birkaç dosyayı göreceğiz. `e2e` klasörünü uçtan uca testleri içerir. Buna daha sonra göz atacağız. (Testlerin kaderi bu.) Projemizin tüm kaynak dosyaları `src` klasöründe bulunur. Diğer dosyalar da proje konfigürasyonlarıyla ilgili bilgileri, paket bağımlılıklarını ve benzeri detayları içerirler. İhtiyaç duyduğumuzda onlarla tekrar ilgileneceğiz.

`src` klasörünün içinde birden fazla dosya var. Bu dizindeki en önemli dosya `index.html` dosyası. Bu dosya projemizin en üst noktası. Eğer dosyayı açarsanız aşağıdaki gibi olduğunu göreceksiniz.


```html
<!doctype html>
<html>
<head>
    <meta charset="utf-8">
    <title>MyFirstApp</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="icon" type="image/x-icon" href="favicon.ico">
</head>
<body>
    <app-root>Loading...</app-root>
</body>
</html>
```

Body etiketinin içinde html standardına uymayan özel bir etiketimiz var, `app-root` elementi.

Eğer `app` klasörüne göz atarsanız ve `app.component.ts` adlı dosyayı açarsanız aşağıdaki gibi olduğunu göreceksiniz.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
}
```

Gördüğünüz gibi 'selector' olarak 'app-root' seçilmiş. Angular komponentleri elementlere `selector` adı verilen seçiciler ile bağlanırlar. Seçiciler bir bir çeşit css element seçicisi gibidir. Eğer `name` yazarsanız bir `etiket` seçmiş olursunuz, `.name` yazarsanız bir `class` seçmiş olursunuz ya da `[name]` yazarsanız bir `property` seçmiş olursunuz.

`templateUrl` özelliği komponentin arayüz şablonunun konumunu tutar. Bunun yerine `template` özelliğini kullanarak direkt bu dosyaya da html şablon yazabilirsiniz, ihtiyacınıza göre buna siz karar verebilirsiniz.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <b>hi</b>
  `,
  styleUrls: ['./app.component.css']
})
export class AppComponent {
}
```

`styleUrls` özelliği bize komponentin stil dosyasının konumunu gösterir. Yine yukarıda olduğu gibi `styles` kullanarak da css dosyası kullanmadan direkt olarak bu dosyaya css yazabilirsiniz. Ancak `template` ile `styles` arasında bir fark bulunur, styles bir string dizisi kabul eder, doğrudan string veremezsiniz.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <b>hi</b>
  `,
  styles: [
      `b {
          color: red;
      }`
  ]
})
export class AppComponent {
}
```

`app.component.spec.ts` dosyası testler hakkında işlemler içerir. Şimdilik bunu da erteliyoruz. (Söylemiştim testlerin kaderi bu.)

Angular projeleri modüller ile çalışır. Bu moduller `java` daki paketlere ya da `c#` daki isim uzaylarına benzerler. Sizin komponentleriniz bir modulde tanımlanır. `app.module.ts` dosyası ana modulu içerir.


```ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';

import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

Projede kullanılacak tüm komponentler bu dosyada deklare edilmelidir. Eğer burada deklare etmezsek kullandığımız zaman angular bu komponentleri bulamaz.

Şu anda diğer dosyaları ayrıntılı olarak açıklamak istemiyorum. Bunlara da sonra geleceğiz.

> Daha derine gitmeden önce typescript öğrenmenizi tavsiye ediyorum. Eğer konu hakkında bilginiz yoksa bi göz atıp sonra buradan devam edin.


### Yeni bir komponent oluşturmak

Yeni bir komponent oluştururken; önce `./src/app` dizininde bir `server` adında bir klasör oluşturalım.
Bu klasör içinde de `server.component.ts` adında bir dosya oluşturalım. Ayrıca `server.component.html` adında bir dosya daha oluşturmalısınız.

server.component.ts içinde;

```ts
export class ServerComponent {

}
```

`ServerComponent` adında bir sınıf oluşturduk ve sınıfı export ettik. Eğer export etmeseydik bu sınıfı dışarıda kullanamazdık. Hala yapmamız gereken işler var. Bu sınıfı bir komponente çevirecek bir `decorator` oluşturmalıyız. Hadi yapalım o zaman?

```ts
@Component({

})
export class ServerComponent {

}
```

Bu şekilde derlenmeyecektir. Bir şey daha dahil etmeliyiz. `Component` dekoratörü `@angular/core` paketi içinde tanımlı. Bu paketi şu şekilde import edebiliriz.

```ts
import { Component } from '@angular/core';

@Component({

})
export class ServerComponent {

}
```
Artık anguların kullanabileceği bir komponent oluşturmuş durumdayız. Fakat hala geçersiz. Çünkü bir `selector`'e sahip değil. Var olmasına rağmen herhangi bir yerde çağırılmış değil. Bu yüzden ona bir `selector` deklare etmeliyiz.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-server'
})
export class ServerComponent {

}
```

`selector` css seçicisi gibidir. Herhangi bir yere direkt olarak `app-server` yazarsanız; `<app-server></app-server>` şeklinde görünecektir. Eğer `.app-server` şeklinde kullanırsanız `<div class="app-server"></div>`. Hatta `[app-server]` bir özellik(property, attribute) olarak bile kullanabilirsiniz. (şöyle `<div app-server></div>`).

Komponentin html dosyasını komponente bağlamalıyız. Bunun için `templateUrl` kullanacağız. Tıpkı `app.component` içinde olduğu gibi.

```ts
import {Component} from '@angular/core';

@Component({
  selector: 'app-server',
  templateUrl: './server.component.html'
})
export class ServerComponent {

}
```

Bu komponenti kullanabilmek için `app.module.ts` içinde deklare etmeliyiz.


```ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';

import { AppComponent } from './app.component';
import { ServerComponent } from './server/server.component' // <<-- önce buradan import ediyoruz

@NgModule({
  declarations: [
    AppComponent,
    ServerComponent // <<-- ardından burada deklarasyonumuza ekliyoruz
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

```

Şimdi `server.component.html` dosyasını değiştireceğim.

```html
<b> server component </b>
```

Artık bu komponenti kullanbiliriz. Hemen `app.component.html` içinde kullanalım.

```html
<b> app component </b>

<app-server></app-server>
```

Şimdi [http://localhost:8080](http://localhost:8080) adresine bir göz atalım.

![](images/1.png)

### Komut satırı ile bir komponent oluşturmak

Bazen sürekli kendini tekrar eden yapıları üst üste oluşturmak istemeyebiliriz. Bu durum için `@angular/cli`'in bir çözümü var. `ng` nin generate fonksiyonu bize yeni komponentler oluşturmak için yardımcı oluyor.

```
ng generate component <name>
or
ng g c <name>
```

Eğer bir servers adında bir komponent oluşturmak istersek.

```
ng generate component servers
```

`app` dizini içine `servers` klasörü oluşturacak, onun da içine `ts`i `html`, `css` ve `.spec.ts` dosyalarını otomatik oluşturacaktır. Ayrıca `app.module.ts` içine bizim yerimize deklarasyon ekleyecek kısaca komponenti direkt olarak kullanıma hazır hale getirecektir.


### Projeye bootstrap css eklemek

Projemizde Boostrap'e ihtiyaç duyabiliriz. Nasıl import edeceğiz? İlk olarak indirmek zorundayız.

```
npm install bootstrap --save
```

Ardından `.angular-cli.json` dosyasını açarak şu şekilde düzenlemeliyiz.

```js
{
  "$schema": "./node_modules/@angular/cli/lib/config/schema.json",
  "project": {
    "version": "1.0.0-beta.32.3",
    "name": "new-cli"
  },
  "apps": [
    {
      "root": "src",
      "outDir": "dist",
      "assets": [
        "assets",
        "favicon.ico"
      ],
      "index": "index.html",
      "main": "main.ts",
      "polyfills": "polyfills.ts",
      "test": "test.ts",
      "tsconfig": "tsconfig.json",
      "prefix": "app",
      "styles": [
        "../node_modules/bootstrap/dist/css/bootstrap.min.css", // <<-- bu satırı ekledik
        "styles.css"
      ],
      "scripts": [],
      "environmentSource": "environments/environment.ts",
      "environments": {
        "dev": "environments/environment.ts",
        "prod": "environments/environment.prod.ts"
      }
    }
  ],
  "e2e": {
    "protractor": {
      "config": "./protractor.conf.js"
    }
  },
  "lint": [
    {
      "files": "src/**/*.ts",
      "project": "src/tsconfig.json"
    },
    {
      "files": "e2e/**/*.ts",
      "project": "e2e/tsconfig.json"
    }
  ],
  "test": {
    "karma": {
      "config": "./karma.conf.js"
    }
  },
  "defaults": {
    "styleExt": "css",
    "component": {}
  }
}

```

Artık bootstrap kullanıma hazır.

>**Note:** Bootstrap için bir kütüphane mevcut [bootstrap](https://github.com/ng-bootstrap/ng-bootstrap). Kolayca kullanabileceğimiz bir çok komponent içeriyor.


### Databinding

Databinding basitçe şablonlar ve sınıflar arasında verilerin bağlanmasını sağlar.

* **OUT** String Interpolation: Değişkeni şablona bağlar. Yazımı `{{ data }}` şeklindedir.
* **OUT** Property Binding: Bir değişkeni şablonun bir özelliğine atar. Yazımı `[property]="data"` şeklindedir.
* **IN** Olay yakalama: Olayı sınıftaki bir methoda bağlama. Yazımı `(event)="expression"` şeklindedir.

#### String Interpolation

Hadi isim yazan basit bir komponent yaratalım. İsim String Interpolation ile bizim sınıfımız içinde tanımlansın.  

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <p> My name is {{name}} </p>
  `
})
export class NameComponent {
  name: string = "Doğan";
}
```

Sonuç:

![](images/2.png)


Bu sefer 1 saniyelik bir gecikme ekleyelim. 1 saniyenin ardından ismin Göksel olarak değişeceğini göreceğiz. Ne kadar güzel bir isim.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <p> My name is {{name}} </p>
  `
})
export class NameComponent {
  name: string = "Doğan";

  constructor() {
    setTimeout(() => {
      this.name = "Göksel";
    }, 1000);
  }
}
```

Başlangıçta bize ` My name is Doğan ` yazmasının 1 saniye sonrasında ` My name is Göksel ` yazısını gördük. Databinding şablonu render etti. Yani render konusunu kafanıza takmayın.

#### Property binding and Event Binding

Şimdi diğer databinding(veri bağlama) tiplerini de görelim.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <button [disabled]="isDisabled" (click)="someAction()">Regular button</button>
    <button (click)="changeDisabled()"> {{isDisabled}} </button>
  `
})
export class NameComponent {
  isDisabled = true;

  someAction() {
    alert("hello");
  }

  changeDisabled() {
    this.isDisabled = !this.isDisabled; // değeri ters çevir
  }
}
```

Başlangıçta button tıklanamaz durumda. Ancak diğer butona tıkladığımızda artık tıklanabilir duruma geçiyor ve siz butona tıkladığınızda "merhaba" diyen bir alert görüyorsunuz.

#### Two way databinding

Angular'da bir databinding tipi daha var. Bu da `Two way databinding` (İki yönlü veri bağlama). Bu sefer olaylar, özellikler ve sınıflar bağlanacak.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <input [(ngModel)]="name"> 
    
    <p> My name is {{name}} </p>
  `
})
export class NameComponent {
  name: string = "Doğan";
}
```

Göreceksiniz input içindeki name özelliği değiştiğinde ` My name is _____ ` kısmı da otomatik olarak yeniden render edilecek. Eğer sınıftaki name özelliğini değiştirirseniz de input içindeki değer değişecektir.

> **Note:** `ngModel` `app.module.ts` dosyasında import edilmek zorundadır. Gerekli modülün adı `FormsModule`.

### Direktifler

3 tip direktif var.

* Komponentler
* Yapısal Direktifler (bunları `*` yıldız karakteri olarak göreceksiniz) 
* Özellik Direktifleri

Komponentleri artık zaten biliyorsunuz. Hadi yapısal direktiflere geçelim.

Bu direktifler dom'un tamamını kontrol ederler. Neden diye sorabilirsiniz.

#### ngIf

Hadi `*ngIf` örneğine bir göz atalım


```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <button (click)="visible = !visible">{{visible}}</button>
    <p *ngIf="visible">
      I'm visible now
    </p>
  `
})
export class NameComponent {
  visible: boolean = false;
}
```

Bu örnekte biz butona tıkladığımızda bir metin beliriyor. Ancak ilginç olan visible değişkeni false olduğunda p elementi henüz yok. Sadece visible değeri true olduğunda yaratılıyor. Yapısal direktifler var olan domu düzenler ya da yok ederler.

Ayrıca else de (Angular 4) kullanabilirsiniz.


```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <button (click)="visible = !visible">{{visible}}</button>
    <p *ngIf="visible; else hidden">
      I'm visible now
    </p>
    <ng-template #hidden>
      <p>
        I'm hidden
      </p>
    </ng-template>

  `
})
export class NameComponent {
  visible: boolean = false;
}
```

Devam etmeden önce lütfen deneyin.

#### ngFor

ngFor da yapısal bir direktifdir. Verilen diziye göre kendini düzenler ve kopyalar. Örneğin;

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <ul>
      <li *ngFor="let car of cars">{{car}}</li>
    </ul>
  `
})
export class NameComponent {
  cars = [
    'Toyota',
    'Honda',
    'Ford'
  ]
}
```

![](images/3.png)

ngFor ayrıca index'e de sahiptir. Eğer `;` bu kapsamda kullanabileceğiniz bir index değişkeni tanımlayabilirsiniz.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <ul>
      <li *ngFor="let car of cars; let i = index">({{i}}) {{car}}</li>
    </ul>
  `
})
export class NameComponent {
  cars = [
    'Toyota',
    'Honda',
    'Ford'
  ]
}
```

![](images/4.png)


#### ngStyle

ngStyle bir özellik direktifidir. Yapısal direktifler gibi görünmez.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <ul>
      <li *ngFor="let car of cars" [ngStyle]="{backgroundColor: car.total > 0 ? 'green' : 'red'}">{{car.name}}</li>
    </ul>
  `
})
export class NameComponent {
  cars = [
    {
      name: 'Toyota',
      total: 1
    },
    {
      name: 'Ford',
      total: 0
    }
  ]
}
```

Toyota elemanının yeşil Ford elemanının kırmızı olduğunu göreceksiniz.

#### ngClass

ngClass da özellik direktifidir.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <ul>
      <li *ngFor="let car of cars" [ngClass]="{notInStock: car.total == 0}">{{car.name}}</li>
    </ul>
  `,

  styles: [
    `.notInStock {
      background-color: red
    }`
  ]
})
export class NameComponent {
  cars = [
    {
      name: 'Toyota',
      total: 1
    },
    {
      name: 'Ford',
      total: 0
    },
  ]
}
```

Toyota elemanının normal ancak Ford elemanının kırmızı göründüğünü göreceksiniz.

#### ngSwitch

ngSwitch birden fazla durum arasında geçiş içindir. Çok kullanışlı bir ön tanımlı direktif.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <div [ngSwitch]="count">
      <p *ngSwitchCase="5"> Count is 5 </p>
      <p *ngSwitchCase="10"> Count is 10 </p>
      <p *ngSwitchDefault> Count is Default </p>
    </div>
  `
})
export class NameComponent {
  count: number = 5;
}
```


### Input

Bu bölümde hedefimiz bazı özellikleri dışarıdan erişilebilir hale getirmek olacak. Buna neden ihtiyaç duyalım diye sorabilirsiniz. Biz komponentleri kendi kapsamımızda yaratıyoruz. Örneğin "yeni bir kullanıcı yarat" adında bir komponenti ve "kullanıcıları listele" komponenti oluşturalım. Bu komponentler birbirleriyle etkileşime geçmek zorunda.

Yapmak istediklerimize başlarsak, birkaç komponent oluşturacağız.

```bash
ng new my-second-app
cd my-second-app
ng g c users --spec false    #-- spec false blocks spec file generation
ng g c users/user-list --spec false # users/list syntax will create a component in users folder. 
ng g c users/user-item --spec false
ng g c users/user-create --spec false
```

app.component.html dosyasını bu şekilde

```html
<app-users></app-users>
```


users.component.html dosyasını da bu şekilde düzenleyelim

```html
<app-user-create></app-user-create>
<hr>
<app-user-list></app-user-list>
```

ardından komponent dosyamıza bir kullanıcı dizisi ekleyelim.

```ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-user-list',
  templateUrl: './user-list.component.html',
  styleUrls: ['./user-list.component.css']
})
export class UserListComponent implements OnInit {
  users = ['Jack', 'George', 'Another common name']; // << bu satır
  
  constructor() { }

  ngOnInit() {
  }
}
```

user-list.component.html komponentini de şu şekilde düzenleyelim.

```html
<app-user-item *ngFor="let user of users"></app-user-item>
```

user-item.component.html ve user-item.component.ts dosyalarını da şöyle

```html
<p>
  User name: {{name}} 
  <button>Edit</button>
  <button>Delete</button>
</p>
```

```ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-user-item',
  templateUrl: './user-item.component.html',
  styleUrls: ['./user-item.component.css']
})
export class UserItemComponent implements OnInit {
  name: string;
  constructor() { }

  ngOnInit() {
  }

}
```

Sonuç olarak artık hazırız. Eğer bu noktaya kadar hatasız geldiyseniz şu ekranı görüyor olmalısınız.

![](images/5.png)

Kullanıcı alanları oluşturuldu fakat isim kısmı tam çalışıyor gibi görünmüyor. Yapmadığımız bir şeyi yapmak zorundayız. UserItemComponent elementinin name özelliği diğer komponent tarafından erişilemez çünkü kendi kapsamıyla sınırlı. Erişim için bir dekoratör eklemek zorundayız. Dekoratörümüzün adı `@Input`

Şimdi user.component.ts dosyamızı şu şekilde düzenliyoruz


```ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-user-item',
  templateUrl: './user-item.component.html',
  styleUrls: ['./user-item.component.css']
})
export class UserItemComponent implements OnInit {
  @Input() name: string;
  constructor() { }

  ngOnInit() {
  }

}
```

`@Input` dekoratörü aslında bir dekoratör oluşturma fonksiyonu. O yüzden onu bir method çağırır gibi çağırıyoruz `@Input()`. İlk parametreye bir isim verebilirsiniz. Bununla ilgili bir örnek de göstereceğim.

Şimdi uygulamamızı tekrar test ediyoruz ama sonuç değişmiyor. :worried:

![](images/5.png)

Şimdi de name değişkenini set etmeyi unuttuk çünkü ona user-item komponentinin dışından erişimimiz yok.

Bu kez user-list.component.html dosyasını düzenliyoruz:

```html
<app-user-item *ngFor="let user of users" [name]="user"></app-user-item>
```

Gördüğünüz gibi property binding kullandık. Basitçe `@Input` bir özellik olarak çalışıyor. Biz değeri user olarak tanımladık, çünkü değişkeni ngFor içinde `user` olarak tanımlamıştık.

Şimdi bir kez daha bakalım.

![](images/6.png)

Şimdi de isim vererek `@Input()` kullanımına bir örnek verelim.

app-user-item.ts

```ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-user-item',
  templateUrl: './user-item.component.html',
  styleUrls: ['./user-item.component.css']
})
export class UserItemComponent implements OnInit {
  @Input('user') name: string; // << gördüğünüz gibi bir parametre verdik
  constructor() { }

  ngOnInit() {
  }

}
```

Şimdi komponent `user` özelliği arayacak. 


Tekrar user-list.component.html dosyamızı düzenleyelim:

```html
<app-user-item *ngFor="let user of users" [user]="user"></app-user-item>
```

### Output

Input'tan bahsedeceğimiz son kısım. Örneğimizde ekleme ve silme butonları eklemiştik. Ayrıca bir user-create komponenti de. Bir göz atalım.

user-create.component.html

```html
name: <input type="text" [(ngModel)]="name">
<button (click)="onUserCreate()">create</button>
```

user-create.component.ts

```ts
import { Component, OnInit, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-user-create',
  templateUrl: './user-create.component.html',
  styleUrls: ['./user-create.component.css']
})
export class UserCreateComponent implements OnInit {

  constructor() { }

  ngOnInit() {
  }

  name: string; // two-way-binding property

  @Output()
  onUserCreated = new EventEmitter<string>(); // bu komponent dışından çağırılabilen bir olayımız
  // not: @angular/core modülünden EventEmitter import edilmiş olmalı 

  onUserCreate() { // kullanıcı butona tıkladığında bu method tetiklenecek
    this.onUserCreated.emit(this.name);  // buradan eventEmitter'e veri yollayacağız
  }
}
```

> **Not:** Kullanıcıları üst komponente taşıyacağım.

users.component.html

```html
<app-user-create (onUserCreated)="onUserCreated($event)"></app-user-create>
<hr>
<app-user-list [users]="users"></app-user-list>
```

users.component.ts

```ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-users',
  templateUrl: './users.component.html',
  styleUrls: ['./users.component.css']
})
export class UsersComponent implements OnInit {
  users = ['Jack', 'George', 'Another common name'];

  constructor() { }

  ngOnInit() {
  }

  onUserCreated(name) {
    this.users.push(name);
  }
}
```

user-list.component.ts

```ts
import { Component, OnInit, Input } from '@angular/core';

@Component({
  selector: 'app-user-list',
  templateUrl: './user-list.component.html',
  styleUrls: ['./user-list.component.css']
})
export class UserListComponent implements OnInit {
  @Input() // added this
  users; 
  
  constructor() { }

  ngOnInit() {
  }

}
```

Uygulamamıza bir göz atalım. Eğer inputumuza bir isim yazarsak ve ardından create butonuna tıklarsak. :sunglasses:

### View Encapsulation

Komponentlerin css dosyaları o komponente özeldir. Örneğin;

```css
b {
  color: red;
}
```

Bu css derlendiğinde diğer komponentlerin b elementleri de bundan etkilenebilir fakat biz bunun olmasını istemeyiz. View Encapsulation tam olarak bu soruna çözüm buluyor.

```ts
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'app-some',
  templateUrl: './some.component.html',
  styleUrls: ['./some.component.css'],
  encapsulation: ViewEncapsulation.None
})
export class SomeComponent {

}
```

### Local reference

Local reference DOM elemanlarını işaretlemek için kullanılır. `*ngIf` gibi yapısal direktiflerin içinde kullanırız. Yazmam gereken bir şey daha var, `@ViewChild` dekoratörü.

Bu dekoratör DOM elementlerine kod içinden erişime müsade eder. Eğer ne yaptığınızı biliyorsanız kullanın ancak aksi halde bu deokratörü kullanmaktan kaçının.

```ts
import { Component, ViewChild, ElementRef } from '@angular/core';

@Component({
  selector: 'app-some',
  template: `
  <div #localReference>

  </div>
  `
})
export class SomeComponent {
  @ViewChild('localReference') 
  localReferenceDiv: ElementRef;
}
```


### ng-content

ng-content elementlerin içeriklerine erişmemizi sağlayan özel bir direktiftir. Normal şartlarda angular komponentlerin içeriklerini ezer. `<app-root>Loading...</app-root>` bu konsept için iyi bir örnektir. Angular `app-root` içine komponenti yerleştirdiği anda Loading metni yok olacaktır. Fakat ya kaybolmasını bunu istemezsek.

Bir örnek göstermeme izin verin;

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-bold',
  template: `
    <b>
      <ng-content></ng-content> <!-- tüm içerik buraya gelecek -->
    </b>
  `
})
export class BoldComponent {
}
```

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <app-bold> bu metin kalın yazılacak </app-bold>
  `
})
export class AppComponent {
}
```

> **Not:** Son bölümde ViewChild'ı öğrnemiştik. Eğer içeriğin içinde ViewChild kullanmak isterseniz çalışmayacaktır. Bunun yerine `@ContentChild` kullanmak zorundasınız.

### Komponentlerin Yaşam Döngüsü

Komponentler standart bir yaşam döngüsüne sahiptir. Sahip olduğu tüm methodlar aşağıda. Bunların hepsini kullanabiliriz.

* ngOnChanges: Bir inputun değeri değiştiğinde.
* ngOnInit: Komponent ilk kez yüklendiğinde
* ngDoCheck: Her değişiklik algılandığından çağırılır.
* ngAfterContentInit: İçerik oluşturulduktan (ng-content) sonra çağırılır
* ngAfterContentChecked: Yansıtılan içerik her kontrol edildiğinde çağırılır
* ngAfterViewInit: Komponentin viewları ve alt viewları yansıtıldıktan sonra çağırılır
* ngAfterViewChecked: View ve alt viewları her kontrol edildiğinde çağırılır
* ngOnDestroy: Komponent yok edilmeden önce çağırılır

```ts
import { Component, OnInit, OnChanges, SimpleChanges, DoCheck, AfterContentInit, AfterContentChecked, AfterViewInit, AfterViewChecked, OnDestroy } from '@angular/core';

@Component({
  selector: 'app-some',
  template: ` `
})
export class SomeComponent implements OnInit, OnChanges, DoCheck, AfterContentInit, AfterContentChecked, AfterViewInit, AfterViewChecked, OnDestroy {

    ngOnChanges(changes: SimpleChanges): void {
    console.log('ngOnChanges', changes);
  }

  ngOnInit(): void {
    console.log('ngOnInit');
  }

  ngDoCheck(): void {
    console.log('ngDoCheck');
  }

  ngAfterContentInit(): void {
    console.log('ngAfterContentInit');
  }

  ngAfterContentChecked(): void {
    console.log('ngAfterContentChecked');
  }

  ngAfterViewChecked(): void {
    console.log('ngAfterViewChecked');
  }

  ngAfterViewInit(): void {
    console.log('ngAfterViewInit');
  }

  ngOnDestroy(): void {
    console.log('ngOnDestroy');
  }
}
```


### Yeni bir direktif yaratmak

Şimdiye kadar birkaç tane tanımlı direktif gördük. Fakat ya kendimiz yeni bir tane tanımlamak istersek. Bu bölümde buna göz atacağız.

Direktifler tıpkı komponentler gibi tanımlanır. Onları da app.module.ts dosyasına eklemek zorundasınız. Elle de oluşturabilirdik ancak ben @angular/cli kullanacağım.

```
ng generate directive <name>
or
ng g d <name>
```

Üzerine gelindiğinde elementleri yeşil yapan green adında bir direktif tanımlayacağım.

```
ng g d green
```

Şimdilik spec.ts dosyalarını yok ediyorum çünkü şu an testlerle ilgilenmiyoruz. Dosyanın adı green.directive.ts olmalı. Direktif dosyaları `<ad>.directive.ts` formatında oluşturulur.

```ts
import { Directive } from '@angular/core';

@Directive({
  selector: '[appGreen]'
})
export class GreenDirective {
  constructor() { }
}
```

Bu direktif `appGreen` özelliği ile temsil edilecek. Eğer bu direktifi bir elemente özellik olarak eklerseniz çalıştığını göreceksiniz.

#### HostListener

Hover olayında elementi yeşil yapmayı denemiştik yani bir olayı yakalamak zorundayız.

```ts
import { Directive, HostListener } from '@angular/core';

@Directive({
  selector: '[appGreen]'
})
export class GreenDirective {
  constructor() { }

  @HostListener('mouseenter')
  mouseenter() {
    // mouse enters
  }

  @HostListener('mouseleave')
  mouseleave() {
    // mouse leaves
  }
}
```

#### HostBinding

Peki ya renk değişimi? Bunun için de `@HostBinding` i kullanmalıyız.

```ts
import { Directive, HostBinding, HostListener } from '@angular/core';

@Directive({
  selector: '[appGreen]'
})
export class GreenDirective {
  @HostBinding('style.backgroundColor') backgroundColor: string = 'transparent';

  @HostListener('mouseenter')
  mouseenter() {
    this.backgroundColor = 'green';
  }

  @HostListener('mouseleave')
  mouseleave() {
    this.backgroundColor = 'transparent';
  }
}
```

### Servisler ve bağımlılıkların zerki

Servisler komponentler arası veri taşımak için oldukça kullanışlıdır. Servis oluşturmak için herhangi bir dekoratöre ihtiyaç duymayız. Hadi bir kullanıcı servisi oluşturalım.

Şu şekilde `<ad>.service.ts` bir söz dizimi ile oluşturmanızı tavsiye ederim.

Hadi  `app` klasörü içine users.service.ts adında bir dosya oluşturalım.

```ts
export class UserService {
  users = [
    {id: 1, name: 'co3moz'},
    {id: 2, name: 'goxel'}
    {id: 3, name: 'Ilrkhoaktul'}
  ]

  getUsers() {
    return this.users;
  }

  addUser(user: {id: number, name: string}) {
    this.users.push(user);
  }

  removeUser(id: number) {
    this.users.splice(id, 1);
  }
}
```

Basitçe bazı fonksiyon ve özellikler içeren bir sınıf oluşturduk.

Şimdi bir komponent içinde kullanalım.

```ts
import { UserService } from 'user.service';
import { Component } from '@angular/core';

@Component({
  selector: 'app-user-list',
  template: `
    <p *ngFor="let user of users"> {{ user.name }} </p>
  `,
  providers: [
    UserService
  ]
})
export class UserListComponent implements OnInit {
  users;
  constructor(private userService: UserService) {} // userService's type must be declared. Otherwise it won't work.

  ngOnInit() {
    this.users = this.userService.getUsers(); // pass reference of array to local variable.
  }
}
```

> **Önemli Not:** Providers(Sağlayıcılar) komponente servis sağlarlar ancak userlistComponent her oluşturulduğunda kendi UserService servisini oluşturur. Çünkü biz komponente yapıcı fonksiyon içinde her oluşturulduğunda bir UserService oluşturmasını söyledik. Fakat ya bunun uygulama çapında olmasını isteseydik. Bu verileri komponent dışında da kullanmaya ihtiyaç duyabiliriz. Bu iş için app.module.ts dosyasını kullanacağız. Bu dosyanın içindeki providers alanına servisimizi ekleyeceğiz.

> **Önemli Not 2:** Eğer yeni bir UserService sağlayıcıs deklare edilmezse userListComponent'in alt komponentleri aynı servisi kullanabilir. Yani komponentin sağlayıcılar kısmı sadece yeni bir sağlayıcı yaratmak için kullanılmalıdır.

Ayrıca `@angular/cli`'i de servis oluşturmak için kullanabilirsiniz

```
ng generate service <name>
or
ng g s <name>
```

#### Bir servisi diğer servis içine çağırmak

Bir servise bir başka servisin içinde ihtiyaç duyabiliriz. Örneğin bir loglama servisimiz vardır ve diğer servislerden çağırılması gerekiyordur. Peki bu servisi diğerlerinin içinde nasıl kullanabiliriz?

İşte gidiyoruz, `@Injectable` örnekleri;

```ts
import { LoggingService } from 'logging.service';
import { Injectable } from '@angular/core';

@Injectable()
export class UserService {
  users = [
    {id: 1, name: 'co3moz'},
    {id: 2, name: 'goxel'}
    {id: 3, name: 'Ilrkhoaktul'}
  ];

  constructor(private loggingService: LoggingService) {

  }

  getUsers() {
    return this.users;
  }

  addUser(user: {id: number, name: string}) {
    this.users.push(user);
    this.loggingService.log('user added');
  }

  removeUser(id: number) {
    this.users.splice(id, 1);
    this.loggingService.log('user removed');
  }
}
```


#### Event emitting servisi

Bazı bilgileri yayınlayan olaylara ihtiyaç duyabiliriz.


```ts
import { LoggingService } from 'logging.service';
import { Injectable, EventEmitter } from '@angular/core';

@Injectable()
export class UserService {
  users = [
    {id: 1, name: 'co3moz'},
    {id: 2, name: 'goxel'}
    {id: 3, name: 'Ilrkhoaktul'}
  ];

  constructor(private loggingService: LoggingService) {

  }

  userCreated = new EventEmitter<{id: number, name: string}>();

  getUsers() {
    return this.users;
  }

  addUser(user: {id: number, name: string}) {
    this.users.push(user);
    this.userCreated.emit(user);
    this.loggingService.log('user added');
  }

  removeUser(id: number) {
    this.users.splice(id, 1);
    this.loggingService.log('user removed');
  }
}
```

Komponent içinde sadece bu olaya abone olalım. Daha iyi bir özellik öğreneceğiz ancak bu özelliği de bilmiş olalım.

```ts
import { UserService } from 'user.service';
import { Component } from '@angular/core';

@Component({
  selector: 'app-user-list',
  template: `
    <p *ngFor="let user of users"> {{ user.name }} </p>
  `,
  providers: [
    UserService
  ]
})
export class UserListComponent implements OnInit {
  users;
  constructor(private userService: UserService) {
    this.userService.userCreated.subscribe((user) => {
      console.log('new user just created');
    });
  } // userService's type must be declared. Otherwise it won't work.

  ngOnInit() {
    this.users = this.userService.getUsers(); // pass reference of array to local variable.
  }
}
```

> **Önemli Not:** Bir olaya manuel olarak abone olduğunuz zaman, komponent yok olurken `ngOnDestroy` içinde abonelikten çıkmayı unutmayın.


### Router

Router komponentleri birer sayfaya yönlendirir. Router ilk önce `app.module.ts`'a gider.

Öncelikle `@angular/router` modülünden Routes objesini import etmeliyiz

```ts
import { Routes, RouterModule } from '@angular/router';
```

Ardından bu obje ile bir dizi tanımlayacağız:

```ts
const appRoutes: Routes = [
  { path: 'users', component: UsersComponent}
];
```

`path` tarayıcıdaki rotayı tanımlar, örneğin `users` pathi `/users` adresini tanımlar. Eğer path kısmı boş verildiyse ana sayfa olarak kullanılabilir.

```ts
const appRoutes: Routes = [
  { path: '', component: HomeComponent},
  { path: 'users', component: UsersComponent}
];
```
Ardından bu nesneyi `RouterModule.forRoot(appRoutes)` modülüne parametre olarak geçmeliyiz.

> **Not** `app.route.ts` ya da `app.routing.ts` adından dosyalar yaratabilirsiniz. Sizin kararınıza kalmış.

Şimdi routerın komponentleri nerede göstereceğini tanımlayacağız. `<router-outlet></router-outlet>`.

Bu componenti app.component.html içine ekliyoruz.

#### Linkler

Bu bölümde router linklerini öğreneceğiz.

Normalde basitçe `href` kullanırız.

```html
<a href="/home">Home</a>
```
Ancak angularda bu geçersiz çünkü tıklamalar tam sayfa yenilenmesine neden olur. Uygulamamız mümkün olduğunda kararlı olmak zorunda.

Biz `routerLink` direktifini kullanacağız.

```html
<a routerLink="/home">Home</a>
```

Bu şekilde `[]` de kullanabilirsiniz.

```html
<a [routerLink]="['/user', id]">Home</a>
```

#### Active route

Bazen aktif sayfaya özel bir stil vermek ya da başka bir şey yapmak isteyebiliriz. Bunu başarmak için `routerLinkActive` kullanırız.

```html
<div routerLinkActive="active">
  <a routerLink="/">Home</a>
</div>
```

routerLinkActive direktifi `routerLinkActiveOptions` adında başka bir direktife sahiptir. Bu routerLinkActiveOptions direktifiyle birlikte ek opsiyonlar verebiliriz. Örneğin tam path doğrulaması:

```html
<div routerLinkActive="active" [routerLinkActiveOptions]="{exact: true}">
  <a routerLink="/">Home</a>
</div>
```

#### Navigating from code

Bazen router'a kod içinden erişmek çok kullanışlı olabilir.

```ts
import { Component } from '@angular/core';
import { Router } from '@angular/router';

@Component({
  selector: 'app-user-list',
  template: ``
})
export class UserListComponent  {
  constructor(private router: Router) {
  } 

  navigateSomewhereElse() {
    this.router.navigate(['/home']);
  }

}
```


#### Parameters of routes

Örnekler her şeyi gösteriyor.

```ts
const appRoutes: Routes = [
  { path: '', component: HomeComponent},
  { path: 'users/:id', component: UsersComponent}
];
```

```ts
import { Component } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'app-user-list',
  template: ``
})
export class UsersComponent  {
  constructor(private route: ActivatedRoute) {
  } 

  getIdParameter() {
    return this.route.snapshot.params['id'];
  }

}
```

#### Nested routes

Birleşik rotalar birden fazla komponenti aynı anda göstermek istediğimiz zaman kullanışlı olabilir.

```ts
const appRoutes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'users', component: UsersComponent, children: [
    { path: ':id', component: UserComponent },
    { path: ':id/edit', component: UserEditComponent }
  ]}
];
```

Ana komponente `<router-outlet></router-outlet>` eklemeyi unutmayın.


#### Redirecting

Bazen bir route'u yönlendirme isteyebiliriz. Basitçe redirectTo parametresiyle bunu gerçekleştirebiliriz. Örneğin;

```ts
const appRoutes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'users', component: UsersComponent },
  { path: 'people', redirectTo: '/users' }
];
```

Bu özellikle wildcard özelliği ve 404 sayfaları yapabilirz.

```ts
const appRoutes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'users', component: UsersComponent },
  { path: 'not-found', component: NotFoundComponent },
  { path: '**', redirectTo: '/not-found' } // make sure wildcard is at the end.
];
```

Diğer tüm karşılıksız adresler `NotFoundComponent` komponentine gidecektir.
