***

# 2D Laser Engraver
### A laser engraver made with modified grbl. Can also be used as 3D and on CNC milling applications.
**English ReadMe will be uploaded soon!**

***

Merhaba, ben Kutluhan. Bu klas�rde grbl altyap�s�yla ger�ekle�tirmi� oldu�um **2D Lazer Yaz�c�** projesine ait kaynak kodlar� ve tasar�m dosyalar�n� bulacaks�n�z.

_**1)Dikkat Edilmesi Gerekenler:**_
* Devrelere g�� verilmi�ken ba�lant�lar ��kar�lmamal� veya tak�lmamal�d�r.
* Arduino, belle�ine ilk defa **grbl** yaz�l�m� y�klenirken herhangi bir �evresel elemana ba�l� olmamal�d�r. (I/O Pinlerine herhangi bir�ey tak�l� olmamal�.)
* �al��ma esnas�nda step motor d�zenlerine ve elektriksel devrelere dokunulmamal� ve ESD korumas� yap�lmadan devreler �zerinde herhangi bir bak�m/onar�m i�lemi yap�lmamal�d�r.

_**2)Lazer Mod�l� ile ilgili dikkat edilmesi gerekenler ve g�venlik �nlemleri:**_
* Bu projede Class 4 Lazer Mod�l� kullan�lmaktad�r. Bu g��teki lazerlerin ani k�rl�k ve deri hasar� olu�turma tehlikesinden dolay� �al���rken dikkatli olunmal� ve 405nm de�erine uygun koruyucu g�zl�k kullan�lmal�d�r.
* Lazer diyotlar ak�ma ve voltaj de�i�imlerine �ok fazla duyarl�d�rlar. Herhangi bir g�� kayna�� veya pil ile �al��t�r�ld�klar�nda saniyeler i�erisinde kal�c� zarar alacaklard�r. Bu y�zden diyodun �zelliklerine uygun olarak ayarlanm�� sabit ak�m s�r�c�s� ve ESD koruma devresi kullan�lmal�d�r. Ayr�ca y�ksek g�� de�erine sahip diyotlar �al��ma esnas�nda �ok fazla �s�n�rlar. So�utucu bir tertibat kullan�lmazsa lazer diyotun �mr� h�zla azal�r. Projenin kapsam� d���nda olan bu konular ara�t�r�lmal� ve gerekli devreler lazer diyotla birlikte al�nmal�d�r.
* Lazerin odak noktas� �al��ma tablas�na konulan malzemenin y�ksekli�ine g�re yeniden ayarlanmal�d�r. Lazerin **405nm** olmas� dolay�s�yla uygun odak noktas� yakalan�rsa sadece UV ���k alt�nda g�r�nen �izimler de yap�labilmektedir.

_**3)Gerekli Olan Malzemeler:**_
* 0.5W 405nm TTL Industrial Laser+Driver(12v)
* Arduino Nano (Atmega328P-5v/16Mhz)
* Easydriver Step S�r�c� Mod�l�*2
* CD/DVD Reader/Writer Step Motor ve Ray D�zeni*2
* Frame (Solidworks tasar�m dosyas� mevcuttur ve 3 boyutlu yaz�c�dan ��kt� al�nabilir.)
* Step Down Buck D�n��t�r�c�(Min. 15v INPUT)

_**4)Fiziksel Kurulum:**_
* Sistem elemanlar� frame �zerine yerle�tirildikten sonra step motorlar�n 4 kablosu uygun s�rayla s�r�c�lere ba�lanmal�d�r. Test yap�l�rken eksenlerin ters �al��t��� g�r�l�rse bu 4 kablo s�k�l�p tam tersi �ekilde ba�lanmal�d�r. 
* �al��t�rma �ncesi �st eksen soldan, Taban eksen �st eksene uzak olarak konumland�r�lmal�d�r. 
* S�r�c�ler ve step motorlar 5v, lazer devresi ise 12v ile g��lendirilmelidir. 
* **Arduino, Step Motor S�r�c�leri ve Lazer S�r�c�s�**'n�n GND raylar� birbirine ba�lanmal�d�r. 
* Yaz�c�n�n sol y�z� kullan�c�ya bakacak �ekilde ��kt� al�nmal�d�r.

_**5)Sinyal Ba�lant�lar�:**_
* D8 Stepper Cut (Easydriver EN' pinine)
* D12 Laser Enable (Lazer s�r�c� TTL giri�ine)
---
Step  /   Dir
D2    /   D3           X-Taban
D4    /   D5           Y-�st

_**6)Yaz�l�m Kurulumu:**_
* Atmega328P kullan�lmal�d�r. Atmega168 �zerinde grbl �al��t�r�lamaz.
* **grbl-K13** i�erisindeki **grbl** klas�r� **Arduino IDE**'nin kurulu oldu�u konumda bulunan libraries klas�r�ne kopyalanmal�d�r. Daha sonra Arduino IDE a��larak �st sekmeden File>Examples>grbl>grblUpload kodu a��larak daha �nceden USB portuna ba�lanm�� Arduino Nano'ya y�klenmelidir.
* Baud Rate:115200 CariageReturn Ayarlar�yla **Tools** sekmesinin alt�ndaki **Serial Monitor** a��larak �u kod girilmelidir: **$RST=***
Test i�in s�ras�yla:
G91 G28 X0 Y0
X10 Y10
girilmelidir. Bu kod X ve Y eksenlerini 10'ar mm + y�n�nde hareket ettirecektir. E�er step motorlar tersi y�nde hareket etmeye �al���yorlarsa s�r�c�ye ba�land�klar� 4 kablo tam tersi �ekilde ba�lanmal�d�r.
* Bu projedeki donan�ma uygun olarak grbl �zerinde baz� ayarlamalar yap�lm��t�r. Proje yeniden yap�lacak ise; y�ksek do�ruluk ve hassasiyet i�in a�a��da verilen grbl linkinden yararlanarak steps/mm, mm/sec^2, max travel-mm, max rate vb. de�erleri deneysel veya �l��msel metodlarla bulunmal�d�r.

_**7)Kullan�m:**_
* Lazer CNC uygulamas� i�in haz�rlanm�� herhangi bir GCode, a�a��daki linklerden indirilebilecek **Universal Gcode Sender** kullan�larak 2 boyutlu lazer yaz�c�ya aktar�labilir.

_**8)Linkler:**_
* https://github.com/grbl/grbl
* https://github.com/grbl/grbl/wiki
* https://github.com/winder/Universal-G-Code-Sender