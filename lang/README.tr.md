Angular 4 - Notları (Türkçe çeviri)
====================

Çeviri durumu: :black_medium_square: :black_square_button: :black_square_button: :black_square_button: :black_square_button: :black_square_button: :black_square_button: :black_square_button: :black_square_button: :black_square_button:

Bu repository benim angular 4 maceramı içermektedir. Angular 2'e geçiş yapamamıştım. Şimdide neden olmasın diye düşündüm ve bir eğitim programı ile angular 4'ü öğreniyorum. Öğreneceğim her türlü bilgiyi burada yazacağım. Umarım bu reposity sizi yönlendirir.

 [Maximilian Schwarzmuller](https://www.udemy.com/the-complete-guide-to-angular-2)'e güzel dersleri için teşekkürler


kg.


İçindekiler
----------------

- [Kurulum](#kurulum)
- [Proje yaratma](#proje-yaratma)
- [Proje sunma](#proje-sunma)

### Kurulum

Uygulama yapmak için node.js'in kurulu olması gerekmektedir. Eğer node.js hakkında bir bilginiz yoksa angular 4'ten önce mutlaka incelemeniz gerekiyor. Angular cli'i kullanacağız. Bu bir takım şeyler yaratmamızı sağlayacak. Çok kullanışlı bir tooldur kendileri.

```
npm i @angular/cli -g
```

`@angular/cli` paketini global parametresiyle kurmamız gerekmekte. Bu parametre lokal node_modules klasörü yerine global klasörü kullanmamızı sağlayacak.

Artık `ng` komutunu terminalde kullanabiliriz.


### Proje yaratma

Proje oluşturmak için `ng` komutunu kullanacağız. Terminale `ng` yazmayı deneyin eğer hata alıyorsanız `Kurulum` adımı başarısız olmuştur. Lütfen geri gidin ve adımların doğru yapıldığından emin olun.

ng komutu birden çok argümana sahip. Hepsine bakmaktansa bize lazım olana atlıyorum. Projeyi yaratmak için `new` argumentini kullanacağız.

Bu argument aktif bulunan klasör altında yeni bir proje çatısı oluşturmamızı sağlayacak ancak oluşturma işlemi için bizim bir proje adı girmemiz gerekiyor. Proje adını şimdilik "my-first-app" olarak belirliyorum.

```
ng new my-first-app
```

Bu komutu terminale yazdıktan sonra bazı dosyalar `ng` tarafından oluşturulacak. Gerekli paketlerin kurulumu npm sayesinde yapılacak. Kurulum bitene kadar bekleyin.


### Projeyi sunma

Yeni projemizi oluşturduk. `my-first-app` klasörümüze girelim. `ng` komutunun `serve` argumentini kullanalım. Bu paketleme işlemleri yapacak ve http sunucusu oluşturacak.

```
cd my-first-app
ng serve
```

Terminal çıktısında, bir url adresi olmalı. eğer bulamıyorsanız portu `--port xxx` parametresini kullanarak değiştirebilirsiniz.

```
ng serve --port 8080
```

Typescript derlendi ve webpack uygulamanızı paketledi.

Şimdi bu adrese girmeye çalışın [http://localhost:8080](http://localhost:8080)

