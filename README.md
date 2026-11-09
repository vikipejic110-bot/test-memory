# Rezerviši – ikonice apartmana i precrtane prethodne cijene

[Preuzmi datoteku za uvoz u Code Snippets](https://github.com/vikipejic110-bot/test-memory/raw/refs/heads/delivery/booking-icons-prices-20261110/Memory-Rezervisi-ikonice-cijene-Code-Snippets.json)

[Preuzmi kod za ručno lijepljenje](https://github.com/vikipejic110-bot/test-memory/raw/refs/heads/delivery/booking-icons-prices-20261110/memory-booking-room-details-snippet.txt)

[Preuzmi samostalan PHP](https://github.com/vikipejic110-bot/test-memory/raw/refs/heads/delivery/booking-icons-prices-20261110/memory-booking-room-details-snippet.php)

Samostalan PHP isječak za **Code Snippets**. Nije nadogradnja niti zamjena
plugina za uputstva gostima i Wellness.

## Uvoz

1. Preuzmite `Memory-Rezervisi-ikonice-cijene-Code-Snippets.json`.
2. U WordPressu otvorite **Snippets → Import / Uvoz** i izaberite JSON.
3. Uvezite isječak **Memory – ikonice apartmana i precrtane cijene u rezervacijama**.
4. Aktivirajte ga. Obuhvat je **front-end / samo javni dio sajta**.
5. Očistite postojeći keš stranice Rezerviši i provjerite desktop i mobilni prikaz.

Alternativno: sadržaj `memory-booking-room-details-snippet.txt` zalijepite u novi
PHP isječak, sačuvajte i aktivirajte. Ne aktivirajte i uvezeni i ručno zalijepljeni
primjerak. PHP datoteka sadrži isti kod uz početnu PHP oznaku.

## Izvor podataka i obuhvat

Potreban je postojeći aktivan dodatak **Memory – ikonice apartmana**
(`Memory_Apartment_Icons`), koji već sadrži podatke za pojedinačne apartmane.
Isječak čita njegov javni katalog i koristi njegov postojeći crtač ikonica.
Nema nove liste pogodnosti koju bi trebalo posebno održavati.

Na stranici `rezervisi` / WordPress stranici 1887 u izboru smještaja prikazuje
odrasle + djecu, površinu, krevete, sofu, kupatila i ostale stavke koje su uključene
za baš taj apartman. Kapacitet se prikazuje prvi, a ostale stavke zadržavaju
redoslijed iz urednika. Promjene podataka preuzimaju se prilikom otvaranja stranice
i osvježavanjem javnog kataloga pri povratku na karticu, najviše jednom u 30 sekundi.

Identitet povezuje po jedinstvenom nazivu/slug-u (npr. Blue Memory ↔ BUSINESS LUX
APT-BLUE) ili tačnom lokalnom linku. WordPress ID i WebBookingPro ID nisu isti i
ne izjednačavaju se. Neprepoznat ili dvosmislen naziv zadržava izvorni prikaz;
ne prikazuje podatke nasumično izabranog apartmana. Kapacitet prikazan u ikonicama
dolazi iz postojećeg urednika; ograničenja rezervisanja u WebBookingPro se ne mijenjaju.

Kod ponude sa oznakom popusta (npr. -10%) traži dvije već prikazane cijene iste
valute u istom cjenovnom stupcu i precrtava višu. Poredi i prikazani procenat,
uz toleranciju od dva procentna poena zbog zaokruživanja/naknada. Jednake cijene,
različite valute, dvije odvojene ponude i ponude bez oznake popusta ne precrtava.
Ako struktura nije dovoljno jasna, ostavlja je neizmijenjenu. Ne obračunava popust
ponovo, ne mijenja nijedan iznos i ne precrtava ukupne iznose u završnom koraku.

Promjene su ograničene na prikaz rezultata unutar `#wbproot`; isječak ne šalje
rezervacije, ne mijenja zahtjeve pretrage, ne upisuje podatke i ne pristupa
privatnim linkovima gostiju. Postojeći snippet-i za jezik, pretragu i popunjenost
ostaju aktivni. Ikonice zadržavaju zlatnu boju i prelamaju se na manjim ekranima.

## Provjere i ograničenje provjere na produkciji

PHP sintaksa je provjerena u PHP 8.4. Chromium provjere koriste izolovanu DOM
maketu zasnovanu na poznatim selektorima postojeće WebBookingPro integracije,
uz svih 11 naziva iz postojećeg dodatka. Obuhvaćeni su ispravan apartman i
kapacitet, promjena izvora, deaktivirane/neprepoznate/dvosmislene stavke,
popusti i redovne cijene, više ponuda, razne valute i formati, promjena DOM-a,
SR/EN pristupačni nazivi, neizmijenjeni unosi/iznosi/dugmad, završni korak i
mobilni prikaz. Nisu korišćeni lični podaci gostiju niti stvarne rezervacije.

Direktan pristup produkcijskom sajtu iz razvojnog okruženja trenutno je blokiran
mrežnim pravilima (CONNECT 403). Trenutni HTML sajta i povezivanje svakog stvarnog
WebBookingPro naziva zato nisu provjereni uživo. Vlasnik treba poslije aktiviranja
provjeriti reprezentativnu ponudu i nazive apartmana; ako je struktura promijenjena,
potreban je primjer HTML-a kartice za doradu selektora. Deaktiviranje isječka
uklanja njegove izmjene nakon ponovnog učitavanja stranice.

