# Microbash_Unige

# Progetto Micro-bash

Questo repository contiene `microbash`, un interprete di comandi (shell) minimale sviluppato in C. Il progetto è stato originariamente realizzato a supporto del laboratorio di Sistemi di Elaborazione e Trasmissione dell'Informazione (SETI) presso l'Università degli Studi di Genova.

## Autori e Riconoscimenti

**Nota importante:** L'architettura del software e gran parte del codice sorgente di base sono stati progettati e scritti dal professore **Giovanni Lagorio**.

Il mio contributo all'interno di questo repository si è limitato al completamento delle routine mancanti (sostituendo i marcatori didattici `/*** TO BE DONE ***/`), necessarie per rendere la shell pienamente funzionale.

## Modifiche e Funzionalità Implementate

Nel rispetto dei termini di licenza per i lavori derivati, dichiaro di aver modificato il file `microbash.c` implementando la logica operativa per le seguenti funzionalità:
* **Gestione della Memoria:** Implementazione delle routine `free_command` e `free_line` per il corretto rilascio della memoria allocata dinamicamente (alberi sintattici e path) durante il parsing della linea di comando.
* **Variabili d'Ambiente:** Aggiunta della logica di espansione per risolvere i valori delle variabili (tramite `getenv`) quando viene utilizzato il prefisso `$`.
* **Validazione e Redirezioni:** Sviluppo dei controlli per garantire che la redirezione dell'input (`<`) avvenga esclusivamente sul primo comando della pipeline e quella di output (`>`) esclusivamente sull'ultimo.
* **Comandi Built-in:** Implementazione dei controlli sintattici e dell'esecuzione nativa del comando `cd` (tramite `chdir`), assicurando che non venga concatenato ad altri comandi o redirezioni.
* **Pipeline ed Esecuzione:** Cablaggio inter-processo dei descrittori di file (`pipe`, `dup2`, `fcntl` con `FD_CLOEXEC`), creazione dei processi figli (`fork`), e lancio dei comandi di sistema (`execvp`).
* **Sincronizzazione:** Gestione dell'attesa dei processi (`wait_for_children`), intercettando e stampando su standard error sia gli *exit status* anomali sia le terminazioni causate da segnali esterni.
* **Prompt Dinamico:** Risoluzione della directory di lavoro corrente (tramite `getcwd`) per l'aggiornamento dinamico del prompt testuale.

## Compilazione ed Esecuzione

Per compilare il progetto, eseguire il comando `make` all'interno della root del repository. Il `Makefile` si occuperà di generare il binario eseguibile linkando la libreria `readline` per supportare la cronologia e l'editing della riga di comando.

```bash
make
```
Per avviare l'interprete:
```bash
./microbash
```

## Struttura del Repository
Il repository è stato configurato per tracciare esclusivamente i file sorgente necessari:

microbash.c: Codice sorgente della shell.

Makefile: Script di automazione della compilazione.

Questo file README.md.

## Licenza
Questo progetto è distribuito sotto la licenza GNU General Public License (GPL) v2, conformemente al progetto originale.

Tutti gli avvisi di copyright originali appartenenti a Giovanni Lagorio sono mantenuti intatti all'inizio del file sorgente. Le modifiche apportate in questo repository vengono redistribuite sotto la medesima licenza a titolo gratuito.
