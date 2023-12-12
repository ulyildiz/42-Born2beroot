# Virtualization (Sanallaştırma)
Fiziksel bir donanımda ayrık ortam(sanal makine) oluşturulmasıdır. Oluşan sanal makinelerin birbiri ile bağı olmaz(biz sağlamadıkça!). Bu sanal makinelerde kurulacak herhangi bir uygulama direkt olarak donanım kullanmak yerine bir yazılım kullanır(yazılım üzerinden donanıma erişir.). Virtualization bir donanımda birbirinden bağımsız ortamlar ile bağımsız OS(Operating System)ler çalıştırmaya fırsat verdiği için esneklik, kaynak kontrolü gibi yararlar sağlar. 

## Hypervisor (Hiper Yönetici)
Sanallaştırmanın temelini oluşturan bir donanım yazılımıdır. Sanal makieneler hypervisorler üzerinden oluştup kontrol ederiz. 2 tip hypervisor vardır.

### Type 1 (Tip 1)
Bare-Metal Hypervizor olarak da adlandırılan bu tip doğudan fiziksel donanım üzerinde çalışan ve sanal makineleri yöneten bir katman sunar. VMware ESXi, Microsoft Hyper-V Server, Proxmox örnek verilebilir.

Direkt donanıma bağlandığından daha yüksek bir ***performans*** sunarlar.

Daha düşük seviyede kontrol yapılması, yüksek performans ve doğrudan donanıma erişimi sayesinde etkin şekilde sanal makinelerin yönetilmesi makineler arasında ***sıkı bir izolasyon*** sağlar.

### Type 2 (Tip 2)
Hosted Hypervisor olarak da adlandırılan
bu tip ise bir OS üzerinden sanal makineleri oluşturup yöneten bir katmandır.

Bir OS katmanı aracılığı ile çalıştığından type 1'e kıyasla ***daha düşük performans*** sunar.

Direkt donanımı kontrol edemediğinden, performans kaybı olduğundan ve bir host OS üzerindeki başka programla etkileşime girebileceğinden ***izolasyon seviyesini biraz daha azaltabilir***.

## Virtual Machine (Sanal Makine)
Hypervisorler aracılığı ile oluşturduğumuz şey sanal makinelerdir. Başka bir benzetmeyle fiziksel bilgisayarın emüle edilmesidir. Her VM kendi OS'e sahip olabilir. Aynı anda biri Windows biri Linux olcak şekilde 2 VM çalışabilir ve bir sanal makinenin içinde olan hata durumu diğerini etkilemez.

## VM'in Yararları
Sanal makineler host OSden bağımsız olmaları veya birbirinden bağımsız olmaları gibi nedenlerden dolayı stabilliğinden veyahut güvenilirliğinden emin olmadığımız bir uygulamayı denemek için güvenli ortam sağlar.

Tek bir fiziksel donanımı gerekli kaynak kullanımlarına göre birden fazla sisteme parçalayarak pozitif bir kaynak tasarrufu sağlar.

*Örn.: Birbiri ile çakışabilecek sistematik programları farklı VMlere koyarak izolasyon sağlanılabilir*

# Disk Yönetimi
## File System (Dosya Sistemleri)
Veri tutan her fiziksel ortam (ör: sabit disk), bilgi saklayan/tutan küçük birimlerin sıralanmasından, yani “bloklardan” oluşur. Her dosya sistemi ise bu blokları farklı biçimde yönetir. Dosya sistemi temelde bir dosyanın disk üzerinde nasıl saklandığını bilgisayarın dosyaları nasıl yöneteceğini ve erişeceğini kontrol eden sistemdir. RAM dışındaki ki belleklerin yönetimi dosya sistemi tarafından ele alınır.

Dosya sisteminin görevleri üç maddede özetlenebilir:
- Mantıksal dosya yapılarından fiziksel yapılara geçişin sağlanması.
- İkincil belleklerin verimli kullanılmasını sağlanması.
- Dosyaların paylaşılması, korunması ve kurtarılması ile ilgili araçların sağlanması.

## Partition & Volume (Bölüm & Birim)
Bölüm (Partition) ve birim (volume), bir fiziksel diski veya depolama birimini mantıksal olarak bölümlere ayırmak için kullanılan terimlerdir.

Bölüm, bir fiziksel diski veya depolama birimini mantıksal olarak ayıran bir alan veya alan kümesidir. Her bölüm farklı bir işletim sistemi veya dosya sistemini içerebilir.

Birim, bir bölümün veya birden çok bölümün bir araya getirilmesiyle oluşturulan bir depolama alanıdır. Bir birim, bir fiziksel diskin veya depolama biriminin tamamına veya bir kısmına genişletilebilir.

Bölüm ve birim arasındaki temel fark, bölümün bir fiziksel diski veya depolama birimini mantıksal olarak ayırırken, birim bir bölümün veya birden çok bölümün bir araya getirilmesiyle oluşturulmasıdır.

Bölümler genellikle aşağıdaki amaçlar için kullanılır:
- Farklı işletim sistemlerini veya dosya sistemlerini desteklemek için
- Farklı kullanıcılara veya uygulamalara farklı depolama alanları sağlamak için
- Verileri korumak için

Birimler genellikle aşağıdaki amaçlar için kullanılır:
- Bir fiziksel diskin veya depolama biriminin tamamını veya bir kısmını yönetmek için
- Bir işletim sisteminin veya uygulamanın düzgün çalışması için gerekli depolama alanını sağlamak için

Örneğin, bir fiziksel diski iki bölüme ayırabiliriz. Bir bölümde Windows işletim sistemi ve diğer bölümde Linux işletim sistemi kurabiliriz. Bu durumda, her işletim sistemi kendi bölümüne sahip olacaktır. Alternatif olarak, iki bölümü tek bir birimde birleştirebiliriz. Bu durumda, iki işletim sistemi aynı depolama alanını paylaşacaktır.

## Boot (Önyükleyici)
Boot bilgisayar başlatma işlemidir. Bilgisayar başlatıldığında 2 aşamalı bir boot işlemi gerçekleşir. Güç kaynağı çalıştırıldığında JUMP(!), POST(Power-On-Self-Test) talimatları gerçekleşir. Donanım testi başarı ile sonuçlandığında ilk önyükleme aşaması olan bios başlatılır. Bios, başlangıç aygıtını belirler ve bölüm tablosunu RAM'e yükler. Bu aşamadan sonra Bootloader(2. aşama) varsa yükler, gerekli bilgileri ve yetkileri ona verir. Bootloader(Örn.: GNU GRUB) İşletim sistemini yükler ve başlatır.

Bootloader için ayrı bir primary partitions açılmasının sebepleri MBR bölüm tablosuna dayanır. MBR sadece primary partitionsdan önyükleme yapabilmesidir.

## Mount Point
Mount point, diskte ayrılmış yapının hiyerarşisindeki en üst noktayı belirler. Tek partition ve bir diski düşünürsek root(/) mount pointi olmak zorundadır ya da primary partitiona mount point olarak /boot belirlediğimizde kök dizin altındaki boot klasörü bu partition için en üst dosyayı oluşturur(O parçanın kök dizini haline gelir.). (**bu yerler linklimi kontrol et**)

## Root (Kök dizin)
Dosya sistemindeki hiyerarşide en üst dizindir. Bütün klasörler ve dosyalar bu dizin altında bulunur, başlangç noktası oluşturur.

Root, home veya tmp gibi kısımları ayrı nölümlere ya da birimlere bölmenin nedenlerine:
- Bu tür yerlerde güvenlik için farklı izinleri açık bırakmak,
- Sistemsel sorunlarda home'un ayrı bir bölüm olması sayesinde veri koruması,
- tmp dizinindeki geçici dosyaların fazlalaşması ile oluşabilecek yer sıkıntısı nedeniyle sistem performansının aksamaya uğramasını engellemek,
gibi durumlar gösterilebilir.

# Debian - Rocky
|   Debian  |   Rocky   |
|-----------|-----------|
|Debian, tamamen özgür yazılım ilkelerini benimser ve bu ilkeler doğrultusunda özgür yazılım topluluğuna odaklanır.|Rocky Linux, RHEL (Red Hat Enterprise Linux) uyumluluğu odaklıdır ve RHEL'in sunduğu özelliklere benzer bir deneyim sunmayı amaçlar.|
|Debian, Debian Paket Yönetim Sistemi (APT) üzerine kurulmuştur ve bu sistem, paketlerin kurulumu ve güncellenmesi için kullanılır.|Yum (Yellowdog Updater, Modified) paket yönetim sistemini kullanır. Bu, CentOS ve RHEL toplulukları için aşina oldukları bir paket yönetim sistemidir.|
|Debian, geniş bir topluluk ve geliştirici kitlesine sahiptir ve Debian tabanlı birçok popüler dağıtım mevcuttur (örneğin, Ubuntu)|Rocky Linux, topluluk destekli bir projedir ve CentOS topluluğu tarafından desteklenmektedir.|
|Sabit bir odağı olmamakla beraber bir çok durum için kullanılabilir yapıları vardır.|Özellikle kurumsal ortamlar ve sunucular için tasarlanmıştır ve bu nedenle güvenilirlik ve performans odaklıdır|

## Rocky
### SELinux
### DNF

## Debian
### Aptitude - Apt
|  	Apt	|   Aptitude    |
|-------|---------------|
|Daha basittir ve doğrudan terminalden kullanılır.|Daha gelişmiştir ve ekstradan interaktif bir arayüz sunar.|
|Güncelleme, yükleme, silme vb. temel işlemleri yapar.|Öneride bulunma, paketleri izleme vb. gibi gelişmiş işlemleri sunar.|
|||

### AppArmor
AppArmor Linux dağıtımlarında yer alan bir güvenlik uygulamasıdır. Diğer uygulamaların sisteme erişimini ve izinlerini kontrol eder gerektiğinde de kısıtlayabilir.

Profil-Tabanlı Güvenlik(PBS), Zorunlu Erişim Kontrolü(MAC), uygulama izolasyonu ve günlük tutma gibi işlevleri vardır. (**PBS bak**)

# Sudo & Superuser
**Superuser**(Administrator, root user) OSin bütün dosyalarını okuma, yazma ve çalıştırma yetkisine sahiptir. Terminal komutlarının işlevini değiştirebilir veya sistem dosyalarını silebilir.

**Sudo**(superuser do) aslında superuser yetkisini bir komuta atanmasıdır. Sudo komutunun hangi komutlar veya komut grupları ile çalıştığı ve kimlerin kullanabileceği gibi değişiklikler /etc/sudoers dosyasında görülebilir ve değiştirilebilir.

Sudo belirli kullanıcalara verilebilir ve sudoers dosyasından güvenlik politikaları değiştirilebilir. İzleme ve günlük tutma imkanı sunar. Bu şekilde daha düzgün bir güvenlik sunar.

# Firewall (Güvenlik Duvarı)
Belirli kurallar çerçevesinde ağa gelen ve ağdan giden verileri kontrol eden bir güvenlik sistemidir. Veriyi her daim bazı filtrelerden kontrollerden geçirir(Farklı türleri farklı çalışma prensiblerine sahip.).

## UFW (Uncomplicated Firewall)
IPv4 ve IPv6 desteğine sahip olmakla beraber portlara veya servislere, belirli IP adreslerine ve Ağlara izin vermek işlemleri için kullanılan bir güvenlik duvarıdır.

Varsayılan bir politika ile gelmektedir. Bu politikayı değiştirmek mümkündür. "/etc/ufw/" dizininden detaylı konfigürasyonlar yapılabilir .

## Firewalld

## Port
Port, ağda kurulan bağlantının başladığı ve bittiği noktalar olarak düşünülebilir. Portlar sayesinde tek bir bağlantı üzerinden birden fazla hizmete veya servise veriler karışmadan gönderilebilir. 

Port bağlantıları bazı protokoller kullanabilir:
- **TCP**, bağlantının sağlanıp sağlanmadığını ve verilerin gönderilip gönderilmediğini kontrol eder.(!)
- **UDP**, bağlantı kontrolü veya veri kontrolü yoktur.(!)

# SSH (Secure Shell)
SSH bir ağ protokolüdür. 2 makine arasında bir kimlik doğrulama yapar ve gönderilen veriyi şifreleyerek gönderir. (**port oluşuyor mu bak**)

# Cron
Belirli zaman aralığında veya belirli zaman diliminde tekrarlanan görevleri yapma imkanı tanıyan yazılımdır. Bu görev(cron job) bir komut veya bir script olabilir. Cron bir daemondır(daemon -> kullanıcı kontrolünde çalışmayan, arkaplanda çalışan hizmet veren process).

Varsayılan cron dosyası /etc/crontab'dir. Kullanıcılar kendi crontab dosyasını ayarlayabilir(!).
