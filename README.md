# Metsapraktika päevik

Failid peavad olema samas kaustas ja **majutatud HTTPS-is** (GitHub Pages, Netlify, Cloudflare Pages — tasuta):
`index.html`, `manifest.webmanifest`, `sw.js`. Telefonis: ava leht → "Lisa koduekraanile".
(Ilma majutuseta, lihtsalt faili avades töötab põhiosa, aga offline-tugi ja ntfy-nupud ei tööta.)

## Mis rakendus teeb

- **Töö langil**: "Alusta tööd langil" (lank, kvartal, eraldis, masin; algusaeg automaatselt). "Vaheta lanki" lõpetab praeguse ja alustab uue — igal langil on oma tunnid ja koormad.
- **Koorem**: koormate arv (+/−) ja kas täituvus 1/4–4/4 (arvutab tm) **või** otse tm sisestus. "↻ Sama uuesti" kordab eelmist koormat ühe vajutusega.
- **Palk**: Seadetes tunnipalk (€/h) ja/või tm-hind (€/tm; sortimendi juures saab panna oma hinna). Kokkuvõttes näidatakse mõlemat hinnangut, peamiseks loetakse valitud.
- **Kokkuvõte**: täna / nädal / kuu / kõik — tunnid, koormad, tm, tm/h, raha; päevade, langide ja sortimentide kaupa.
- **RMK nimetused**: Sortimendid → "+ RMK nimetused" lisab RMK ametlikes dokumentides esinevad nimed (Männipalk, Kuusepalk, Kasevineeripakk, Kasespoonipakk, Kasepeenpalk, Haavapalk, Sanglepapalk, Hall-lepapalk, Kuusepaberipuit, Küttepuit, D-kvaliteet). Koefitsient on 1 — kalibreeri ise.
- **Praktikapäevik**: iga päev (kõik selle päeva langid) saab ühe rea sinu Wordi tabeli lõppu. Tegevuste tekst koostatakse koormatest; "isiklik panus" jääb sinu kirjutada. Eelvaates saab kellaaegu parandada ja koormaid kustutada. Seaded → "Lae praegune praktikapäevik alla" annab hetkeseisu.
- **"Kas töö veel käib?"**: kui koormaid pole X tundi (Seaded, vaikimisi 2 h), küsib rakendus: "Töö käib" või "Päev läbi" (siis saad panna tegeliku lõppkellaaja). Kell 22:00 (muudetav) lõpeb töö automaatselt.

## Teavitused telefonis (ntfy)

Veebileht ei saa suletuna ise kella jälgida. Seepärast ajastab rakendus teate **ette** tasuta teenusesse ntfy.sh
(`delay` + `sequence-id`) ja tühistab/ajastab selle uuesti iga koorma lisamisel.

1. Installi ntfy rakendus. 2. Seaded → "Loo teema", tellige sama teema ntfy rakenduses. 3. "Saada test".

Ausalt: seda päris ntfy serveri ja telefoniga pole minu keskkonnas (võrguta) läbi testitud — päringud on kontrollitud
(saadetavad URL-id ja järjekord), aga tühistamise (DELETE) toimimine brauserist sõltub ntfy CORS-seadistusest.
Halvimal juhul tuleb üks üleliigne "kas töö käib?" teade; vajutades "Töö käib" läheb kõik korda.
Ilma ntfy-ta küsib rakendus sama asja kohe, kui oled selle avanud/taustal lahti ja aeg täis.
