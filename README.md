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
- **Vista Altimetria**: profili altimetrici da montare sui file di stampa,
  con i paesi e i passi presi da un GPX di waypoint — vedi sotto

## Altimetria

La seconda scheda del tool (in alto a sinistra) disegna il profilo
altimetrico delle tracce caricate e lo esporta in PNG ad alta risoluzione,
anche **a sfondo trasparente** per montarlo direttamente sul file di stampa.
Non serve il token Mapbox: il profilo nasce tutto dai dati GPX.

- Si caricano le stesse tracce della mappa, più un **GPX di waypoint**
  (paesi, passi, laghi, rifugi): i punti entro la distanza scelta vengono
  proiettati sul profilo — pallino e nome per i paesi, triangolo per passi
  e luoghi
- Il percorso si può **spezzare in più tratti**: i tagli cadono a intervalli
  regolari ma si agganciano al paese più vicino (preferendo i centri più
  grandi), e ogni taglio si può spostare a mano su un altro paese
- Ogni tratto stampa lunghezza, dislivello positivo e chilometro assoluto
  di inizio e fine, così il partecipante sa sempre dove si trova
- Sul profilo intero si possono imporre i **totali ufficiali** dell'evento
  al posto di quelli calcolati dal GPX (il D+ ricavato dal GPX è sempre un
  po' diverso da quello dichiarato)
- Quota livellata su 200 m e dislivello con isteresi di 5 m, per non
  gonfiare il D+ col rumore del GPS

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

Il file contiene il token pubblico Mapbox di AdventureLab (variabile `TOKEN`
in cima allo script). I token `pk.` sono pensati per stare nel codice client,
**ma vanno protetti con le restrizioni URL**, altrimenti chiunque può usarli
consumando la quota dell'account:

1. Vai su [account.mapbox.com](https://account.mapbox.com) → Tokens
2. Apri il token e in **URL restrictions** aggiungi i domini dove gira la
   pagina, ad esempio `https://advlabbik.github.io`
3. Salva

Se il token viene revocato o rifiutato, la pagina ne chiede uno nuovo
all'avvio e lo conserva nel browser. Chi fa un fork deve sostituire il token
con il proprio nella variabile `TOKEN`.

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
