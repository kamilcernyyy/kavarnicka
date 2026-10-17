# Kavárna Paulus — web (kavarnapaulus.cz)

Všechny soubory jsou v **jedné složce bez podsložek** — nic se při nahrávání nerozháže.

## Nasazení
**Wedos (ostrý web):** přes FTP nahraj *celý obsah* složky do `www/` — včetně skrytého `.htaccess`.
Až bude na kavarnapaulus.cz aktivní SSL, odkomentuj v `.htaccess` přesměrování na HTTPS.

**Vercel (jen testování):** nahraj stejný obsah do repa. Díky `.vercelignore` se tam PHP soubory
(editor, rezervace) nenahrají — formulář na Vercelu proto nabídne odeslání e-mailem. Vše ostatní funguje.

## Úprava textů — `kavarnapaulus.cz/admin.php`
- Heslo jsem předal v chatu; v souborech je uložen jen jeho otisk. **Po prvním přihlášení ho změň** (dole v editoru).
- Upravit jde: fotky, texty všech sekcí, kontakt, otevírací doba (dny + časy), menu, vybavení (karty s ikonkami), akce, časté dotazy,
  odkazy na Instagram/Facebook, SEO popisky a ID Google Analytics.
- Po uložení se web znovu vygeneruje jako statické HTML — zůstává stejně rychlý.
- Otevírací doba se změní najednou na webu, ve strukturovaných datech pro Google i v odpovědi v dotazech
  (do odpovědi stačí napsat `{otevreno}`).
- Před každým uložením se udělá záloha (`content-zaloha-*.json`, posledních 5). Interní soubory nejsou z webu dostupné.

## Zvýraznění v nadpisech
V editoru stačí slovo obalit: `*slovo*` = oranžově, `_slovo_` = tyrkysově (např. „Co u nás *dostanete*“).

## Rezervace
Formulář posílá e-mail na adresu kavárny z editoru (odpověď jde rovnou hostovi) a host hned dostane
automatické potvrzení „rezervaci jsme přijali“ se shrnutím — jeho úvodní text jde změnit v editoru.
Ochrana: past na roboty, minimální doba vyplnění, limit 5 rezervací/hod. z jedné adresy, kontrola všech polí.
**Po nasazení pošli zkušební rezervaci.** Kdyby nedorazila, na Wedosu založ schránku `rezervace@kavarnapaulus.cz`
(odesílatel musí být z vaší domény).

## Google Analytics
V editoru vlož měřicí ID (`G-…`). Teprve pak se objeví lišta cookies; bez souhlasu se nic neměří.
Odkaz „Nastavení cookies“ v patičce umožní souhlas změnit.

## Doplnit před spuštěním
- adresa a telefon (editor → Kontakt), odkazy na Instagram a Facebook
- `soukromi.html` → správce údajů (název/jméno, IČO, sídlo) — v souboru `soukromi.tpl.html`, řádek „Správce“
- fotky: v editoru sekce **Fotky** (galerie 3×, vchod, Instagram 6×). Stačí vybrat fotku z mobilu — editor ji
  zmenší, ořízne na správný poměr, opraví otočení a uloží v 4–6 velikostech (WebP, a AVIF pokud ho server umí).

## Logo
Na webu je zatím **dočasné logo** („Paulus“ + oblouk „KAVÁRNA“). Je v ikonách, náhledu pro sdílení i ve strukturovaných datech.
Až dorazí finální logo (ideálně SVG), vymění se na všech místech najednou.

## Animace
- Hlavička: na mobilu i na počítači stejné video s rukama a šálky, nahoře běžící oranžový text, dole tlačítka Menu a Kde jsme.
  Na počítači je video velké uprostřed a jeho okraje se ztrácejí do pozadí — to je zapečené přímo ve videu a obrázku
  (`hero-d-*`), protože CSS maska stála na počítači ~0,7 s výpočtu. Výroba: work/hd/mask.png + ffmpeg (viz work/hd).
- Druhá obrazovka („Pár kroků od baziliky“, #kde): kreslený pohled na Svatý Kopeček. Na počítači přes celou obrazovku
  s kartou na trávníku, na mobilu výřez kolem baziliky s kartou pod obrázkem. Texty karty jsou v administraci.
  Z obrázku jsou vystřižené stromy, mraky a auto: stromy se kývají ve větru, mraky plují, auto občas odjede.
  Po cestičkách chodí lidé, ze střechy baziliky občas vzlétnou holubi, v nádvoří stříká kašna, oblohou přeletí ptáci.
  Obrázek se stáhne až ve chvíli, kdy návštěvník začne stránkou posouvat (AVIF/WebP ve 3 velikostech).
  Úprava výřezů: tools/hero_pano.py (souřadnice v pixelech obrázku), pak build.py.
- Pořadí sekcí: hlavička (Dobrá káva pod svatým dohledem) → Konec cesty do kopce (panorama) → Méně spěchu, víc kofeinu →
  Co u nás dostanete → Stálice na baru (menu) → Fotky → Vyhlídka, terasa a klid od města (ikonky) → Kam na Kopečku (mapa) →
  Kousek Kopečku s sebou → Instagram → Kudy k nám → FAQ → Držet vám stůl? (rezervace) → patička Zastavte se na kopci.
- Menu „Stálice na baru“: jedna velká karta s obálkou „Menu“. Tlačítko Nahlédni ho otevře jako knížku, tlačítka sekcí
  (Káva, Nealko, Pečivo, Zákusky, Slané) listují rovnou na danou stránku, šipky a na mobilu i přejetí prstem listují po stránkách.
  Na počítači dvoustrana s obsahem, na mobilu jedna stránka. Sekce a položky (název, cena, poznámka) jsou v administraci;
  každá sekce = jedna stránka. Bez JavaScriptu se menu ukáže jako karty pod sebou. Pro Google je menu i ve strukturovaných datech.
- Přechody kolem panoramatu jsou plynulé: spodek hlavičky se rozplyne do barvy oblohy a spodek panoramatu do stránky.
  Knížka se výškou přizpůsobí obrazovce; delší sekce, které se na stránku nevejdou, automaticky pokračují na další stránce
  („Káva pokračování“) a obsah i čísla stránek se dopočítají. Telefon na šířku má dvoustranu; tlačítka sekcí stránku posunou jen tak, aby byla vidět celá.
- Texty webu jsou v novém tónu (kopecký nadhled, lehký humor, fakta místo frází). Všechny jsou v administraci.
  Výhody (karty s ikonkami): text v závorce se ukáže menším písmem pod nadpisem karty.
- „Najdete nás“: dokud v administraci není fotka vchodu, stojí vedle karty kreslené průčelí kavárny s točícím se
  odznakem „Nově otevřeno“. Po nahrání fotky se místo kresby ukáže fotka.
- „Spojte kávu s výletem“: kreslená mapa Svatého Kopečku (src/tripmap.svg). Po silnici z Olomouce jezdí autobus,
  po tečkované stezce cyklista. Na mapě je 6 míst (kavárna, bazilika, výhled, ZOO, autobus, pěšky a na kole) — po klepnutí
  se vedle mapy (na mobilu pod ní) ukáže karta s textem a tlačítkem. Texty karet jsou v administraci (sekce Výlet).
  Na mobilu se mapa posouvá do strany. Kresba se vloží až ve chvíli, kdy se k mapě blížíte (zrychluje start stránky);
  bez JavaScriptu se ukáže hned a karty jsou pod sebou. Polohu štítků mění `--x/--y` u tlačítek `.tpin` v index.tpl.html.
- „Sedněte si, zůstaňte chvíli“: karta pro každou výhodu z administrace s vlastní animací — vozíčkář dojede ke dveřím,
  které se otevřou; pejsek vrtí ocasem a olizuje se; karta ťukne na terminál a mince dopadne na sloupek; slunečník se kývá.
  Obrázek se vybírá podle slova v textu (bezbariérový / psi / karta, platba / terasa, výhled), jiný text dostane šálek.
- Po celé stránce se občas objeví drobnost: padající zrnka, listí, mráčky, ptáci, jiskřičky, balón nad mapou,
  papírová vlaštovka u rezervace, otazníky u dotazů. Vždy nejvýš dvě v sekci, jen když je sekce na obrazovce.
- Vlnitý text zrychlí podle scrollu a při scrollu nahoru jede pozpátku.
- Při „omezení pohybu“ v systému se nic z toho nespouští.

## Kontrola zobrazení
Ověřeno na 22 velikostech (telefony 320–430 px na výšku i na šířku, tablety, notebooky 1280×720 až 1536×864,
monitory 1920–3440 px), bez JavaScriptu (☰ pak vede na navigaci v patičce), s omezeným pohybem a bez videa.
Kontrolní skripty: tools/audit.mjs, tools/strip.mjs.

## Výsledky (Lighthouse, Chrome bez GPU = přísnější než běžný telefon)
Mobil i desktop: výkon 96–100 · přístupnost 100 · osvědčené postupy 100 · SEO 100.
Ověřeno na 9 velikostech obrazovky (telefon 360 px → monitor 2560 px), na výšku i na šířku, bez přetékání,
všechny ovládací prvky ≥ 44 px, funguje bez JavaScriptu i s omezením pohybu.

## Technika
- Fonty lokálně, ořezané na češtinu; metricky sladěné náhradní fonty (text při načtení neposkakuje).
- Hero: obrázek s průhledností (rychlé první vykreslení), video AV1/H.264 se spustí po načtení.
- Animace skoku do šálku: video AV1 674 kB (SSIM 0,9985 vůči originálu = okem nerozeznatelné; originál 1,95 MB).
- Bublinové pozadí se kreslí do malého plátna — stejný vzhled, zlomek výpočtu.
- Animace se připraví až u obrazovky a mimo ni se pozastaví; při „omezení pohybu“ se nespouští.
- Soubory s otiskem v názvu (`site.1a2b3c4d.js`) se cachují natrvalo; service worker zrychlí opakované návštěvy
  a umožní přidat web na plochu telefonu jako aplikaci.
