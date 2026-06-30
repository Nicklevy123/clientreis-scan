# Clientreis Scan | Growtivity

Interactieve lead magnet scan voor zorgorganisaties (GGZ, VVT, GHZ). Negen vragen over instroom, doorstroom en uitstroom, gevolgd door een resultaatpagina op basis van score en een formulier dat gegevens naar Make.com stuurt.

Gehost via GitHub Pages.

---

## Webhook URL aanpassen

Open `index.html` en zoek op regel met:

```js
var WEBHOOK_URL = 'VUL_HIER_UW_MAKE_WEBHOOK_URL_IN';
```

Vervang de placeholder door uw Make.com webhook URL, bijvoorbeeld:

```js
var WEBHOOK_URL = 'https://hook.eu1.make.com/abcdef1234567890';
```

Sla het bestand op en push naar GitHub (zie volgende stap).

---

## Wijzigingen live zetten via git push

```bash
# Eenmalig (al gedaan bij aanmaken repo):
git remote add origin https://github.com/Nicklevy123/clientreis-scan.git

# Bij elke wijziging:
git add index.html
git commit -m "Omschrijving van wijziging"
git push origin main
```

GitHub Pages publiceert automatisch binnen circa 30 seconden na elke push.

---

## Wat wordt er verstuurd naar Make.com?

Bij inzending stuurt de scan een JSON POST met de volgende velden:

| Veld | Beschrijving |
|---|---|
| `naam` | Ingevulde naam |
| `organisatie` | Naam van de organisatie |
| `email` | E-mailadres |
| `sector` | GGZ, VVT, GHZ of Anders |
| `bron` | Waarde van `utm_source` uit de URL, of `onbekend` |
| `totaalscore` | Totaalscore (9 tot 36) |
| `maximumscore` | Altijd 36 |
| `akkoord_privacybeleid` | `true` als checkbox aangevinkt |
| `antwoorden` | Array met per vraag: sectie, vraagtekst, antwoord en score |

---

## Foutafhandeling

Als het versturen naar de webhook mislukt, toont de pagina een foutmelding met een `mailto:` link. Die opent automatisch een e-mailconcept naar `info@growtivity.nl` met alle ingevulde antwoorden al in de body, zodat een ingevulde scan nooit volledig verloren gaat.
