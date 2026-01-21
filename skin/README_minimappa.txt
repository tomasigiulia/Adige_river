Guida rapida: Minimappa personalizzata krpano
============================================

1. Copia il file skin/skin_minimap_custom.xml in ogni progetto dove vuoi la minimappa.

2. Nel file vtourskin.xml del tuo tour, aggiungi questa riga dove vuoi che venga caricata la minimappa:

   <include url="skin/skin_minimap_custom.xml" />

3. Sostituisci il pulsante mappa standard:
   Cerca il layer con name="skin_btn_map" e sostituiscilo con:

   <layer name="skin_btn_map"
          style="skin_base|skin_glow"
          crop="64|128|64|64"
          align="left"
          x="90"
          y="0"
          scale="0.5"
          visible="true"
          onclick="switch_minimap_custom();"
   />

4. Assicurati che l'action switch_minimap_custom sia presente (se non c'è, aggiungila):

   <action name="switch_minimap_custom">
       if(layer[skin_minimap_container].visible == true,
           tween(layer[skin_minimap_container].alpha, 0.0, 0.25, default, set(layer[skin_minimap_container].visible,false));
       ,
           set(layer[skin_minimap_container].visible, true);
           tween(layer[skin_minimap_container].alpha, 1.0, 0.25);
       );
   </action>

5. Risultato:
   - Il pulsante mappa apre/chiude la minimappa laterale.
   - La minimappa si può espandere/ridurre con il nuovo tasto in alto a destra.
   - La mappa grande standard non verrà più aperta.

Consiglio: puoi personalizzare dimensioni, colori e posizione modificando skin_minimap_custom.xml.
