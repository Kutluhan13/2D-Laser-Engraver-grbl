***

# 2D Laser Engraver
### A laser engraver made with modified grbl. Can also be used as 3D and on CNC milling applications.
**English ReadMe will be uploaded soon!**

***

Merhaba, ben Kutluhan. Bu klasörde grbl altyapýsýyla gerçekleþtirmiþ olduðum **2D Lazer Yazýcý** projesine ait kaynak kodlarý ve tasarým dosyalarýný bulacaksýnýz.

_**1)Dikkat Edilmesi Gerekenler:**_
* Devrelere güç verilmiþken baðlantýlar çýkarýlmamalý veya takýlmamalýdýr.
* Arduino, belleðine ilk defa **grbl** yazýlýmý yüklenirken herhangi bir çevresel elemana baðlý olmamalýdýr. (I/O Pinlerine herhangi birþey takýlý olmamalý.)
* Çalýþma esnasýnda step motor düzenlerine ve elektriksel devrelere dokunulmamalý ve ESD korumasý yapýlmadan devreler üzerinde herhangi bir bakým/onarým iþlemi yapýlmamalýdýr.

_**2)Lazer Modülü ile ilgili dikkat edilmesi gerekenler ve güvenlik önlemleri:**_
* Bu projede Class 4 Lazer Modülü kullanýlmaktadýr. Bu güçteki lazerlerin ani körlük ve deri hasarý oluþturma tehlikesinden dolayý çalýþýrken dikkatli olunmalý ve 405nm deðerine uygun koruyucu gözlük kullanýlmalýdýr.
* Lazer diyotlar akýma ve voltaj deðiþimlerine çok fazla duyarlýdýrlar. Herhangi bir güç kaynaðý veya pil ile çalýþtýrýldýklarýnda saniyeler içerisinde kalýcý zarar alacaklardýr. Bu yüzden diyodun özelliklerine uygun olarak ayarlanmýþ sabit akým sürücüsü ve ESD koruma devresi kullanýlmalýdýr. Ayrýca yüksek güç deðerine sahip diyotlar çalýþma esnasýnda çok fazla ýsýnýrlar. Soðutucu bir tertibat kullanýlmazsa lazer diyotun ömrü hýzla azalýr. Projenin kapsamý dýþýnda olan bu konular araþtýrýlmalý ve gerekli devreler lazer diyotla birlikte alýnmalýdýr.
* Lazerin odak noktasý çalýþma tablasýna konulan malzemenin yüksekliðine göre yeniden ayarlanmalýdýr. Lazerin **405nm** olmasý dolayýsýyla uygun odak noktasý yakalanýrsa sadece UV ýþýk altýnda görünen çizimler de yapýlabilmektedir.

_**3)Gerekli Olan Malzemeler:**_
* 0.5W 405nm TTL Industrial Laser+Driver(12v)
* Arduino Nano (Atmega328P-5v/16Mhz)
* Easydriver Step Sürücü Modülü*2
* CD/DVD Reader/Writer Step Motor ve Ray Düzeni*2
* Frame (Solidworks tasarým dosyasý mevcuttur ve 3 boyutlu yazýcýdan çýktý alýnabilir.)
* Step Down Buck Dönüþtürücü(Min. 15v INPUT)

_**4)Fiziksel Kurulum:**_
* Sistem elemanlarý frame üzerine yerleþtirildikten sonra step motorlarýn 4 kablosu uygun sýrayla sürücülere baðlanmalýdýr. Test yapýlýrken eksenlerin ters çalýþtýðý görülürse bu 4 kablo sökülüp tam tersi þekilde baðlanmalýdýr. 
* Çalýþtýrma öncesi üst eksen soldan, Taban eksen üst eksene uzak olarak konumlandýrýlmalýdýr. 
* Sürücüler ve step motorlar 5v, lazer devresi ise 12v ile güçlendirilmelidir. 
* **Arduino, Step Motor Sürücüleri ve Lazer Sürücüsü**'nün GND raylarý birbirine baðlanmalýdýr. 
* Yazýcýnýn sol yüzü kullanýcýya bakacak þekilde çýktý alýnmalýdýr.

_**5)Sinyal Baðlantýlarý:**_
* D8 Stepper Cut (Easydriver EN' pinine)
* D12 Laser Enable (Lazer sürücü TTL giriþine)
---
Step  /   Dir
D2    /   D3           X-Taban
D4    /   D5           Y-Üst

_**6)Yazýlým Kurulumu:**_
* Atmega328P kullanýlmalýdýr. Atmega168 üzerinde grbl çalýþtýrýlamaz.
* **grbl-K13** içerisindeki **grbl** klasörü **Arduino IDE**'nin kurulu olduðu konumda bulunan libraries klasörüne kopyalanmalýdýr. Daha sonra Arduino IDE açýlarak üst sekmeden File>Examples>grbl>grblUpload kodu açýlarak daha önceden USB portuna baðlanmýþ Arduino Nano'ya yüklenmelidir.
* Baud Rate:115200 CariageReturn Ayarlarýyla **Tools** sekmesinin altýndaki **Serial Monitor** açýlarak þu kod girilmelidir: **$RST=***
Test için sýrasýyla:
G91 G28 X0 Y0
X10 Y10
girilmelidir. Bu kod X ve Y eksenlerini 10'ar mm + yönünde hareket ettirecektir. Eðer step motorlar tersi yönde hareket etmeye çalýþýyorlarsa sürücüye baðlandýklarý 4 kablo tam tersi þekilde baðlanmalýdýr.
* Bu projedeki donanýma uygun olarak grbl üzerinde bazý ayarlamalar yapýlmýþtýr. Proje yeniden yapýlacak ise; yüksek doðruluk ve hassasiyet için aþaðýda verilen grbl linkinden yararlanarak steps/mm, mm/sec^2, max travel-mm, max rate vb. deðerleri deneysel veya ölçümsel metodlarla bulunmalýdýr.

_**7)Kullaným:**_
* Lazer CNC uygulamasý için hazýrlanmýþ herhangi bir GCode, aþaðýdaki linklerden indirilebilecek **Universal Gcode Sender** kullanýlarak 2 boyutlu lazer yazýcýya aktarýlabilir.

_**8)Linkler:**_
* https://github.com/grbl/grbl
* https://github.com/grbl/grbl/wiki
* https://github.com/winder/Universal-G-Code-Sender