# Metsapraktika päevik

Failid samas kaustas, majutatud **HTTPS-is** (GitHub Pages, Netlify, Cloudflare Pages — tasuta): `index.html`, `manifest.webmanifest`, `sw.js`.
Uue versiooni üleslaadimine **samale aadressile** ei puuduta andmeid (need on brauseris ja pilves, mitte failis).
Aadressi vahetamisel / brauseriandmete tühjendamisel kaovad kohalikud andmed → tee varukoopia (Seaded → Andmed) või kasuta pilvesünki.

## Uus selles versioonis

- **Andmed jäävad alles**: kohalik salvestus + palve brauserile mitte andmeid kustutada + JSON-varukoopia ja taastamine.
- **Sama nimi teises seadmes = samad andmed**: pilvesünk (Firebase, tasuta). Liidab, mitte ei kirjuta üle: kahes seadmes lisatud koormad jäävad mõlemad alles, kustutamised kanduvad üle.
- **Kustutamine**: üksik koorem (✕), töö, terve päev (praktikapäeviku eelvaates) ja "Kustuta kõik tööd ja koormad" (kandub kõigisse seadmetesse). Wordi faili kustutamised ei puuduta.
- **Nutikas sisestus**: koorma lisamisel kirjuta nt `3 koormat männipalk 45 tm` või `kuusepaberipuit 2 koormat 3/4` → täidab vormi.
- **💬 Abiline** (all paremal): ilma võtmeta lisab koormaid samast tekstist. Anthropicu API võtmega oskab ka tööd alustada/lõpetada, muuta seadeid ja sortimente, öelda kokkuvõtteid, kustutada koormaid (sinu kinnitusel) ja kirjutada päeviku teksti (isiklikku panust ainult kui palud). Rakenduse koodi see ei muuda — muudatused tehakse rakenduse enda tegevustega.

## Uuendamine ilma andmeid kaotamata

- Lae uus `index.html` **samale aadressile** nagu vana — andmed jäävad alles (need on brauseris/pilves, mitte failis). Esimesel avamisel salvestab rakendus ka koopia algsest seisust (Seaded → Andmed → "Enne uuendust").
- Rakendus hoiab lisaks 3 viimast päevakoopiat; need on samas kohas alla laaditavad.
- **Vana Koorma Arvutaja andmed** (kui kasutasid seda varasemat rakendust samal aadressil): rakendus leiab need ise ja küsib esimesel sisselogimisel, kas importida. Vanu andmeid ei kustutata ega muudeta; korduv import ei tekita topelt. Fotosid uus rakendus ei impordi (need jäävad vana andmestiku sisse alles).
- Kui uus rakendus on **teisel aadressil**: pane `vana-andmete-varukoopia.html` vana rakenduse kausta, ava see seal, lae fail alla ja impordi uues rakenduses (Seaded → Andmed → Taasta varukoopiast).

## Öövahetus / keskööst üle

- Avaleht näitab **vahetuse päeva** (töö algus), mitte kalendripäeva: töö käies ja 12 h pärast lõppu püsivad tm, koormad ja tunnid ekraanil ka pärast kella 24.
- Seaded → "Töö lõpeb automaatselt kell": **−1 = ei lõpeta automaatselt** (sobib öövahetusele).
- Kokkuvõttes puuduta päeva (või avalehel "Ava päev"): näed koormaid, masinat, kellaaegu ja sortimente.

## Pilvesünk (5 min, ühekordne)

1. [console.firebase.google.com](https://console.firebase.google.com) → **Add project** (Analytics võib välja lülitada).
2. **Build → Authentication → Get started → Sign-in method → Anonymous → Enable.**
3. **Build → Firestore Database → Create database** (production mode, piirkond nt `eur3`).
4. Firestore → **Rules** → asenda sisuga ja **Publish**:
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /users/{id} {
         allow get, create, update: if request.auth != null;
         allow list, delete: if false;
       }
     }
   }
   ```
5. **Project settings (⚙) → General**: kopeeri **Project ID** ja **Web API Key** (kui API key'd ei näe: lisa seal veebirakendus `</>`, see näitab `apiKey`).
6. Rakenduses: **Seaded → Pilvesünk** → sisesta mõlemad (iga seadme jaoks üks kord) — või kirjuta need `index.html` algusesse konstanti `FIREBASE`.

Turvalisus ausalt: pilvedokumendi nimi on hash(nimi + salasõna). Kes teab nime ja salasõna, pääseb su andmetele; **ilma salasõnata piisab ainult nimest** — pane salasõna. Andmed on Firestore'is krüpteerimata (Firebase projekti omanik näeb neid). Dokumentide loetelu ega kustutamine pole reeglitega lubatud.

## AI võti

Anthropicu konsoolist (console.anthropic.com) oma API võti → Seaded → AI abiline. Võti jääb ainult selle seadme brauserisse (ei sünkroonita), kulu läheb sinu arvele — sea konsoolis kuupiir. Vaikimisi mudel `claude-haiku-5-5` (muudetav väljal "Mudel").

## Testimise staatus

Päris Chromiumis testitud (võltsitud Firebase/ntfy/Anthropic vastustega): kahe seadme liitmine (samaaegsed lisamised, kustutamised, kogu andmete kustutamine), vale salasõna → eraldi andmed, varukoopia, tekstisisestus, AI tööriistakutsed, Wordi eksport. **Päris Firebase'i, ntfy ja Anthropicu serveritega pole testitud** (mu keskkonnal pole internetti) — päringuvormingud järgivad dokumentatsiooni, aga esimesel kasutusel vaata Seaded → Pilvesünk olekut ja "Saada test".

## Teavitused (ntfy)

Eelmisest versioonist: Seaded → Teavitused telefonis → loo teema, telli ntfy rakenduses, "Saada test".
