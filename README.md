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

_________________________________________________________________

# Microbash_Unige

# Micro-bash Project

This repository contains `microbash`, a minimal command interpreter (shell) developed in C. The project was originally created to support the Information Processing and Transmission Systems (SETI) laboratory at the University of Genoa.

## Authors and Acknowledgments

**Important note:** The software architecture and much of the base source code were designed and written by professor **Giovanni Lagorio**.

My contribution within this repository was limited to completing the missing routines (replacing the educational markers `/*** TO BE DONE ***/`), necessary to make the shell fully functional.

## Modifications and Implemented Features

In compliance with the license terms for derivative works, I declare that I have modified the `microbash.c` file, implementing the operational logic for the following features:
* **Memory Management:** Implementation of the `free_command` and `free_line` routines for the proper release of dynamically allocated memory (syntax trees and paths) during command-line parsing.
* **Environment Variables:** Addition of expansion logic to resolve variable values (via `getenv`) when the `$` prefix is used.
* **Validation and Redirections:** Development of checks to ensure that input redirection (`<`) occurs exclusively on the first command of the pipeline and output redirection (`>`) exclusively on the last
* **Built-in Commands:** Implementation of syntax checks and native execution of the `cd` command (via `chdir`), ensuring it is not chained to other commands or redirections.
* **Pipeline and Execution:** Inter-process wiring of file descriptors (`pipe`, `dup2`, `fcntl` with `FD_CLOEXEC`), creation of child processes (`fork`), and launching of system commands (`execvp`).
* **Synchronization:** Process wait management (`wait_for_children`), intercepting and printing to standard error both abnormal exit statuses and terminations caused by external signals.
* **Dynamic Prompt:** Resolution of the current working directory (via `getcwd`) for the dynamic update of the text prompt.

## Compilation and Execution

To compile the project, run the `make` command inside the repository root. The `Makefile` will handle generating the executable binary by linking the `readline` library to support command-line history and editing.

```bash
make
```
To start the interpreter
```bash
./microbash
```

## Repository Structure
The repository has been configured to exclusively track the necessary source files:

microbash.c: Shell source code.

Makefile: Compilation automation script.

This README.md file.

## License
This project is distributed under the GNU General Public License (GPL) v2, in accordance with the original project.

All original copyright notices belonging to Giovanni Lagorio are kept intact at the beginning of the source file. The modifications made in this repository are redistributed under the same license free of charge.
