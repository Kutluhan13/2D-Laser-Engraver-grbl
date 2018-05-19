***

# 2D Laser Engraver
### A laser engraver made with modified grbl. Can also be used as 3D and on CNC milling applications.
**English ReadMe will be uploaded soon!**

***

Merhaba, ben Kutluhan. Bu klasörde grbl altyapısıyla gerçekleştirmiş olduğum **2D Lazer Yazıcı** projesine ait kaynak kodları ve tasarım dosyalarını bulacaksınız.

_**1)Dikkat Edilmesi Gerekenler:**_
* Devrelere güç verilmişken bağlantılar çıkarılmamalı veya takılmamalıdır.
* Arduino, belleğine ilk defa **grbl** yazılımı yüklenirken herhangi bir çevresel elemana bağlı olmamalıdır. (I/O Pinlerine herhangi birşey takılı olmamalı.)
* Çalışma esnasında step motor düzenlerine ve elektriksel devrelere dokunulmamalı ve ESD koruması yapılmadan devreler üzerinde herhangi bir bakım/onarım işlemi yapılmamalıdır.

_**2)Lazer Modülü ile ilgili dikkat edilmesi gerekenler ve güvenlik önlemleri:**_
* Bu projede Class 4 Lazer Modülü kullanılmaktadır. Bu güçteki lazerlerin ani körlük ve deri hasarı oluşturma tehlikesinden dolayı çalışırken dikkatli olunmalı ve 405nm değerine uygun koruyucu gözlük kullanılmalıdır.
* Lazer diyotlar akıma ve voltaj değişimlerine çok fazla duyarlıdırlar. Herhangi bir güç kaynağı veya pil ile çalıştırıldıklarında saniyeler içerisinde kalıcı zarar alacaklardır. Bu yüzden diyodun özelliklerine uygun olarak ayarlanmış sabit akım sürücüsü ve ESD koruma devresi kullanılmalıdır. Ayrıca yüksek güç değerine sahip diyotlar çalışma esnasında çok fazla ısınırlar. Soğutucu bir tertibat kullanılmazsa lazer diyotun ömrü hızla azalır. Projenin kapsamı dışında olan bu konular araştırılmalı ve gerekli devreler lazer diyotla birlikte alınmalıdır.
* Lazerin odak noktası çalışma tablasına konulan malzemenin yüksekliğine göre yeniden ayarlanmalıdır. Lazerin **405nm** olması dolayısıyla uygun odak noktası yakalanırsa sadece UV ışık altında görünen çizimler de yapılabilmektedir.

_**3)Gerekli Olan Malzemeler:**_
* 0.5W 405nm TTL Industrial Laser+Driver(12v)
* Arduino Nano (Atmega328P-5v/16Mhz)
* Easydriver Step Sürücü Modülü*2
* CD/DVD Reader/Writer Step Motor ve Ray Düzeni*2
* Frame (Solidworks tasarım dosyası mevcuttur ve 3 boyutlu yazıcıdan çıktı alınabilir.)
* Step Down Buck Dönüştürücü(Min. 15v INPUT)

_**4)Fiziksel Kurulum:**_
* Sistem elemanları frame üzerine yerleştirildikten sonra step motorların 4 kablosu uygun sırayla sürücülere bağlanmalıdır. Test yapılırken eksenlerin ters çalıştığı görülürse bu 4 kablo sökülüp tam tersi şekilde bağlanmalıdır. 
* Çalıştırma öncesi üst eksen soldan, Taban eksen üst eksene uzak olarak konumlandırılmalıdır. 
* Sürücüler ve step motorlar 5v, lazer devresi ise 12v ile güçlendirilmelidir. 
* **Arduino, Step Motor Sürücüleri ve Lazer Sürücüsü**'nün GND rayları birbirine bağlanmalıdır. 
* Yazıcının sol yüzü kullanıcıya bakacak şekilde çıktı alınmalıdır.

_**5)Sinyal Bağlantıları:**_
* D8 Stepper Cut (Easydriver EN' pinine)
* D12 Laser Enable (Lazer sürücü TTL girişine)
---
Step  /   Dir
D2    /   D3           X-Taban
D4    /   D5           Y-Üst

_**6)Yazılım Kurulumu:**_
* Atmega328P kullanılmalıdır. Atmega168 üzerinde grbl çalıştırılamaz.
* **grbl-K13** içerisindeki **grbl** klasörü **Arduino IDE**'nin kurulu olduğu konumda bulunan libraries klasörüne kopyalanmalıdır. Daha sonra Arduino IDE açılarak üst sekmeden File>Examples>grbl>grblUpload kodu açılarak daha önceden USB portuna bağlanmış Arduino Nano'ya yüklenmelidir.
* Baud Rate:115200 CariageReturn Ayarlarıyla **Tools** sekmesinin altındaki **Serial Monitor** açılarak şu kod girilmelidir: **$RST=***
Test için sırasıyla:
G91 G28 X0 Y0
X10 Y10
girilmelidir. Bu kod X ve Y eksenlerini 10'ar mm + yönünde hareket ettirecektir. Eğer step motorlar tersi yönde hareket etmeye çalışıyorlarsa sürücüye bağlandıkları 4 kablo tam tersi şekilde bağlanmalıdır.
* Bu projedeki donanıma uygun olarak grbl üzerinde bazı ayarlamalar yapılmıştır. Proje yeniden yapılacak ise; yüksek doğruluk ve hassasiyet için aşağıda verilen grbl linkinden yararlanarak steps/mm, mm/sec^2, max travel-mm, max rate vb. değerleri deneysel veya ölçümsel metodlarla bulunmalıdır.

_**7)Kullanım:**_
* Lazer CNC uygulaması için hazırlanmış herhangi bir GCode, aşağıdaki linklerden indirilebilecek **Universal Gcode Sender** kullanılarak 2 boyutlu lazer yazıcıya aktarılabilir.

_**8)Linkler:**_
* https://github.com/grbl/grbl
* https://github.com/grbl/grbl/wiki
* https://github.com/winder/Universal-G-Code-Sender
