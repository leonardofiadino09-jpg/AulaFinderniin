# AulaFinder V20 - PWA (Android + iPhone)

Questa versione parte dalla **V19**. Non modifica il layout né la logica di ricerca/orari/piantine.
Aggiunge soltanto: `manifest.webmanifest`, `sw.js`, `pwa.js`, le quattro icone PNG e i collegamenti nell'`<head>` di `index.html`.

## Avvio in locale

Aprire `index.html` direttamente consente di vedere il sito, ma **non installa la PWA**: i service worker richiedono HTTPS o localhost.

Per fare una prova completa sul PC, aprire un terminale **dentro la cartella AulaFinder** ed eseguire:

```bash
python -m http.server 8000
```

Aprire `http://localhost:8000/` nel browser. Per provare l'installazione sul telefono, è più semplice pubblicarla su HTTPS.

## Pubblicazione gratis su GitHub Pages

1. Su GitHub creare un repository **pubblico** ad esempio `aulafinder` (verificare prima con la scuola le autorizzazioni a diffondere gli orari).
2. Caricare **i file dentro `AulaFinder/` alla radice del repository**: `index.html`, `style.css`, gli altri `.js`, `manifest.webmanifest`, `sw.js`, `pwa.js`, e le cartelle `assets/` e `icons/`.
3. Aprire **Settings > Pages**, selezionare **Deploy from a branch**, ramo `main`, cartella `/ (root)` e salvare.
4. Quando GitHub Pages pubblica il sito, aprire l'indirizzo HTTPS mostrato nella pagina Pages. Non serve modificare percorsi: manifest, scope e worker sono relativi e funzionano anche nei sottopercorsi.

## Installazione sul telefono

- **iPhone**: aprire il sito con Safari, menu Condividi > **Aggiungi alla schermata Home**, tenere attivo **Apri come app web**, poi Aggiungi.
- **Android**: aprire il sito con Chrome, menu **⋮ > Installa app** (oppure **Aggiungi a schermata Home**, secondo browser/dispositivo).

L'app non compare automaticamente su App Store o Play Store e non richiede il loro pagamento.

## Offline e aggiornamenti

Dopo la prima apertura su HTTPS, attendere che siano stati scaricati i file (circa 14 MB). La PWA memorizza HTML, CSS, JS, piantine, immagini e dati degli orari. Dopo il primo caricamento e attivazione del service worker, le sezioni possono funzionare anche senza rete.

- **Le lezioni non vengono sincronizzate con un registro scolastico:** i dati sono quelli incorporati nel progetto, non informazioni in tempo reale.
- Quando pubblicate una nuova versione, aggiornare la stringa `CACHE_NAME` nel file `sw.js`. Un servizio offline può continuare a servire risorse vecchie finché l'aggiornamento non è stato installato e la pagina ricaricata.
- Se una pagina viene aperta offline prima che il download iniziale sia completo, può non funzionare.
- `file://` non abilita le funzioni di installazione e offline.

## File aggiunti

- `manifest.webmanifest`: nome, icone, colori, avvio in modalità standalone.
- `sw.js`: cache e navigazione offline.
- `pwa.js`: registrazione del service worker.
- `icons/icon-192.png`, `icons/icon-512.png`: icone installabili.
- `icons/icon-maskable-512.png`: icona con area sicura per Android.
- `icons/apple-touch-icon-180.png`: icona Home per iPhone.

Sono state mantenute tutte le immagini e le funzionalità della V19.
