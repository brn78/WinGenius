# WinGenius

**L'assistente sistemista con memoria per Windows desktop e server.**

Gli descrivi un problema in italiano. Lui analizza la macchina, ti dice cosa non va e cosa si
può migliorare, ti propone un piano passo per passo e lo esegue solo dopo il tuo via libera.
E si ricorda tutto quello che ha fatto su quella macchina.

Pensato per chi gestisce host Hyper-V, server con backup, domini e piccole reti, ma utile su
qualunque PC Windows.

> Questa pagina distribuisce i pacchetti pronti all'uso. Il codice sorgente non è pubblico.

## Scarica

Dalla pagina [Releases](../../releases/latest):

| File | Cosa è |
|---|---|
| `WinGenius-<versione>-Setup.exe` | Installer in italiano. Per tutti gli utenti (chiede l'elevazione) o solo per il tuo account. |
| `WinGenius-<versione>-win-x64.zip` | Pacchetto portabile: estrai e avvia `WinGenius.exe`, niente da installare. |
| `SHA256SUMS.txt` | Impronte dei file, per verificare che il download sia integro. |

Entrambi i pacchetti includono il runtime .NET: non serve installare altro.

Per verificare un file scaricato:

```powershell
Get-FileHash .\WinGenius-0.2.0-Setup.exe -Algorithm SHA256
```

e confronta il risultato con la riga corrispondente di `SHA256SUMS.txt`.

## Requisiti

- Windows 10 (1809) o Windows 11, Windows Server 2019 o successivi, a 64 bit.
- PowerShell 5.1 (già presente in Windows).
- Una chiave API per il modello che vuoi usare (Claude di Anthropic o Gemini di Google), oppure
  un server OpenAI-compatibile raggiungibile (Ollama, LM Studio, vLLM) per lavorare senza
  inviare nulla fuori dalla tua rete.

## Primo avvio

1. Apri **Impostazioni → Cervello**, inserisci la chiave API del modello scelto e premi
   «Prova il cervello attivo».
2. In **Impostazioni → Sicurezza** imposta una passphrase per la cassaforte: protegge chiavi e
   credenziali. Con il tuo account Windows la cassaforte si apre da sola; con altri account
   serve la passphrase.
3. In **Impostazioni → Approvazioni** scegli quanto deve chiederti: la politica consigliata
   esegue da solo le letture e si ferma prima di ogni modifica.
4. Scrivi la richiesta, oppure usa uno dei suggerimenti della schermata iniziale:
   *Analizza questa macchina*, *Esplora la rete*, *Controlla Hyper-V*, *Verifica i backup*.

Per lavorare davvero su un server, avvialo come amministratore: senza elevazione analizza ma
molte modifiche fallirebbero (te lo segnala e offre il riavvio elevato).

## Come lavora

- **Osserva prima di toccare**: raccoglie un'istantanea della macchina (sistema, memoria,
  dischi, rete, Hyper-V e VM, servizi, attività pianificate, eventi) e la tiene in memoria.
- **Ogni comando è classificato**: sola lettura, modifica o pericoloso. In base alla politica
  scelta ti mostra il comando e aspetta la tua approvazione. Riavvii, cancellazioni, dischi,
  VM, firewall e utenti chiedono sempre conferma.
- **Prima di intervenire propone un piano** con passi, rischio e come tornare indietro: puoi
  approvarlo, spegnere singoli passi o rifiutarlo con un commento.
- **Ricorda**: ogni azione eseguita, con esito, e le note che prende restano nella memoria
  della macchina (`C:\ProgramData\WinGenius`), consultabile dall'app.
- **Credenziali per altri host** vengono chieste in una finestra dell'app, custodite nella
  cassaforte cifrata e consegnate a PowerShell solo per la durata del comando. Il modello non
  le vede mai e nell'output vengono oscurate.

## Dati e riservatezza

- WinGenius non invia nulla all'autore. Non ci sono account, telemetria o statistiche.
- Quello che scrivi, l'output dei comandi eseguiti e il contesto della macchina (nome, sistema,
  istantanea, memoria) vengono inviati **al provider del modello che hai configurato**
  (Anthropic, Google o il server OpenAI-compatibile che indichi), secondo le condizioni di quel
  provider. Con un modello locale nulla lascia la tua rete.
- Chiavi API e credenziali stanno in `vault.json`, cifrate con AES-256-GCM. Le impostazioni
  non contengono segreti.
- La disinstallazione lascia `C:\ProgramData\WinGenius`: se non ti serve più, eliminala.

## Avvertenze e limitazione di responsabilità

WinGenius esegue comandi reali sui sistemi su cui lo usi, su proposta di un modello di
intelligenza artificiale e dopo la tua approvazione. **Leggi sempre il comando o il piano
prima di approvarlo.** Un modello può sbagliare, interpretare male una situazione o proporre
un intervento inadatto al tuo ambiente.

- Il programma è fornito **«così com'è»**, senza garanzie di alcun tipo, espresse o implicite,
  comprese quelle di idoneità a uno scopo particolare e di assenza di errori.
- **L'autore non risponde** di danni diretti o indiretti, perdita di dati, interruzioni di
  servizio, costi di API o altre conseguenze derivanti dall'uso, dall'uso improprio o
  dall'impossibilità d'uso del programma, né delle azioni che tu o altri utenti approvate.
- Ogni azione eseguita è stata approvata da chi usa il programma, secondo la politica che ha
  scelto nelle impostazioni: la responsabilità di ciò che viene eseguito sui tuoi sistemi è tua.
- Prima di usarlo su macchine di produzione provalo su una macchina di test, **tieni backup
  aggiornati** e usa la politica di approvazione più prudente finché non hai preso confidenza.
- Le chiavi API, i relativi costi e il rispetto delle condizioni dei provider sono a tuo carico.
- Non usare il programma su sistemi che non sei autorizzato ad amministrare.

Le condizioni complete sono nel file [LICENZA.md](LICENZA.md).

## Segnalazioni

Problemi e proposte si segnalano nella sezione [Issues](../../issues) di questa pagina.
Non incollare mai chiavi, password o dati riservati nelle segnalazioni.

---

Bruno Leonardi · b.leonardi78@gmail.com
