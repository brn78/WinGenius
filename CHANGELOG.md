# Novità

## 0.5.0 · 31 ottobre 2026

- **Servizio Windows «WinGenius Agent»**: il motore gira in sottofondo come LocalSystem, parte con
  Windows prima di qualunque accesso e sopravvive alla chiusura della finestra. Sorveglianza della
  rete e degli accessi, routine pianificate, piani e agente vivono nel servizio; la finestra si
  collega su una pipe locale riservata (SYSTEM, amministratori elevati e gli operatori autorizzati)
  e diventa un telecomando con streaming, approvazioni e avvisi in tempo reale. Senza servizio tutto
  continua a funzionare dentro la finestra come prima. Il setup per tutti gli utenti lo installa e
  lo avvia (`/NOSERVICE=1` per saltarlo); dalle Impostazioni → Servizio si installa, ferma, rimuove
  e si decide chi può collegarsi.
- **Cassaforte e servizio**: su tua scelta esplicita il servizio riceve una copia della chiave della
  cassaforte, custodita con DPAPI nel profilo dell'account di servizio, così lavora anche a finestra
  chiusa e dopo un riavvio; altrimenti la chiave gli viene prestata solo finché resta acceso.
- **Piani con checkpoint e ripresa dopo il riavvio**: ogni piano approvato viene registrato; il
  modello dichiara i passi con `plan_step` e i comandi coerenti con un passo approvato non chiedono
  una seconda conferma (fino al rischio dichiarato per il passo). Prima di un riavvio il piano salva
  il checkpoint; al nuovo avvio il servizio riconosce la sessione cambiata, esegue la verifica
  post-riavvio e prosegue con i soli passi approvati. Politica per il lavoro non presidiato: si
  ferma sempre, oppure continua i passi approvati e si ferma per tutto il resto avvisando.
- **Riavvio sicuro delle macchine** (`machine_restart`): chi è collegato (console, desktop remoto,
  condivisioni, file aperti), messaggio agli utenti con conto alla rovescia, periodo di grazia,
  nuovo controllo, riavvio, attesa del ritorno e verifica; vale per la macchina locale e per quelle
  remote.
- **Macchine gestite**: elenco delle macchine amministrate (controller di dominio, DNS, host
  Hyper-V, file server…) con metodo di collegamento (WinRM, WinRM su SSL, PowerShell Direct, SSH) e
  credenziali della cassaforte; strumenti `machine_list/save/remove/test/run/who/message/restart`
  e scheda «Macchine» nella vista Rete; «Gestisci» da un dispositivo dell'archivio.
- **Notifiche fuori dalla finestra**: e-mail (SMTP) e Telegram, con scelta degli eventi (piani,
  dispositivi nuovi, avvisi di accesso, routine fallite, servizio), prova dei canali e registro delle
  consegne; strumento `send_notification` per il genio.
- **Routine pianificate**: gli script della libreria eseguiti a orario (ogni N minuti o ore, ogni
  giorno, settimanale, mensile) dal servizio o dalla finestra, con esito, prossima esecuzione e avviso
  quando falliscono; strumenti `routine_*` e scheda «Routine» nella vista Script.
- **Area di notifica**: icona accanto all'orologio con stato, menu rapido a tema (apri, scansiona,
  chi è collegato, script, memoria, nuova conversazione, impostazioni, esci), chiusura della finestra
  che riduce a icona, avvio con Windows, fumetti per gli avvisi quando la finestra è nascosta.
- **Dettatura**: pulsante microfono nel compositore con riconoscimento locale Whisper (modello
  scaricato una volta dalle Impostazioni → Voce, nulla esce dalla macchina), tieni premuto e parla
  oppure clic per iniziare e fermare, `Ctrl+Spazio`.
- **Identità**: nome del programma (soprannome) e nome dell'operatore nelle Impostazioni → Programma,
  usati dall'interfaccia e dal modello («rivolgiti a me come Bruno»).
- Memoria e cassaforte condivise tra finestra e servizio senza conflitti (attesa su database
  occupato, rilettura delle voci, lucchetto sul file della cassaforte).

## 0.4.0 · 31 ottobre 2026

- **Archivio della rete nel tempo**: motore di scansione in C# (ping e ARP in parallelo, MAC e
  produttore da tabella IEEE incorporata, nomi DNS e NetBIOS, porte comuni con servizi e banner,
  riconoscimento del tipo di dispositivo: router, NAS, stampante, telecamera, host Hyper-V,
  domotica, smart TV, telefono…). Una /24 completa in una decina di secondi. Ogni scansione
  aggiorna l'archivio SQLite e viene confrontata con la precedente: nuovi, ricomparsi, assenti,
  cambi di IP, nome o porte. Vista **Rete** con scheda per dispositivo (alias, fiducia, note,
  porte, storia), elenco dei cambiamenti e storico delle scansioni; scansioni automatiche a
  intervalli regolabili.
- **Chi è collegato alla macchina**: sorveglianza di sessioni SMB, file aperti via rete, accessi
  console e desktop remoto, connessioni TCP in ingresso e condivisioni, con osservazione dei file
  nelle cartelle condivise attribuita a chi li aveva aperti; se il programma è elevato legge anche
  il registro Security (accessi, accessi negati, condivisioni e file). Vista **Accessi** con
  fotografia in tempo reale, eventi filtrabili e condivisioni.
- **Schedine di avviso**: dispositivo nuovo o sospetto in rete, collegamenti alle condivisioni,
  file modificati, accessi negati compaiono in basso a destra con «Chiedi al genio» e «Apri»;
  contatore e riepilogo nel pannello laterale, storico della sessione.
- **Script riutilizzabili**: libreria di script PowerShell parametrici (file `.ps1` con
  intestazione di aiuto in `ProgramData\WinGenius\scripts`), che il genio crea e riusa con gli
  strumenti `script_save`, `script_list`, `script_get`, `script_run` e `script_delete`; vista
  **Script** per consultarli, eseguirli con i parametri (sempre con approvazione) ed eliminarli.
- Nuovi strumenti dell'agente: `network_inventory`, `access_activity`; `network_discover` usa il
  motore C# e l'archivio. Il contesto del modello include il digest della rete, i cambiamenti non
  ancora visti e l'elenco degli script in libreria.
- Gli script più lunghi del limite della riga di comando passano da un file temporaneo.
- Impostazioni: sezioni **Rete** e **Sorveglianza**.

## 0.3.0 · 31 ottobre 2026

- **Check-up automatico al primo avvio**: WinGenius capisce da solo dove è installato e su che
  macchina gira (server, controller di dominio, host Hyper-V o postazione; ruoli e servizi,
  risorse, dischi, rete, chi c'è in rete, Internet) e lo ricorda. Si può rifare in qualunque
  momento dalla barra laterale; al termine propone di chiedere subito al genio cosa ottimizzare.
- **Monitor di Internet**: controllo ogni minuto e ai cambi di rete; quando manca, avviso in
  evidenza e blocco delle richieste ai cervelli online con spiegazione (i server locali
  OpenAI-compatibili restano usabili).
- **Aggiornamento automatico**: controllo giornaliero delle release, note di versione, download
  con verifica di dimensione e impronta SHA-256, installazione silenziosa e riavvio del programma.
  Si governa dalle Impostazioni (sorgente, intervallo, «Controlla ora»); la copia portabile riceve
  solo l'avviso con il collegamento.
- Il profilo del check-up e lo stato di Internet entrano nel contesto del modello.

## 0.2.0 · 31 ottobre 2026

Prima versione pubblica.

- Interfaccia WPF: orb animato che cambia umore con la fase dell'agente, conversazione con
  testo in streaming e resa del markdown, schede espandibili per ogni comando eseguito, linea
  del tempo delle attività, overlay per approvazioni, piani, domande, credenziali e impostazioni.
- Analisi della macchina (istantanea completa, capacità e strumenti disponibili), esplorazione
  della rete locale, esecuzione PowerShell e cmd con classificazione del rischio e approvazione.
- Piano di intervento a passi con rischio e rollback, da approvare passo per passo.
- Memoria per macchina: profilo, azioni eseguite, note e conversazioni, riletti a ogni richiesta.
- Cervello intercambiabile: Claude, Gemini, endpoint OpenAI-compatibili (anche locali).
- Cassaforte cifrata per chiavi e credenziali: sblocco automatico solo per l'account Windows che
  l'ha creata, passphrase per gli altri, blocco per inattività e al blocco di Windows.
- Setup con Inno Setup (per tutti gli utenti o per l'utente corrente) e pacchetto portabile.
