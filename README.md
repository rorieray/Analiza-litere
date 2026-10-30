# Litera — analiză de text din Wikipedia

O pagină HTML autonomă pentru analiza literelor unui articol Wikipedia. Interfața este în română. Fișierul `index.html` include toate stilurile CSS și tot codul JavaScript; nu are nevoie de Python, npm, biblioteci externe, chei API sau un server propriu. Conexiunea la internet este necesară pentru a prelua articolele. Introducerea manuală a textului funcționează și fără internet.

## Română și engleză — alegerea automată a alfabetului

Poți introduce un link de pe `ro.wikipedia.org` sau `en.wikipedia.org`, inclusiv varianta mobilă. Pentru fiecare articol, pagina solicită metadatele Wikipedia prin [API:Info](https://www.mediawiki.org/wiki/API:Info) și citește câmpul `pagelanguage`. Folosește limba paginii, fără să ghicească din diacritice și fără să salveze ultima limbă în cookie-uri sau în memoria permanentă a browserului.

- **Română (`ro`):** 31 de litere, vocalele `aăâeiîou`.
- **Engleză (`en`):** 26 de litere (a–z), vocalele `aeiou`.
- În ambele cazuri, `y` este clasificat drept consoană pentru acest exercițiu.

Exemplu în engleză: https://en.wikipedia.org/wiki/World_War_II

Limba identificată apare lângă sursă. Graficul, tabelul, literele lipsă și explicația metodei folosesc automat alfabetul potrivit. Interfața și explicațiile rămân în română. Alte limbi afișează un mesaj că nu sunt acceptate. Pentru textul lipit manual, alege **Română** sau **Engleză** din selector: textul simplu nu are metadatele unei pagini Wikipedia. Alegerea manuală nu influențează analiza linkurilor.

Pentru a actualiza site-ul deja publicat, încarcă noul `index.html` peste cel existent în repository și salvează un commit, de exemplu `Adaugă identificarea limbii și analiza în engleză`. După publicare, reîncarcă site-ul cu **Ctrl + F5**.

## Ce înveți în acest exercițiu

### Compararea a două articole

Comparația include încă două grafice:

1. **Diacritice asimilate:** `ă/â → a`, `î → i`, `ș → s`, `ț → t`. Numerele de apariții se adună, iar totalul literelor fiecărui text se păstrează. După asimilare, procentele a–z însumează 100% pentru fiecare text, înainte de rotunjire. Analiza individuală și primul grafic păstrează diacriticele distincte.
2. **Vocale și consoane:** bare alăturate pentru fiecare categorie, galben pentru textul 1 și albastru pentru textul 2. Fiecare text folosește propriul total și propria listă de vocale. Procentele sunt afișate pe cele patru bare; asimilarea diacriticelor nu schimbă împărțirea în vocale și consoane.

Ambele grafice pot fi descărcate separat ca SVG. Graficul cu linii păstrează valorile în informațiile afișate la poziționarea cursorului, fără a aglomera liniile cu numere.

Completează **Textul 1** și câmpul opțional **Textul 2**, apoi apasă **Analizează / Compară**. Limba fiecărui articol este identificată separat. Graficul comparativ afișează literele **a–z în ordine alfabetică**, cu frecvența relativă (%) pe axa verticală:

- **Galben, linie continuă:** textul 1.
- **Albastru, linie întreruptă:** textul 2.

Fiecare punct are un procent exact afișat la poziționarea cursorului. Literele absente au frecvența zero. Legenda arată titlul, limba și totalul literelor fiecărui text. Graficul poate fi descărcat ca SVG sau inclus în pagina tipărită/PDF.

Frecvența folosește totalul literelor acceptate din fiecare text, separat. Într-un text român, diacriticele sunt incluse în total, dar nu apar pe axa a–z și nu sunt combinate cu literele fără diacritice. Așadar, procentele celor 26 de puncte pot însuma mai puțin de 100% pentru română. Asta păstrează aceeași definiție a frecvenței ca în analiza individuală. Comparația folosește procente pentru a putea compara texte de lungimi diferite.

Rezultatele apar în această ordine: **analiza completă a textului 1**, **analiza completă a textului 2**, apoi **cele trei grafice comparative**. Fiecare analiză are propria sursă și limbă, totaluri, litere lipsă, grafic al probabilităților, grafic de vocale/consoane, tabel complet și text extras. Butoanele de descărcare din fiecare analiză salvează datele textului respectiv, iar fișierele au numărul textului în nume.

Rezultatele sunt organizate în trei file sub **Rezultatele analizei**: **Analiza textului 1**, **Analiza textului 2**, **Comparație**. Poți schimba filele prin clic sau cu săgețile stânga/dreapta când o filă are focus. La un singur text, apar doar rezultatele primei file.

Numele ambelor articole apar în legenda de deasupra fiecărui grafic comparativ. Nu sunt repetate în interiorul graficului. Imaginile SVG descărcate păstrează numele în titlul accesibil, vizibil ca informație despre imagine, fără etichete suplimentare desenate pe grafic.

**Text introdus manual:** deschide **Ai deja textul? Îl poți lipi aici.**, alege limba, lipește textul și apasă **Analizează textul introdus**. În această versiune, opțiunea analizează un singur text și înlocuiește rezultatele curente; nu îl combină cu linkurile Wikipedia și nu afișează filele textului 2 și comparației. Comparația dintre două texte folosește cele două câmpuri de link Wikipedia. Textul lipit este procesat local, fără a fi trimis pe un server.

**PDF pe o singură pagină:** butonul **Tipărește / Salvează PDF** pregătește o copie pentru tipărire cu toate cele trei secțiuni în coloane, indiferent de fila activă. Copia este scalată pentru o singură pagină **A4, orientare peisaj (landscape)**, cu margini de 8 mm. În dialogul de tipărire păstrează formatul A4, orientarea peisaj și scara implicită/100%; dezactivează antetul și subsolul browserului dacă sunt activate. Tabelele și explicațiile se micșorează pentru a încăpea. Textul integral extras, aflat în secțiunea pliabilă de previzualizare, rămâne disponibil în aplicație și la descărcare; nu este inclus în PDF. Fila selectată pe ecran nu este schimbată de tipărire.

Pentru un singur articol, lasă al doilea link gol; analiza textului 2 și comparația nu sunt afișate. Pentru publicarea modificării, încarcă noul `index.html` în repository și salvează un commit.

Instrucțiunile de mai sus folosesc un repository nou, cu `index.html` direct în rădăcină. Dacă încarci întregul proiect și păstrezi pagina în `html-version/index.html`, poți publica tot din `main` și `/ (root)`, apoi deschide `https://NUMELE-TAU.github.io/NUME-REPOSITORY/html-version/`. GitHub nu oferă selectarea directă a folderului `html-version` ca sursă de publicare din ramură; opțiunile sunt rădăcina sau `/docs`.

## Cum este extras textul

Pagina folosește [MediaWiki Action API — action=parse](https://www.mediawiki.org/wiki/API:Parsing_wikitext), cu `origin=*` pentru [cereri din browser de pe alt site](https://www.mediawiki.org/wiki/API:Cross-site_requests). Se solicită articolul întreg, nu doar rezumatul. Sunt acceptate linkuri de articol desktop și mobil, precum și linkuri cu `title` și `oldid`.

Din HTML-ul primit se păstrează **doar paragrafele**. Sunt eliminate tabelele, listele, casetele de navigare, imaginile, legendele, referințele și marcajele notelor. Titlurile secțiunilor sunt excluse. Cuvintele pe care există legături sunt păstrate, dar adresele URL nu sunt numărate. HTML-ul articolului nu este introdus în pagina vizibilă; este folosit doar pentru extragerea textului.

Rezultatul este o selecție a prozei articolului, nu fiecare caracter vizibil pe Wikipedia. Șabloanele Wikipedia pot varia; verifică secțiunea **Vezi textul folosit în analiză** înainte de a folosi rezultatele într-o lucrare. Rezultatele pot diferi de cele din `text.txt` dacă textul copiat manual include alte secțiuni sau provine din altă versiune a articolului.

Se normalizează diacriticele Unicode, se transformă literele în minuscule și se păstrează alfabetul limbii identificate. Vocalele și alfabetul sunt alese conform regulilor de mai sus. Celelalte litere acceptate, inclusiv `y`, sunt clasificate drept consoane. Probabilitatea este numărul de apariții împărțit la totalul literelor acceptate. Literele lipsă sunt incluse cu zero în grafic și tabel. O analiză fără litere acceptate afișează un mesaj, fără împărțire la zero.

Sursa și versiunea articolului analizat sunt afișate în rezultate. Wikipedia este contactată direct din browser; nu există un serviciu intermediar și textul introdus manual nu este trimis nicăieri. Cererile pot eșua dacă nu ai internet, Wikipedia limitează accesul sau o extensie le blochează; există și opțiunea de introducere manuală.

## Documentație pentru GitHub Pages

- [Crearea unui site GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)
- [Alegerea ramurii și a folderului publicat](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

Proiect educațional realizat cu asistența inteligenței artificiale. Textele analizate aparțin autorilor Wikipedia; consultați condițiile de reutilizare ale articolului sursă.
