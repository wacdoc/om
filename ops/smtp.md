# Sarvarii ergaa erguu SMTP mataa keetii ijaari

## seensa

SMTP kallattiin tajaajiloota daldaltoota duumessaa irraa bitachuu danda'a, kanneen akka:

* [Amaazoon SES SMTP jedhamuun beekama](https://docs.aws.amazon.com/ses/latest/dg/send-email-smtp.html)
* [Ali duumessa email dhiibuu](https://www.alibabacloud.com/help/directmail/latest/three-mail-sending-methods)

Akkasumas sarvarii poostaa mataa keetii ijaaruu dandeessa - erguun daangaa hin qabne, baasii waliigalaa xiqqaa.

Armaan gaditti akkaataa mail server mataa keenyaa itti ijaarru tartiiba tartiiba agarsiifna.

## Filannoo sarvarii

Sarvariin SMTP ofumaan keessummeefame IP uummataa kan buufata 25, 456, fi 587 banaa ta'e barbaada.

Duumessi ummataa yeroo baay'ee itti fayyadamnu buufatawwan kana durtiidhaan ugguuraniiru, ajaja hojii kennuudhaan banuun ni danda'ama ta'a, garuu hundumaafuu baay'ee rakkisaadha.

Host kan ports kana banaa qabuu fi maqaa domeenii duubatti deebi'uu saaguu deeggaru irraa bitachuu nan gorsa.

Asitti, [Contabo](https://contabo.com) jedheen gorsa.

Contabo dhaabbata keessummeessituu kan teessoo isaa Jarmanii Muuniik godhate yoo ta'u, bara 2003 gatii baayyee dorgomaa ta'een hundeeffame.

Yoo akka maallaqa bittaatti Yuuroo filattan gatiin isaa salphaa ta'a (sarvariin mimoorii 8GB fi CPU 4 qabu waggaatti gara yuuwaan 529, kaffaltiin jalqabaa fe'uu waggaa tokkoof bilisa).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/UoAQkwY.webp)

Yeroo ajaja kennitu, remark `prefer AMD` , fi sarvariin AMD CPU qabu ga'umsa fooyya'aa qabaata.

Kan armaan gadii keessatti akkaataa mail server mataa keessanii itti ijaartan agarsiisuuf VPS Contabo akka fakkeenyaatti fudhadha.

## Qindaa'ina sirna Ubuntu

Sirni hojii asitti argamu Ubuntu 22.04 dha

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/smpIu1F.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/m7Mwjwr.webp)

Yoo sarvariin ssh irratti mul'ate `Welcome to TinyCore 13!` (akkuma fakkii armaan gadii irratti mul’atu), sirnichi hanga ammaatti hin fe’amne jechuudha. Mee ssh addaan kutatii daqiiqaa muraasa eegaa irra deebi'aa seenuuf.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/-qKACz9.webp)

Yeroo `Welcome to Ubuntu 22.04.1 LTS` mul'atu, jalqabni xumurama, tarkaanfiiwwan armaan gadii itti fufuu dandeessa.

### [Filannoo] Naannoo misoomaa jalqabsiisuu

Tarkaanfiin kun filannoodha.

Mijachuuf, fe'iinsaa fi qindeessaa sirna sooftiweerii ubuntu [github.com/wactax/ops.os/tree/main/ubuntu](https://github.com/wactax/ops.os/tree/main/ubuntu) keessa kaa'e.

Cuqaasuu tokkoon fe'uuf ajaja armaan gadii hojjedhu.

```
bash <(curl -s https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

Fayyadamtoonni Chaayinaa, maaloo bakka isaa ajaja armaan gadii fayyadamaa, afaan, naannoon sa'aatii fi kkf ofumaan ni saagama.

```
CN=1 bash <(curl -s https://ghproxy.com/https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

### Contabo IPV6 dandeessisa

IPV6 dandeessisi akka SMTP iimeelii teessoo IPV6 qabus erguu danda'uuf.

/fi `/etc/sysctl.conf` gulaali

Sararoota armaan gadii fooyyessi ykn itti dabali

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
net.ipv6.conf.lo.disable_ipv6 = 0
```

[Barnoota contabo hordofaa: Walitti hidhamiinsa IPv6 gara sarvarii keessanitti dabaluu](https://contabo.com/blog/adding-ipv6-connectivity-to-your-server/)

Gulaali `/etc/netplan/01-netcfg.yaml` , sararoota muraasa akka fakkii armaan gadii irratti mul'atutti dabali (Faayilii qindeessaa durtii Contabo VPS duraan sararoota kana qaba, yaada isaanii haquu qofa).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/5MEi41I.webp)

Sana booda `netplan apply` .

Erga qindeessaan milkaa'ee booda, teessoo ipv6 networkii alaa keetii ilaaluuf `curl 6.ipw.cn` fayyadamuu dandeessa.

## Kuusaa qindeessaa ops kloonii godhi

```
git clone https://github.com/wactax/ops.soft.git
```

## Maqaa domeenii keetiif ragaa SSL bilisaa uumi

Ergaa erguun icciitii fi mallattoodhaaf ragaa SSL barbaada.

Ragaa maddisiisuudhaaf [acme.sh](https://github.com/acmesh-official/acme.sh) fayyadamna.

acme.sh meeshaa mallattoo ragaa ofumaan madda banaa ta'eedha, .

Kuusaa qindeessaa ops.soft galchi, `./ssl.sh` hojjedhu, galmeen `conf` **galmee gubbaa** keessatti ni uuma.

Dhiyeessaa DNS kee [acme.sh dnsapi](https://github.com/acmesh-official/acme.sh/wiki/dnsapi) irraa barbaadi, `conf/conf.sh` gulaali.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Qjq1C1i.webp)

Sana booda `./ssl.sh 123.com` fiiguun maqaa domeenii keessaniif ragaalee `123.com` fi `*.123.com` maddisi.

Fiigichi jalqabaa ofumaan [acme.sh](https://github.com/acmesh-official/acme.sh) ni fe'a, hojii sagantaa qabame ofumaan haaromsuuf ni dabala. `crontab -l` arguu dandeessa, sararri akkasii akka armaan gadii jira.

```
52 0 * * * "/mnt/www/.acme.sh"/acme.sh --cron --home "/mnt/www/.acme.sh" > /dev/null
```

Daandiin ragaa uumameef waan akka `/mnt/www/.acme.sh/123.com_ecc。`

Haaromsi waraqaa ragaa iskiriiptii `conf/reload/123.com.sh` ni waama, iskiriiptii kana gulaali, ajajoota akka `nginx -s reload` dabaluun kuusaa waraqaa ragaa aplikeeshiniiwwan walqabatan haaromsuu dandeessa.

## Chasquid waliin SMTP server ijaari

[chasquid](https://github.com/albertito/chasquid) madda banaa SMTP server afaan Go tiin barreeffame dha.

Akka bakka bu'aa sagantaalee sarvarii poostaa durii kan akka Postfix fi Sendmail, chasquid salphaa fi itti fayyadamuuf salphaadha, akkasumas guddina sadarkaa lammaffaatiif salphaadha.

Run `./chasquid/init.sh 123.com` cuqaasuu tokkoon ofumaan ni fe'ama (123.com maqaa domeenii ergaa keetiin bakka buusi).

## DKIM Mallattoo Imeelii Qindeessi

DKIM xalayaaleen akka spam akka hin ilaalamneef mallattoo email erguuf kan gargaarudha.

Erga ajajni milkaa'inaan hojjetamee booda, galmee DKIM akka saagdu si gaafatama (akkuma armaan gadiitti agarsiifame).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/LJWGsmI.webp)

Galmee TXT DNS keessanitti dabaluu qofa (akkuma armaan gaditti mul'atu).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/0szKWqV.webp)

## Haala tajaajilaa & galmeewwan ilaali

 `systemctl status chasquid` Haala tajaajilaa ilaali.

Haalli hojii idilee akka fakkii armaan gadii irratti mul’atutti

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/CAwyY4E.webp)

 `grep chasquid /var/log/syslog` ykn `journalctl -xeu chasquid` galmee dogongoraa ilaaluu danda'a.

## Qindaa'ina maqaa domeenii duubatti deebisuu

Maqaan domeenii duubatti deebi'aa teessoo IP gara maqaa domeenii walgitutti akka furmaata argatu hayyamuudha.

Maqaa domeenii duubatti deebi'aa saaguun iimeelii akka spam adda baafamuu dhorkuu danda'a.

Yeroo ergaan fudhatamu, sarvariin fudhatu teessoo IP sarvarii erguu irratti xiinxala maqaa domeenii duubatti deebi'uu raawwata, sarvariin erguu maqaa domeenii duubatti deebi'aa sirrii qabaachuu isaa mirkaneessuuf.

Yoo sarvariin erguu maqaa domeenii duubatti deebi'aa hin qabne ykn maqaan domeenii duubatti deebi'aa teessoo IP sarvarii erguu wajjin wal hin simne, sarvariin fudhatu iimeelii akka spam beekuu ykn diduu danda'a.

[https://my.contabo.com/rdns](https://my.contabo.com/rdns) daawwachuun akka armaan gadiitti qindeessaa

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/IIPdBk_.webp)

Erga maqaa domeenii duubatti deebi'aa saagdee booda, furmaata fuulduraa maqaa domeenii ipv4 fi ipv6 gara sarvariitti qindeessuu yaadadhu.

## Maqaa keessummeessituu chasquid.conf gulaali

`conf/chasquid/chasquid.conf` gara gatii maqaa domeenii duubatti deebi'uutti fooyyessi.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/6Fw4SQi.webp)

Sana booda tajaajila deebisee jalqabuuf `systemctl restart chasquid` hojjedhu.

## Duubdeebii conf gara kuusaa git

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Fier9uv.webp)

Fakkeenyaaf, galmee conf gara adeemsa github mataa kootti akka armaan gadiitti backup godha

Dursa mana kuusaa dhuunfaa uumuu

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ZSCT1t1.webp)

Galmee conf galchiiti gara mana kuusaatti galchi

```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin git@github.com:wac-tax-key/conf.git
git push -u origin main
```

## Ergaa itti dabali

fiiguu

```
chasquid-util user-add i@wac.tax
```

Ergaa dabaluu danda'a

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/khHjLof.webp)

### Jechi icciitii sirritti saagamuu isaa mirkaneessi

```
chasquid-util authenticate i@wac.tax --password=xxxxxxx
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/e92JHXq.webp)

Fayyadamaa erga dabaltanii booda `chasquid/domains/wac.tax/users` ni update ta'a, gara mana kuusaatti galchuu hin dagatinaa.

## DNS galmee SPF dabaluu

SPF ( Sender Policy Framework ) teknooloojii mirkaneessuu email yoo ta'u, hanna email ittisuuf gargaarudha.

Teessoon IP ergaa sanaa galmee DNS maqaa domeenii inni jedhu waliin walsimuu isaa mirkaneessuun eenyummaa nama ergaa erge mirkaneessa, kunis gowwoomsitoonni iimeelii sobaa akka hin ergine taasisa.

Galmee SPF dabaluudhaan hanga danda'ametti iimeelonni akka spam ta'anii akka hin adda baafamne dhorkuu danda'a.

Yoo sarvariin maqaa domeenii kee gosa SPF hin deeggarre, galmee gosa TXT qofa dabali.

Fakkeenyaaf SPF `wac.tax` akka armaan gadiitti argama

`v=spf1 a mx include:_spf.wac.tax include:_spf.google.com ~all`

SPF `_spf.wac.tax`

`v=spf1 a:smtp.wac.tax ~all`

Hubadhaa ani asitti `include:_spf.google.com` qaba, kunis `i@wac.tax` akka teessoo ergaa booda saanduqa ergaa Google keessatti waanan qindeessuuf.

## Qindaa'ina DNS DMARC

DMARC gabaabduu (Mirkaneessuu Ergaa Domeenii irratti hundaa'e, Gabaasa fi Walsimsiisaa) ti.

Innis SPF bounces qabachuuf fayyadama (tarii dogongora qindeessaa irraa kan ka'e, ykn namni biraa si fakkeessee spam erguuf).

Galmee TXT itti dabali `_dmarc` , .

Qabiyyeen isaa akka armaan gadiiti

```
v=DMARC1; p=quarantine; fo=1; ruf=mailto:ruf@wac.tax; rua=mailto:rua@wac.tax
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/k44P7O3.webp)

Hiikni tokkoon tokkoon paarameetira akka armaan gadiitti argama

### p (Imaammata) .

Akkaataa iimeelota mirkaneessuu SPF (Sender Policy Framework) ykn DKIM (DomainKeys Identified Mail) hin dandeenye itti qabamu agarsiisa. Paarameetariin p gatiiwwan sadii keessaa tokkotti saaguun ni danda'ama:

* tokkollee hin jiru: Tarkaanfiin hin fudhatamu, bu'aan mirkaneessuu qofatu karaa mala gabaasa iimeelii erguuf deebi'a.
* Adda baafamuu: Ergaa mirkaneessa hin dabarsin galmee spam keessa kaa'i, garuu kallattiin ergaa hin didu.
* reject: Imeelii mirkaneessuu hin dandeenye kallattiin diduu.

### fo (Filannoo Kufaatii) .

Hamma odeeffannoo mala gabaasaatiin deebi'u ifteessa. Gatii armaan gadii keessaa tokkotti saaguun ni danda'ama:

* 0: Bu'aa mirkaneessuu ergaawwan hundaaf gabaasuu
* 1: Ergaawwan mirkaneessuu dadhaban qofa gabaasuu
* d: Kufaatii mirkaneessa maqaa domeenii qofa gabaasuu
* s: kufaatii mirkaneessa SPF qofa gabaasuu
* l: Kufaatii mirkaneessa DKIM qofa gabaasuu

### rua & ruf jedhamuun beekama

* rua (URI gabaasa Walitti qabameef gabaasuu): Teessoo iimeelii gabaasa walitti qabame fudhachuuf
* ruf (URI gabaasa Fooreensikii gabaasuu): teessoo imeelii gabaasa bal’aa argachuuf

## Galmeewwan MX dabaluudhaan email gara Google Mail tti dabarsuu

Sanduuqa ergaa dhaabbataa bilisaa kan teessoo waliigalaa deeggaru argachuu waanan hin dandeenyeef (Catch-All, iimeelii kamiyyuu gara maqaa domeenii kanaatti ergamu argachuu danda'a, durtii irratti daangaa malee), iimeelii hunda gara saanduqa ergaa Gmail kootti dabarsuudhaaf chasquid fayyadame.

**Yoo saanduqa poostaa daldalaa kaffaltii qabu mataa keetii qabaatte, maaloo MX hin fooyyessin tarkaanfii kana darbi.**

Gulaali `conf/chasquid/domains/wac.tax/aliases` , saanduqa ergaa dabarsuu saagi

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/OBDl2gw.webp)

`*` email hunda agarsiisa, `i` durtii teessoo email fayyadamaa erguu armaan olitti uumame dha. Ergaa dabarsuudhaaf, tokkoon tokkoon fayyadamaa sarara dabaluu qaba.

Sana booda galmee MX itti dabali (akkuma sarara jalqabaa fakkii armaan gadii irratti mul'atutti kallattiin teessoo maqaa domeenii duubatti deebi'aa asitti akeeka).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/7__KrU8.webp)

Erga qindeessaan xumuramee booda teessoo email biroo fayyadamuun email gara `i@wac.tax` fi `any123@wac.tax` erguun email Gmail keessatti argachuu dandeessu ilaaluu dandeessu.

Yoo hin taane, galmee chasquid ( `grep chasquid /var/log/syslog` ) ilaali.

## Google Mail tiin i@wac.tax irratti email ergaa

Google Mail erga poostaa sana argatee booda, uumamaan i.wac.tax@gmail.com osoo hin taane `i@wac.tax` jedhee deebii akkan kennu abdadhe.

[https://mail.google.com/mail/u/1/#settings/accounts](https://mail.google.com/mail/u/1/#settings/accounts) daawwachuun "Add another email address" jedhu cuqaasaa.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/PAvyE3C.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/_OgLsPT.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/XIUf6Dc.webp)

Sana booda, koodii mirkaneessaa email gara itti dabarfamee dhufe galchi.

Dhumarratti, akka teessoo ergaa durtiitti saaguu ni danda'ama (filannoo teessoo walfakkaatuun deebii kennuu wajjin).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/a95dO60.webp)

Haala kanaan hundeeffama SMTP mail server xumurree yeroo walfakkaatutti Google Mail fayyadamuun email erguu fi fudhachuu dandeenya.

## Qindaa'inni milkaa'uu fi dhiisuu isaa ilaaluuf iimeelii qormaataa ergi

`ops/chasquid` galchaa

Fiigi `direnv allow` (direnv adeemsa jalqabbii furtuu tokkoo duraanii keessatti fe'amee jira fi hookiin sheelii irratti dabalameera)

achiis fiigi

```
user=i@wac.tax pass=xxxx to=iuser.link@gmail.com ./sendmail.coffee
```

Hiikni paaraameetotaa akka armaan gadiitti argama

* fayyadamaa: Maqaa fayyadamaa SMTP
* dabarsuu: Jecha icciitii SMTP
* gara: fudhataa

Imeelii qormaataa erguu dandeessu.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ae1iWyM.webp)

Qindaa'inoota milkaa'uu fi dhiisuu isaanii ilaaluuf iimeelii qorannoo fudhachuuf Gmail fayyadamuun ni gorfama.

### Icciitii istaandaardii TLS

Akkuma fakkii armaan gadii irratti mul'atutti, qulfiin xiqqaan kun jira, kana jechuun ragaan SSL milkaa'inaan dandeessifameera.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/SrdbAwh.webp)

Sana booda "Show Original Email" jedhu cuqaasaa.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/qQQsdxg.webp)

### DKIM

Akkuma fakkii armaan gadii irratti mul'atutti, fuul-barruun ergaa jalqabaa Gmail DKIM agarsiisa, kana jechuun qindeessaan DKIM milkaa'eera jechuudha.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/an6aXK6.webp)

Mata duree iimeelii jalqabaa keessatti Fudhatame ilaali, teessoo ergaa IPV6 ta'uu isaa arguu dandeessa, kana jechuun IPV6nis milkaa'inaan qindaa'eera.
