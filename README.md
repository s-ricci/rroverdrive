# Rogue Rush: Overdrive — distribuzione

Canale di distribuzione dell'APK Android di **Rogue Rush: Overdrive**.
Qui non c'è il codice sorgente del gioco: solo il pacchetto da installare e il
manifesto che il gioco stesso legge per accorgersi che esiste una versione nuova.

## Installare

Scarica l'APK dall'ultima release: **[Releases](https://github.com/s-ricci/rroverdrive/releases/latest)**

Al primo avvio Android chiede di consentire l'installazione da questa origine.
Dalla versione 1.8 in poi il gioco si aggiorna da solo: all'apertura controlla se
c'è una versione più recente, la scarica e apre l'installazione.

## Come funziona l'aggiornamento

1. All'avvio il gioco legge `version.json` da questo repository.
2. Se `versionCode` è maggiore di quello installato, mostra l'avviso.
3. Scarica l'APK da `apkUrl` e lo passa all'installer di Android.

## Pubblicare una versione nuova

L'ordine conta: prima la release con l'APK, poi `version.json`. Al contrario, i
telefoni vedrebbero l'aggiornamento prima che il file esista.

1. In `Assets/Scripts/BuildInfo.cs` alzare `VersionCode` e `VersionName`
   (è l'unico posto: `ApkBuilder` legge di lì).
2. Build dell'APK.
3. Creare la release con l'APK allegato:
   `gh release create v1.9 Builds/RogueRushOverdrive.apk --title "v1.9" --notes "..."`
4. Aggiornare `version.json` in questo repository con gli stessi numeri e l'URL
   dell'APK appena caricato.

## Nota sulla firma

L'APK è firmato con la chiave di debug di Unity. Android installa un
aggiornamento solo se è firmato con **la stessa chiave** del pacchetto già
presente: finché si compila dalla stessa installazione di Unity va bene, ma
cambiando macchina o versione dell'editor la chiave cambia e l'aggiornamento
verrebbe rifiutato. Per un canale duraturo serve un keystore dedicato, tenuto
fuori da questo repository — il passaggio richiede una disinstallazione manuale.
