# Tool per stampare le cartine e le mappe degli eventi

Realizza l'esportazione con le tracce .gpx dell'evento. Strumento web per
creare cartine e mappe da stampa dei percorsi gravel e bikepacking, costruito
da AdventureLab per gli eventi della Bike Adventure Series.
Un singolo file HTML, nessuna installazione: si apre nel browser e si esporta
un PNG ad alta risoluzione pronto per la tipografia.

## Cosa fa

- Mappa Mapbox (stile Outdoors, Satellite, Streets o Light) con ombreggiatura
  del rilievo a doppia luce regolabile
- Rete off-road evidenziata: strade sterrate in tratteggio marrone, sentieri e
  mulattiere in punteggiato rosso, in stile carta escursionistica
- Caricamento di **più tracce GPX insieme**, ognuna con il proprio colore
  scelto da una palette di colori accesi. La prima traccia caricata resta
  sopra a tutte le altre
- **Frecce di direzione** lungo ogni traccia (seguono il verso di percorrenza
  del GPX) e **spessore delle tracce regolabile** con uno slider
- Toponimi integrativi del Trentino sempre visibili, con gerarchia a tre ranghi
- Tonalità "atlante d'epoca" attivabile, effetto vissuto regolabile
  (tinta calda, vignettatura leggera, grana di carta)
- Inclinazione della vista a volo d'uccello, con terreno 3D opzionale
- Export PNG a 150/200/300 DPI nei formati 30×40, 50×70, A2, A1, con opzione
  di dettaglio maggiorato per la rete sentieristica

## Come si usa

1. Apri la pagina GitHub Pages del repository (o `index.html` nel browser)
2. Al primo avvio la pagina chiede un token pubblico Mapbox — vedi sotto
3. Inquadra l'area: la cornice bianca mostra esattamente cosa verrà stampato
4. Trascina i GPX nell'area di caricamento, scegli i colori delle tracce
5. Regola rilievo, tonalità, inclinazione
6. Scegli formato e risoluzione, poi "Esporta PNG per la stampa"

Il formato predefinito è A1 orizzontale a 200 DPI.
Sulla stampa va riportata l'attribuzione **© Mapbox © OpenStreetMap**.

## Token Mapbox

Il repository **non contiene nessun token**. Al primo avvio la pagina ne
chiede uno pubblico (`pk.…`), lo salva nel browser e non lo richiede più.

Per crearne uno gratis:

1. Vai su [account.mapbox.com](https://account.mapbox.com) → Tokens
2. Crea un token dedicato a questo strumento (basta il tipo pubblico `pk.`)
3. In **URL restrictions** aggiungi il dominio dove è pubblicata la pagina,
   ad esempio `https://TUOUTENTE.github.io` — così il token funziona solo lì
4. Incolla il token nella pagina al primo avvio

Chi fa un fork può in alternativa scrivere il proprio token nella variabile
`TOKEN` in cima allo script, ricordandosi le restrizioni URL. GitHub blocca
le push che contengono token Mapbox riconoscibili, quindi il token hardcoded
va usato solo su copie locali o dove la protezione segreti lo consente.

## Pubblicare con GitHub Pages

Nel repository: **Settings → Pages → Source: Deploy from a branch →
Branch: main / (root) → Save**. Dopo qualche minuto la mappa è online su
`https://TUOUTENTE.github.io/NOMEREPOSITORY/`.

## Adattare lo strumento a un altro evento

- **Area iniziale**: cerca `bounds:` nella funzione `loadMap` e imposta le
  coordinate della tua zona
- **Toponimi garantiti**: modifica l'array `EXTRA_PLACES`
  (`[nome, longitudine, latitudine, rango]`, rango 1 = città, 3 = paese)
- **Scritta regionale**: cerca `region-names` e cambia nome e coordinate
- **Palette tracce**: modifica l'array `PALETTE`

## Limiti noti

- I dati di sentieri e sterrate arrivano nelle tile Mapbox solo da zoom 11-12
  in su: su inquadrature molto ampie usa l'opzione "Dettaglio off-road
  nell'export"
- L'export con vista inclinata riproduce la vista corrente, non la cornice
  esatta (con vista dall'alto la corrispondenza cornice-stampa è invece esatta)
- La dimensione massima dell'export dipende dalla scheda grafica del computer
  (lo strumento la rileva e avvisa)

## Licenza

MIT — vedi [LICENSE](LICENSE). I dati cartografici sono di Mapbox e
OpenStreetMap e seguono le rispettive licenze.
