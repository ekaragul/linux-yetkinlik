# Linux Temel Yetkinlik Değerlendirme Testi

## Senaryo: Sistem Teşhis ve Raporlama Otomasyonu

Bu pratik yetkinlik testi; temel gezinti, dosya/dizin yönetimi, izinler, süreç yönetimi, filtreleme/yönlendirme, donanım/ağ analizi ve paket yönetimi becerilerinizi **tek bir akışta** ölçmek üzere tasarlanmıştır.

### 1. Genel Kurallar

* Tüm adımları **yalnızca terminal** üzerinden gerçekleştirin.

* Grafiksel arayüz (GUI) araçları kullanmayın.

* Komutları ezbere çalıştırmaktan ziyade çalışma mantıklarını anlamaya odaklanın.

### 2. Uygulama Adımları

#### Aşama 1: Ortam Hazırlığı ve Paket Yönetimi  *

1. Ev dizininize (`~`) geçiş yapın.

2. `sistem-testi` adında bir dizin oluşturun ve bu dizine girin.

3. Paket listelerini güncelleyin (`sudo apt update`).

4. Sistemde mevcut değilse `curl` paketini sisteme kurun (`sudo apt install curl`).

#### Aşama 2: Betik Geliştirme (`teshis.sh`)  *

Klasör içinde `nano` veya `vim` metin düzenleyicilerinden birini kullanarak `teshis.sh` adında bir Bash betiği oluşturun. Betik, çalıştığında tüm çıktıları tek bir `rapor.log` dosyasına yönlendirmelidir.

Betik içeriğinde bulunması gereken bilgiler:

* **Kullanıcı ve Konum:** Çalıştıran aktif kullanıcı adı (`whoami`) ve mutlak dizin yolu (`pwd`).

* **Sistem & Çekirdek:** Linux çekirdek sürümü (`uname -r`) ve sistem çalışma süresi (`uptime`).

* **Kaynak Tüketimi:** RAM bellek durumu (`free -h`) ve kök disk doluluk oranı (`df -h /`).

* **Ağ Bilgisi:** Aktif yerel IP adresi (`ip a` veya `hostname -I`).

* **Bağlantı Testi:** `google.com` adresine tek paketlik ping (`ping -c 1`) veya `curl -I` ile HTTP durum kodu kontrolü.

> **İpucu:** Dosyayı ilk açışta baştan yazmak için `>`, sonraki verileri dosyanın sonuna eklemek için `>>` operatörünü kullanın.

#### Aşama 3: İzinler ve Güvenlik (Permissions)  *

1. `teshis.sh` dosyasının mevcut izinlerini ve sahipliğini inceleyin (`ls -l`).

2. Dosya izinlerini **yalnızca sahibi okuyabilir, yazabilir ve çalıştırabilir** (`rwx------` / sayısal: `700`) olacak biçimde ayarlayın.

#### Aşama 4: Süreç Yönetimi ve Çalıştırma  *

1. Betiği arka planda (`&` operatörüyle) çalıştırın:

   ```
   ./teshis.sh &
   
   ```

2. Süreç çalışırken PID değerini yakalayın (`ps`, `pgrep` veya `jobs`).

3. Betik tamamlandığında çıkış kodunu kontrol ederek hatasız bittiğini (`0`) doğrulayın:

   ```
   echo $?
   
   ```

#### Aşama 5: Arama, Filtreleme ve Doğrulama *

1. Üretilen `rapor.log` dosyasının son 10 satırını görüntüleyin (`tail`).

2. `grep` kullanarak `rapor.log` içinden yalnızca RAM veya IP adresinin geçtiği satırı filtreleyin.

3. `/var/log` sistem dizininde adı `.log` ile biten dosyaları listeleyin (`find`).

4. Sistemdeki blok aygıtlarını ve bağlı disk bölümlerini listeleyin (`lsblk`).


### 3. Değerlendirme Kriterleri (Rubrik)

| Alan | Kriter | Puan | 
| ----- | ----- | ----- | 
| **Gezinme & Dosya İşlemleri** | Dizin oluşturma, geçiş yapma, mutlak/göreli yol kullanımı ve silme | 15 | 
| **Paket Yönetimi & Root** | `sudo` kullanımı, paket güncelleme ve kurulum adımları | 10 | 
| **Bash Betiği & Düzenleyici** | Metin düzenleyici ile betik yazma, yönlendirme (`>`, `>>`) | 20 | 
| **Dosya İzinleri** | Sayısal izin mantığını anlama (`chmod 700`) ve doğrulama | 15 | 
| **Süreç Yönetimi** | Arka plan çalıştırma (`&`), PID ve çıkış kodu (`$?`) kontrolü | 15 | 
| **Filtreleme & Arama** | `grep`, `tail`, `find` ve boru hattı kullanımı | 10 | 
| **Sistem/Ağ Analizi** | Çekirdek, disk, RAM ve ağ parametrelerini doğru komutlarla alma | 15 | 
| **Toplam** |  | **100** | 

### 4. İlgili Komutlar Özeti

```
Gezinme & Dosya : cd, pwd, mkdir, rm, ls -l
Düzenleme       : nano, vim, cat, echo
Yönlendirme     : >, >>, |
İzinler         : chmod, chown
Süreçler        : ps, pgrep, jobs, & , $?
Sistem/Donanım  : whoami, uname, uptime, free, df, lsblk
Ağ              : ip, ping, curl
Arama & Filtre  : grep, find, tail, head

```
