# 5 Perces Doksik
A NetAcademia tudástár videóinak jegyzetei

## Fogalomtár

### Mi az a webes alkalmazás?
Képzeljük el a következőt: hasonlít ahhoz, amikor egy teremben sok ember van, és mindegyik képes a másikhoz beszélni. Célszerűen vagy kérdezni vagy kérni tőle valamit. A megszólított pedig udvarias és jól nevelt ember lévén, mindig válaszol is a megszólításra.

Ha annyi fogalmazásbeli kiegészítést megengedünk, hogy a kérdés is kérés, méghozzá információ kérés, akkor egyszerűsíthetjük a leírásunkat: sok szereplő, egymástól tudnak kérni, a kérés címzettje pedig válaszol.

Példának okáért az is lehet, hogy csak megkérdezzük tőle, hogy merre van a mosdó, és erre vagy azt válaszolja, hogy

- ő ugyan nem tudja, de ott megy egy fiatalember egyenruhában, kérdezzük meg tőle 
- vagy részletes leírást ad, hogy merre találjuk
- esetleg mondja, hogy mosdó az nincs,
- sőt, az is lehet, hogy ő a beléptetést végző biztonsági őr, és visszakérdezve elkéri tőlünk a jegyünket.

A lehetőségek száma innentől már csak a regényíró fantáziáján múlik.

Ugyanezt elmondva sokkal unalmasabban, a webes alkalmazás egy két szereplőből álló (kliens/szerver) alkalmazás, aminek a kliens (kérő vagy kérdező) oldala általában webes böngésző (client agent, de a továbbiakban *böngészőnek* nevezzük), a szerver pedig (a válaszoló oldal) a webes kiszolgáló. 

A beszélgetés során a **kliens** tehát kéréseket (HTTP request) küld a **szerver** felé, a **szerver** pedig válaszol (HTTP response). 

Minden HTTP beszélgetés ilyen kérés-válasz párokból áll. 

Egy nagyon fontos jellemzője van még ezeknek a beszélgetéseknek: a beszélgetés **állapotmentes**, azaz miután egy ilyen kérés/válasz lezajlik, a kettejük (hálózati) kapcsolata meg is szűnik. Ezt úgy kell elképzelni, mintha a kliens oldali kérő a választ megkapva előhúznű a [Man in Black Neuralyzerét](https://en.wikipedia.org/wiki/Neuralyze) és az [egész beszélgetést](https://www.youtube.com/watch?v=PnEWvBsRjBo) kiütné a választ megadó szerverből. 

> Ez a későbbiekben ad majd feladatot, hiszen képzeljük el, megkérdezzük a mosdót, majd a biztonsági őr kérésének eleget téve megmutatjuk a jegyünket. A biztonsági őrnek fogalma sincs róla, hogy miért mutattuk meg a jegyünket, hiszen (a memóriatörlésnek köszönhetően) most lát minket életében először. De menjünk tovább, miután megmutattuk a jegyünket és újra töröltük emlékeit, megkérdezzük újra a mosdót. Szintén úgy fog ránk nézni, mintha most pillantottuk volna meg egymást, és ismét kérni fogja a jegyünket. Ez jelzi, hogy a beszélgetési etikettünk korántsem lezárt könyv, kell bele még néhány fejezet.

#### A kérés elemei:

Képzeljük magunkat egy kicsit a sztoriba:
A kérésnek józan paraszti ésszel tartalmaznia kell (1) *egy igényt*, hogy mit is szeretnénk kérdezni vagy kérni.  Ki kell választanunk (2) *egy személyt* a teremből, akinek a kérdésünket feltesszük. Majd jöhetnek aztán a kérés jellemző adatai, attól függően, hogy mit kérünk vagy kérdezünk. Így a kérés három részből áll, kockanyelven a következőkből.

##### első sor

A kérés első sora áll (1) egy kérés típusból (*metódus*), (2) és egy Internetes címből (*erőforrás*). 

Mivel az örökéletre való vágy természetesen a HTTP protokoll létrehozóit is megkísértette, így időtlenségüket biztosítandó a kérésben szerepel még egy (3) verziószám is. Így ha ki kell egészíteni vagy akár meg kell változtatni a szabályokat, akkor a verziószámmal lehet jelezni, hogy a beszélgetés melyik protokoll szerint zajlik, de a kiötlőit nem fogja engedni a feledés homályába veszni.

Tehát egy kérés például a maga valóságában:

```
GET https://tools.ietf.org/html/rfc2616  HTTP/1.1
```
Ebben az esetben a **GET** a *metódus*, a **https://tools.ietf.org/html/rfc2616** az *Internetcím*, vagyis a szerver, akitől kérdezünk, a **HTTP/1.1** pedig a *verziószám*, ami a beszélgetésünk szabályait meghatározza. 

###### metódus: megmondja, hogy milyen jellegű művelet elvégzését kéri a kérésben a kliens a szervertől (például információ lekérdezése, adatok módosítása, új adat rögzítése, stb.) A metódusok a következők lehetnek:

    - HEAD
    - GET
    - POST
    - PUT
    - DELETE
    - TRACE
    - OPTIONS
    - CONNECT

##### fejlécek (headers)
Tetszőleges számú fejlécet küldhetünk a kérésben, ahol az egyes fejlécek **név: érték** alakban szerepelnek:
```

```
A fejléc a HTTP/1.0-ban bevezetett lehetőség, hogy a kéréshez a kliens, előre, a protokollban meghatározott módon képes legyen további paramétereket csatolni.

##### kérés tartalma (request body)
Ez vagy van vagy nincs, ha a kérésünkhöz tartozik elküldendő információ, akkor itt tudjuk például adatainkat elküldeni a szerverhez.

#### A válasz elemei:

##### Státusz sor
A válaszban jelzi a szerver, hogy (1) melyik verziót használja, rögtön az elején, és jelzi, hogy a kérés/kérdésre elvégzett feladat (2) milyen eredménnyel zárult (státusz). Ennek rögtön két formáját is visszaküldi, az első a státuszkód (status code), ami egy szám, a második pedig egy szöveges leírás, vagy indoklás (reason phrase), ami egy szöveges válasz. Pl:

```
HTTP/1.1 200 OK
```

##### Fejlécek (headers)
hasonlatosan a kéréshez

##### üzenet tartalma (response body)

### Mi az a böngésző?
A böngésző, vagy internetböngésző egy olyan alkalmazás, ami képes HTTP protokoll szerinti beszélgetésre tetszőleges, ezt a protokollt használó szerverrel. (Az ilyen szervereket hívjuk webszervernek.) Ezen túlmenően a böngésző a kapott válasz (HTML) dokumentumot meg is jeleníti.

### Mi az a cookie?
(HTTP cookie, vagy web cookie, Internet cookie, browser cookie, vagy egyszerűen csak cookie) 

Egy információ, amit a **szerver** küld a **felhasználó böngészőjébe**. A böngésző innentől kezdve eltárolhatja, és kérései mellé csatolhatja.

>Vagyis, ugyan töröljük a biztonsági őrünk emlékeit, de előtte kapunk tőle egy jelszót. Amikor ezt a jelszót bemondjuk, *folytatni* tudjuk a beszélgetést, nem minden alkalommal újrakezdeni.

Célja: A böngésző ezzel képessé válik kérések között fontos információk megjegyzésére, így segítségével az eredetileg állapotmentes (stateless) HTTP protokol is képessé válik egy beszélgetés során (munkamenet) a kéréseket túlélő állapotokat kezelni (stateful sessions).

### Mire használjuk a cookie-t?

Például használhatjuk 

- állapotok kezelésére (játék pontszám nyilvántartása, bejelentkezési adatok megjegyzése, bevásárló kosár tartalmának tárolása)

- megszemélyesítés (felhasználói igények, megjelenítési és egyéb beállítások megjegyzése)

- nyomonkövetés (a felhasználó viselkedésének rögzítése és elemzése)

### Hogy működik a cookie?

a [Set-Cookie](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie) HTTP válasz fejléc tartalmazza az adatcsomagot a szervertől a felhasználó böngészője felé.

A fejléc maga ilyesmi lehet, miután megmutattuk a jegyünket, hogy a beengedőember végre elmondja, hogy hol találom a mosdót:

```
Set-Cookie: vanjegye=igen
```

De ezt kiegészíthetjük még ilyenekkel is:
```
Set-Cookie: jelszo=szezamtarulj; Domain=ingyenpenz.org
Set-Cookie: kampanyneve=keresdapenzt; HttpOnly
```
vagyis egy cookie egy név/érték pár, amit még, ha a szerver akar, kiegészíthet utasításokkal (directives), és ebből lehet egy vagy több is egy válaszban. Az utasítások a böngészőnek szólnak.

Ha egy ilyen válasz érkezik, akkor a böngésző elmentheti ezt az információt, és a következő kérésben így küldheti vissza:

```
GET https://beengedoember.com/merretalalomamosdot HTTP/1.1
Cookie: vanjegye=igen; jelszo=szezamtarulj; kampanyneve=keresdapenzt
```

Egy kicsit hasonlít ahhoz, hogy átadom a jegyem, a beengedő lekezeli, majd visszakapom a lepecsételt jegyet. Amikor a mosdót kérdezem, akkor mellé felmutatom a kezelt jegyem, így immáron a biztonsági őr látja, hogy van jegyem, és megmondja, hogy hol találom a mosdót.

#### Mi ezzel a probléma?
Mivel a jegykezelés után neutralizáltuk a szerencsétlen biztonsági őrt, így simán megtehetjük, hogy összeállunk, és miután egyikünk a mosdót használta, a jegyet átadjuk egymásnak, és felmutatva a jegyet mindenki bejut a mosdóba.

Ja igen, ezt még nem árultam el, de fontos lehet, mi természetesen a biztonsági őrrel (szerver oldal) vagyunk egy csapatban, velünk együtt ő a jó fiú, tehát feladatunk a visszaélések lehetőségének a kiküszöbölése.

#### Miért van ez így?
Ha ez ilyen lyukas, akkor felmerül a kérdés, hogy miért ezt használjuk?

Amiről még nem beszéltünk, az a HTML. Ez az a nyelv, amin a weboldalakat írják. És az eredeti cél ilyen oldalak segítségével összekapcsolódó dokumentumhálózat létrehozása és közzé tétele.

Az egyszerű válasz tehát az, hogy a HTTP protokollt azért hozták létre, hogy a webes kiszolgálók HTML formátumú állományokat szolgáltassanak a kliensek felé. Ez a hiperlinkek nagy áttörése volt, először sikerül olyan rendszert létrehozni, ami igazán elterjedt, egymástól teljesen független, egymást nem is ismerő emberek és szervezetek mindenféle információt tudnak közzétenni, egymás dokumentációira hivatkozni. Szóval létrejött az Internet.

Azonban az igények életrehívták a *webes alkalmazásokat* is, ami ugyanezt az infrastruktúrát használja, de ahol már nem elég a weboldalak letöltögetése a böngészőben. 

Szükség van felhasználó azonosításra, jogosultságkezelésre, dinamikus oldalakra, és még sok minden másra. A vicc az, hogy ezt a HTTP eszközeivel fel lehet ugyan építeni, de a bevezető példánk jól mutatja, egyáltalán nem mindegy, hogy hogy tesszük ezt.

#### Megjegyzések
A HTTP alapvető alkotóelemei az üzenetek. A beszélgetés üzenet párokból áll: egy kérés üzenetre egy válasz üzenetet definiál. Arról nem beszél, hogy ezek az üzenetek milyen közvetítőn keresztül jutnak el a böngésző és a szerver között. Sőt, az esetek többségében több közvetítő is részt vesz a kommunkációban: routerek, proxy kiszolgálók és tűzfalak. Vagyis a közvetlen azonosítás azon a módon, hogy jól megnézik a szemben lévő eszközök egymást nem is lehetséges, mert eleve nem is látják egymást, csak az üzenetek léteznek.

A munkamenet és egyéb perzisztens adatok azonosíthatósága egyedül azon múlik, hogy a kliens birtokában van-e a kérdéses információnak. Ha már a birtokában van, akárhogy is került a birtokába, segítségükkel akkor is jogosultnak számít, ha lopta.

A beállított cookie-kat a böngésző automatikusan küldi, így ha a böngészőnkben betöltünk egy oldalt, akkor az hozzáfér a cookie-khoz, ami a böngészőnkben be van állítva, így ha elküld egy kérést a háttérben, akkor küldi vele a cookie-kat automatikusan.

#### Request Verification Token

__RequestVerificationToken input mező és ugyanilyen nevű cookie, amik egymáshoz tartoznak. Nem elég csak a cookie és nem elég csak az input mező, mindkettőnek jönnie kell a kérésben.

#### Támadás típusok
##### XSS
Nincs a felhasználó bejelentkezve

[Cheat Sheet](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet)

[XSS: Cross Site Scripting](https://www.youtube.com/watch?v=dMwxIHIabeg)

[Video](https://www.youtube.com/watch?v=cbmBDiR6WaY)


##### CSRF/XSRF
A felhasználó be van jelentkezve

[Cheat sheet](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)_Prevention_Cheat_Sheet)
[CSRF: Cross Site Request Forgery](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))

[Tesztelés](https://www.owasp.org/index.php/Testing_for_CSRF_(OTG-SESS-005))

[Troy Hunt Video](https://www.youtube.com/watch?v=hW2ONyxAySY)
[Troy Hunt cikk](https://www.troyhunt.com/owasp-top-10-for-net-developers-part-5/)
[FAQ](http://www.cgisecurity.com/csrf-faq.html#)

[Coding Horror](https://blog.codinghorror.com/preventing-csrf-and-xsrf-attacks/)
[Korábbi Coding Horror](https://blog.codinghorror.com/cross-site-request-forgeries-and-you/)

[video](https://www.youtube.com/watch?v=m0EHlfTgGUU)