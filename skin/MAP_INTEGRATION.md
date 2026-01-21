Breve guida: integrare la mappa in un altro progetto krpano

Breve guida: integrare la mappa in un altro progetto krpano

1) Copia lo snippet
- Copia il file `skin/map-snippet.xml` nella cartella `skin/` del nuovo progetto.

2) Aggiungi il contenuto nel tuo skin
- Opzione A (consigliata): apri il tuo skin XML (`skin/vtourskin.xml`) e incolla i blocchi del file `map-snippet.xml` nei posti corrispondenti:
  - La riga `<skin_settings ...>` vicino all'inizio (o sovrascrivila in `tour.xml`).
  - Il layer `skin_btn_map` dentro il container dei bottoni (`skin_control_bar` -> `skin_control_bar_buttons`).
  - La `skin_map_container` nella struttura del layout (dove ci sono `skin_thumbs_container` / `skin_scroll_layer`).
  - Le `<action>` (`skin_showmap`, `skin_load_maps_plugin`, `skin_addmapspots`) insieme alle altre azioni del skin.

- Opzione B: includi il file dalla tua skin (se preferisci non incollare):
  - All'interno del tuo `<krpano>` o del file skin, aggiungi: `<include url="skin/map-snippet.xml" />`
  - Nota: l'`<include />` funziona solo se il file è valido nel contesto dove lo includi; potresti dover spostare o adattare blocchi duplicati.

3) Impostazioni e API key
- Se usi Google o Bing, modifica le chiavi in `skin_settings`:
  - `maps_google_api_key="YOUR_KEY"` oppure `maps_bing_api_key="YOUR_KEY"`.
- Scegli il provider con `maps_type` (es. `openstreetmaps`, `google`, `bing`, oppure un tileprovider custom).
- Se vuoi caricare subito il plugin, usa `maps_loadonfirstuse="false"`. Altrimenti il plugin sarà caricato al primo uso.

4) Esempio di `tour.xml` per sovrascrivere le impostazioni (metti nella root del tour):

<krpano>
    <!-- include your skin as usual -->
    <include url="skin/vtourskin.xml" />

    <!-- override skin settings to enable maps -->
    <skin_settings maps="true" maps_type="openstreetmaps" maps_loadonfirstuse="false" maps_google_api_key="" maps_bing_api_key="" />

</krpano>

5) Evitare duplicati
- Se il tuo skin attuale già definisce `skin_map`, `skin_btn_map` o le azioni nominate, non duplicare: copia solo le parti mancanti o riusa i nomi esistenti.

6) Test
- Apri `index.html` o `tour.html` nel browser e verifica:
  - Il pulsante mappa è visibile nel control bar (se non visibile, imposta `visible="true"` temporaneamente sul layer `skin_btn_map` oppure metti `skin_settings.maps="true"`).
  - Cliccando il pulsante compare la mappa e i map-spots (se hai definito `lat`/`lng` nelle scene).

7) Esempio rapido di scena con coordinate (per creare spot sulla mappa):

<scene name="panorama1" lat="45.12345" lng="9.12345" mapzoom="14">
    <!-- scene content -->
</scene>

8) Quale API usa questo progetto e come cambiarla
- Provider predefinito: OpenStreetMap. In questo progetto `maps_type` è impostato su `openstreetmaps` (vedi `tour.xml` o il `skin_settings` del tuo skin).
- Quando `maps_type` è `google` o `bing`, lo snippet carica rispettivamente `plugins/googlemaps.js` o `plugins/bingmaps.js` e usa la relativa API key.
- Se `maps_type` è diverso (es. `openstreetmaps` o un tileprovider custom), viene usato lo stile/plugin definito in `plugins/krpanomaps.xml`.
- Dove cambiare: imposta `maps_type="google"` o `maps_type="bing"` e inserisci la chiave in `maps_google_api_key` / `maps_bing_api_key` (in `tour.xml` o nel blocco `skin_settings`).
- File plugin inclusi in questo progetto:
  - `plugins/krpanomaps.xml`
  - `plugins/googlemaps.js`
  - `plugins/bingmaps.js`
- Caricamento: se `maps_loadonfirstuse` è `true` la libreria viene caricata al primo uso; se `false` viene caricata immediatamente all'avvio.

Fine.

Nota: in questo progetto il plugin delle mappe è fornito come `plugins/krpanomaps.xml` (vedi `plugins/krpanomaps.xml`). Se copi lo snippet in un altro progetto assicurati che lo stesso file (o `krpanomaps.js`) sia presente nella cartella `plugins/` del tour, oppure modifica l'attributo `url` del `<plugin>` per puntare al plugin che usi.
