B1 – Quadcopter
Deprem sonucunda enkazda arama-kurtarma çalışmalarına katılacak bir quadcopter geliştirilmesi,

Büyük makine veya insanların giremediği dar alanlarda arama-kurtarma çalışmalarının yapılması,

Bünyesindeki termal kamera, RGB kamera ve mikrofon gibi sensörlerle; yüksek manevra hakimiyeti ve havada asılı kalarak yüksek doğrulukta veri çekme kabiliyetlerinden faydalanılarak bu verilerin GCS'ye (Yer Kontrol İstasyonu) iletilmesi ve orada okunması sonucunda enkaz altında insan tespitinin yapılması.


B2 - 1. Otonom uçuş için GCS üzerinden belirlenen alanları tarayabilmesi:

Manuel uçuşa gerek kalmadan hiçbir noktanın atlanmadan araştırılması,

GCS üzerinde belirlenen alanların drone'a telemetri protokolüyle iletilmesi.

2. Termal görüntüleme yapabilmesi:

Vücut ısısıyla çevre sıcaklığı arasındaki farktan yararlanarak tespit etme,

Drone'un tespit ettiği anormal sıcak bölgelerin GCS'de bir harita haline getirilmesi ve tespitin kolaylaştırılması.

3. Mikrofonla ses tespit edebilmesi:

Termal kameranın ulaşamadığı alanlardan insan tarafından çıkarılabilecek seslerin tespiti,

Pervane sesi gibi insan sesini algılamayı zorlaştıracak seslerin filtrelenmesi ve bu konuda eğitilmiş yapay zekâların kullanılması.

4. RGB kamera ile görüntü alabilmesi:

Termal kamera ve mikrofondan gelen verilerin; hareket, insan uzvu veya silüeti gibi görüntülerle desteklenmesi veya yok sayılması,

Bu doğrultuda eğitilmiş yapay zekâ araçlarının kullanılması.

5. Tespit noktalarının verilerini GCS'ye iletebilmesi:

Termal kamera, RGB kamera ve mikrofon verilerinin yanında GPS verilerinin de GCS'ye iletilmesi,

Verilerin MAVLink protokolüyle telemetri radyosuna iletilip oradan radyo sinyallerine dönüştürülmesi, GCS'de tekrardan MAVLink'e dönüştürülerek anlamlı hale getirilmesi.

B3 - 
<img width="1199" height="1312" alt="İHA Görev Algoritması Akış Şeması" src="https://github.com/user-attachments/assets/b3b38fab-526c-4063-8f2d-e01c9b12766e" />



B4 - BAŞLA

görev = devam
taralı alan = 0
tüm alan = 100

görev = devam olduğu sürece

    eğer pil sağlığı < %20 veya GCS den sinyal gelmiyor veya GCS ye sinyal gitmiyor veya taralı alan = tüm alan ise
        görev = iptal
    değilse
        taralı alan = taralı alan + 1

        eğer termal kamera sensörü = evet ise
            5dk havada asılı kal
            mikrofonları çalıştır

            eğer mikrofon = evet ise
                aşağıya yaklaş
                rgb kamerayı çalıştır

                eğer rgb kamera = evet ise
                    tespit uyarısı ver
                    konum bilgilerini gönder
                eğer sonu

            eğer sonu

        eğer sonu
    eğer sonu

döngü sonu

eğer görev = iptal ise
    eğer taralı alan != 0 ise
        kalkış yapılan noktaya dön
        motorları durdur
    değilse
        motorları durdur
    eğer sonu
eğer sonu

BİTİR

B5 - 

<img width="1536" height="1024" alt="Drone Sistemi Veri Akış Şeması" src="https://github.com/user-attachments/assets/23ec8fca-bdc8-449f-b20b-ade5820b94f3" />


B6 - 1. Pervane sesinden kaynaklı akustik verilerin bastırılması:

Pervane sesini filtreleyecek algoritmalar kullanılması veya termal tespitler sonucunda drone'un o noktaya iniş yaparak pervanelerini durdurup salt dinleme moduna geçmesi.

2. Termal verilerin hayvan veya ortam sıcaklığına nazaran yüksek sıcaklıkta olan başka bir nesne yüzünden doğrulanamaması sonucu yanlış alarm oluşması:

Termal verilerin, mikrofon ve RGB kamera verileriyle desteklenmesi ve doğrulanması.

3. Enkaz diplerine inildikçe GPS sinyalinin kaybolması, yerdeki demir yığınları nedeniyle pusulaların çalışmaması ve drone'un konumunu belirleyememesinden ötürü savrulması:

Çift pusula kullanılması; saniyede onlarca fotoğraf çekerek drone'un belli bir yöne hızını tespit etmesini ve tersi yönde itki oluşturmasına yardımcı olan optik akış sensörü ile kızılötesi ışınlar göndererek drone'un yerden yüksekliğini ve etrafındaki cisimlerin mesafelerini ölçen LiDAR sensörü gibi ek önlemlerin alınması.

4. Yüksek sensör ve yapay zekâ kullanımı nedeniyle çekilen akımın artması ve batarya ömrünün kısalması sonucu sıklıkla batarya değiştirmek zorunda kalınması:

Yapay zekâ araçlarının çektiği akımı azaltan algoritmaların kullanılması ve batarya değişiminden önceki son görev koordinatlarının kaydedilerek batarya değişimi sonucu göreve kalınan yerden devam edilmesi.

5. Yoğun toz nedeniyle RGB kameraların istenen sonucu vermemesi:

Drone'a LED'ler yerleştirilerek aydınlatmanın sağlanması ve toz geçirmeyen lensler tercih edilmesi.


Kaynakça: ArduPilot Documentation, PX4 User Guide, MAVLink Developer Guide, ROS 2 Documentation ve OpenCV / Ultralytics YOLOv8 Documentation, Gemini, Chat GPT


