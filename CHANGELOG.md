# Novità

## 0.8.2 · 1 novembre 2026

- **Modello sovraccarico: si riprova da soli**: quando il provider risponde 503 («il modello è molto richiesto»), 429
  o un altro errore passeggero, oppure la rete si inceppa, il genio riprova fino a tre volte con attese crescenti
  (3, 8 e 15 secondi) scrivendo nello stato cosa sta succedendo; «Prova il cervello attivo» riprova una volta.
- **Errori dei provider spiegati**: al posto del JSON grezzo compare una frase in italiano con il codice e cosa fare
  (sovraccarico → aspetta o scegli un altro modello dall'Elenco; 429 → quota o limite; 401/403 → chiave; 404 → modello
  non trovato), con il messaggio originale del provider in coda.
- **Gemini pensante e strumenti**: i modelli Gemini dalla famiglia 3 in su allegano a ogni chiamata di funzione una
  firma del ragionamento (`thoughtSignature`) e rifiutano il passo successivo se non la ricevono indietro («Function
  call is missing a thought_signature», errore 400 dopo il primo comando). Ora la firma si conserva con la chiamata,
  anche nella memoria, e si rimanda tale e quale; per le conversazioni nate prima si salta la verifica come
  documentato da Google.

## 0.8.1 · 1 novembre 2026

- **«Scarica e installa» ora installa davvero**: il setup silenzioso chiedeva a WinGenius di chiudersi tramite il
  Restart Manager, ma WinGenius si riduceva nell'area di notifica invece di uscire; il setup trovava i file in uso,
  annullava tutto senza dirlo e lasciava fermo il servizio. Ora WinGenius esce davvero quando glielo chiede un
  programma di installazione (o taskkill), la finestra di aggiornamento chiude l'app per intero, l'installatore
  chiude lui stesso le istanze rimaste prima di copiare i file e, se mai si interrompe, riavvia il servizio.

## 0.8.0 · 1 novembre 2026

- **Widget flottante**: una pillola sempre in primo piano, da tenere dove vuoi sullo schermo (si trascina dall'orb e
  si attacca ai bordi, la posizione si ricorda per monitor), per scrivere o dettare al genio senza aprire la finestra.
  Mentre scrivi un nome di file compaiono i primi risultati dell'indice (freccia giù, Invio apre); la risposta arriva
  in una bolla con «Leggi», «Copia» e «Apri»; se serve una tua decisione la finestra viene portata davanti. Si mostra
  e si nasconde dal menu dell'icona, con **Ctrl+Alt+G** da qualunque programma o avviando WinGenius con `--widget`;
  se era in vista alla chiusura ricompare all'avvio. Impostazioni → Widget: tasto rapido, opacità a riposo, risultati
  dell'indice, bolla, «Riporta nell'angolo». WinGenius ora gira in una sola istanza: lanciarlo di nuovo porta davanti
  quella aperta.
- **Elenco dei modelli dai provider**: accanto a ogni modello in Impostazioni → Cervello c'è «Elenco», che scarica dal
  provider (Anthropic, Google, server OpenAI-compatibili) i modelli disponibili per la tua chiave, dal più recente, e
  li propone in una tendina; «Aggiorna» lo rilegge quando vuoi e l'ultimo elenco resta anche senza Internet. Niente
  più nomi da cercare su Internet; scrivere a mano resta possibile.
- **Tema chiaro, scuro o automatico** (Impostazioni → Programma): Scuro è la notte della lampada, Chiaro la stessa
  lampada di giorno su carta calda; Automatico segue il tema delle app di Windows e cambia con lui. Si applica subito,
  finestra, widget e menu compresi; `--theme light|dark|auto` lo forza per una sola esecuzione.
- **Correzioni**: con il servizio installato un turno partiva e si fermava con «Manca la chiave API» anche se la chiave
  era salvata, perché la cassaforte del servizio era chiusa: ora il servizio chiede la chiave alla finestra (e la
  finestra gliela presta appena si collega, se la sua è aperta) e vede le chiavi aggiunte dopo il suo avvio. La tendina
  del cervello nell'intestazione mostra subito il modello scritto nelle Impostazioni, non quello letto all'avvio. Il
  pulsante del microfono è nel tema (lo usa anche il widget).

## 0.7.1 · 1 novembre 2026

- **Finestra ingrandita entro l'area di lavoro**: ingrandita, la finestra copriva tutto lo schermo e il compositore con
  la scheda della memoria finivano sotto la barra delle applicazioni. Ora occupa solo lo spazio libero del monitor su
  cui sta (anche con la barra in alto o di lato) e il contenuto rientra di quanto la cornice invisibile di Windows
  sporge davvero, misurato ogni volta.

## 0.7.0 · 1 novembre 2026

- **Indice dei file**: WinGenius tiene un indice di tutti i file e le cartelle delle unità locali (come la ricerca
  istantanea di WinTools, con in più la dimensione di ogni file e quella cumulativa delle cartelle). Si costruisce in
  sottofondo a bassa priorità, si aggiorna da solo seguendo le modifiche del disco e si rilegge per intero a orario;
  quando il servizio è installato è lui a tenerlo, così vede tutti i file anche a finestra chiusa. Impostazioni →
  Indice dei file: radici (anche di rete), cartelle da saltare, nascosti, frequenza, stato e «Aggiorna ora».
- **Ricerca** (lente nella barra laterale, Ctrl+K): i risultati compaiono mentre si digita, senza badare a maiuscole
  e accenti, con filtri per file o cartelle e ordine per pertinenza, più grandi, più recenti o nome. «Più grandi»
  senza testo mostra dove va lo spazio. Invio apre, Ctrl+Invio mostra in Esplora, Ctrl+C copia il percorso, «Chiedi
  al genio» porta la voce nella conversazione.
- **Il genio cerca con l'indice**: nuovi strumenti `find_paths` (parole, tipo, estensioni, dimensione, data,
  cartella, ordine), `index_status` e `index_refresh`; il prompt gli dice di usarli invece di Get-ChildItem
  ricorsivo. «I VHDX più grandi», «le cartelle più pesanti», «i file toccati nelle ultime 24 ore» si rispondono
  con una chiamata.

## 0.6.0 · 31 ottobre 2026

- **La voce di WinGenius**: le risposte si possono ascoltare con una voce di Windows. Su ogni risposta compare il
  pulsante «Leggi» (passando il mouse sul messaggio); l'interruttore accanto al microfono le legge tutte da sole
  appena complete; con «Leggi dopo la dettatura» la risposta a una domanda dettata viene letta anche a interruttore
  spento, per una conversazione a mani libere. Elenchi, tabelle e comandi diventano frasi semplici e le unità di
  misura si leggono per esteso. Accanto alle voci classiche ci sono quelle moderne di Windows 10 e 11 (Elsa, Cosimo),
  più naturali. Voce, velocità e prova in Impostazioni → Voce. Il microfono che si apre ferma la lettura.
- **Telegram con messaggio vocale**: dopo il testo arriva anche un vocale con la versione parlata dell'avviso, da
  ascoltare in auto o senza guardare lo schermo. L'assistente scrive da sé la frase da leggere (nuovo parametro
  `spoken` di send_notification); per gli avvisi automatici la compone il programma. Se il vocale non parte, il testo
  arriva comunque e il motivo compare in «Ultime consegne» sulla riga «Telegram (vocale)». L'opzione «Messaggio
  vocale» è nella scheda Telegram, attiva; la prova di collegamento lo include.
- **Gemini 4 Argon**: nelle installazioni nuove il modello predefinito per Google è `gemini-4-argon`; chi ha già
  scelto un modello lo mantiene.

## 0.5.1 · 31 ottobre 2026

- **Dettatura**: corretto un arresto improvviso dell'applicazione (errore di accesso alla memoria) che
  poteva capitare fermando il microfono mentre si stava già chiudendo, per esempio con un clic rapido
  sul pulsante o annullando subito dopo l'avvio. Ora il dispositivo si apre, si ferma e si chiude un
  thread alla volta e ogni registrazione si conclude una volta sola.

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
