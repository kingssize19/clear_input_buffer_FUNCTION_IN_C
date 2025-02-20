# clear_input_buffer Fonksiyonunun Amacı ve Detaylı Açıklaması

* clear_input_buffer fonksiyonu, genellikle scanf veya diğer giriş işlemlerinden sonra, kullanıcının girilen verileri okuduktan sonra geri kalan geriye kalan (veya fazladan) giriş verilerini temizlemek için kullanılır. Bu tür fonksiyonlar, özellikle scanf kullanıldığında, bazen kullanıcı tarafından girilen geçersiz veya ekstra karakterlerin (örneğin, **Enter** tuşuna basıldığında girilen **\n** karakteri) akışa dahil olması nedeniyle, sonraki giriş işlemleri düzgün çalışmayabilir. Bu durumu önlemek için clear_input_buffer fonksiyonu devreye girer.

--------------------------------------------------------------------------------------------------------------------------------------------------------

## clear_input_buffer Fonksiyonu :

* Bu fonksiyon, standart giriş akışındaki (stdin) herhangi bir fazla karakteri (mesela, **\n**, **\r**, boşluklar veya diğer girilen karakterler) temizler. Çünkü scanf ile bir sayı okuduktan sonra, kullanıcı Enter tuşuna basar ve bu da bir **\n** (yeni satır) karakterini bırakır. Bu fazladan karakter, sonraki getchar() veya başka giriş fonksiyonları tarafından yanlışlıkla okunabilir.

### Fonksiyonun İçeriği

```c
void clear_input_buffer(void)
{
    int ch;
    // Karakterleri okur ve her biri '\n' veya EOF ile karşılaşana kadar siler
    while ((ch = getchar()) != '\n' && ch != EOF)
        ; // boş bir işlem (null statement)
}
```

### Nasıl Çalışır?

**1. getchar() :** Bu fonksiyon, kullanıcıdan bir karakter alır. Bu karakterler genellikle stdin (standart giriş akışı) üzerinden gelir.
**2. while ((ch = getchar()) != '\n' && ch != EOF) :** Bu döngü, **getchar()** tarafından okunan her karakteri kontrol eder. Karakter bir \n (yeni satır) veya EOF (dosya sonu) değilse, döngü devam eder ve o karakteri **"tüketir"**. \n genellikle **Enter** tuşuna basıldığında gelir.
**3. ch != '\n' :** Bu koşul, eğer okunan karakter bir yeni satır (\n) değilse döngüyü devam ettirir. Bu, kullanıcının **Enter** tuşuna basıp fazladan boşlukları veya karakterleri temizlememizi sağlar.
**4. ch != EOF :** Bu koşul, dosya sonuna gelene kadar devam eder. Bu tip bir senaryo nadiren gerçekleşir, ancak tüm karakterler okunana kadar temizleme işlemi yapılır.

### clear_input_buffer Kullanım Amacı :

Bu fonksiyon özellikle şu durumlarda kullanılır.
* scanf gibi fonksiyonlar, bazen tam olarak beklenen türde veri almaz ve geri kalan karakterler **stdin**'de kalabilir. Bu karakterler, sonraki getchar() veya scanf işlemlerini engelleyebilir.
* **Kullanıcı Enter tuşuna bastığında, \n karakteri akışta kalır.** Bu, sonraki giriş işlemlerini etkiliyebilir çünkü scanf veya getchar bu karakteri yanlışlıkla okuyabilir. clear_input_buffer bu karakterleri temizler.

### Kodu Adım Adım Açıklama :

**1. Kullanıcıdan Sayı Girişi :**
* scanf("%d", &x); ile kullanıcıdan bir tamsayı alınır.

**2. clear_input_buffer() Çalıştırılması :**
* clear_input_buffer(); çağrısı ile fazladan kalan karakterler temizlenir. Bu durumda, kullanıcı Enter tuşuna bastığında bir \n karakteri kalır, bu karakter temizlenir.

**3. getchar() Kullanımı :**
* (void)getchar(); satırı, ekrana bir şey yazdırılmadan önce kullanıcının Enter tuşuna basmasını bekler. Bu sayede, kullanıcıdan ekstra giriş alınmadan program devam eder.

**4. printf Çıkışı :**
* Son olarak, kullanıcı tarafından girilen x değeri ekrana yazdırılır.

### Önemli Not :

* Eğer clear_input_buffer() fonksiyonu kullanılmazsa, fazladan kalan \n karakteri, sonraki getchar() veya scanf çağrılarını etkileyebilir. Örneğin, getchar() hemen bir \n karakteri okuyabilir ve hemen sonrasındaki kullanıcıdan girdi beklenmeden program çalışmaya devam eder.

### Örnek Senaryo :

1. Kullanıcı 123 girer ve Enter tuşuna basar.
2. scanf("%d", &x); ile bu 123 sayısı alınır, ancak \n karakteri hala giriş tamponunda kalır.
3. clear_input_buffer(); çalıştırılır ve giriş tamponundaki \n temizlenir.
4. (void)getchar(); çağrısı, \n karakterini okuyarak işlemi tamamlar ve kullanıcıyı tekrar bir tuşa basmaya zorlar.
5. printf("x : %d\n", x); ile x ekrana yazdırılır.

* Eğer clear_input_buffer kullanılmazsa, son getchar() hemen bir \n karakterini okuyarak hiçbir şey yapmadan devam eder, ve program doğrudan printf kısmına geçer.


### Sonuç :
* clear_input_buffer fonksiyonu, kullanıcının girdiği fazla karakterlerden, özellikle de Enter tuşuyla eklenen \n karakterinden kurtulmak için kullanılır.
* Bu, sonraki kullanıcı girişi bekleyen fonksiyonların doğru çalışması için gereklidir.



































